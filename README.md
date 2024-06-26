# Net-Year2-CapstoneProject
- Led network planning and infrastructure design, including VLAN setup.  
- Configured FortiGate firewall policies and IPsec tunnels.  
- Implemented OSPF/OSPFv3 routing protocols for efficiency.  
- Integrated IPv6 addressing and deployed SD-WAN technology.  
- Set up the Teams phone system and configured QoS for traffic shaping.  
- Implemented security measures like ACLs and SSL VPN for remote access.  
- Maintained documentation for configurations and troubleshooting.  


For our build, we focused on constructing Site 1 (HQ) and Site 3 (Plant).we configured our own ISP router for the purposes of SD-WAN and assigned static IP addresses to ourselves. This setup allows us full control to troubleshoot connectivity issues that may arise. 
Site 1 routes all traffic through the FortiGate routers, which are configured in an Active-Active HA (High Availability) mode. Furthermore, we have a fully link-aggregated group (LAG) environment, including connections to our FortiGate firewalls. Initially, our topology differed significantly from our current layout. However, we quickly learned that we were unable to route similar VLANs through multiple LAGs. Consequently, we limited the FortiGate LAG interfaces to one by having our endpoint switches connect to our two distribution switches. These two distribution switches provide added redundancy. The advantages of this topology include enhanced scalability and a fully LAG-configured environment, resulting in improved speeds and link redundancy. Additionally, this configuration allows us to have an isolated switch dedicated solely to clients and servers, which can alleviate traffic stress and increase device reliability. 
Each ESXi server has two management links connected to its own switch, along with two additional links directly connecting server to server. One link is used for data replication, while the other serves as a heartbeat connection when clustered in our two-node vSAN configuration. 
Site 3 is similarly routed through the firewall, like Site 1, but with a difference: it lacks distribution switches. Instead, it relies on redundant links connected to a software switch on the FortiGate using LAG. In this setup, we have a switch for clients/servers, a dedicated switch for OT (Operational Technology), and another switch for our wireless access point (AP) to simulate the need for wireless access in the Site 4 warehouse. 

Additionally, we have two IPsec tunnels running from site-to-site for inter-site connectivity and redundancy. We also maintain an offsite IPsec tunnel from each site to our designated UltraCloud router, which facilitates offsite backups. 
