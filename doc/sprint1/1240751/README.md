RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1240751 folder
===========================================
(This folder is to be created/edited by the team member 1240751 only)

# Cabling Infrastructure Plan: Terminal 4 Layout

- Terminal 4 is covered on **Level 0 (Arrivals)** and **Level 2 (Departures)**. Both levels require wireless LAN coverage (Wi‑Fi).
- The **Intermediate Cross‑Connect (IC)** and **Horizontal Cross‑Connect for Level 0 (HC0)** share the telecommunications enclosure in **Room 4, Level 0**. The **Horizontal Cross‑Connect for Level 2 (HC2)** is in **Room 3, Level 2**.
- Backbone cabling uses **Monomode 10** optical fibre (campus backbone and vertical link between IC/HC0 and HC2).

---

## Description of Level 0

- Level 0 has rooms 1–16 with an underfloor cable raceway and a vertical passageway in Room 4.
- Room 4 houses the IC and HC0 (no user outlets in that room per project rules).

### Level 0 Measurements – Outlet Requirements

See `Terminal4_Level0/Level0_Description.md` for the full room table and dimensions.

> **Note on calculations:** Outlet counts follow **two RJ45 ports per 10 m²** of area (rounded up), with the exceptions listed in the Level 0 description.

---

# Level 0 – Hardware Inventory

| Item                             | Units used |
|:---------------------------------|:----------:|
| Outlets (RJ45 user ports)        |     665    |
| CAT7 Cables                      |     682    |
| Monomode 10                      |     4\*    |
| 24-port Patch Panels  (ISO 8877) |     2      |
| 48-port Patch Panels  (ISO 8877) |     16     |
| Access Points                    |     17     |
| IC (Intermediate Cross-Connect)  |     1      |
| HC (Horizontal Cross-Connect)    |     1      |
| Telecommunication Enclosures     |     1      |

\*Monomode 10 fibre runs: 2 pairs IC ↔ campus backbone and 2 pairs IC/HC0 (L0) ↔ HC2 (L2), as in the detailed inventory.

### Notes

- Patch panel counts are chosen so that **24‑port + 48‑port** capacity covers all horizontal CAT7 runs at HC0 plus IC termination, with spare ports for dressing and future use.

---

## Telecommunication Enclosure Sizes (Room 4, Level 0 – IC + HC0)

In **Room 4**, the telecommunications enclosure stores the following equipment:

| Item                      | Units used | Total U Patch Panels (U) |
|---------------------------|:----------:|:------------------------:|
| HC (24-port Patch Panel)  |     1      |            1             |
| HC (48-port Patch Panel)  |     14     |           28             |
| IC (24-port Patch Panel)  |     1      |            1             |
| IC (48-port Patch Panel)  |     2      |            4             |
| **Total**                 |  **18**    |          **34**          |

Each **48‑port** patch panel occupies **2U**; each **24‑port** patch panel occupies **1U**.

The total space required for patch panels is **S = 34U**.

According to the project guidelines, the same space must be reserved for active equipment and an additional 100% oversize must be considered for future expansion.

Therefore:

Required rack space = 4 × S  
Required rack space = 4 × 34U  
Required rack space = **136U**

Considering that standard racks are commonly available with **48U**, the infrastructure requires **3** telecommunications racks (**48U** each) for the Level 0 cross‑connect area.

---

## Level 0 – Cable Lengths

| Level | CAT7 copper cable | Monomode 10 optic fibre cable |
|:-----:|:-----------------:|:-----------------------------:|
|   0   |     ~12 900 m     |            (see pairs)        |

*Notes:*

- The total copper length is estimated from the number of horizontal links and an assumed average run length (~40 m per link for Level 0), rounded for procurement.

---

## Description of Level 2

- Level 2 has rooms 1–21 with an underfloor raceway; HC2 is in **Room 3**.

### Level 2 Measurements – Outlet Requirements

