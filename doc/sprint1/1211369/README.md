RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1211369 folder
===========================================
(This folder is to be created/edited by the team member 1211369 only)


## 2. Outlet Requirements & Area Calculations 

| Room ID          | Width (m) | Length (m) | Area (m²) | Required Outlets            |
|:-----------------|:----------|:-----------|:----------|:----------------------------|
| **Room 1 & 2**   | 21.73     | 11.19      | 242.94    | 49                          |
| **Room 3 & 4**   | 19.04     | 11.19      | 217.58    | 44                          |
| **Room 5**       | 38.69     | 13.74      | 531.33    | 107                         |
| **Room 6**       | 33.14     | 13.74      | 455.34    | 94                          |
| **Room 7**       | 35.96     | 13.74      | 494.09    | 101                         |
| **Room 8**       | 8.35      | 13.51      | 112.81    | **Infrastructure (IC Hub)** |
| **Room 9 & 11**  | 13.66     | 19.33      | 264.04    | 53                          |
| **Room 10**      | 27.63     | 13.61      | 376.04    | 93                          |
| **Room 12 & 13** | 13.66     | 18.98      | 263.63    | **Infrastructure**          |
| **Room 14**      | 13.66     | 13.66      | 186.6     | 38                          |
| **Room 15 & 16** | 18.75     | 27.64      | 518.25    | **Infrastructure**          |
| **Room 17 & 18** | 11.13     | 11.13      | 123.88    | **Infrastructure**          |

> **Calculations Rule:** 2 outlets per 10m² rounded up.
> **Standardization Note:** (*) Measurements averaged or standardized to account for minor measurement variance.



# 2 - Hardware Inventory
| Item                            | Units used |
| :------------------------------ |:----------:|
| Outlets                         |    640     |
| CAT6/CAT6A Cables               |    660     |
| 24-port Patch Panels (ISO 8877) |     2      |
| 48-port Patch Panels (ISO 8877) |     14     |
| Access Points                   |     16     |
| IC (Intermediate Cross-Connect) |     1      |
| HC (Horizontal Cross-Connect)   |     7      |




## 3. Deployment & Justification

### 3.1 Distribution Points (HCs)

* Multiple *Horizontal Cross-Connects (HCs)* are distributed across the floor to ensure balanced coverage and minimize cable lengths.
* A HC is placed in the upper area to serve Rooms 1–8.
* A central HC supports the open area and nearby outlets.
* A lower HC provides coverage for Rooms 15–18.
* Additional HCs are deployed along the right wall due to its large extension, ensuring all cable runs remain within the 90-meter limit.



### 3.2 Cable Pathway Strategy

* The design primarily uses the *underfloor cable raceway* for horizontal cabling.
* Cable distribution follows the perimeter (right and bottom walls), leveraging existing infrastructure.
* Main horizontal lines are used for distribution, with short branch connections to outlets.
* A central vertical line acts as a distribution spine, connecting different horizontal segments.


### 3.3 Wireless Infrastructure (Access Points)

* Access Points (APs) are evenly distributed to ensure full wireless coverage.
* A grid-based placement is used in the central area to avoid dead zones.
* Additional APs are placed near Rooms 1–3 and Room 10 to improve coverage in critical areas.
* All APs are ceiling-mounted and connected to the nearest HC using *CAT7 copper cabling*.


---



## 4. Design Justifications & Hard Rules

* **The 90-Meter Rule:** Placement of the Core Island HC and ceiling-routed backbones ensures all horizontal CAT7 runs are under 90 meters.
* **The 200-Cable Limit:** High-density zones utilize multiple physical enclosures to prevent physical congestion and heat buildup.
* **Island Security:** The Core Island HC is specified as a **secured, NEMA-rated floor cabinet** for public-access protection.
