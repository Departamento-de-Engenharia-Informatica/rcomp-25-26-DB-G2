RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1211920 folder
===========================================
(This folder is to be created/edited by the team member 1211920 only)

This document describes the **structured cabling project for Terminal 5 – Level 2 (Departures)**.
It complements the main README by detailing the measurements and cabling decisions specific to
Level 2. All work in this folder corresponds to the task **T.1.3 – Terminal 5**.

## 1. Physical environment – Terminal 5 Level 2

- **Building**: Terminal 5 of the imaginary airport (approx. 400 m × 150 m).
- **Floor included in this document**:
  - **Level 2 (Departures)** – plan with rooms 1 to 26, an underfloor cable raceway along the external walls with access points marked on the plan, and **four** vertical cable passageways (at the corners) connecting to the underground technical passageway via Level 0. Vertical distance from this floor to the underground connection: **15 m**.
- **Ceiling**: Level 2 has a structural ceiling at 5 m and a dropped (false) ceiling at 4 m, creating an empty space suitable for cable trays, wireless access points and other networking hardware.
- **External wall outlets**: One network outlet (ISO 8877) every **5 m** along the **right** external wall and along the **upper** external wall of the plan (30 + 80 = 110 outlets).

## 2. Measurements and specifications – Level 2 (Departures)

### 2.1 Level 2 measurements

The floor plan with measurements is available in this folder (see the plan image). A larger image is referenced in the project appendix (Figure 11).

### 2.2 Level 2 room specifications

| Room Number | Width (m) | Length (m) | Area (m²) | Number of Outlets |
|-------------|-----------|------------|-----------|-------------------|
| 1 & 2       | 12.00     | 12.00      | 144.00    | N.R               |
| 3 & 4       | 14.00     | 17.00      | 238.00    | 48                |
| 5           | 15.00     | 22.00      | 330.00    | 66                |
| 6 & 16      | 28.00     | 13.00      | 364.00    | 74 each           |
| 7           | 16.00     | 25.00      | 400.00    | 80                |
| 8           | 15.00     | 30.00      | 450.00    | 90                |
| 9           | 15.00     | 14.00      | 210.00    | 42                |
| 10          | 16.00     | 30.00      | 480.00    | 96                |
| 11          | 16.00     | 41.00      | 656.00    | 132               |
| 12          | 16.00     | 33.00      | 528.00    | 106               |
| 13          | 16.00     | 38.00      | 608.00    | 122               |
| 14          | 17.00     | 20.00      | 340.00    | 68                |
| 15          | 17.00     | 35.00      | 595.00    | 120               |
| 17          | 16.00     | 24.00      | 384.00    | 78                |
| 18          | 13.48     | 28.00      | 377.37    | N.R               |
| 19          | 14.00     | 24.80      | 347.24    | N.R               |
| 20 & 21     | 29.00     | 14.00      | 406.00    | N.R               |
| 22          | 11.00     | 10.57      | 116.28    | N.R               |
| 23          | 33.79     | 14.00      | 473.02    | 96                |
| 24          | 38.63     | 14.00      | 540.77    | 110               |
| 25          | 27.00     | 14.00      | 378.00    | 76                |
| 26          | 11.62     | 10.00      | 116.22    | N.R               |

*Note: The number of outlets for each room is determined by the area ratio, requiring two outlets for every 10 m² of area.*

*Exceptions and special uses on Level 2:*
- **Rooms 1, 2, 18, 19, 20, 21, 22 and 26** do not require user outlets (N.R) according to the project description; rooms 1, 2, 22 and 26 are suitable for housing network infrastructure. Ceiling outlets for Wi‑Fi access points are provided where needed for coverage.
- **Room 1** houses the **Horizontal Cross‑Connect for Level 2 (HC2)**, connected via optical fibre to the IC/HC0 rack in Room 1 on Level 0 through the vertical passageway.
- **External wall outlets**: 30 along the right wall and 80 along the upper wall (one every 5 m), in addition to the room outlets above.

## 3. Cabling system – Level 2 (Departures)

### 3.1 Cross‑connects and hierarchy

- **Intermediate Cross‑Connect (IC) – Room 1, Level 0**
  - Located in Room 1 on Level 0 (see Level 0 Description), connecting Terminal 5 to the campus main cross‑connect through optical fibre in the underground technical passageway.

- **Horizontal Cross‑Connect for Level 2 (HC2) – Room 1, Level 2**
  - Copper CAT7 patch panels terminate all horizontal cables from the room outlets, external wall outlets, and Wi‑Fi access points on Level 2.
  - HC2 is housed in a telecommunications enclosure in Room 1.
  - HC2 is connected to the IC/HC0 rack in Room 1 Level 0 by multimode optical fibre along the vertical passageway.

### 3.2 Cable types

- **Horizontal cabling**: copper **CAT7** cables, maximum 90 m per link between HC2 and each outlet or access point.
- **Backbone cabling**: multimode optical fibre between HC2 (Level 2) and IC/HC0 (Level 0) in the vertical passageway.

### 3.3 Horizontal pathways

- The **underfloor cable raceway** (marked on the plan) is used as the main horizontal pathway on Level 2.
- From HC2, cable bundles enter the underfloor raceway and follow the raceway along the external perimeter (and internal branches where shown).
- At **floor cable passageway** points, cables rise to wall outlets or to the space above the dropped ceiling for outlet drops and Wi‑Fi access points.
- **External wall outlets** (right and upper walls): cables run in the underfloor raceway along those walls and emerge at 5 m intervals to wall‑mounted outlets.

### 3.4 Outlets grouping and distribution

- Room outlets are grouped in **clusters of four RJ45 ports** (two double sockets), distributed along the perimeter walls of rooms 3–17, 23, 24, 25 with typical spacing of **3–4 m**.
- External wall outlets are single outlets (ISO 8877) every 5 m along the right and upper walls, fed from the perimeter raceway.


## 4. Wireless LAN – Level 2 (Departures)

- Wireless coverage is provided using **13 Wi‑Fi access points** (ceiling outlets) installed in the space above the false ceiling.
- Access points are distributed along the left vertical corridor, in the open areas (including the zone to the right of rooms 6, 7, 8), in or above rooms 18, 19, 20, 21, 22, 26, and in the bottom corridor to ensure full coverage.
- Rooms without user outlets (1, 2, 18, 19, 20, 21, 22, 26) each have at least one AP in or above the room or in the adjacent corridor.
- Cables for the APs: HC2 → underfloor raceway / ceiling tray → AP.
- Non‑overlapping channels are assigned to neighbouring and vertically adjacent APs to reduce interference.
