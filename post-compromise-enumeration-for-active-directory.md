# Post Compromise Enumeration for Active Directory

## Ldapdomaindump

```
sudo ldapdomaindump ldaps://<IP_DC> -u '<domain>\<user>\' -p <password>
```

## Bloodhound

```
sudo bloodhound-python -d <domain>.local -u <user> -p <password> -ns <DC-ip> -c all 
```

\
\
