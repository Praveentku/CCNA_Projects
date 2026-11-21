# Project 3: Dynamic Routing with EIGRP (AS 10) in PNETLab

## Overview
Configured and verified **EIGRP (Autonomous System 10)** dynamic routing on Cisco IOS routers (**R1**, **R2**, and **R3**) in PNETLab following the `EIGRP.pdf` lab topology[cite: 19, 20, 24, 26]. Checked interface status, established EIGRP neighbor adjacencies, and inspected EIGRP topology and IP routing tables.

---

## Interface & IP Addressing Observed

| Router | Interface | IP Address | Status / Protocol | Reference |
| :--- | :--- | :--- | :--- | :--- |
| **R1** | `Ethernet0/0` | `10.0.0.1` | up / up | `r1-int-brief.jpeg` |
| **R1** | `Ethernet0/1` – `Ethernet0/3` | `unassigned` | administratively down / down | `r1-int-brief.jpeg` |
| **R2** | `Ethernet0/0` | `10.0.0.2` | up / up | `r2-int-brief.jpeg` |
| **R2** | `Ethernet0/1` | `20.0.0.1` | up / up | `r2-int-brief.jpeg |
| **R2** | `Ethernet0/2` | `60.0.0.1` | up / up | `r2-int-brief.jpeg` |
| **R2** | `Ethernet0/3` | `unassigned` | administratively down / down | `r2-int-brief.jpeg` |
| **R3** | `Ethernet0/0` | `20.0.0.2` | up / up | `r3-int-brief.jpeg`[ |
| **R3** | `Ethernet0/1` | `30.0.0.1` | up / up | `r3-int-brief.jpeg`|
| **R3** | `Ethernet0/2` – `Ethernet0/3` | `unassigned` | administratively down / down | `r3-int-brief.jpeg`

---

## Key Configuration & Verification Commands
* **Interface Verification:** `show ip int brief` on `R1`, `R2`, and `R3`
* **EIGRP Configuration:** `router eigrp 10` and `network` statements (`10.0.0.0` on `R1`; `20.0.0.0` and `30.0.0.0` on `R3`)
* **Neighbor Verification:** `show ip eigrp neighbor` (confirmed EIGRP-IPv4 neighbors in AS 10: `10.0.0.2` on `R1` `Et0/0` and `20.0.0.1` on `R3` `Et0/0`)
* **Topology & Routing Verification:** `show ip eigrp topology` and `show ip route

---

## Screenshots & Lab Outputs

### Router R1
* **Interface Status (`show ip int brief`):**
![R1 Interface Brief](r1-int-brief.jpeg)

* **EIGRP Configuration (`router eigrp 10`):**
![R1 EIGRP Config](r1-eigrp-config.jpeg)

* **EIGRP Neighbors (`show ip eigrp neighbor`):**
![R1 EIGRP Neighbor](r1-eigrp-neighbor.jpeg)

* **EIGRP Topology Table (`show ip eigrp topology`):**
![R1 EIGRP Topology](r1-eigrp-topology.jpeg)

* **IP Routing Table (`show ip route`):**
![R1 IP Route](r1-ip-route.jpeg)

### Router R2
* **Interface Status (`show ip int brief`):**
![R2 Interface Brief](r2-int-brief.jpeg)

### Router R3
* **EIGRP Configuration & Neighbor Adjacency (`router eigrp 10`):**
![R3 EIGRP Config](r3-eigrp-config.jpeg)

* **Interface Status (`show ip int brief`):**
![R3 Interface Brief](r3-int-brief.jpeg)

* **EIGRP Neighbors (`show ip eigrp neighbor`):**
![R3 EIGRP Neighbor](r3-eigrp-neighbor.jpeg)

* **EIGRP Topology Table (`show ip eigrp topology`):**
![R3 EIGRP Topology](r3-eigrp-topology.jpeg)