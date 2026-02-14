**End User Client**

The third virtual machine in this AD homelab is a Windows 11 Virtual Client. Lab-PC is utilized for testing domain features such as Active Directory user login, FileShare, DNS, and Group Policy Objects. It also functions as an endpoint for SIEM detections and log generation, making it a realistic representation of how administrators and users operate within an enterprise Windows environment. 


Windows Sign In Screen: 

This photo indicates Lab-PC is connected to the domain, with a user credential, Luke Skywalker, already cached.

![Sign In](images/Lab-PC/Windows%20Sign%20In.png)


Lab-PC Device Information:

![PC Info](images/Lab-PC/Lab-PC%20System%20Info.png)


IP Configuration: 

This ipconfig screen shows all three IP addresses explained the in Archecture diagram working simultaneously.

![IPCONFIG](images/Lab-PC/IPCONFIG%20for%20Lab-PC.png)


Group Policy In Action: 

This video shows the group policy shown in the AD-Setup portion of this lab in action on the end user side. Darth Vader, an HR user, is logged into the machine in this example. The group policy is manually updated and automatically maps the HR shared drive.

[Group Policy in Action](images/Lab-PC/Recording%20of%20Group%20Policy.mp4)
