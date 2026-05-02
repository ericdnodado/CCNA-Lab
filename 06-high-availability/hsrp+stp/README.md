# Enterprise Redundancy Design with HSRP and STP

## 📌 Objective
Design a resilient campus network using STP at Layer 2 and HSRP at Layer 3 to ensure loop-free switching and gateway redundancy.

---

## 🏗️ Network Design
This topology simulates an enterprise campus network with redundant switches and routers:

- STP ensures loop-free Layer 2 topology
- HSRP provides default gateway redundancy per VLAN
- STP root bridge aligned with HSRP active router for optimal traffic flow

---

## 🔄 Design Concept (IMPORTANT)

- STP Root Bridge = Primary distribution switch
- HSRP Active Router = Same distribution layer device
- Goal: Avoid suboptimal routing and asymmetric paths

---

## ⚙️ Key Configurations

### HSRP Configuration

standby 1 ip 192.168.10.1
standby 1 priority 110
standby 1 preempt

---

### STP Configuration (Root Bridge)

spanning-tree vlan 10 root priority 4096

---

## 🔍 Verification

- ✔ HSRP active/standby state:
  - `show standby`
- ✔ STP root bridge:
  - `show spanning-tree`
- ✔ Failover test:
  - Shut primary link → traffic maintained

---

## ⚠️ Issues & Fixes

| Issue | Cause | Fix |
|------|------|-----|
| Suboptimal path | STP root mismatch | Aligned root with HSRP active |
| Gateway failover delay | Missing preempt | Enabled preempt |

---

## 📊 Key Takeaways

- STP controls switching topology, not routing
- HSRP controls gateway availability
- Aligning both improves traffic efficiency and failover behavior





