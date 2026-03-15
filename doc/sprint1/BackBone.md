# RCOMP 2025-2026 Project 1 - Campus Backbone Infrastructure
===========================================

## 1. Executive Summary: Campus Backbone Design
This document outlines the **Subsystem 3 (Campus Backbone)** infrastructure connecting the Main Cross-connect (MC) to the various terminals (T2, T3, T4, and T5). The design prioritizes **Redundancy** and **Fault Tolerance** to ensure the airport's critical operations are never compromised by a single point of failure.

---

## 2. Backbone Topology & Strategy
To meet international standards for mission-critical infrastructure, the campus utilizes a **Physical Star Topology**.

* **Dedicated Pathways:** Each terminal is served by its own independent fiber optic cable run originating from the MC. This ensures that a cable failure or "crash" in one sector does not affect the connectivity of other terminals.
* **Media Type:** High-count **Singlemode Optical Fiber** is used for all campus backbone runs to support long-distance transmission and high bandwidth capacity between buildings.
* **Star vs. Bus:** While the schematic may appear to show a single path for visual simplicity, the implementation involves separate, discrete cable stretches for every terminal link.

---

## 3. Distance Calculations (Main Fiber Links)
The following measurements represent the "Main" fiber connections from the MC to the Primary Entrance Facility (EF) of each terminal. These lengths account for the vertical and horizontal routing required through the campus conduits.

| Destination | Distance Calculation (m) | Total Length (m) |
| :--- | :--- | :--- |
| **Terminal 5 (T5)** | $130.15 + 15.11$ | **145.26 m** |
| **Terminal 3 (T3)** | $871.93 + 210.56 + 16.12$ | **1,098.61 m** |
| **Terminal 2 (T2)** | $1,114.75 + 277.63 + 17.44$ | **1,409.82 m** |
| **Terminal 4 (T4)** | $1,114.75 + 940.67$ | **2,055.42 m** |

---

## 4. Redundancy & Secondary Entry Points
To guarantee 99.99% availability, the design incorporates **Path Diversity**:

1.  **Primary Entry (North/Main):** The distances calculated above represent the primary data highway for each terminal.
2.  **Secondary Entry (South):** Each terminal features a secondary fiber entry point located at the **South Entry**.
3.  **Failover Logic:** In the event of accidental damage to the primary northern conduit (e.g., during construction), the terminal automatically fails over to the secondary southern fiber link, maintaining uninterrupted service.
4.  **Schematic Note:** For the sake of visual clarity in the campus map, individual cable stretches and secondary redundant paths are not implicitly drawn but are fully accounted for in the hardware inventory and procurement requirements.

---

## 5. Hardware at the Main Cross-connect (MC)
The MC acts as the central hub for the entire airport. It is equipped with:
* **High-Density Optical Distribution Frames (ODF):** To terminate the hundreds of fiber strands coming from across the campus.
* **Chassis-Based Core Switches:** Designed for high availability with redundant power supplies and processing modules.
* **Singlemode Transceivers:** To interface with the long-distance campus cabling.