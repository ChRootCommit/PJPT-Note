# AD Basis

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

* **Centralised identity management:** All users across the network can be configured from Active Directory with minimum effort.
* **Managing security policies:** You can configure security policies directly from Active Directory and apply them to users and computers across the network as needed.

## AD CS

* Users (People & services)
* Machines&#x20;
* _Security Groups :_
  * Domain Admins
  * Server Operators
  * Backup Operators
  * Account Operators
  * Domain Users
  * Domain Computers
  * Domain Controllers

The most common difference between a Container and an Organizational Unit is that an Organizational Unit can receive Group Policies. You cannot apply Group Policies to Container objects and you cannot deploy them to the builtinDomain folder.

Other containers:&#x20;

* Builtin: Contains default groups available to any Windows host.&#x20;
* Computers: Any machine joining the network will be put here by default. You can move them if needed.&#x20;
* Domain Controllers: Default OU that contains the DCs in your network.&#x20;
* Users: Default users and groups that apply to a domain-wide context.&#x20;
* Managed Service Accounts: Holds accounts used by services in your Windows domain.

##
