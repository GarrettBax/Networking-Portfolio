# 08 - Spine-Leaf  Topology with LAG

Click into 06_Spine_Leaf_LAG and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.

---

## Overview

A spine-leaf topology using Link Aggregation (LAG / EtherChannel) on the spine-to-spine interlink for redundancy and increased bandwidth. Each leaf switch connects to both spines via single Gigabit trunk uplinks. All inter-VLAN routing is handled by Spine SVIs. Full end-to-end connectivity is verified across all VLANs.

---

## Topology



<img width="892" height="574" alt="image" src="https://github.com/user-attachments/assets/b903e80f-2901-401d-8afe-23b29dcecb16" />



---

## Device Overview

| Device  | Model        | Role         | Description                              |
|---------|--------------|--------------|------------------------------------------|
| Spine-1 | 3650/3560    | Spine Switch | Core aggregation, inter-VLAN routing     |
| Spine-2 | 3650/3560    | Spine Switch | Redundant core, inter-VLAN routing       |
| Leaf-1  | 2960         | Leaf Switch  | L2 access, hosts VLAN 10                 |
| Leaf-2  | 2960         | Leaf Switch  | L2 access, hosts VLAN 20                 |
| Leaf-3  | 2960         | Leaf Switch  | L2 access, hosts VLAN 30                 |
| Leaf-4  | 2960         | Leaf Switch  | L2 access, hosts VLAN 40                 |

---

## IP Scheme

**Spine-to-Spine LAG (Port-Channel 1)**

| Link              | Spine-1 Ports       | Spine-2 Ports       | Port-Channel |
|-------------------|---------------------|---------------------|--------------|
| Spine-1 ↔ Spine-2 | Gi1/0/5, Gi1/0/6    | Gi1/0/5, Gi1/0/6    | Po1          |

**Spine-to-Leaf Trunk Uplinks (Single Gig)**

| Link              | Spine Port  | Leaf Port | VLANs Allowed |
|-------------------|-------------|-----------|---------------|
| Spine-1 ↔ Leaf-1  | Gi1/0/1     | Gi0/1     | 10            |
| Spine-1 ↔ Leaf-2  | Gi1/0/2     | Gi0/1     | 20            |
| Spine-1 ↔ Leaf-3  | Gi1/0/3     | Gi0/1     | 30            |
| Spine-1 ↔ Leaf-4  | Gi1/0/4     | Gi0/1     | 40            |
| Spine-2 ↔ Leaf-1  | Gi1/0/1     | Gi0/2     | 10            |
| Spine-2 ↔ Leaf-2  | Gi1/0/2     | Gi0/2     | 20            |
| Spine-2 ↔ Leaf-3  | Gi1/0/3     | Gi0/2     | 30            |
| Spine-2 ↔ Leaf-4  | Gi1/0/4     | Gi0/2     | 40            |

**LAN Subnets and SVIs**

| Leaf   | VLAN | Subnet           | Spine-1 SVI    | Spine-2 SVI    | PC Access Port |
|--------|------|------------------|----------------|----------------|----------------|
| Leaf-1 | 10   | 192.168.10.0/24  | 192.168.10.1   | 192.168.10.2   | Fa0/1          |
| Leaf-2 | 20   | 192.168.20.0/24  | 192.168.20.1   | 192.168.20.2   | Fa0/1          |
| Leaf-3 | 30   | 192.168.30.0/24  | 192.168.30.1   | 192.168.30.2   | Fa0/1          |
| Leaf-4 | 40   | 192.168.40.0/24  | 192.168.40.1   | 192.168.40.2   | Fa0/1          |

**Loopback Addresses**

| Device  | Loopback | IP          |
|---------|----------|-------------|
| Spine-1 | Lo0      | 10.0.0.1/32 |
| Spine-2 | Lo0      | 10.0.0.2/32 |

**PC Addressing**

| PC   | IP Address    | Gateway      |
|------|---------------|--------------|
| PC-1 | 192.168.10.10 | 192.168.10.1 |
| PC-2 | 192.168.20.10 | 192.168.20.1 |
| PC-3 | 192.168.30.10 | 192.168.30.1 |
| PC-4 | 192.168.40.10 | 192.168.40.1 |

---

## Concepts Covered

| Concept | Description |
|---|---|
| Spine-Leaf Topology | Two-tier fabric where every leaf connects to every spine for redundant paths |
| LAG / EtherChannel | Two physical links between the spines bundled into a single logical Port-Channel for redundancy and increased bandwidth |
| LACP (802.3ad) | Dynamic Link Aggregation Control Protocol used to negotiate and maintain the spine-to-spine port-channel |
| Port-Channel Best Practice | Trunk mode and allowed VLANs configured on the Po1 interface; physical member ports inherit settings automatically |
| SVI (Switched Virtual Interface) | Layer 3 VLAN interfaces on the spine switches providing inter-VLAN routing and default gateways for each subnet |
| Inter-VLAN Routing | All routing between VLANs handled at the spine layer via SVIs and `ip routing` |
| VLAN Segmentation | Each leaf isolates its access hosts in a dedicated VLAN, trunked up to both spines |
| Spanning Tree (PVST) | With dual uplinks from each L2 leaf, STP blocks one uplink per VLAN to prevent loops — redundancy is maintained at the spine-to-spine LAG level |

---

## Key Commands

**Verify port-channel status and member links:**
```
show etherchannel summary
```

**Verify LACP neighbor negotiation:**
```
show lacp neighbor
```

**Verify trunk interfaces:**
```
show interfaces trunk
```

**Verify inter-VLAN routing on spine:**
```
show ip route
```

**Verify spanning tree uplink states on a leaf:**
```
show spanning-tree vlan 10
```

**Test end-to-end connectivity across VLANs:**
```
ping 192.168.40.10
```
