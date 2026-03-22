## Hardware Inventory – Terminal 5 Level 2 (Departures)

| Item                                      |   Quantity   |
|-------------------------------------------|:------------:|
| RJ45 ports for user outlets (rooms)       |    1 404     |
| RJ45 ports for external wall outlets      |     110      |
| Wi‑Fi 6 access points                     |      27      |
| RJ45 ports for APs                        |      27      |
| Outlet groups (4 RJ45 ports per room grp) |     351      |
| Active Consolidation Points (Enclosures)  |      7       |
| CAT7 horizontal cables                    |    1 541     |
| Total CAT7 horizontal length (approx.)    |   ~54.0 km   |
| Multimode OM3 Fibre (Backbone + FTTZ)     |   ~1 200 m   |
| Fibre pairs HCs (L2) ↔ IC/HCs (L0)        |      4       |
| Fibre pairs HCs ↔ Active CPs (FTTZ)       |      7       |
| Copper patch panels (24 ports)            |      74      |
| Fibre patch panels (24 ports)             |      4       |
| Telecommunications enclosure Rooms 1,2,22,26| 4 × 24U    |

### Notes

- Horizontal cabling uses CAT7 copper. Thanks to the 4 HCs and the 7 Active CPs (FTTZ strategy), all runs are strictly kept below 90 m. An average of **35 m** per link was assumed for length estimation (1 541 cables × 35 m ≈ 54.0 km).
- Level 2 receives its core connectivity via the vertical multimode fibre backbone connecting the 4 HCs to the main infrastructure (IC) on Level 0.
- **Patch Panel Distribution:** The quantity of 24-port copper patch panels accounts for the physical distribution of the network across 4 HCs and 7 Active CPs. A safety margin was added to the absolute minimum mathematical requirement to accommodate partially filled panels at each distributed location.
- **Terminology Note:** To maintain project-wide nomenclature consistency with the team's legends, the distributed active nodes are referred to as "Active Consolidation Points (CPs)". However, strictly according to TIA-568 / ISO 11801 standards, because these points house active switching equipment to support the Fiber-to-the-Zone architecture and overcome the 90m limit, they technically act as **Telecommunications Enclosures (TEs)** or distributed HCs.