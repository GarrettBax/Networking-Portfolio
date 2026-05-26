02 - Router on a Stick (Inter-VLAN Routing)

Click into 02_Router_on_a_Stick and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.


Topology


PC1 (192.168.10.10) ──┐
PC2 (192.168.10.11) ──┤                        ┌── [Router G0/0.10 - 192.168.10.1]
PC3 (192.168.20.10) ──┼── [Layer 2 Switch] ────┤
PC4 (192.168.20.11) ──┘                        └── [Router G0/0.20 - 192.168.20.1]


PC0 and PC1 are on VLAN 10. PC2 and PC3 are on VLAN 20.
The switch uplink to the router is configured as a trunk port.


IP Scheme

| Device | VLAN | IP Address | Subnet Mask | Default Gateway |

| PC0 | VLAN 10 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC1 | VLAN 10 | 192.168.10.11 | 255.255.255.0 | 192.168.10.1 |
| PC2 | VLAN 20 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| PC3 | VLAN 20 | 192.168.20.11 | 255.255.255.0 | 192.168.20.1 |
| Router G0/0.10 | VLAN 10 | 192.168.10.1 | 255.255.255.0 | N/A |
| Router G0/0.20 | VLAN 20 | 192.168.20.1 | 255.255.255.0 | N/A |



Concepts Covered

| Concept | Description |

| VLANs | Logical network segmentation separating SALES and IT traffic |
| 802.1Q Trunking | Tagged VLAN traffic traveling over a single trunk link |
| Subinterfaces | Single router interface split into virtual interfaces per VLAN |
| Inter-VLAN Routing | Router forwards traffic between VLAN 10 and VLAN 20 |
| Access Ports | Switch ports assigned to a single VLAN for end devices |



Key Commands

Verify VLAN assignments on the switch:

show vlan brief


Verify trunk port on the switch:

show interfaces trunk


Verify routing table on the router:

show ip route


Test connectivity within VLAN:

ping 192.168.10.11


Test connectivity across VLANs:

ping 192.168.20.10
