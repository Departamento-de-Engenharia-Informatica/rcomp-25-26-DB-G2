# RCOMP 2025-2026 Project 1 - Sprint 1 - Member 1222215
===========================================

# Cabling Infrastructure Plan: Terminal 2 Layout (Level 1)

## 1. Executive Summary of Infrastructure Design
This project implements a high-performance, future-proofed structured cabling system for Terminal 2. The design prioritizes scalability, signal integrity, and strict adherence to international structured cabling standards.

* **Backbone Strategy:** All distribution points (ICs/HCs) are interconnected using **Multimode Optical Fiber**. This ensures total immunity to electromagnetic interference (EMI) and supports data rates up to 100 Gbps.
* **Horizontal Strategy:** **CAT7 S/STP Copper** cabling is used for all work area outlets and Access Points. This supports 10 Gbps and provides necessary shielding for the terminal's high-density environment.
* **Topology:** The network utilizes an **Extended Star Topology** to span the 200m facility while keeping copper runs within strict horizontal distance limits.

---

## 2. Outlet Requirements & Area Calculations (Arrivals)

| Room ID | Width (m) | Length (m) | Area (m²) | Required Outlets |
|:---|:---|:---|:---|:---|
| **Room 1** | 27.20 | 13.84* | 376.45 | 76 |
| **Room 2** | 21.05 | 13.84* | 291.33 | 59 |
| **Room 3 & 5** | 33.35 | 13.84* | 461.56 | 93 |
| **Room 4** | 38.99 | 13.84* | 539.62 | 108 |
| **Room 6** | 8.05 | 11.07 | 89.11 | **Infrastructure (IC Hub)** |
| **Room 7 & 8** | 27.41 | 16.87 | 462.40 | 93 |
| **Room 9 & 10** | 24.38* | 18.96 | 462.24 | 93 |
| **Room 11 & 12** | 10.85* | 10.85* | 117.72 | **Infrastructure** |
| **South & East wall** | N/A | 200 | N/A | 40 |

> **Calculations Rule:** 2 outlets per 10m² rounded up.
> **Standardization Note:** (*) Measurements averaged or standardized to account for minor measurement variance.

---

## 3. Deployment & Justification

### 3.1 Distribution Points (ICs and HCs)
* **Primary Hub (Room 6):** Centrally houses the **Intermediate Cross-connect (IC)**.
* **Core Island HC:** A specialized floor-standing enclosure is placed in the center of the terminal floor. This hub manages the "Islands" in Rooms 9 and 10 and the ceiling-mounted Wireless APs, ensuring no copper run exceeds the 90-meter limit.
* **High-Density HC:** Handles ~400 connections using a **dual enclosure** setup to respect the 200-cable limit per rack.

### 3.2 Cable Pathway Strategy
The installation utilizes two distinct pathway methods to maximize the use of existing infrastructure while overcoming architectural limitations:
* **Underfloor Cable Raceway:** This is the primary pathway used for the majority of the floor plan, leveraging pre-existing underfloor conduits for clean, hidden cable distribution.
* **Lowered Ceiling Pathways:** For **Rooms 7, 8, 9, and 10**, no pre-existing underfloor raceways were available. In these areas, cables are routed through the lowered ceiling. On the schematic, these transitions are marked by **yellow "up and down" arrows**.
* **Central Backbone:** The fiber backbone connecting the IC to the **Core Island HC** is routed via the ceiling to ensure an unobstructed, direct path across the terminal's open floor.

### 3.3 Wireless Infrastructure (Access Points)
* **Theoretical Density:** A grid of approximately **69 APs** is required to ensure no point is further than 12m from a signal source.
* **Implementation:** A representative grid is used for schematic clarity. All APs are ceiling-mounted and connected via **CAT7 Copper** to the nearest HC.

---

## 4. Hardware Inventory: Distribution Points

| Location / ID | Role | Configuration | Size ($4 \times S$) |
| :--- | :--- | :--- | :--- |
| **High Density HC** | User Dist. | 2 x Enclosures | **2 x 36U Floor Racks** |
| **Core Island HC** | Wireless/Island Hub | 1 x Secure Enclosure | **32U Floor Rack** |
| **Interior HC 1** | User Dist. | 1 x Enclosure | **32U Floor Rack** |
| **Interior HC 2** | User Dist. | 1 x Enclosure | **24U Floor Rack** |
| **Wall HCs (x7)** | Wall Outlets | 1 x Enclosure each | **6U Wall Cabinets** |

---

## 5. Design Justifications & Hard Rules

* **The 90-Meter Rule:** Placement of the Core Island HC and ceiling-routed backbones ensures all horizontal CAT7 runs are under 90 meters.
* **The 200-Cable Limit:** High-density zones utilize multiple physical enclosures to prevent physical congestion and heat buildup.
* **Island Security:** The Core Island HC is specified as a **secured, NEMA-rated floor cabinet** for public-access protection.
