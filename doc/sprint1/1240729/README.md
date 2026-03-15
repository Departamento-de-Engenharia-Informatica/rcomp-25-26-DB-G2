RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1240729 folder
===========================================
(This folder is to be created/edited by the team member 1240729 only)

# Cabling Infrastructure Plan: Terminal 3 Layout
- The Terminal 3 building has five floors; however, this project will only encompass Level 1 (Departures) and Level 2 (Arrivals). Both the encompassed floors are required to have wireless LAN coverage (WiFi).

## Description of level 1 
- Level 1 is 200x200m and consists of 15 rooms.
- There are also four vertical cable passageways traveling along all the floors of the building, at a lower floor, these vertical cable passageways have a direct connection to the external underground passageway. 
- The vertical distance between this floor and the connection to the external underground passageway is 10 meters.
- Only the rooms  2, 4, 5, 7, 8, 9, 10, 12, 13 and 14 are provided with the standard number of network outlets.

### Level 1 Measurements - Outlet Requirements
| Room ID | Width (m) | Length (m) | Area (m²) | Required Outlets |
| :--- | :--- | :--- | :--- | :--- |
| **Room 1** | 9.50 | 14.80 | 140.60| not required |
| **Room 2 & 4 & 7** | 14.30 | 19.0 | 271.70 | 54 |
| **Room 3 & 6** | 17.10 | 25.2 | 430.92 | not required |
| **Room 5** | 20.5 | 14.3 | 293.15 | 59 |
| **Room 8** | 14.30 | 14.30 | 204.49 | 41 |
| **Room 9** | 14.30 | 16.7 | 238.81 | 48 |
| **Room 10** | 14.3 | 25.2 | 360.36 | 72 |
| **Room 11** | 11.9 | 11.9 | 141.61 | not required |
| **Room 12** | 14.3 | 30.5 | 436.15 | 87 |
| **Room 13** | 14.3 | 33.3 | 476.19 | 95 |
| **Room 14** | 14.3 | 21.4 | 306.02 | 61 |
| **Room 15** | 14.3 | 11.9 | 170.17 | not required |

> **Note on Calculations:** Outlet counts are calculated based on 2 outlets per 10m² and rounded up to the nearest whole unit. 


### Cabling System
- The cables used inside the floor are, as reccomended, copper cables CAT7, with only a Monomode 10 cable being used to connect the Intermediate Cross-Connect to the Horizontal Cross-Connect and this one to the floor above.
- Horizontal Cross-Connect (HC) are distributed in some rooms(1,13,20) and in some walls to to prevent it from exceeding the maximum length of the copper wire.(<=90m)
- The HC connects directly to all the Consolidation Points 
- CAT7 cables were chosen for Terminal 3 because they provide high-speed 10 Gbps transmission, excellent shielding against interference, support distances up to 100 m, and ensure compatibility and scalability for future network upgrades.


### Access Points

- The Access Points are strategically placed in the celling, providing optimal coverage for all the area of the level.

# Hardware Inventory

| Item                             | Units used |
|:---------------------------------|:----------:|
| Outlets                          |     642    |
| CAT7 Cables                      |     658    |
| Monomode 10                      |     3      |
| 24-port Patch Panels  (ISO 8877) |     1      |
| 48-port Patch Panels  (ISO 8877) |     31     |
| Access Points                    |     16     |
| IC (Intermediate Cross-Connect)  |     3      |
| HC (Horizontal Cross-Connect)    |     9      |
| Telecommunication Enclosures     |     3      |

### Notes: 

- There is 1 HC with a 24-port Patch Panel only.

## Telecommunication Enclosure Sizes

In the **storage room**, the Telecommunication Enclosure stores the following equipment:

| Item                      | Units used | Total U Patch Pannels (U) |
|---------------------------|:----------:|:------------------------:|
| HC (24-port Patch Panel)  |    4       |            4             | 
| HC (48-port Patch Panel)  |    15      |           30             | 
| IC (24-port Patch Panel)  |    1       |            1             |
| IC (48-port Patch Panel)  |    16      |           32             |
| **Total**                 |  **36**    |          **67**          |

The total space required for patch panels is S = 67U.
According to the project guidelines, the same space must be reserved for active equipment and an additional 100% oversize must be considered for future expansion.

Therefore:

Required rack space = 4 × S
Required rack space = 4 × 67U
Required rack space = 268U

Considering that standard racks are commonly available with 48U, the infrastructure requires 6 telecommunications racks (48U each).



## Cable Lengths-Level 1

|  Level  | CAT7 copper cable | Monomode 10 optic fiber cable |
|:-------:|:-----------------:|:-----------------------------:|
|    1    |       5000m       |              6 m              |

*Notes:*
- The total cable length is the sum of all cable lengths used in the building.
- The total quantity is rounded in excess, to ensure that there is enough cable to cover the entire building.

---

