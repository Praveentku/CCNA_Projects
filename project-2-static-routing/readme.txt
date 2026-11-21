# Project 2: Multi-Router Static Routing & Equal-Cost Multipath (ECMP) Load Balancing

## Overview
Configured static routes across a **6-router enterprise network topology (R1–R6)** with redundant parallel transit paths (`R2 → R3 → R5` and `R2 → R4 → R5`) in PNETLab / QEMU[cite: 15, 17]. Implemented equal-cost static routes on edge/distribution routers (`R2` and `R5`) to enable load balancing across both paths while connecting three remote Windows host subnets (`192.50.20.0/24`, `223.0.50.0/24`, and `172.36.0.0/16`)[cite: 14, 17].

![Network Topology](topology.jpeg)

---

## Network Addressing & Interface Table

| Device | Interface | IP Address | Connected To |
| :--- | :--- | :--- | :--- |
| **Win-1** | `e0` | `192.50.20.100` | Switch → R1 (`e0/0`) |
| **R1** | `e0/0` / `e0/1` | `192.50.20.1` / `12.0.0.1` | Win-1 LAN / R2 (`e0/0`)  |
| **R2** | `e0/0` / `e0/1` / `e0/2` / `e0/3` | `12.0.0.2` / `26.0.0.1` / `23.0.0.1` / `24.0.0.1` | R1 / R6 (`e0/1`) / R3 (`e0/0`) / R4 (`e0/0`) |
| **R3** | `e0/0` / `e0/1` | `23.0.0.2` / `32.0.0.1` | R2 (`e0/2`) / R5 (`e0/1`) |
| **R4** | `e0/0` / `e0/1` | `24.0.0.2` / `45.0.0.1` | R2 (`e0/3`) / R5 (`e0/2`) |
| **R5** | `e0/1` / `e0/2` / `e0/0` | `32.0.0.2` / `45.0.0.2` / `172.36.0.1` | R3 (`e0/1`) / R4 (`e0/1`) / Win-3 LAN|
| **Win-3** | `e0` | `172.36.0.10` | Switch → R5 (`e0/0`) |
| **R6** | `e0/1` / `e0/0` | `26.0.0.2` / `223.0.50.1` | R2 (`e0/1`) / Win-2 LAN[|
| **Win-2** | `e0` | `223.0.50.10` | Switch → R6 (`e0/0`) |

---

## Key Tasks Performed
* Configured IPv4 interface addressing and enabled all links across **R1–R6**.
* Configured static routes (`ip route`) across stub, transit, and parallel core routers (`R1` through `R6`).
* Implemented **Equal-Cost Multipath (ECMP)** static routing on `R2` (via next-hops `23.0.0.2` and `24.0.0.2` for `172.36.0.0/16`) and symmetric return paths on `R5`.
* Verified routing tables via `show ip route` on `R1`, `R2`, and `R3`, and confirmed full end-to-end ICMP reachability across all three client subnets with 0% packet loss.

---

## Verification Outputs

### 1. Cisco IOS Routing Tables (`show ip route`)
* **R1 Routing Table:** Static routes pointing to next-hop `12.0.0.2` (`R2`) for all remote networks.
![R1 Routing Table](r1-routing-table.jpeg)

* **R2 Routing Table (ECMP Load Balancing):** Dual equal-cost static routes (`[1/0]`) installed for `172.36.0.0/16` via `24.0.0.2` and `23.0.0.2`.
![R2 Routing Table](r2-routing-table.jpeg)

* **R3 Routing Table:** Transit static routes forwarding traffic toward `12.0.0.0/8`, `192.50.20.0/24`, and `223.0.50.0/24` via `23.0.0.1` and toward `45.0.0.0/8` and `172.36.0.0/16` via `32.0.0.2`.
![R3 Routing Table](r3-routing-table.jpeg)

### 2. End-to-End ICMP Ping Results
* **From Win-1 (`192.50.20.100`) → Win-2 (`223.0.50.10`) & Win-3 (`172.36.0.10`):** 0% packet loss.
![Win-1 Ping Verification](ping-from-win1.jpeg)

* **From Win-2 (`223.0.50.10`) → Win-1 (`192.50.20.100`) & Win-3 (`172.36.0.10`):** 0% packet loss.
![Win-2 Ping Verification](ping-from-win2.jpeg)

* **From Win-3 (`172.36.0.10`) → Win-2 (`223.0.50.10`) & Win-1 (`192.50.20.100`):** 0% packet loss.
![Win-3 Ping Verification](ping-from-win3.jpeg)