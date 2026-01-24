When designing this homelab environment, I decided to deploy two Windows Server 2022 domain controllers to mirror best practices used in a real enterprise environment. Having multiple domain controllers provides high availability, replication, load distribution, and disaster recovery. 

DC01 - Primary Domain Controller (Server Core)

Why server core? DC01 is intentionally designed to be deployed as a Windows Server 2022 server core because it:
-Provides a smaller attack surface
-Allows for redundancy and lower resource usage
-Simpler patching requirements
