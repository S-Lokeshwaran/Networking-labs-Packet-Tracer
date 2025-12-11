# 🌍 Static Routing Lab — Chennai ➜ Bangalore ➜ Thailand ➜ Malaysia

### 📘 Objective
To configure **Static Routing** across four routers (Chennai, Bangalore, Thailand, Malaysia) so that a PC in **Chennai (192.168.10.0/24)** can successfully communicate with a PC in **Malaysia (192.168.20.0/24)**.

---

## 🗺️ Network Topology
> The network consists of four routers connected in series, simulating communication between Chennai, Bangalore, Thailand, and Malaysia.


---

## 💻 Device & IP Address Details

| Router     | Interface | Connected To | IP Address      | Network          |
|-------------|------------|---------------|------------------|------------------|
| **Chennai** | Gi0/2      | LAN           | 192.168.10.1     | 192.168.10.0/24 |
|             | Gi0/1      | Bangalore     | 10.10.10.1       | 10.10.10.0/30   |
| **Bangalore** | Gi0/0   | Chennai       | 10.10.10.2       | 10.10.10.0/30   |
|             | Gi0/1      | Thailand      | 20.20.20.1       | 20.20.20.0/30   |
| **Thailand** | Gi0/0     | Bangalore     | 20.20.20.2       | 20.20.20.0/30   |
|             | Gi0/1      | Malaysia      | 30.30.30.1       | 30.30.30.0/30   |
| **Malaysia** | Gi0/0     | Thailand      | 30.30.30.2       | 30.30.30.0/30   |
|             | Gi0/2      | LAN           | 192.168.20.1     | 192.168.20.0/24 |

---

## ⚙️ Static Routing Configuration

### 🏙️ 1️⃣ Chennai Router
```bash
enable
configure terminal
ip route 192.168.20.0 255.255.255.0 10.10.10.2
ip route 30.30.30.0 255.255.255.0 10.10.10.2
ip route 20.20.20.0 255.255.255.0 10.10.10.2
end
write memory

### 🏢 2️⃣ Bangalore Router

enable
configure terminal
ip route 192.168.10.0 255.255.255.0 10.10.10.1
ip route 192.168.20.0 255.255.255.0 20.20.20.2
ip route 30.30.30.0 255.255.255.0 20.20.20.2
end
write memory


### 🏖️ 3️⃣ Thailand Router

enable
configure terminal
ip route 192.168.10.0 255.255.255.0 20.20.20.1
ip route 10.10.10.0 255.255.255.0 20.20.20.1
ip route 192.168.20.0 255.255.255.0 30.30.30.2
end
write memory



### 🏯 4️⃣ Malaysia Router
enable
configure terminal
ip route 192.168.10.0 255.255.255.0 30.30.30.1
ip route 20.20.20.0 255.255.255.0 30.30.30.1
ip route 10.10.10.0 255.255.255.0 30.30.30.1
end
write memory
