RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1211920 folder
===========================================

This document describes the **structured cabling project for Terminal 5**, focused on the floor assigned in the sprint backlog: **Level 0 (Arrivals)**. Task **T.1.3 – Terminal 5**.


## 1. Physical environment – Terminal 5

- [cite_start]**Building**: Terminal 5 of the imaginary airport (approx. 400 m × 150 m)[cite: 193].
- **Floors included in Sprint 1**:
  - **Level 0 (Arrivals)** – plan with rooms 1 to 22, an underfloor cable raceway with access points marked on the plan, and **four** vertical cable passageways (at the corners) that connect to the underground technical passageway. [cite_start]Vertical distance from this floor to the underground connection: **3 m**[cite: 200].
- [cite_start]**Ceiling**: Level 0 has a structural ceiling at 5 m and a dropped (false) ceiling at 4 m, creating an empty space suitable for cable trays, wireless access points and other networking hardware[cite: 218, 219].


## 2. Measurements and specifications – Level 0 (Arrivals)

### 2.1 Level 0 measurements

The floor plan with measurements is available in this folder (see the plan image). [cite_start]A larger image is referenced in the project appendix (Figure 10)[cite: 198].

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
- [cite_start]**Rooms 1, 2, 12, 13, 16, 17, 18 and 22**: according to the project description they do not require network outlets (N.R)[cite: 221].
- [cite_start]**Rooms 1, 2, 18 and 22**: as per the guidelines, these rooms at the building's corners are suitable and will be used for housing the network infrastructure hardware (Horizontal Cross-Connects)[cite: 222]. Room 1 also houses the Intermediate Cross-Connect (IC).


## 3. Cabling system – Level 0 (Arrivals)

### 3.1 Architectural Strategy and Cross‑connects hierarchy
[cite_start]Due to the massive scale of Terminal 5 (approx. 400x150 meters) [cite: 193] [cite_start]and the restriction of housing main infrastructure only in the corner rooms[cite: 222], standard horizontal copper cabling would systematically violate the TIA/EIA-568 90-meter length limit. To solve this, a **Fiber-To-The-Zone (FTTZ)** architecture was implemented.

- **Intermediate Cross‑Connect (IC) – Room 1, Level 0**
  - Acts as the main gateway, receiving the Campus Backbone from the underground technical passageway.

- **4 Horizontal Cross‑Connects (HCs) – Rooms 1, 2, 18, 22**
  - The floor is divided into 4 main quadrants. Each designated corner room houses an HC.
  - These 4 HCs are interconnected by a multimode optical fibre ring (Building Backbone) to ensure redundancy.

- **10 Active Consolidation Points (CPs / Telecom Enclosures)**
  - To cover the central areas and large open spaces that exceed 90 meters from any HC, 10 Active CPs (equipped with mini-switches) are strategically deployed in the dropped ceiling and underfloor raceways.

### 3.2 Cable types

- **Horizontal cabling**: copper **CAT7** cables, maximum 90 m per link. These originate either directly from an HC (for nearby rooms) or from an Active CP (for central zones) to each outlet or access point.
- **Backbone cabling**: **OM3 Multimode optical fibre** is used to interconnect the 4 HCs, to link the HCs to the Active CPs, and to provide the vertical link to Level 2. Single-mode OS2 fibre connects the IC to the Campus Backbone.

### 3.3 Horizontal pathways

- The **underfloor cable raceway** (marked in the plan) and the **dropped ceiling** are used as the main horizontal pathways.
- From the HCs, optical fibre travels to the central Active CPs.
- From the HCs and CPs, bundles of CAT7 cables run through the raceways and ceiling trays, dropping down to wall outlets, floor boxes, or Wi-Fi access points.

### 3.4 Outlets grouping and distribution

- The number of RJ45 ports per room is given in the table above.
- Outlets are grouped in **clusters of four RJ45 ports**, implemented as two adjacent double sockets, spaced every 3–4 m along perimeter walls.
- In large rooms (e.g. Rooms 3, 10, 19, 20) and central open spaces, floor-embedded outlets (floor boxes) are utilized via the underfloor raceway.


## 4. Wireless LAN – Level 0 (Arrivals)

- To support the high passenger density typical of an arrivals terminal without causing Co-Channel Interference (CCI), a **High-Density micro-cell Wi-Fi strategy** was implemented.
- Coverage is provided using **26 Wi‑Fi 6 Access Points (APs)** installed in the space above the false ceiling.
- This carefully planned grid ensures that each AP operates at lower transmit power, servicing a localized radius (approx. 20-30 meters), preventing signal overlap on channels 1, 6, and 11 while massively increasing concurrent user capacity.
- APs are distributed across the central corridors, large open waiting areas (like Room 3 and 19), and above rooms without user outlets.