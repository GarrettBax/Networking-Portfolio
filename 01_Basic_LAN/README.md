Click into 01_Basic_LAN and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.

01 - Basic LAN

A simple Local Area Network demonstrating fundamental switching and IPv4 concepts using Cisco Packet Tracer.

Topology


<img width="602" height="531" alt="image" src="https://github.com/user-attachments/assets/7b926df6-f812-4056-ac9b-c7d3604be313" />


All devices are connected to the switch via straight-through copper cables.

IP Scheme

| Device | IP Address | Subnet Mask | Default Gateway |

| PC1 | 192.168.1.10 | 255.255.255.0 | N/A |
| PC2 | 192.168.1.11 | 255.255.255.0 | N/A |
| PC3 | 192.168.1.12 | 255.255.255.0 | N/A |
| PC4 | 192.168.1.13 | 255.255.255.0 | N/A |
| PC5 | 192.168.1.14 | 255.255.255.0 | N/A |

> All devices share the same subnet "192.168.1.0/24" so no router is needed.  
> Default Gateway is not required for same-subnet communication.

Concepts Covered

| Concept | Description |
| Ethernet (IEEE 802.3) | Wired connectivity between PCs and switch |
| IPv4 Addressing | Static IP assignment within a /24 subnet |
| Subnetting | All hosts on the same 192.168.1.0/24 network |
| ARP | Automatic MAC address resolution before communication |
| ICMP | Connectivity testing using the `ping` command |
| MAC Address Table | Switch learns and stores MAC-to-port mappings |

Key Commands

Test connectivity from any PC:

ping 192.168.1.10


View the switch MAC address table:

enable
show mac address-table
