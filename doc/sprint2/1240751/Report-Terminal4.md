# Terminal 4 – Network Implementation

## 1. Objective

The objective of this work is to implement a network simulation for Terminal 4 using Cisco Packet Tracer, focusing on Layer 2 infrastructure and Layer 3 IPv4 addressing and routing.

---

## 2. VLAN Design

The network was segmented using VLANs to separate different types of traffic, as required:

| VLAN ID | Name         | Purpose |
|--------|-------------|--------|
| 749    | SWITCH_DMZ  | Switch management network |
| 758    | T4_USERS    | User devices |
| 759    | T4_WIFI     | Wireless network |
| 760    | T4_VOIP     | IP phones |
| 761    | T4_SERVERS  | Servers |

All VLANs are present on every switch and trunk links were configured between switches and router, as required by the project.

---

## 3. IPv4 Addressing

Each VLAN was assigned a subnet according to the number of required hosts for Terminal 4:

- Users → ~800 hosts → /22
- Wi-Fi → ~1800 hosts → /21
- VoIP → ~400 hosts → /23
- Servers → ~120 hosts → /25

The resulting subnets are:

| Network | Subnet |
|--------|--------|
| T4_WIFI | 10.51.48.0/21 |
| T4_USERS | 10.51.56.0/22 |
| T4_VOIP | 10.51.60.0/23 |
| T4_SERVERS | 10.51.62.0/25 |
| SWITCH_DMZ | 10.51.2.0/23 |
| BACKBONE | 10.51.0.0/24 |

All IP addresses belong to the assigned address block and do not overlap, as required.

---

## 4. Inter-VLAN Routing

Inter-VLAN routing was implemented using a router (Cisco 2811) with a Router-on-a-Stick configuration:

- One physical interface connected to a trunk port
- Multiple subinterfaces (Fa0/0.x)
- Each subinterface corresponds to one VLAN

This allows communication between all internal VLANs.

---

## 5. DMZ Network

The Switches DMZ network is isolated:

- No routing configured to other VLANs
- Used only for switch management

This follows the requirement of having an independent management network.

---

## 6. End Devices

Each VLAN includes at least one end device, as required:

- PC (Users VLAN)
- PC (DMZ VLAN)
- Laptop (Wi-Fi VLAN)
- Server (Servers VLAN)
- IP Phone (VoIP VLAN)

All devices use static IPv4 configuration, except VoIP.

---

## 7. Multi-floor Design

Two floors were implemented:

- Floor 1: main switch and all devices
- Floor 2: secondary switch and user PC

Switches are connected via trunk, allowing VLANs to span across floors.

---

## 8. Testing

Connectivity tests were performed:

- Inter-VLAN communication 
- Same VLAN across floors 
- DMZ isolation 

---

## 9. Conclusion

The network was successfully implemented according to the project requirements, including VLAN segmentation, IPv4 addressing, and inter-VLAN routing.

The solution is ready to be integrated into the campus backbone.