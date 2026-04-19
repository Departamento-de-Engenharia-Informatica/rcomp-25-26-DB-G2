RCOMP 2025-2026 Project 1 - Sprint 2 - Member 1240729 folder
===========================================
(This folder is to be created/edited by the team member 1240729 only)

#### This is just an example for a team member with number 4444444 ####
### Each member should create a folder similar to this, matching his/her number. ###
The owner of this folder (member number 4444444) will commit here all the outcomes (results/artifacts/products)		       of his/her work during sprint 2. This may encompass any kind of standard file types.



# Configuration Report: Terminal 3

## 1. Executive Summary
This report documents the network implementation for Terminal 3. The design utilizes a **Router-on-a-Stick** architecture to segment traffic into functional VLANs, ensuring optimized performance and security for Data, Voice (VoIP), Wireless, and Management traffic.

---

## 2. Network Topology & Addressing
The following VLAN and IP addressing scheme was implemented at the core router (**R-T3**):

| Service | VLAN ID | Subnet | Gateway IP |
| :--- | :---: | :--- | :--- |
| **Management (Native)** | 749 | 10.51.2.0/23 | 10.51.2.1 |
| **Users (Data)** | 754 | 10.51.40.0/22 | 10.51.40.1 |
| **Wi-Fi** | 755 | 10.51.32.0/21 | 10.51.32.1 |
| **Voice (VoIP)** | 756 | 10.51.44.0/23 | 10.51.44.1 |
| **Servers** | 757 | 10.51.46.0/24 | 10.51.46.1 |

---

## 3. DEVICE IP INVENTORY
Below are the specific IP addresses assigned to the infrastructure and end-devices within Terminal 3:

### 3.1. Infrastructure Devices
| Device | Interface | IP Address | Description |
| :--- | :--- | :--- | :--- |
| **R-T3** | Fa0/0.749 | 10.51.2.1 | Management Gateway |
| **R-T3** | Fa0/0.754 | 10.51.40.1 | Users Gateway |
| **R-T3** | Fa0/0.755 | 10.51.32.1 | Wi-Fi Gateway |
| **R-T3** | Fa0/0.756 | 10.51.44.1 | Voice Gateway (TFTP/CME) |
| **R-T3** | Fa0/0.757 | 10.51.46.1 | Servers Gateway |
| **SW-T3-IC** | Vlan 749 | 10.51.2.21 | Core Switch Management |
| **SW-T3-HC1** | Vlan 749 | 10.51.2.22 | Access Switch Management |
| **SW-T3-HC2** | Vlan 749 | 10.51.2.23 | Access Switch Management |

### 3.2. End-User Devices
| Device | VLAN | IP Method | IP Address |
| :--- | :---: | :--- | :--- |
| **PC 1** | 754 | Static/DHCP | 10.51.40.10 |
| **PC 2** | 754 | Static/DHCP | 10.51.40.11 |
| **IP Phone** | 756 | DHCP | 10.51.44.2 |
| **Laptop (Wi-Fi)** | 755 | DHCP | 10.51.32.10 |
| **Server** | 757 | Static | 10.51.46.10 |

---

## 4. TECHNICAL CONFIGURATION

### 4.1. Inter-VLAN Routing (R-T3)
The **R-T3** router manages all inter-VLAN communication. Sub-interfaces were defined on the `Fa0/0` physical link using the **IEEE 802.1Q** protocol. VLAN 749 was explicitly set as the **Native VLAN**.

### 4.2. IP Telephony & DHCP Services
The router serves as the central **CallManager Express (CME)** and DHCP server.
* **DHCP Option 150:** Provides the TFTP server IP (10.51.44.1) to handsets.
* **Telephony Service:** - Max E-phones: 5
  - Max DN: 5
  - Source Address: 10.51.44.1 (Port 2000)
  - Extension: 3001 (Assigned to ephone-dn 1)

### 4.3. Switching Infrastructure
* **Trunks:** Configured on all inter-switch links with `switchport trunk native vlan 749`.
* **Access Ports:** Ports connecting to IP Phones (e.g., Fa2/1) use `switchport voice vlan 756` to prioritize voice traffic while allowing data on the access VLAN.

---