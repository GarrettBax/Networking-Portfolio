03 - Small Office/Home Office (SOHO) Network

Click into 03_SOHO_Network and it will provide an option to view raw.
This will allow the file to be downloaded and then it can be opened to review the packet tracer network.


Topology

<img width="847" height="430" alt="image" src="https://github.com/user-attachments/assets/d7f0aa08-20b6-457c-9cf7-35b19f33a99d" />



Wired PCs and the Access Point connect to the switch.
Laptops connect wirelessly via the Access Point.
The SOHO Router connects to a simulated ISP Router representing the WAN.


IP Scheme

| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| SOHO Router G0/1 (LAN) | 192.168.1.1 | 255.255.255.0 | N/A |
| SOHO Router G0/0 (WAN) | 203.0.113.1 | 255.255.255.252 | 203.0.113.2 |
| ISP Router G0/0 | 203.0.113.2 | 255.255.255.252 | N/A |
| PC0 – PC2 | DHCP assigned | 255.255.255.0 | 192.168.1.1 |
| Laptop0 – Laptop1 | DHCP assigned | 255.255.255.0 | 192.168.1.1 |

> All end devices receive their IP address automatically via DHCP from the SOHO Router.


Concepts Covered

| Concept | Description |
|---|---|
| DHCP | Router automatically assigns IP addresses to all wired and wireless devices |
| NAT/PAT | Internal 192.168.1.0/24 addresses are translated to the single WAN IP for internet access |
| Default Route | Static default route on the SOHO router forwards all unknown traffic to the ISP |
| Wireless (WPA2) | Laptops connect securely to the network via WPA2-PSK on the Access Point |
| Default Gateway | All LAN devices use the router as their exit point for outside traffic |



Key Commands

Verify DHCP assignments on the router:
```
show ip dhcp binding
```

Verify NAT translations after pinging the ISP:
```
show ip nat translations
```

Verify the default route:
```
show ip route
```

Test LAN connectivity:
```
ping 192.168.1.1
```

Test WAN connectivity:
```
ping 203.0.113.2
```
