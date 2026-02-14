**SolarWinds Security Event Manager**

This section documents the integration of my Active Directory environment with SolarWinds Security Event Manager (SEM). The goal was to simulate a realistic SOC workflow by forwarding Windows Security logs from my Windows 
machines, validating event ingestion, creating custom filters and rules, and generating alerts based on domain activity.

SolarWinds was deployed as a VirtualBox appliance on the SIEM network (192.168.1.0/24) and configured to ingest logs from both domain controllers and Lab-PC. 


SEM Dashboard Overview: 

This photo shows the SolarWinds main dashboard. Customizable widgets display security events and information for easy access. 

![SEM Dashboard](images/SolarWinds/Main%20Dashboard.png)


Network Nodes:

![Nodes](images/SolarWinds/Nodes.png)


Normalized Event (Failed Logon): 

This photo shows a normalized event broadcasted to the Live Events panel. I triggered this event by doing a few failed login attempts for my administrator account on DC01. 

![Failed Login](images/SolarWinds/Normalized%20Event%20(Failed%20Logon).png)

Expanding the event highlights its details, as seen below: 

![Expanded](images/SolarWinds/Failed%20Logon%20Expanded.png)


In SolarWinds, custom filters and rules help analysts in sorting out important security events. The following photos showcase internal rules and filters within the program. 


**INCIDENT: User added to Domain Admins**

These photos show a custom rule firing off that alerts analysts when an AD account was added to the Domain Admins group.

Live Event Reading of Internal Rule: 

![Rule Fired](images/SolarWinds/Incident%20and%20Internal%20Rule%20Firing.png)

Dedicated Incident Category:

![User Added](images/SolarWinds/Incident%20Category%20(Admin%20Added).png)

Rule Setup: 

![Setup](images/SolarWinds/Rule%0Setup%20(Added%20Admin).png)


Custom Filter: 

This filter allows for analysts to see each time a user is removed from the Administrators group. 

![Admin Removed](images/SolarWinds/Custom%20Filter%20(Admin%20Removed).png)


Finally, this photo shows the SolarWinds program running on a Linux Debian machine within the environment. It shows the IP address of the machine as well as how to access the console.

![SEM Health](images/SolarWinds/SEM%20Health.png)



