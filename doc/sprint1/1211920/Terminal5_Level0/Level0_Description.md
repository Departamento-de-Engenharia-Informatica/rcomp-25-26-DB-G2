RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1211920 folder
===========================================
(This folder is to be created/edited by the team member 1211920 only)

This document describes the **structured cabling project for Terminal 5**, focused on the floor assigned in the sprint backlog: **Level 0 (Arrivals)**. Task **T.1.3 – Terminal 5**.


## 1. Physical environment – Terminal 5

- **Building**: Terminal 5 of the imaginary airport (approx. 400 m × 150 m).
- **Floors included in Sprint 1**:
  - **Level 0 (Arrivals)** – plan with rooms 1 to 22, an underfloor cable raceway with access points marked on the plan, and **four** vertical cable passageways (at the corners) that connect to the underground technical passageway. Vertical distance from this floor to the underground connection: **3 m**.
- **Ceiling**: Level 0 has a structural ceiling at 5 m and a dropped (false) ceiling at 4 m, creating an empty space suitable for cable trays, wireless access points and other networking hardware.


## 2. Measurements and specifications – Level 0 (Arrivals)

### 2.1 Level 0 measurements

The floor plan with measurements is available in this folder (see the plan image). A larger image is referenced in the project appendix (Figure 10).

### 2.2 Level 0 room specifications

| Room Number | Width (m) | Length (m) | Area (m²) | Number of Outlets |
|-------------|-----------|------------|-----------|-------------------|
| 1           | 11.38     | 11.92      | 135.65    | N.R               |
| 2           | 11.08     | 11.53      | 127.75    | N.R               |
| 3           | —         | —          | 468.71    | 94                |
| 4 & 5       | 14.40     | 21.93      | 315.79    | 64                |
| 6           | 14.40     | 24.65      | 354.96    | 72                |
| 7           | 14.40     | 27.65      | 398.16    | 80                |
| 8           | 14.40     | 25.35      | 365.04    | 74                |
| 9           | 14.40     | 22.33      | 321.55    | 66                |
| 10          | 30.95     | 14.21      | 439.80    | 88                |
| 11          | 29.56     | 13.73      | 405.86    | 82                |
| 12 & 13     | 29.56     | 13.73      | 405.86    | N.R               |
| 14          | 28.05     | 14.12      | 396.07    | 80                |
| 15          | 15.91     | 24.86      | 395.52    | 80                |
| 16          | 13.33     | 27.65      | 368.57    | N.R               |
| 17          | 14.12     | 24.86      | 351.02    | N.R               |
| 18          | 11.85     | 11.63      | 137.82    | N.R               |
| 19          | 33.78     | 13.66      | 461.43    | 94                |
| 20          | 39.19     | 13.66      | 535.34    | 108               |
| 21          | 27.05     | 13.66      | 369.50    | 74                |
| 22          | 11.08     | 11.26      | 124.76    | N.R               |

*Note: The number of outlets for each room is determined by the area ratio, requiring two outlets for every 10 m² of area. Room 3 is composed of two rectangular blocks; total area is given.*

*Exceptions and special uses on Level 0:*
- **Rooms 1, 2, 12, 13, 16, 17, 18 and 22**: according to the project description they do not require network outlets (N.R); rooms 1, 2, 18 and 22 are suitable for housing network infrastructure. Ceiling outlets for Wi‑Fi access points are provided where needed for coverage.
- **Room 1**: houses the **Intermediate Cross‑Connect (IC)** and the Level 0 **Horizontal Cross‑Connect (HC0)**, next to one of the four vertical cable passageways connecting to the underground technical passageway.


## 3. Cabling system – Level 0 (Arrivals)

### 3.1 Cross‑connects and hierarchy

- **Intermediate Cross‑Connect (IC) – Room 1, Level 0**
  - Located in Room 1, sharing a telecommunications rack with HC0.
  - Connects Terminal 5 to the campus **main cross‑connect** through optical fibre in the underground technical passageway (3 m below this floor).

- **Horizontal Cross‑Connect for Level 0 (HC0) – Room 1**
  - Copper CAT7 patch panels terminate all horizontal cables from the outlets and Wi‑Fi access points on Level 0.
  - HC0 is connected to the IC through short patch cords inside the same rack.

### 3.2 Cable types

- **Horizontal cabling**: copper **CAT7** cables, maximum 90 m per link between HC0 and each outlet or access point.
- **Backbone cabling**: multimode optical fibre between:
  - IC in Room 1 and the campus backbone (via underground technical passageway).
  - IC/HC0 in Room 1 and the **Horizontal Cross‑Connect on Level 2 (HC2)** (via one vertical passageway).

### 3.3 Horizontal pathways

- The **underfloor cable raceway** (marked in the plan) is used as the main horizontal pathway on Level 0.
- From HC0, bundles of CAT7 cables run through the raceway along the left and bottom external walls and corridors.
- At each **floor cable passageway** the cables can:
  - rise directly into the room and up inside the wall to reach wall‑mounted outlets, or
  - rise to the false ceiling, follow ceiling trays above the rooms and then drop down to wall outlets or to Wi‑Fi access points.

### 3.4 Outlets grouping and distribution

- The number of RJ45 ports per room is given in the table above. For the physical layout:
  - Outlets are grouped in **clusters of four RJ45 ports**, implemented as two adjacent double sockets.
  - Clusters are distributed mainly along the **perimeter walls** of each room with a typical spacing of **3–4 m**, denser on the longer walls where more work positions are expected.
  - In large rooms (e.g. Rooms 3, 10, 19, 20) the clusters cover all walls to provide flexibility for desks and counters along the perimeter.


## 4. Wireless LAN – Level 0 (Arrivals)

- Wireless coverage is provided using **13 Wi‑Fi access points** (ceiling outlets) installed in the space above the false ceiling.
- The access points are distributed to guarantee overlapping coverage of all passenger and service areas, including:
  - APs in or above rooms 1, 2 and in the corridor; along the left vertical corridor (between room blocks); in or above rooms 12, 13, 16, 17, 18, 22; in the open area to the right of rooms 6, 7, 8; and in the bottom corridor.
- Rooms without user outlets (1, 2, 12, 13, 16, 17, 18, 22) each have at least one AP in or above the room or in the adjacent corridor for full coverage.
- Cables for the APs follow the same pattern as outlets: HC0 → underfloor raceway → floor passageway → false ceiling → AP.
- RF interference is controlled by assigning different **non‑overlapping channels** to neighbouring and vertically adjacent APs.
