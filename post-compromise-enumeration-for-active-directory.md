# Post Compromise Enumeration for Active Directory

## Ldapdomaindump

```
sudo ldapdomaindump ldaps://<IP_DC> -u '<domain>\<user>\' -p <password>
```

## Bloodhound

```
sudo bloodhound-python -d <domain>.local -u <user> -p <password> -ns <DC-ip> -c all 
```

## Plumhound

```
sudo python3 PlumHound.py --easy -p [YOUR_PASS]
sudo python3 PlumHound.py -x tasks/default.tasks -p [YOUR_PASS]
```

