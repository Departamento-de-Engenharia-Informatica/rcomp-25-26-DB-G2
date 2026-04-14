RCOMP 2025-2026 Project 1 - Sprint 2 planning
===========================================
### Sprint master: 1240729 ###
(This file is to be created/edited by the sprint master only)
# 1. Sprint's backlog #
(Copy here a summary of the provided sprint's backlog)
# 2. Technical decisions and coordination #
In this section, all technical decisions taken in the planning meeting should be mentioned. 		Most importantly, all technical decisions impacting on the subtasks implementation must be settled on this 		meeting and specified here.

#### Examples: ####
  * Packet Tracer version to be used
  * Devices naming
  * VLAN IDs to be used
  * VTP domains' names
  * IPv4 networks' addresses and routers' addresses

# 3. Subtasks assignment #
(For each team member (sprint master included), the description of the assigned subtask in sprint 2)

## 3. Subtasks Assignment

Each team member is responsible for developing a complete Layer 2 and Layer 3 network simulation for a specific terminal, based on the structured cabling project from Sprint 1. All simulations must include the campus backbone and follow the common planning decisions defined by the team.

---

- **[Member(s) 1222215 & 1211369] – Terminal 2 (T.2.1)**  
  Responsible for developing the Packet Tracer simulation for Terminal 2, including:
  - Implementation of the Layer 2 topology with two switches (one per floor)
  - Configuration of all VLANs (global and terminal-specific)
  - Configuration of trunk links between switches and towards the router
  - VTP configuration (domain and mode)
  - Assignment of IPv4 networks to each VLAN according to requirements
  - Configuration of the router (2811) using router-on-a-stick (subinterfaces)
  - Static routing configuration
  - Implementation of the Internet connection (DSL modem + ISP router)
  - Configuration of end devices (PCs, Wi-Fi, server, VoIP phone)

---

- **[Member 1240729] – Terminal 3 (T.2.2)**  
  Responsible for developing the Packet Tracer simulation for Terminal 3, including:
  - Full Layer 2 and Layer 3 configuration (as described for other terminals)
  - VLAN and VTP configuration
  - IPv4 addressing and subnetting
  - Router configuration and static routing
  - Configuration of end devices

  Additionally responsible for:
  - Integration of all team members’ simulations into a single file (**campus.pkt**)
  - Rebuilding backbone connections between terminals
  - Ensuring consistency across all configurations

---

- **[Member 1240751] – Terminal 4 (T.2.4)**  
  Responsible for developing the Packet Tracer simulation for Terminal 4, including:
  - Layer 2 topology implementation
  - VLAN creation and trunk configuration
  - VTP configuration
  - IPv4 addressing for all VLANs
  - Router-on-a-stick configuration
  - Static routing setup
  - Configuration of required end devices

---

- **[Member 1211920] – Terminal 5 (T.2.3)**  
  Responsible for developing the Packet Tracer simulation for Terminal 5, including:
  - Layer 2 topology implementation
  - VLAN and trunk configuration
  - VTP configuration
  - IPv4 addressing and subnetting
  - Router configuration (subinterfaces)
  - Static routing
  - Configuration of end devices


---
 # Sprint 2 – Planning

## Team Information
- **Sprint Master:** [Rita Oliveira]  
- **Members:**
  - [Simão Guedes & Martim Penedones] – Terminal 2
  - [Rita Oliveira] – Terminal 3
  - [Afonso Simões] – Terminal 4
  - [Gonçalo Silva] – Terminal 5

---

## Packet Tracer Version
All team members will use:
- **Cisco Packet Tracer version:** [a definir ]

---

## VTP Configuration
- **VTP Domain:** `rc2526dbg2`
- **VTP Mode:**
  - Core switches → Server
  - Remaining switches → Client

---

## VLAN Plan

| VLAN ID | VLAN Name        | Description |
|--------|----------------|------------|
| 748 | BACKBONE        | Campus backbone network |
| 749 | SWITCH_DMZ      | Switch management network |
| 750 | T2_USERS        | Terminal 2 user outlets |
| 751 | T2_WIFI         | Terminal 2 Wi-Fi |
| 752 | T2_VOIP         | Terminal 2 VoIP |
| 753 | T2_SERVERS      | Terminal 2 servers |
| 754 | T3_USERS        | Terminal 3 user outlets |
| 755 | T3_WIFI         | Terminal 3 Wi-Fi |
| 756 | T3_VOIP         | Terminal 3 VoIP |
| 757 | T3_SERVERS      | Terminal 3 servers |
| 758 | T4_USERS        | Terminal 4 user outlets |
| 759 | T4_WIFI         | Terminal 4 Wi-Fi |
| 760 | T4_VOIP         | Terminal 4 VoIP |
| 761 | T4_SERVERS      | Terminal 4 servers |
| 762 | T5_USERS        | Terminal 5 user outlets |
| 763 | T5_WIFI         | Terminal 5 Wi-Fi |
| 764 | T5_VOIP         | Terminal 5 VoIP |
| 765 | T5_SERVERS      | Terminal 5 servers |

- **Default VLAN:** 1  
- **Native VLAN:** 749 SWITCH_DMZ
The native VLAN will be VLAN 749 (SWITCH_DMZ), used for switch management and untagged traffic on trunk links.

---

## IPv4 Addressing Plan

### Global Networks

| Network | Address | Description |
|--------|--------|------------|
| Backbone | 10.0.0.0/24 | Inter-terminal communication |
| Switches DMZ | 10.0.1.0/23 | Switch management |

---

### Router IPs (Backbone)

| Terminal | Router IP |
|--------|-----------|
| T2 | 10.0.0.1 |
| T3 | 10.0.0.2 |
| T4 | 10.0.0.3 |
| T5 | 10.0.0.4 |

---

### VLAN Networks per Terminal

#### Terminal 2

| VLAN | Network | Description |
|------|--------|------------|
| T2_USERS | 10.0.4.0/22 | User outlets |
| T2_WIFI | 10.0.8.0/21 | Wi-Fi |
| T2_VOIP | 10.0.16.0/23 | VoIP |
| T2_SERVERS | 10.0.18.0/25 | Servers |

---

#### Terminal 3

| VLAN | Network | Description |
|------|--------|------------|
| T3_USERS | 10.0.20.0/22 | User outlets |
| T3_WIFI | 10.0.24.0/21 | Wi-Fi |
| T3_VOIP | 10.0.32.0/23 | VoIP |
| T3_SERVERS | 10.0.34.0/25 | Servers |

---

#### Terminal 4

| VLAN | Network | Description |
|------|--------|------------|
| T4_USERS | 10.0.36.0/22 | User outlets |
| T4_WIFI | 10.0.40.0/21 | Wi-Fi |
| T4_VOIP | 10.0.48.0/23 | VoIP |
| T4_SERVERS | 10.0.50.0/25 | Servers |

---

#### Terminal 5

| VLAN | Network | Description |
|------|--------|------------|
| T5_USERS | 10.0.52.0/22 | User outlets |
| T5_WIFI | 10.0.56.0/21 | Wi-Fi |
| T5_VOIP | 10.0.64.0/23 | VoIP |
| T5_SERVERS | 10.0.66.0/25 | Servers |

---

### Address Blocks per Member

| Member | Terminal | Assigned Block |
|--------|---------|----------------|
| [Simão Guedes & Martim Penedones] | T2 | 10.0.4.0/20 |
| [Rita Oliveira] | T3 | 10.0.20.0/20 |
| [Afonso Simões] | T4 | 10.0.36.0/20 |
| [Gonçalo Silva] | T5 | 10.0.52.0/20 |

---

## Device Naming Convention

| Device Type | Format Example |
|------------|---------------|
| Switch | SW-T2-F1 |
| Router | R-T3 |
| Access Point | AP-T4 |
| PC | PC-T5-USER |

---

## Technical Decisions

- All inter-switch links use **trunk mode**
- All VLANs must exist on every switch
- STP remains enabled (default)
- Router-on-a-stick will be used for inter-VLAN routing
- Static routing will be used between terminals

---

## Notes

- All IP ranges must be non-overlapping  
- All VLAN IDs must be within range **748–768**  
- All switches must use the same VTP domain  
- Configurations must be exported regularly  