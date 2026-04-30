# ROAS + PAT Enterprise Lab

## 📌 Objective
Design and implement a multi-VLAN network with inter-VLAN routing using Router-on-a-Stick (ROAS) and provide internet access using Port Address Translation (PAT).

## 🏗️ Network Design
This lab simulates a small enterprise network where multiple VLANs require internal communication and shared internet access through a single public IP.

- VLAN segmentation for department isolation
- Centralized routing via router subinterfaces
- NAT overload (PAT) for internet connectivity

---

## 🌐 IP Addressing Plan

| VLAN | Subnet | Gateway |
|------|--------|--------|
| 100   | 192.168.100.0/24 | 192.168.100.1 |
| 101   | 192.168.101.0/24 | 192.168.101.1 |

---

## ⚙️ Key Configurations


### Inter-VLAN Routing (ROAS)
- Configured subinterfaces on router:
  - G0/0.100 → VLAN 100
  - G0/0.101 → VLAN 101
- Applied `encapsulation dot1Q`

### NAT (PAT Overload)
- Defined inside and outside interfaces
- Configured ACL for internal networks
- Enabled PAT using:
    - ip nat inside source list 1 interface g0/1 overload

 
## 🔍 Verification & Validation

### ✔ Inter-VLAN Communication
- Successful ping between VLAN 100 and VLAN 101

### ✔ Internet Access
- Internal hosts can reach external network via PAT

### ✔ NAT Operation
- Verified using:
    - show ip nat translations
    - show ip nat statistics


 ## ⚠️ Troubleshooting

| Issue | Cause | Resolution |
|------|------|-----------|
| No VLAN communication | Missing dot1Q encapsulation | Added encapsulation |
| No internet access | NAT not applied correctly | Fixed NAT inside/outside |


## 📊 Key Takeaways
- ROAS enables efficient inter-VLAN routing using a single interface
- PAT allows multiple private hosts to share one public IP
- Proper interface designation (`inside/outside`) is critical for NAT

---

## 📂 Included Files
- Packet Tracer lab file
- Router and switch configurations
- Topology diagram
