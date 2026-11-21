# Project 1: Multi-Router Static Routing Configuration (Cisco IOS)

## Overview
Configured static routes across a **6-router enterprise network topology (R1–R6)** in an emulated lab environment (EVE-NG / QEMU) to enable full end-to-end Layer 3 connectivity across three isolated Windows client LANs (`10.0.0.0/8`, `15.0.0.0/8`, and `162.14.0.0/16`)[cite: 3, 5].

![Network Topology](topology.jpeg)[cite: 3]

---

## Network Addressing & Interface Table

| Device | Interface | IP Address | Connected To |
| :--- | :--- | :--- | :--- |
| **Win-1** | `e0` | `10.0.0.10` | R1 (`e0/0`) |
| **R1** | `e0/0` / `e0/1` | `10.0.0.1` / `20.0.0.1` | Win-1 / R2 (`e0/0`) |
| **R2** | `e0/0` / `e0/1` | `20.0.0.2` / `30.0.0.1` | R1 (`e0/1`) / R3 (`e0/0`) |
| **R3** | `e0/0` / `e0/1` / `e0/2` | `30.0.0.2` / `172.19.0.1` / `21.0.0.1` | R2 (`e0/1`) / R4 (`e0/1`) / R5 (`e0/0`) |
| **R4** | `e0/1` / `e0/0` | `172.19.0.2` / `15.0.0.1` | R3 (`e0/1`) / Win-2 (`e0`) |
| **Win-2** | `e0` | `15.0.0.10` | R4 (`e0/0`) |
| **R5** | `e0/0` / `e0/1` | `21.0.0.2` / `192.168.168.1` | R3 (`e0/2`) / R6 (`e0/1`) |
| **R6** | `e0/1` / `e0/0` | `192.168.168.2` / `162.14.0.1` | R5 (`e0/1`) / Win-3 (`e0`) |
| **Win-3** | `e0` | `162.14.0.10` | R6 (`e0/0`)[cite: 3] |

---

## Key Tasks Performed
* Configured IPv4 addresses and enabled interfaces (`no shutdown`) across routers **R1 through R6**.
* Configured static and default routes (`ip route`) on all intermediate and edge routers to establish bidirectional routing paths across 7 transit and stub subnets.
* Verified end-to-end reachability between all three remote Windows hosts (`Win-1`, `Win-2`, and `Win-3`) with 0% packet loss.

---

## Connectivity Verification (ICMP Ping Results)

### 1. From Win-1 (`10.0.0.10`) → Win-2 (`15.0.0.10`) & Win-3 (`162.14.0.10`)
* **4/4 packets received (0% loss)** across both destination subnets.
![Win-1 Ping Verification](ping-from-win1.jpeg)

### 2. From Win-2 (`15.0.0.10`) → Win-1 (`10.0.0.10`) & Win-3 (`162.14.0.10`)
* **4/4 packets received (0% loss)** across both destination subnets.
![Win-2 Ping Verification](ping-from-win2.jpeg)

### 3. From Win-3 (`162.14.0.10`) → Win-1 (`10.0.0.10`) & Win-2 (`15.0.0.10`)
* **4/4 packets received (0% loss)** across both destination subnets.
![Win-3 Ping Verification](ping-from-win3.jpeg)