When designing this homelab environment, I decided to deploy two Windows Server 2022 domain controllers within VirtualBox to mirror best practices used in a real enterprise environment. Having multiple domain controllers provides high availability, replication, load distribution, and disaster recovery. 

DC01 - Primary Domain Controller (Server Core)

Why server core? DC01 is intentionally designed to be deployed as a Windows Server 2022 server core because it:

-Provides a smaller attack surface
-Allows for redundancy and lower resource usage
-Simpler patching requirements

Configuration:
OS: 
      -2022 Windows Server Core
Roles: 
      -Active Directory Domain Services
      -DNS Server
Networking:
      -Primary NIC: 192.168.10.10
      -Secondary NIC (SIEM Subnet): 192.168.1.239
Tools Used: 
      -Powershell
      -sconfig
      -RSAT (Allows for disaster recovery if DC02 goes down)
Responsibiliy:
      -Host main local domain (lab.local)
      -Hold all FSMO roles initially
      -Provide primary DNS services
      -Act as primary Domain Controller


DC02 - Full GUI

DC02 is designed to be a redundant Domain Controller and primary FileShare for the network. It provides fault tolerance, replication, and a GUI-based interface for
server management.

Why full GUI?
DC02 is intentionally deployed as a Windows Server 2022 Desktop Experience to:

-Visual access to AD tools
-Fallback management interface if RSAT fails
-Simulate real world environments with a mix of Core and GUI DCs
-Easier troubleshooting and management

Configuration:
OS: 
    -Windows Server 2022 Desktop Experience
Roles Installed:
    -Active Directory Domain Services
    -DNS Server





