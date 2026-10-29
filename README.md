# Static Default Routing Lab — Cisco Packet Tracer

**Student:** Gaurav Dhakar  
**Platform:** Cisco Packet Tracer  
**Lab Type:** Static Default Routing

## 1. Topology

![Static Default Routing Lab Topology](screenshots/static-default-routing-topology.jpg)

### Network Devices
- 3 × Cisco 2811 Routers
- 2 × Cisco 2950 Switches
- 2 × PCs

## 2. IP Addressing Table

| Device | Interface | IP Address | Subnet Mask |
|---|---|---|---|
| PC0 | NIC | 192.168.10.2 | 255.255.255.0 |
| Router3 | FastEthernet0/0 | 192.168.10.1 | 255.255.255.0 |
| Router3 | Serial0/0/0 | 192.168.20.1 | 255.255.255.0 |
| Router1 | Serial0/0/1 | 192.168.20.2 | 255.255.255.0 |
| Router1 | Serial0/0/0 | 192.168.30.1 | 255.255.255.0 |
| Router4 | Serial0/0/0 | 192.168.30.2 | 255.255.255.0 |
| Router4 | FastEthernet0/0 | 192.168.40.1 | 255.255.255.0 |
| PC1 | NIC | 192.168.40.2 | 255.255.255.0 |

**Default Gateways**
- PC0: `192.168.10.1`
- PC1: `192.168.40.1`

> Note: Verify these IP addresses and interface numbers against your actual Packet Tracer topology.

## 3. Configure Router3

Router3 connects the left LAN to Router1.

```text
enable
configure terminal
hostname Router3

interface fastEthernet0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit

interface serial0/0/0
ip address 192.168.20.1 255.255.255.0
no shutdown
exit

ip route 0.0.0.0 0.0.0.0 192.168.20.2

end
write memory
```

## 4. Configure Router1

Router1 connects both edge routers.

```text
enable
configure terminal
hostname Router1

interface serial0/0/1
ip address 192.168.20.2 255.255.255.0
no shutdown
exit

interface serial0/0/0
ip address 192.168.30.1 255.255.255.0
no shutdown
exit

ip route 192.168.10.0 255.255.255.0 192.168.20.1
ip route 192.168.40.0 255.255.255.0 192.168.30.2

end
write memory
```

## 5. Configure Router4

Router4 connects the right LAN to Router1.

```text
enable
configure terminal
hostname Router4

interface fastEthernet0/0
ip address 192.168.40.1 255.255.255.0
no shutdown
exit

interface serial0/0/0
ip address 192.168.30.2 255.255.255.0
no shutdown
exit

ip route 0.0.0.0 0.0.0.0 192.168.30.1

end
write memory
```

## 6. Configure PCs

### PC0
Open **Desktop → IP Configuration**.

- IP Address: `192.168.10.2`
- Subnet Mask: `255.255.255.0`
- Default Gateway: `192.168
