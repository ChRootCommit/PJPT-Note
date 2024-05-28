# Scanning & enumeration

## Scanning with nmap

```bash
# discover network
arp-scan -l
netdiscover -r <ip>/<cidr>
# nmap
nmap -sS <ip># stealth scanning, SYN SYNACK RST
nmap -T4 -p- -A <ip>
nmap -sU <ip> # udp scan

```

## Enumeration HTTP and https

```bash
# nikto
nikto -h <url> 
# gobuster or dirbuster 
# Use burpsuite sitemap
```

## Enumerating SMB

```
auxiliary/scanner/smb/smb_version
smbclient -L \\\\\<ip>\\ 
smbclient \\\\\<ip>\\<share>


Question: My enum4linux and/or smbclient are not working. I am receiving "Protocol negotiation failed: NT_STATUS_IO_TIMEOUT". How do I resolve?

Resolution:

On Kali, edit /etc/samba/smb.conf

Add the following under global:

client min protocol = CORE

client max protocol = SMB3
```

## Enumerating ssh

If there is following pb :&#x20;

<figure><img src=".gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

```
# Resolving
ssh <ip> -oKexAlgorithms=+diffie-hellman-group1-sha1
# PB where therie is no banner
```

