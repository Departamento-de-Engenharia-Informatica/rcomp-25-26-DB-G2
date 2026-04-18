
# COMP 2025-2026 Project 1 - Sprint 2 planning
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
  - Core switches (Backbone) → Server
  - Remaining switches → Client

---

## VLAN Plan

| VLAN ID | VLAN Name | Description |
|--------|----------------|------------|
| 748 | BACKBONE | Campus backbone network |
| 749 | SWITCH_DMZ | Switch management network |
| 750 | T2_USERS | Terminal 2 user outlets |
| 751 | T2_WIFI | Terminal 2 Wi-Fi |
| 752 | T2_VOIP | Terminal 2 VoIP |
| 753 | T2_SERVERS | Terminal 2 servers |
| 754 | T3_USERS | Terminal 3 user outlets |
| 755 | T3_WIFI | Terminal 3 Wi-Fi |
| 756 | T3_VOIP | Terminal 3 VoIP |
| 757 | T3_SERVERS | Terminal 3 servers |
| 758 | T4_USERS | Terminal 4 user outlets |
| 759 | T4_WIFI | Terminal 4 Wi-Fi |
| 760 | T4_VOIP | Terminal 4 VoIP |
| 761 | T4_SERVERS | Terminal 4 servers |
| 762 | T5_USERS | Terminal 5 user outlets |
| 763 | T5_WIFI | Terminal 5 Wi-Fi |
| 764 | T5_VOIP | Terminal 5 VoIP |
| 765 | T5_SERVERS | Terminal 5 servers |

- **Default VLAN:** 1  
- **Native VLAN:** 749 (SWITCH_DMZ)  

---

# 3. IPv4 Addressing Plan

## Address Space
- **Total Block:** 10.51.0.0/17 (Range: 10.51.0.0 - 10.51.127.255)

## Global Networks

| Network | Address/Mask | Available IPs | Description |
|--------|--------------|---------------|-------------|
| Backbone | 10.51.0.0/24 | 254 | Inter-terminal (Router IPs: .1, .2, .3, .4) |
| Switches DMZ | 10.51.2.0/23 | 510 | Management (IPs: 10.51.2.1 - 10.51.3.254) |

## VLAN Networks per Terminal (Adjusted for Host Requirements)

### Terminal 2 (Requirement: ~3600 nodes)
| VLAN | Network | Mask | Description |
|------|---------|------|-------------|
| T2_USERS | 10.51.8.0/22 | 255.255.252.0 | User outlets (1022 hosts) |
| T2_WIFI | 10.51.16.0/21 | 255.255.248.0 | Wi-Fi (2046 hosts) |
| T2_VOIP | 10.51.4.0/23 | 255.255.254.0 | VoIP (510 hosts) |
| T2_SERVERS | 10.51.6.0/25 | 255.255.255.128 | Servers (126 hosts) |

### Terminal 3 (Requirement: ~2950 nodes)
| VLAN | Network | Mask | Description |
|------|---------|------|-------------|
| T3_USERS | 10.51.24.0/22 | 255.255.252.0 | User outlets (1022 hosts) |
| T3_WIFI | 10.51.32.0/21 | 255.255.248.0 | Wi-Fi (2046 hosts) |
| T3_VOIP | 10.51.28.0/23 | 255.255.254.0 | VoIP (510 hosts) |
| T3_SERVERS | 10.51.30.0/24 | 255.255.255.0 | Servers (254 hosts) |

### Terminal 4 (Requirement: ~3120 nodes)
| VLAN | Network | Mask | Description |
|------|---------|------|-------------|
| T4_USERS | 10.51.40.0/22 | 255.255.252.0 | User outlets (1022 hosts) |
| T4_WIFI | 10.51.48.0/21 | 255.255.248.0 | Wi-Fi (2046 hosts) |
| T4_VOIP | 10.51.44.0/23 | 255.255.254.0 | VoIP (510 hosts) |
| T4_SERVERS | 10.51.46.0/25 | 255.255.255.128 | Servers (126 hosts) |

### Terminal 5 (Requirement: ~6600 nodes)
| VLAN | Network | Mask | Description |
|------|---------|------|-------------|
| T5_WIFI | 10.51.64.0/20 | 255.255.240.0 | Wi-Fi (4094 hosts) |
| T5_USERS | 10.51.80.0/21 | 255.255.248.0 | User outlets (2046 hosts) |
| T5_VOIP | 10.51.88.0/23 | 255.255.254.0 | VoIP (510 hosts) |
| T5_SERVERS | 10.51.90.0/24 | 255.255.255.0 | Servers (254 hosts) |

---

## Address Blocks per Member

| Member | Terminal | Assigned Block |
|--------|---------|----------------|
| Simão Guedes & Martim Penedones | T2 | 10.51.4.0/20 |
| Rita Oliveira | T3 | 10.51.24.0/20 |
| Afonso Simões | T4 | 10.51.40.0/20 |
| Gonçalo Silva | T5 | 10.51.64.0/19 |

---

## Technical Decisions Summary

- **Trunking:** All inter-switch links are configured in `switchport mode trunk`.
- **VTP:** Automatic propagation of the VLAN database for consistency.
- **Inter-VLAN Routing:** Implemented via Router-on-a-stick (Sub-interfaces on Router 2811).
- **Static Routing:** Manual routing tables for each terminal's blocks via the Backbone.
- **Gateways:** The first usable IP of each subnet will be assigned to the Router's sub-interface.
- **Management:** SSH/HTTP access to switches is restricted to the 10.51.2.0/23 network.

---

# 4. Subtasks Assignment
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