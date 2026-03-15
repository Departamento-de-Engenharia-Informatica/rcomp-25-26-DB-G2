RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1240751 folder
===========================================
(This folder is to be created/edited by the team member 1240751 only)

This document describes the **structured cabling project for Terminal 4**, focused on the
two floors assigned in the sprint backlog: **Level 0 (Arrivals)** and **Level 2 (Departures)**.
All work in this folder corresponds to the task **T.1.4 – Terminal 4**.


## 1. Physical environment – Terminal 4

- **Building**: Terminal 4 of the imaginary airport.
- **Floors included in Sprint 1**:
  - **Level 0 (Arrivals)** – plan with rooms 1 to 16, an underfloor cable raceway and a
    vertical cable passageway in Room 4 that connects to the underground technical
    passageway.
  - **Level 2 (Departures)** – plan with rooms 1 to 21, an underfloor cable raceway along
    the external walls and the same vertical cable passageway in Room 4, connecting to
    the underground technical passageway.
- **Ceilings**: both levels have a ceiling at 5 m and a dropped (false) ceiling at 4 m,
  creating an empty space suitable for cable trays and wireless access points.


## 2. Measurements and specifications – Level 0 (Arrivals)

### 2.1 Level 0 measurements

<img src="1240751\measurements_floor0.png">

Figure 1 - Level 0 measurements (Terminal 4 – Arrivals)

### 2.2 Level 0 room specifications

| Room Number | Width (m) | Length (m) | Area (m²) | Number of Outlets |
|------------|-----------|------------|-----------|-------------------|
| 1          | 10.87     | 32.61      | 354.5     | 71                |
| 2          | 10.87     | 30.43      | 330.8     | 67                |
| 3          | 10.87     | 26.09      | 283.6     | 57                |
| 4          | 10.87     | 10.87      | 118.2     | N.R               |
| 5       | 10.87     | 19.57      | 206.85    | 42                |
| 6      | 10.87     | 28.26      | 307.19    | 62                |
| 7      | 10.87     | 23.91      | 259.90    | 52                |
| 8      | 10.87     | 26.09      | 283.6     | N.R               |
| 9      | 10.87     | 26.09      | 283.6     | N.R               |
| 10     | 21.74     | 13.04      | 283.49    | N.R               |
| 11     | 21,74     | 13,04      | 259,90    | N.R               |
|12| 13,04     | 23,91      | 311,79    | 63                |
|13| 13,04     | 21,74      | 283,49    | 57                |
|14| 13,04     | 30,43      | 396,81    | 80                |
|15| 13,04     | 21,74      | 283,49    | 57                |
|16| 13,04     | 21,74      | 283,49    | 57                |

*Note: The number of outlets for each room is determined by the area ratio, requiring two outlets
for every 10 m² of area.*

*Exceptions and special uses on Level 0:*
- **Rooms 8, 9, 10 and 11**: according to the project description they do not require network
  outlets (N.R), so only the horizontal cabling passing nearby is considered.
- **Room 4**: this room does not have user outlets and is used to house the **Intermediate
  Cross‑Connect (IC)** and the Level 0 **Horizontal Cross‑Connect (HC0)**, as well as the
  vertical cable passageway to the underground technical passage.


## 3. Cabling system – Level 0 (Arrivals)

### 3.1 Cross‑connects and hierarchy

- **Intermediate Cross‑Connect (IC) – Room 4, Level 0**
  - Located in Room 4, sharing a telecommunications rack with HC0.
  - Connects Terminal 4 to the campus **main cross‑connect** through optical fibre in the
    underground technical passageway.

- **Horizontal Cross‑Connect for Level 0 (HC0) – Room 4**
  - Copper CAT7 patch panels terminate all horizontal cables from the outlets and Wi‑Fi
    access points on Level 0.
  - HC0 is connected to the IC through short patch cords inside the same rack.

### 3.2 Cable types

- **Horizontal cabling**: copper **CAT7** cables, maximum 90 m per link between HC0 and
  each outlet or access point.
- **Backbone cabling**: multimode optical fibre between:
  - IC in Room 4 and the campus backbone (via underground technical passageway).
  - IC/HC0 in Room 4 and the **Horizontal Cross‑Connect on Level 2 (HC2)**.

### 3.3 Horizontal pathways

- The **underfloor cable raceway** (marked in the plan) is used as the main horizontal
  pathway on Level 0.
- From HC0, bundles of CAT7 cables run through the raceway along the external walls and
  corridors.
- At each **floor cable passageway** the cables can:
  - rise directly into the room and up inside the wall to reach wall‑mounted outlets, or
  - rise to the false ceiling, follow ceiling trays above the rooms and then drop down to
    wall outlets, columns or floor boxes in open areas or between doors.

### 3.4 Outlets grouping and distribution

- The number of RJ45 ports per room is given in the table above. For the physical layout:
  - Outlets are grouped in **clusters of four RJ45 ports**, implemented as two adjacent
    double sockets.
  - Clusters are distributed mainly along the **perimeter walls** of each room with a
    typical spacing of **3–4 m**, denser on the longer walls where more work positions are
    expected.
  - In large rooms (for example Rooms 1, 2, 3 and 14) the clusters cover all walls in order
    to provide flexibility for desks and counters anywhere along the perimeter.
  - In open corners or between doors where there is no continuous wall, clusters are
    implemented as **floor boxes or ceiling‑drop poles**, still fed from the underfloor
    raceway.


## 4. Wireless LAN – Level 0 (Arrivals)

- Wireless coverage is provided using **12 Wi‑Fi access points** installed in the space
  above the false ceiling.
- The access points are distributed to guarantee overlapping coverage of all passenger and
  service areas:
  - Two APs above the block of Rooms **1–3**.
  - Three APs above the block of Rooms **5–7** and the adjacent corridor.
  - Three APs in the **central arrivals hall**, roughly spaced every 35–45 m.
  - Four APs above the block of Rooms **12–16**, including one shifted towards Room 16 to
    cover the isolated right‑hand block.
- Cables for the APs follow the same pattern as outlets: HC0 → underfloor raceway →
  floor passageway → false ceiling → AP.
- RF interference is controlled by assigning different **non‑overlapping channels** to
  neighbouring and vertically adjacent APs (channels 1/6/11 at 2.4 GHz and distinct
  channels at 5 GHz).


