# 07 - Hierarchical 3-Tier Network

Configuration files are not provided for this lab.
(Lost the file)
---

## Overview

A full enterprise-grade hierarchical 3-tier network built in Cisco Packet Tracer demonstrating core, distribution, and access layer design principles. The network incorporates redundancy, security, dynamic addressing, and Layer 3 routing across multiple VLANs. 

---

## Topology Image

<img width="955" height="489" alt="image" src="https://github.com/user-attachments/assets/7c30ff07-5da9-47ad-8b53-a61ed65b5045" />


---

## Network Architecture

### Core Layer
Two Cisco Layer 3 switches providing high-speed backbone connectivity and redundancy. Core switches interconnect with each other and provide uplinks to the distribution layer.

| Device | Role |
|---|---|
| Core1 | Primary backbone switch |
| Core2 | Secondary backbone switch |

### Distribution Layer
Four Cisco Layer 3 switches providing inter-VLAN routing, HSRP gateway redundancy, DHCP relay, and policy enforcement between the core and access layers.

| Device | Connected To | HSRP Role |
|---|---|---|
| D1 | Core1, A1, A2 | Active |
| D2 | Core1, Core2, A3, A4 | Active |
| D3 | Core1, Core2, A5, A6 | Active |
| D4 | Core2, A7, A8 | Active |

### Access Layer
Eight Cisco Layer 2 switches providing end device connectivity with port-level security features.

| Device | VLAN | Connected PCs |
|---|---|---|
| A1, A2 | VLAN 10 — SALES | PC0 – PC3 |
| A3, A4 | VLAN 20 — IT | PC4 – PC7 |
| A5, A6 | VLAN 30 — HR | PC8 – PC11 |
| A7, A8 | VLAN 40 — MANAGEMENT | PC12 – PC15 |

---

## VLAN Design

| VLAN | Name | Subnet | Purpose |
|---|---|---|---|
| VLAN 10 | SALES | 192.168.10.0/24 | Sales department end devices |
| VLAN 20 | IT | 192.168.20.0/24 | IT department end devices |
| VLAN 30 | HR | 192.168.30.0/24 | HR department end devices |
| VLAN 40 | MANAGEMENT | 192.168.40.0/24 | Management devices and server |
| VLAN 99 | NATIVE | N/A | Native VLAN for all trunk links |

---

## Server (DC)

A dedicated server connected to D1 on the MANAGEMENT VLAN providing centralized DHCP and DNS services for all VLANs.

| Service | Details |
|---|---|
| DHCP | Separate pools for VLAN 10, 20, 30, and 40 |
| DNS | Hostname resolution for internal devices |
| IP Address | 192.168.40.100 (static) |
| Default Gateway | 192.168.40.254 (HSRP virtual IP) |

---

## Features Implemented

| Feature | Description |
|---|---|
| VTP | Distribution switches act as VTP servers propagating VLANs to access layer clients |
| 802.1Q Trunking | All inter-switch links configured as trunks with native VLAN 99 |
| HSRP | Distribution switch pairs share virtual gateway IPs providing first-hop redundancy |
| Inter-VLAN Routing | Layer 3 SVIs on distribution switches route traffic between VLANs |
| DHCP Relay | ip helper-address on distribution SVIs forwards DHCP requests to centralized server |
| DHCP Snooping | Enabled on all access switches to prevent rogue DHCP servers |
| Dynamic ARP Inspection | Enabled on all access switches to prevent ARP spoofing attacks |
| PortFast | Enabled on all PC-facing access ports to skip STP convergence delay |
| BPDUGuard | Enabled on all PC-facing access ports to prevent rogue switch connections |
| STP/PVST | Running across all switches to prevent Layer 2 loops |
| Static Routing | Inter-layer routing configured between core and distribution switches |

---

## HSRP Virtual Gateways

All end devices use the HSRP virtual IP as their default gateway ensuring continuity if a distribution switch fails.

| VLAN | Virtual Gateway |
|---|---|
| VLAN 10 | 192.168.10.254 |
| VLAN 20 | 192.168.20.254 |
| VLAN 30 | 192.168.30.254 |
| VLAN 40 | 192.168.40.254 |

---

## Security Features

| Feature | Where Applied |
|---|---|
| DHCP Snooping | All access switches — untrusted on PC ports, trusted on uplinks |
| Dynamic ARP Inspection | All access switches — validates ARP against DHCP binding table |
| BPDUGuard | All PC-facing ports — err-disables port if a switch is connected |
| PortFast | All PC-facing ports — immediate transition to forwarding state |
| Native VLAN 99 | All trunk links — separates native traffic from user VLANs |
| VTP Password | Prevents unauthorized switches joining the VTP domain |
