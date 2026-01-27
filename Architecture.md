This homelab runs on a VirtualBox host and is segmented into three networks, each mapped to a specific VirtualBox adapter type to mirror real enterprise traffic separation. The 192.168.10.0/24 AD Network is implemented using a Host‑Only Adapter, creating an isolated subnet where DC01, DC02, and the LAB‑PC communicate for Active Directory, DNS, Kerberos, and GPO processing without touching the external network. The 192.168.1.0/24 SIEM Network is provided through a Bridged Adapter, placing DC01, DC02, Lab-PC, and the SolarWinds SEM appliance directly onto the host’s physical LAN so the SIEM can ingest logs as if deployed in a real corporate environment. The 10.0.3.0/24 NAT Network is assigned to DC02 and the LAB‑PC through VirtualBox’s NAT Adapter, giving those machines outbound internet access for updates and package downloads while keeping them hidden from the home network. DC01, running Server Core, holds all FSMO roles and forwards security logs to SEM via its bridged interface, while DC02 provides redundancy, DNS, and a file share. The LAB‑PC uses RSAT to administer the domain across the Host‑Only network while leveraging NAT for internet access. This combination of Host‑Only, Bridged, and NAT adapters creates a realistic multi‑segment enterprise environment with isolated domain traffic, dedicated SIEM ingestion, and controlled internet connectivity.

## Network Architecture


<p align="center">
  <img src=AD-Setup-Diagram.png" width="600" />
</p>
