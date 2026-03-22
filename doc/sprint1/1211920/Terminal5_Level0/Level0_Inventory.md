## Hardware Inventory – Terminal 5 Level 0 (Arrivals)

| Item                                         | Quantity |
|----------------------------------------------|:--------:|
| RJ45 ports for user outlets                  |  1 076   |
| Outlet groups (4 RJ45 ports per group)       |   269    |
| Wi‑Fi 6 access points                        |    26    |
| RJ45 ports for APs                           |    26    |
| Active Consolidation Points (Enclosures)     |    10    |
| CAT7 horizontal cables                       |  1 102   |
| Total CAT7 horizontal length (approx.)       | ~33.1 km |
| Multimode OM3 Fibre (Backbone + FTTZ links)  | ~1 500 m |
| Fibre pairs IC ↔ campus backbone (OS2)       |    2     |
| Fibre pairs IC/HCs (L0) ↔ HCs (L2)           |    4     |
| Fibre pairs HCs ↔ Active CPs (FTTZ)          |    10    |
| Copper patch panels (24 ports)               |    54    |
| Fibre patch panels (24 ports)                |    5     |
| Telecommunications enclosure Room 1 (IC+HC_A)| 1 × 42U  |
| Telecommunications enclosure Rooms 2, 18, 22 | 3 × 24U  |

### Notes

- Horizontal links use CAT7 copper with a strict maximum length of 90 m per channel. Due to the Fiber-To-The-Zone (FTTZ) architecture employing 10 Active CPs, horizontal copper runs are kept short. An average of **30 m** per link was assumed for length estimation (1 102 cables × 30 m ≈ 33.1 km).
- The 42U rack in Room 1 houses the IC and HC_A. Rooms 2, 18, and 22 use 24U racks to house their respective HCs.
- **Patch Panel Distribution:** The quantity of 24-port copper patch panels accounts for the physical distribution of the network across 4 HCs and multiple Active CPs. A safety margin was added to the absolute minimum mathematical requirement to accommodate partially filled panels at each distributed location.
- **Terminology Note:** To maintain project-wide nomenclature consistency with the team's legends, the distributed active nodes are referred to as "Active Consolidation Points (CPs)". However, strictly according to TIA-568 / ISO 11801 standards, because these points house active switching equipment to support the Fiber-to-the-Zone architecture and overcome the 90m limit, they technically act as **Telecommunications Enclosures (TEs)** or distributed HCs.