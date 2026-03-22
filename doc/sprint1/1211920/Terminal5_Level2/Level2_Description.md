RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1211920 folder
===========================================

This document describes the **structured cabling project for Terminal 5 – Level 2 (Departures)**.
It complements the main README by detailing the measurements and cabling decisions specific to
Level 2. All work in this folder corresponds to the task **T.1.3 – Terminal 5**.

## 1. Physical environment – Terminal 5 Level 2

- [cite_start]**Building**: Terminal 5 of the imaginary airport (approx. 400 m × 150 m)[cite: 193].
- **Floor included in this document**:
  - [cite_start]**Level 2 (Departures)** – plan with rooms 1 to 26, an underfloor cable raceway along the external walls with access points marked on the plan, and **four** vertical cable passageways (at the corners) connecting to the underground technical passageway via Level 0. Vertical distance from this floor to the underground connection: **15 m**[cite: 232].
- [cite_start]**Ceiling**: Level 2 has a structural ceiling at 5 m and a dropped (false) ceiling at 4 m, creating an empty space suitable for cable trays, wireless access points and other networking hardware[cite: 226, 227].
- [cite_start]**External wall outlets**: One network outlet (ISO 8877) every **5 m** along the **right** external wall and along the **upper** external wall of the plan (30 + 80 = 110 outlets)[cite: 269].

## 2. Measurements and specifications – Level 2 (Departures)

### 2.1 Level 2 measurements

The floor plan with measurements is available in this folder (see the plan image). [cite_start]A larger image is referenced in the project appendix (Figure 11)[cite: 230].

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
- [cite_start]**Rooms 1, 2, 18, 19, 20, 21, 22 and 26** do not require user outlets (N.R)[cite: 266].
- [cite_start]**Rooms 1, 2, 22 and 26**: Located at the building's extremities, these rooms are suitable for housing the network infrastructure hardware (Horizontal Cross-Connects)[cite: 270].
- **External wall outlets**: 30 along the right wall and 80 along the upper wall (one every 5 m), creating a high demand for long-distance connectivity.

## 3. Cabling system – Level 2 (Departures)

### 3.1 Architectural Strategy and Cross‑connects hierarchy
Addressing the 400x150m floor dimensions and the heavy requirement of 110 outlets along the distant external glass walls, a Fiber-To-The-Zone (FTTZ) architecture mirrors the strategy used on Level 0 to respect the 90m copper limit.

- **4 Horizontal Cross‑Connects (HCs) – Rooms 1, 2, 22, 26**
  - Positioned in the designated corner rooms, these 4 HCs divide the departures floor into four management zones.
  - They receive vertical multimode optical fibre links from the IC/HCs located on Level 0.

- **7 Active Consolidation Points (CPs / Telecom Enclosures)**
  - To bridge the geographical gap to the massive departure open-spaces and the continuous line of outlets on the glass wall, 7 Active CPs are deployed.
  - Key CPs are embedded in the underfloor cable raceways along the middle and right-side areas, functioning as FTTZ mini-switches to feed the external wall outlets without exceeding the standard limits.

### 3.2 Cable types

- **Horizontal cabling**: copper **CAT7** cables, maximum 90 m per link between an HC or an Active CP and the final outlet/AP.
- **Backbone cabling**: **OM3 Multimode optical fibre** establishes the vertical building backbone to Level 0 and horizontally feeds the 7 Active CPs from the HCs.

### 3.3 Horizontal pathways

- The **underfloor cable raceway** is vital on Level 2, particularly to serve the 110 external wall outlets.
- From the HCs and CPs, cable bundles enter the underfloor raceway and follow the perimeter.
- At **floor cable passageway** points, cables rise to wall outlets, floor boxes, or to the space above the dropped ceiling for Wi-Fi access points.

### 3.4 Outlets grouping and distribution

- Room outlets are grouped in **clusters of four RJ45 ports** distributed along the perimeter walls.
- External wall outlets are single outlets (ISO 8877) every 5 m along the right and upper walls, heavily relying on the central Active CPs for compliant cable lengths.


## 4. Wireless LAN – Level 2 (Departures)

- Level 2 requires robust wireless LAN coverage for thousands of stationary and waiting passengers.
- A High-Density layout utilizing **27 Wi‑Fi 6 Access Points (APs)** was deployed over the dropped ceiling.
- The distribution is heavily focused on capacity rather than just coverage, establishing micro-cells around the boarding gates (Rooms 23, 24, 25) and the extensive open-space waiting areas along the glass walls.
- Non‑overlapping channels (1, 6, 11) are assigned to neighbouring APs to mitigate Co-Channel Interference (CCI) in this high-density environment.