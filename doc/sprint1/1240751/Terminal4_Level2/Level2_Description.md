RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1240751 folder
===========================================
(This folder is to be created/edited by the team member 1240751 only)

This document describes the **structured cabling project for Terminal 4 – Level 2 (Departures)**.
It complements the main README by detailing the measurements and cabling decisions specific to
Level 2. All work in this folder corresponds to the task **T.1.4 – Terminal 4**.

## 1. Physical environment – Terminal 4 Level 2

- **Building**: Terminal 4 of the imaginary airport.
- **Floor included in this document**:
  - **Level 2 (Departures)** – plan with rooms 1 to 21, an underfloor cable raceway along
    the external walls and the same vertical cable passageway in Room 4, connecting to
    the underground technical passageway through Room 4 on Level 0.
- **Ceiling**: Level 2 has a structural ceiling at 5 m and a dropped (false) ceiling at
  4 m, creating an empty space suitable for cable trays and wireless access points.

## 2. Measurements and specifications – Level 2 (Departures)

### 2.1 Level 2 measurements

<img src="measurements_floor2.png">

Figure 1 - Level 2 measurements and outlet layout (Terminal 4 – Departures)

### 2.2 Level 2 room specifications

| Room Number | Width (m) | Length (m) | Area (m²) | Number of Outlets |
|------------|-----------|------------|-----------|-------------------|
| 1          | 11,67     | 33,33      | 388,61    | 78                |
| 2          | 11,67     | 33,33      | 388,61    | 78                |
| 3          | 11,67     | 10         | 116,7     | N.R               |
| 4          | 11,67     | 20         | 233,4     | 47                |
| 5          | 11,67     | 25         | 291,75    | 59                |
| 6          | 10        | 26,67      | 266,7     | N.R               |
| 7          | 16,67     | 11,67      | 199,54    | 39                |
| 8          | 10        | 26,67      | 266,7     | N.R               |
| 9          | 16,67     | 11,67      | 199,54    | 39                |
| 10         | 21,67     | 15         | 325,05    | 66                |
| 11         | 21,67     | 15         | 308,35    | N.R               |
| 12         | 8,33      | 25         | 207,5     | 42                |
| 13         | 8,33      | 16,67      | 138,83    | 28                |
| 14         | 8,33      | 20         | 166,6     | 34                |
| 15         | 8,33      | 20         | 166,6     | 34                |
| 16         | 8,33      | 20         | 166,6     | 34                |
| 17         | 11,67     | 25         | 291,75    | 54                |
| 18         | 11,67     | 21,07      | 252,8     | 51                |
| 19         | 11,67     | 30         | 350,1     | 71                |
| 20         | 11,67     | 21,07      | 252,8     | 51                |
| 21         | 11,67     | 21,07      | 252,8     | 51                |

*Note: The number of outlets for each room is determined by the area ratio, requiring two outlets
for every 10 m² of area.*

*Exceptions and special uses on Level 2:*
- **Rooms 3, 6, 8, 10 and 11** do not require outlets (N.R) according to the project
  description; they are used as technical or support spaces.
- **Room 3** is used to house the **Horizontal Cross‑Connect for Level 2 (HC2)**, connected
  via optical fibre to the IC/HC0 rack in Room 4 on Level 0 through the vertical
  passageway.

## 3. Cabling system – Level 2 (Departures)

### 3.1 Cross‑connects and hierarchy

- **Intermediate Cross‑Connect (IC) – Room 4, Level 0**
  - Located in Room 4 on Level 0 (see main README), connecting Terminal 4 to the campus
    main cross‑connect through optical fibre in the underground technical passageway.

- **Horizontal Cross‑Connect for Level 2 (HC2) – Room 3, Level 2**
  - Copper CAT7 patch panels terminate all horizontal cables from the outlets and Wi‑Fi
    access points on Level 2.
  - HC2 is housed in a telecommunications enclosure in Room 3.
  - HC2 is connected to the IC/HC0 rack in Room 4 Level 0 by multimode optical fibre along
    the vertical passageway.

### 3.2 Cable types

- **Horizontal cabling**: copper **CAT7** cables, maximum 90 m per link between HC2 and
  each outlet or access point.
- **Backbone cabling**: multimode optical fibre between: