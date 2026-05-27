# 05 - OSPF Multi-Router Network

Click into 05_OSPF_Multi_Router and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.

---

## Overview

A five router OSPF network spanning three areas demonstrating multi-area OSPF, Area Border Routers (ABRs), loopback addressing, DHCP per LAN, and passive interfaces. All routers have formed OSPF neighbor adjacencies and full end-to-end connectivity is verified across all areas.

---

## Topology
<img width="1452" height="566" alt="image" src="https://github.com/user-attachments/assets/d069c89d-fc71-4817-a5ac-3a912902ae4b" />



## IP Scheme

**WAN Links (Serial /30)**

| Link | Router A | IP | Router B | IP |
|---|---|---|---|---|
| R1 ↔ R2 | R1 Se0/0/0 | 10.0.12.1/30 | R2 Se0/0/0 | 10.0.12.2/30 |
| R2 ↔ R3 | R2 Se0/0/1 | 10.0.23.1/30 | R3 Se0/0/0 | 10.0.23.2/30 |
| R1 ↔ R4 | R1 Se0/0/1 | 10.0.14.1/30 | R4 Se0/0/0 | 10.0.14.2/30 |
| R3 ↔ R5 | R3 Se0/0/1 | 10.0.35.1/30 | R5 Se0/0/0 | 10.0.35.2/30 |

**LAN Subnets**

| Router | LAN Subnet | Gateway | DHCP Range |
|---|---|---|---|
| R1 | 192.168.1.0/24 | 192.168.1.1 | 192.168.1.11 - 254 |
| R2 | 192.168.2.0/24 | 192.168.2.1 | 192.168.2.11 - 254 |
| R3 | 192.168.3.0/24 | 192.168.3.1 | 192.168.3.11 - 254 |
| R4 | 192.168.4.0/24 | 192.168.4.1 | 192.168.4.11 - 254 |
| R5 | 192.168.5.0/24 | 192.168.5.1 | 192.168.5.11 - 254 |

**Loopback Addresses**

| Router | Loopback | IP |
|---|---|---|
| R1 | Loopback1 | 1.1.1.1/32 |
| R2 | Loopback2 | 2.2.2.2/32 |
| R3 | Loopback3 | 3.3.3.3/32 |
| R4 | Loopback4 | 4.4.4.4/32 |
| R5 | Loopback5 | 5.5.5.5/32 |

> Loopback addresses are used as OSPF Router IDs and advertised into OSPF for stable router identification.

---

## Concepts Covered

| Concept | Description |
|---|---|
| Multi-Area OSPF | Network split into Area 0 (backbone), Area 1, and Area 2 to reduce LSA flooding |
| ABR (Area Border Router) | R1 and R3 connect multiple areas and summarize routes between them |
| Router ID | Loopback addresses used as stable OSPF router IDs |
| Passive Interface | Enabled on all LAN and loopback interfaces to prevent unnecessary OSPF hellos |
| DHCP per LAN | Each router serves as a DHCP server for its local LAN subnet |
| Serial DCE/DTE | Point-to-point WAN links using serial connections with clock rate on DCE end |
| Intra-Area Routes (O) | Routes learned within the same OSPF area |
| Inter-Area Routes (O IA) | Routes learned from a different OSPF area via an ABR |

---

## Key Commands

**Verify OSPF neighbors:**
```
show ip ospf neighbor
```

**Verify routing table (look for O and O IA routes):**
```
show ip route ospf
```

**Verify OSPF interfaces and areas:**
```
show ip ospf interface brief
```

**Verify DHCP assignments:**
```
show ip dhcp binding
```

**Test end-to-end connectivity across all areas (from R4 LAN to R5 LAN):**
```
ping 192.168.5.x
```