See `Terminal4_Level2/Level2_Description.md` for the full room table.

> **Note on calculations:** Same rule as Level 0: **two RJ45 ports per 10 m²** (rounded up), with exceptions in the Level 2 description.

---

# Level 2 – Hardware Inventory

| Item                             | Units used |
|:---------------------------------|:----------:|
| Outlets (RJ45 user ports)        |     856    |
| CAT7 Cables                      |     869    |
| Monomode 10                      |     0\*\*  |
| 24-port Patch Panels  (ISO 8877) |     6      |
| 48-port Patch Panels  (ISO 8877) |     16     |
| Access Points                    |     13     |
| IC (Intermediate Cross-Connect)  |     0      |
| HC (Horizontal Cross-Connect)    |     1      |
| Telecommunication Enclosures     |     1      |

\*\*Vertical/backbone Monomode pairs to IC/HC0 are counted at Level 0.

### Notes

- **6 × 24‑port** and **16 × 48‑port** panels at HC2 provide **912** RJ45 ports (≥ **869** horizontal links).

---

## Telecommunication Enclosure Sizes (Room 3, Level 2 – HC2)

In **Room 3**, the telecommunications enclosure stores the following equipment:

| Item                      | Units used | Total U Patch Panels (U) |
|---------------------------|:----------:|:------------------------:|
| HC (24-port Patch Panel)  |     6      |            6             |
| HC (48-port Patch Panel)  |     16     |           32             |
| **Total**                 |  **22**    |          **38**          |

The total space required for patch panels is **S = 38U**.

According to the project guidelines, the same space must be reserved for active equipment and an additional 100% oversize must be considered for future expansion.

Therefore:

Required rack space = 4 × S  
Required rack space = 4 × 38U  
Required rack space = **152U**

Considering that standard racks are commonly available with **48U**, the infrastructure requires **4** telecommunications racks (**48U** each) for the Level 2 horizontal cross‑connect area.

---

## Level 2 – Cable Lengths

| Level | CAT7 copper cable | Monomode 10 optic fibre cable |
|:-----:|:-----------------:|:-----------------------------:|
|   2   |     ~23 400 m     |              —                |

*Notes:*

- Copper length is estimated from horizontal link count and an average run (~35–40 m per link), rounded for procurement.

---

### Cabling System (summary)

- Hierarchical star topology: **IC** in Room 4 Level 0 connects to the campus backbone; **HC0** and **HC2** terminate horizontal CAT7; **Monomode 10** links IC/HC0 to HC2 vertically.
- CAT7 horizontal cabling is limited to **90 m** per channel.
- Patch panels terminate horizontal cabling; patch cords connect panels to switches inside the enclosures.

### Access Points

- **Level 0:** **17** Wi‑Fi access points (ceiling) for arrivals coverage.
- **Level 2:** **13** Wi‑Fi access points for departures coverage.

---

## Total Cable Lengths (Terminal 4)

| Terminal | CAT7 copper cable | Monomode 10 optic fibre cable |
|:--------:|:-----------------:|:-----------------------------:|
|    4     |     ~36 300 m     |         (backbone pairs)      |

*Notes:*

- Copper total is the sum of the Level 0 and Level 2 horizontal plant estimates.
- Monomode lengths follow building backbone and vertical paths defined in the Level 0 description and inventories.

---

## Total Hardware Inventory (Terminal 4)

| Item                             | Units used |
|:---------------------------------|:----------:|
| Outlets (RJ45 user ports)        |    1 521   |
| CAT7 Cables                      |    1 551   |
| Monomode 10 (pair runs, L0 inv.) |      4     |
| 24-port Patch Panels  (ISO 8877) |      8     |
| 48-port Patch Panels  (ISO 8877) |     32     |
| Access Points                    |     30     |
| IC (Intermediate Cross-Connect)  |      1     |
| HC (Horizontal Cross-Connect)    |      2     |
| Telecommunication Enclosures     |      2     |
