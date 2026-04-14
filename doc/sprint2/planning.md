COMP 2025-2026 Project 1 - Sprint 2 planning
===========================================
### Sprint master: 1240729 ###

(This file is to be created/edited by the sprint master only)

---

# 1. Sprint's backlog #

Development of a network simulation using Cisco Packet Tracer, focusing on:
- Layer 2 infrastructure (switching, VLANs, trunks, VTP)
- Layer 3 fundamentals (IPv4 addressing and static routing)

Each team member is responsible for one terminal simulation, including the campus backbone.  
Terminal 3 is additionally responsible for integrating all simulations into a single file.

---

# 2. Technical decisions and coordination #

## Packet Tracer Version
All team members will use:
- **Cisco Packet Tracer version:** 9.0.0

---

## Device Naming Convention

| Device Type | Format Example |
|------------|---------------|
| Switch | SW-T2-F1 |
| Router | R-T3 |
| Access Point | AP-T4 |
| PC | PC-T5-USER |

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
- **Native VLAN:** 749 (SWITCH_DMZ)  
The native VLAN will be used for untagged traffic on trunk links and switch management.

---

## IPv4 Addressing Plan

### Address Space
The team will use the IPv4 block:
- **10.51.0.0/17**

All networks are derived from this block and are non-overlapping.

---

### Global Networks

| Network | Address | Description |
|--------|--------|------------|
| Backbone | 10.51.0.0/24 | Inter-terminal communication |
| Switches DMZ | 10.51.1.0/23 | Switch management |

---

### Router IPs (Backbone)

| Terminal | Router IP |
|--------|-----------|
| T2 | 10.51.0.1 |
| T3 | 10.51.0.2 |
| T4 | 10.51.0.3 |
| T5 | 10.51.0.4 |

---

### VLAN Networks per Terminal

#### Terminal 2

| VLAN | Network | Description |
|------|--------|------------|
| T2_USERS | 10.51.4.0/22 | User outlets |
| T2_WIFI | 10.51.8.0/21 | Wi-Fi |
| T2_VOIP | 10.51.16.0/23 | VoIP |
| T2_SERVERS | 10.51.18.0/25 | Servers |

---

#### Terminal 3

| VLAN | Network | Description |
|------|--------|------------|
| T3_USERS | 10.51.20.0/22 | User outlets |
| T3_WIFI | 10.51.24.0/21 | Wi-Fi |
| T3_VOIP | 10.51.32.0/23 | VoIP |
| T3_SERVERS | 10.51.34.0/25 | Servers |

---

#### Terminal 4

| VLAN | Network | Description |
|------|--------|------------|
| T4_USERS | 10.51.36.0/22 | User outlets |
| T4_WIFI | 10.51.40.0/21 | Wi-Fi |
| T4_VOIP | 10.51.48.0/23 | VoIP |
| T4_SERVERS | 10.51.50.0/25 | Servers |

---

#### Terminal 5

| VLAN | Network | Description |
|------|--------|------------|
| T5_USERS | 10.51.52.0/22 | User outlets |
| T5_WIFI | 10.51.56.0/21 | Wi-Fi |
| T5_VOIP | 10.51.64.0/23 | VoIP |
| T5_SERVERS | 10.51.66.0/25 | Servers |

---

### Address Blocks per Member

| Member | Terminal | Assigned Block |
|--------|---------|----------------|
| Simão Guedes & Martim Penedones | T2 | 10.51.4.0/20 |
| Rita Oliveira | T3 | 10.51.20.0/20 |
| Afonso Simões | T4 | 10.51.36.0/20 |
| Gonçalo Silva | T5 | 10.51.52.0/20 |

---

## Technical Decisions

- All inter-switch links use **trunk mode**
- All VLANs will be propagated to all switches using **VTP**
- STP remains enabled (default)
- Router-on-a-stick will be used for inter-VLAN routing
- Static routing will be used between terminals via the backbone network
- The first usable IP of each VLAN will be used as the default gateway

---

# 3. Subtasks Assignment

Each team member is responsible for developing a complete Layer 2 and Layer 3 network simulation for a specific terminal.

All simulations must include the campus backbone and follow the global planning decisions.

---

### Terminal 2 – T.2.1 (Simão Guedes & Martim Penedones)

- Layer 2 topology implementation
- Campus backbone connection
- VLAN and trunk configuration
- VTP configuration
- Switches DMZ configuration (management IPs)
- IPv4 addressing
- Router configuration (2811, router-on-a-stick)
- Static routing
- Internet connection (DSL modem + ISP router)
- End devices configuration:
  - PC (Users)
  - PC (DMZ)
  - Wi-Fi laptop
  - Server
  - VoIP phone

---

### Terminal 3 – T.2.2 (Rita Oliveira)

- Full Layer 2 and Layer 3 implementation
- Campus backbone connection
- VLAN and trunk configuration
- VTP configuration
- Switches DMZ configuration
- IPv4 addressing
- Router configuration
- Static routing
- End devices configuration

**Additional responsibilities:**
- Integration into **campus.pkt**
- Rebuilding backbone connections
- Ensuring consistency across all terminals

---

### Terminal 4 – T.2.4 (Afonso Simões)

- Layer 2 topology implementation
- Campus backbone connection
- VLAN and trunk configuration
- VTP configuration
- Switches DMZ configuration
- IPv4 addressing
- Router-on-a-stick configuration
- Static routing
- End devices configuration

---

### Terminal 5 – T.2.3 (Gonçalo Silva)

- Layer 2 topology implementation
- Campus backbone connection
- VLAN and trunk configuration
- VTP configuration
- Switches DMZ configuration
- IPv4 addressing
- Router configuration
- Static routing
- End devices configuration

---

## Notes

- All IP ranges are non-overlapping and within the assigned block
- All VLAN IDs are within the required range (748–768)
- All switches use the same VTP domain
- Configurations must be exported regularly