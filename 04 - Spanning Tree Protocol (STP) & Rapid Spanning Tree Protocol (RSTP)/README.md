04 - Spanning Tree Protocol (STP) & Rapid Spanning Tree Protocol (RSTP)

Click into 04_STP_RSTP and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.

Overview

This file contains two topologies side by side demonstrating the difference between classic STP (PVST) and RSTP (Rapid-PVST). Both topologies show active loop prevention with a blocked port visible in each, and demonstrate reconvergence behavior when a link failure occurs.

Topology
<img width="937" height="619" alt="image" src="https://github.com/user-attachments/assets/f31f5c87-236e-4ebd-b635-6fefd88af7a7" />

IP Scheme

| Device | IP Address | Subnet Mask |
|---|---|---|
| PC0 | 192.168.1.10 | 255.255.255.0 |
| PC1 | 192.168.1.11 | 255.255.255.0 |
| PC2 | 192.168.2.10 | 255.255.255.0 |
| PC3 | 192.168.2.11 | 255.255.255.0 |



Concepts Covered

| Concept | Description |
|---|---|
| STP (PVST) | Classic spanning tree elects a root bridge and blocks redundant ports to prevent loops |
| RSTP (Rapid-PVST) | Improved version of STP with significantly faster reconvergence |
| Root Bridge Election | Switch with lowest priority becomes root bridge (priority set to 4096) |
| Blocked Port | Redundant link placed in blocking state to prevent a Layer 2 loop |
| PortFast | Enabled on all PC-facing ports to skip STP listening/learning states |
| BPDUGuard | Enabled on all PC-facing ports to shut down the port if a BPDU is received, preventing rogue switches |
| Link Failure & Reconvergence | Shutting down a root bridge link shows STP takes 30-50 seconds to recover vs near instant for RSTP |


Key Commands

Verify STP topology and port roles:
```
show spanning-tree
```

Verify PortFast and BPDUGuard on a port:
```
show spanning-tree interface fastethernet 0/3 detail
```

Simulate a link failure on the root bridge:
```
interface fastethernet 0/1
shutdown
```

Test connectivity between PCs:
```
ping 192.168.1.11
ping 192.168.2.11
