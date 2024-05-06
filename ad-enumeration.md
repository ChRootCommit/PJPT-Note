# AD Enumeration

## Runas /netonly

* Runas&#x20;

```
runas.exe /netonly /user:<domain>\<username> cmd.exe
```

* Read sysvol to verify we are authenticated user in AD (kerberos auth by default)&#x20;

```
$dnsip = "<DC IP>"
$index = Get-NetAdapter -Name 'Ethernet' | Select-Object -ExpandProperty 'ifIndex'
Set-DnsClientServerAddress -InterfaceIndex $index -ServerAddresses $dnsip
```

```shell-session
dir \\<DC IP>\SYSVOL
dir \\<Domain name>\SYSVOL

```

## Enum with cmd

```
net user /domain
net user <user> /domain

net group /domain
net group "<group>" /domain

net accounts /domain
```

\
Enum with powershell
--------------------

```
Get-ADUser -Identity <User> -Server <Domaine> -Properties *
Get-ADUser -Filter 'Name -like "*<User>"' -Server <Domaine> | Format-Table Name,SamAccountName -A

Get-ADGroup -Identity <group> -Server <domaine>
Get-ADGroupMember -Identity <group> -Server <domaine>

PS C:\> $ChangeDate = New-Object DateTime(2022, 02, 28, 12, 00, 00)
PS C:\> Get-ADObject -Filter 'whenChanged -gt $ChangeDate' -includeDeletedObjects -Server <Domaine>

Get-ADObject -Filter 'badPwdCount -gt 0' -Server <domaine>

Get-ADDomain -Server <domaine>

Set-ADAccountPassword -Identity <user> -Server <domaine> -OldPassword (ConvertTo-SecureString -AsPlaintext "old" -force) -NewPassword (ConvertTo-SecureString -AsPlainText "new" -Force)



```

## Bloodhound

### Sharphound

```
SharpHound.exe --CollectionMethods <method> --Domain <domaine> --ExcludeDCs
```

### Bloodhound

```
bloodhound --no-sandbox
neo4j console start
```