## Description of level 2 
- Level 2 is 200x200m and consists of 20 rooms.
- The vertical distance between this floor and the connection to the external underground passageway is 16 meters.
- Only the rooms 2, 3, 4, 7, 10, 11, 12, 14, 15, 16, 17, 18 and 19 are provided with the standard number of network outlets.

### Level 2 Measurements- Outlet Requirements
| Room ID | Width (m) | Length (m) | Area (m²) | Required Outlets |
| :--- | :--- | :--- | :--- | :--- |
| **Room 1** | 9.20 | 14.70 | 135.24 | not required |
| **Room 2 & 4** | 13.80 | 24.50 | 338.10 | 68 |
| **Room 3** | 42.00 | 14.00 | 604.80 |121 |
| **Room 5 & 8** | 16.00 | 23.00 | 368.00 | not required |
| **Room 6 & 9** | 16.90 | 14.40 | 243.36 | not required |
| **Room 7** | 27.60 | 13.80 | 380.88 | 76 |
| **Room 10** | 44.50 | 14.70 | 654.15 | 130 |
| **Room 11** | 15.30 | 23.00 | 351.90 | 70 |
| **Room 12** | 15.30 | 19.60 | 299.88 | 60 |
| **Room 13** | 11.70 | 11.70 | 136.89 | not required |
| **Room 14** | 14.40 | 33.70 | 458.28 | 97 |
| **Room 15** | 14.40 | 39.00 | 561.60 | 112 |
| **Room 16** | 14.40 | 27.60 | 397.44 | 80 |
| **Room 17** | 14.40 | 24.50 | 352.80 | 70 |
| **Room 18** | 14.40 | 33.70 | 485.28 | 97 |
| **Room 19** | 14.40 | 23.00 | 331.20 | 66 |
| **Room 20**| 14.40 | 11.7 | 168.48 | not required |

> **Note on Calculations:** Outlet counts are calculated based on 2 outlets per 10m² and rounded up to the nearest whole unit. 

---
### Cabling System

- The cables used inside the floor are, as reccomended, copper cables CAT7, with only a Monomode 10 cable being used to connect the Intermediate Cross-Connect to the Horizontal Cross-Connect and this one to the floor above.
- Horizontal Cross-Connect (HC) are distributed in some rooms(1,13,20) and in some walls to to prevent it from exceeding the maximum length of the copper wire.(<=90m)
- The HC connects directly to all the Consolidation Points
- CAT7 cables were chosen for Terminal 3 because they provide high-speed 10 Gbps transmission, excellent shielding against interference, support distances up to 100 m, and ensure compatibility and scalability for future network upgrades. 


### Access Points

- The Access Points are strategically placed in the celling, providing optimal coverage for all the area of the level.



# Hardware Inventory

| Item                             | Units used |
|:---------------------------------|:----------:|
| Outlets                          |     1047   |
| CAT7 Cables                      |     1063   |
| Monomode 10                      |     3      |
| 24-port Patch Panels  (ISO 8877) |     6      |
| 48-port Patch Panels  (ISO 8877) |     24     |
| Access Points                    |     16     |
| IC (Intermediate Cross-Connect)  |     3      |
| HC (Horizontal Cross-Connect)    |     11     |
| Telecommunication Enclosures     |     3      |

### Notes: 

- There is 1 HC with a 24-port Patch Panel only.

## Telecommunication Enclosure Sizes

In the **storage room**, the Telecommunication Enclosure stores the following equipment:

| Item                      | Units used | Total U Patch Pannels (U) |
|---------------------------|:----------:|:------------------------:|
| HC (24-port Patch Panel)  |    6       |            6             | 
| HC (48-port Patch Panel)  |    24      |           48             | 
| IC (48-port Patch Panel)  |    27      |           54             |
| **Total**                 |  **57**    |          **108**          |

The total space required for patch panels is S = 108U.
According to the project guidelines, the same space must be reserved for active equipment and an additional 100% oversize must be considered for future expansion.

Therefore:

Required rack space = 4 × S
Required rack space = 4 × 108U
Required rack space = 432U

Considering that standard racks are commonly available with 48U, the infrastructure requires 9 telecommunications racks (48U each).



## Cable Lengths-Level 1

|  Level  | CAT7 copper cable | Monomode 10 optic fiber cable |
|:-------:|:-----------------:|:-----------------------------:|
|    1    |      7000 m       |              2 m             |

*Notes:*
- The total cable length is the sum of all cable lengths used in the building.
- The total quantity is rounded in excess, to ensure that there is enough cable to cover the entire building. 

--- 

## Total Cable Lengths

|   Terminal | CAT7 copper cable | Monomode 10 optic fiber cable |
|:----------:|:-----------------:|:-----------------------------:|
|    3       |      120000 m     |             24m               |

*Notes:*
- The total cable length is the sum of all cable lengths used in the building.
- The total quantity is rounded in excess, to ensure that there is enough cable to cover the entire building.
- the distance in between the two floors is 16m, therefore 16m are part of the total sum of the monomode 10 optic fiber cable