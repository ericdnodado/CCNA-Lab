# L3 Inter-VLAN Routing with PAT

## 📌 Objective
Implement inter-VLAN routing using a Layer 3 switch and provide internet access to multiple VLANs using PAT on an edge router.


## 🏗️ Network Design
This lab simulates an enterprise access layer with a Layer 3 switch performing routing between VLANs, and an edge router providing NAT/PAT for external connectivity.

- Layer 3 switch handles VLAN routing (SVIs)
- Router acts as internet edge
- PAT allows multiple VLANs to share a single public IP
- Default route propagated using OSPF
- OSPF used for dynamic route exchange between L3 switch and edge router

---

## 🌐 IP Addressing

| VLAN | Subnet | Gateway |
|------|--------|--------|
| 100   | 192.168.100.0/24 | 192.168.100.1 |
| 101   | 192.168.101.0/24 | 192.168.101.1 |

---

## ⚙️ Key Configurations

### Layer 3 Switch
- Enabled IP routing
- Configured SVIs:
    - interface vlan 100
    - ip address 192.168.100.1 255.255.255.0
 
    - interface vlan 101
    - ip address 192.168.101.1 255.255.255.0


 ### Edge Router (PAT)

ip nat inside source list 1 interface g0/1 overload
ip nat inside source list 2 interface g0/1 overload


### L3 Switch (OSPF)

router ospf 1
network 192.168.100.0 0.0.0.255 area 0
network 192.168.101.0 0.0.0.255 area 0

### Edge Router (Default Route + OSPF)

ip route 0.0.0.0 0.0.0.0 <ISP_NEXT_HOP>

router ospf 1
default-information originate

---

## 🔍 Verification

- ✔ OSPF adjacency established
  - `show ip ospf neighbor`
- ✔ Routes learned dynamically
  - `show ip route`
- ✔ Default route received on L3 switch
- ✔ NAT translations working
  - `show ip nat translations`

---

## ⚠️ Troubleshooting

| Issue | Cause | Fix |
|------|------|-----|
| No default route in L3 switch | Missing default-information originate | Added command |
| No internet access | NAT or ACL issue | Corrected NAT config |
| No OSPF adjacency | Network mismatch | Fixed OSPF network statements |

---

## 📊 Key Takeaways
- OSPF simplifies route management between internal and edge devices
- Default route injection centralizes internet exit
- PAT enables scalable internet access for multiple VLANs
- L3 switching improves performance over ROAS

