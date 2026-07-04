# Computer-Network-Project
## Introduction to Computer Networks- Final Project Design

__Overview__

The project simulates a small-medium network in Cisco Packet Tracer, using VLAN segmentation, inter-VLAN routing, DHCP,DNS,a Web server, and NAT/ISP connectivity to the outside network.

__Topology__

_Devices_: 
  * 2x Router (2911)-Router1 and ISP Router0
  * 2x Switch(2960-24TT)- Switch0 and Switch1
  * 15x PC-PT
  * 3x Server-DHCP, DNS,and Web Server
    
_VLANs & Subnets_:
|VLAN   |   Subnet |         Gateway  |      Purpose|
|-------|-----------|--------------------|------------|
| VLAN 30 | 192.168.30.0/24 | 192.168.30.1  |  PC0,PC1,PC3,PC4,PC5|
| VLAN 50 | 192.168.50.0/24 | 192.168.50.1  |  PC6,PC7,PC8,PC9,PC10|
| VLAN 60 | 192.168.60.0/24 | 192.168.60.1  |  PC11,PC12,PC13,PC14,PC15|
| VLAN 11 | 192.168.11.0/24 | 192.168.11.1  | Server subnet: DHCP, DNS, Web Server|

|_Router1 Sub-interfaces_ |   
|-------------------------|
| Gi0/1.30 | -> 192.168.30.1|   
| Gi0/1.50 | ->  192.168.50.1 | 
| Gi0/2.60 | -> 192.168.60.1 |         
| Gi0/2.11 | -> 192.168.11.1 |

| _Trunk Links_|
|--------------|
| Switch0 <-> Router1 |VLANs 30,50,60,11 |
| Switch0 <-> Switch1 |VLANs 30,50 |
| Switch1 <-> Router1 |VLANs 60,11 |


_WAN Link_:

Router1 <-> ISP Router0 - point-to-point, ISP 200.100.100.1/24

_Server(VLAN 11)_
| Server | IP Address |
|--------|------------|
| Server1-DHCP | 192.168.11.2 |
| Server2-DNS | 192.168.11.3 |
| Server0-Web Server | 192.168.11.4 |
 
_Routing method_:

**Inter‑VLAN Routing**:  
The network uses a router‑on‑a‑stick setup. Router1 has one physical interface, but it is divided into multiple sub‑interfaces, with each one assigned to a different VLAN. This allows devices in VLANs 30, 50, and 60 to communicate with each other.
**DHCP**:  
Server1 hands out IP addresses to all devices in VLANs 30, 50, and 60.
Router1 forwards DHCP requests to Server1 using an ip helper‑address, so devices in other VLANs can still receive IP addresses.
**DNS**:  
Server2 provides name resolution for the network. This means computers can use hostnames ( webserver.local) instead of IP addresses.
**NAT (Internet Access)**:  
Router1 uses NAT overload on its WAN interface. This allows all internal devices to access the “internet” using a single public IP address.
**ISP Connectivity**:  
Router1 sends all external traffic to the ISP Router using a default route. The ISP Router sends replies back to Router1, completing the simulation of internet access.

__Verification steps__:

* _ping_ and __traceroute_ between VLANs to confirm inter-VLAN routing.
* _ipconfig/all_ on PCs to confirm DHCP-assigned addresses and correct gateway.
* _nslookup_ to confirm DNS resolution.
* Browser test to Web Server IP/hostname to confirm HTTP access.
* _show vlan brief_ and _show interfaces trunk_ on switches to confirm VLAN/trunk config.
<img width="1366" height="768" alt="Screenshot 2026-07-04 114550" src="https://github.com/user-attachments/assets/e7aa5794-e80e-4ade-8a31-abdd28730407" />
