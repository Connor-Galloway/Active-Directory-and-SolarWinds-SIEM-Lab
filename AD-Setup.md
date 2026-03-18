When designing this homelab environment, I decided to deploy two Windows Server 2022 domain controllers within VirtualBox to mirror best practices used in a real enterprise environment. Having multiple domain controllers provides high availability, replication, load distribution, and disaster recovery. 

**DC01 - Primary Domain Controller (Server Core)**

Why server core? DC01 is intentionally designed to be deployed as a Windows Server 2022 server core because it:

-Provides a smaller attack surface

-Allows for redundancy and lower resource usage

-Simpler patching requirements

Configuration
OS: 

      -2022 Windows Server Core
      
Roles: 

      -Active Directory Domain Services
      
      -DNS Server
      
Networking:

      -Primary NIC: 192.168.10.10
      
      -Secondary NIC (SIEM Subnet): 192.168.1.239
      
Tools Used: 

      -PowerShell
      
      -SConfig
      
      -RSAT (Allows for disaster recovery if DC02 goes down)
      
Responsibilities:

      -Host main local domain (lab.local)
      
      -Hold all FSMO roles initially
      
      -Provide primary DNS services
      
      -Act as primary Domain Controller
      

DC01 Main Interface (SConfig):

![DC01 SConfig](images/DC01/SCONFIG.png)

System Information:

![DC01 SystemInfo](images/DC01/System%20Info.png)

DC01 IP Configuration:

![DC01 IP Configuration](images/DC01/DC01%20IPCONFIG.png)

FSMO Roles:

![DC01 FSMO](images/DC01/FSMO%20Roles.png)

Domain Controller Status:

![DC01 DC Status](images/DC01/Domain%20Controller.png)


**DC02 - Full GUI**

DC02 is designed to be a redundant Domain Controller and primary file share for the network. It provides fault tolerance, replication, and a GUI-based interface for
server management.

Why full GUI?
DC02 is intentionally deployed as a Windows Server 2022 Desktop Experience to:

-Give visual access to AD tools

-Provide fallback management interface if RSAT fails

-Simulate real world environments with a mix of Core and GUI DCs

-Have easier troubleshooting and management


Configuration:
OS: 

    -Windows Server 2022 Desktop Experience
    
Roles Installed:

    -Active Directory Domain Services
    
    -DNS Server
Domain:

    -lab.local
    
Networking:

    -Primary NIC 192.168.1.11 (Internal Domain)
    
    -Secondary NIC: 10.0.3.15 (NAT Adapter)
    
    -192.168.1.240 (SIEM Subnet)

Responsibilities:

      -Serve as file share for NTFS permission testing

      -Provide redundancy for authentication, DNS, and GPO delivery

      -Replicate AD objects and DNS zones from DC01

      -Serve as a GUI-based management interface for AD

      -Act as a secondary log source for SIEM integration

Management Tools

Because DC02 has a full GUI, it includes all native Windows Server management consoles, including:

      -Active Directory Users and Computers
      
      -DNS Manager
      
      -Group Policy Management Console
      
      -Event Viewer
      
      -Server Manager     
      
      -PowerShell

All of these tools were used to:

      -Create new users, groups, and OUs

      -Configure and link GPOs
      
      -Verify replication and DNS 
      
      -Monitor security logs and SEM agent activity
      
DC02 Domain Information:

![DC02 Domain](images/DC02/Shows%20lab.local%20Domain.png)
    
Domain Replication with DC01:

![DC02 Replication](images/DC02/Confirm%20Replication%20w%20DC01.png)

IP Configuration for DC02:

![DC02 IPCONFIG](images/DC02/IPCONFIG.png)

DNS Manager: 

![DNS Manager](images/DC02/DNS%20Manager.png)


The four folders within the file share system are shown in the photo below: 

![File Share](images/DC02/FileShare%20on%20DC02.png)

Each folder has its own access control assigned to it via RBAC. Here is an example:

![RBAC for HR](images/DC02/RBAC%20for%20HR%20Write.png) ![RBAC HR Read](images/DC02/RBAC%20for%20HR%20Read.png)

Users inside the Administrators group have full control over the file share, as seen below: 

![ADMIN RBAC](images/DC02/RBAC%20for%20Admins.png)

RBAC is administered through security groups. Expanded below is the IT Administrator Group: 

![IT Group](images/DC02/IT%20Admins%20Security%20Group.png)



**Group Policy**

To showcase group policy in the environment, the following shows an automatic shared network drive mapping layout that allows for users under the HR Admin Groups to have their HR drive automatically map. 
To see this group policy in action, I have provided the video under the Lab-PC portion of this repository. The following is configuration of this group policy on DC02: 

Link to OU: 

![OU Link](images/DC02/HR%20Group%20Policy.png)

Policy Mapped:

![Mapped Policy](images/DC02/Policy%20Mapped.png)

Direct Targeting for Security Groups:

![Direct Target](images/DC02/Applicants%20for%20GP.png)










