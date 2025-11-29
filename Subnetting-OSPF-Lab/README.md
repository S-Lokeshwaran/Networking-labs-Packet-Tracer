# 🌐 Subnetting & OSPF Multi-Router Network Lab (Cisco Packet Tracer)

## 🧭 Overview

This project is a complete **Subnetting + OSPF multi-router lab** built manually in Cisco Packet Tracer.  
I didn’t use any pre-built `.pkt` file — every router, switch, subnet, and DHCP server was configured from scratch.

The main goal was to understand:
- Subnetting a /24 network into multiple /26 networks
- Configuring IP addressing and interfaces for routers and switches
- Implementing **OSPF (Open Shortest Path First)** for dynamic routing
- Configuring **DHCP servers** for automatic IP allocation
- Troubleshooting end-to-end network connectivity across multiple sites

---

## 🗺️ Network Topology Summary

**Devices used:**
- 3 × Cisco Routers (Router0, Router3, Router2)
- 1 × Multilayer Switch (Layer 3)
- 2 × Layer 2 Switches
- 2 × DHCP Servers
- Multiple PCs for Site 1, Site 2, and extra VLAN subnet

**Subnet Plan:**

| Site / Link | Network | Subnet Mask | Description |
|--------------|----------|-------------|--------------|
| Site 1 LAN | 192.168.1.0/26 | 255.255.255.192 | DHCP + PCs |
| Router0 ↔ Router3 | 192.168.1.64/26 | 255.255.255.192 | Serial Link |
| Site 2 LAN | 192.168.1.128/26 | 255.255.255.192 | DHCP + PCs |
| Router3 ↔ Router2 | 192.168.1.192/26 | 255.255.255.192 | Serial Link |
| Site 4 (L3 Switch VLAN 10) | 192.168.2.0/26 | 255.255.255.192 | VLAN-based subnet |

---

## ⚙️ Router Configurations

### 🖧 Router0 – Site 1 Gateway
```bash
enable
configure terminal
hostname Router0

interface gigabitEthernet0/0/0
 ip address 192.168.1.62 255.255.255.192
 no shutdown
exit

interface serial0/1/0
 ip address 192.168.1.65 255.255.255.192
 clock rate 64000
 no shutdown
exit

router ospf 1
 network 192.168.1.0 0.0.0.63 area 0
 network 192.168.1.64 0.0.0.63 area 0
exit
