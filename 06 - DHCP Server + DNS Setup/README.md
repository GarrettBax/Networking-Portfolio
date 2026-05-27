# 06 - DHCP Server + DNS Setup

Click into 06_DHCP_DNS and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.

---

## Overview

A two LAN network with a single server providing both DHCP and DNS services to all devices. A router connects the two LANs and uses `ip helper-address` to forward DHCP broadcast requests from LAN2 across to the server sitting on LAN1. All PCs receive their IP addresses automatically and DNS resolution is verified by pinging hostnames.

---

## Topology


<img width="896" height="483" alt="image" src="https://github.com/user-attachments/assets/e373edb7-216e-4172-a2d1-9b4c55fecbb9" />



The DHCP/DNS server sits on LAN1 and serves address pools for both LANs.
The router forwards LAN2 DHCP broadcasts to the server via `ip helper-address`.


## IP Scheme

**Static Assignments**

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| R1 G0/0 (LAN1) | 192.168.1.1 | 255.255.255.0 | N/A |
| R1 G0/1 (LAN2) | 192.168.2.1 | 255.255.255.0 | N/A |
| Server | 192.168.1.100 | 255.255.255.0 | 192.168.1.1 |

**DHCP Pools (Served by Server)**

| Pool | Subnet | Gateway | DNS Server | Range |
|---|---|---|---|---|
| LAN1_POOL | 192.168.1.0/24 | 192.168.1.1 | 192.168.1.100 | 192.168.1.101 - 150 |
| LAN2_POOL | 192.168.2.0/24 | 192.168.2.1 | 192.168.1.100 | 192.168.2.101 - 150 |

> PC0, PC1 pull from LAN1_POOL. PC2, PC3, PC4 pull from LAN2_POOL via DHCP relay.

---

## DNS Records

| Hostname | Type | IP Address |
|---|---|---|
| server.local | A Record | 192.168.1.100 |
| r1.local | A Record | 192.168.1.1 |

---

## Concepts Covered

| Concept | Description |
|---|---|
| Centralized DHCP | A single server manages address pools for multiple subnets |
| DHCP Relay (ip helper-address) | Router forwards DHCP broadcasts from LAN2 to the server on LAN1 since broadcasts do not cross routers |
| DNS A Records | Hostname to IP mappings allowing devices to ping by name instead of IP |
| Static Server Addressing | Server requires a static IP since it is the addressing authority for the network |
| Inter-LAN Routing | Router connects two subnets enabling cross-LAN communication |

---

## Key Commands

**Verify DHCP relay is configured on the router:**
```
show running-config | section interface
```

**Test DHCP assignment on a PC:**
```
ipconfig
```

**Test connectivity across LANs:**
```
ping 192.168.2.101
```

**Test DNS resolution by hostname:**
```
ping server.local
ping r1.local
```
