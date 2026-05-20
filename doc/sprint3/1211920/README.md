# RCOMP 2025-2026 Project 1 - Sprint 3 - Member 1211920 folder

(This folder is to be created/edited by the team member 1211920 only)

#### This is the Sprint 3 folder for Terminal 5 ####

The owner of this folder will commit here all the outcomes (results/artifacts/products) of his/her work during sprint 3.

---

# 1. Introduction

This report describes the implementation of **Sprint 3** of the RCOMP project for **Terminal 5** (Group cc-gn), focusing on the migration from static routing to **OSPF dynamic routing**, and the integration of additional network services including **DHCPv4, DNS, VoIP, and HTTP/HTTPS**.

The configuration was implemented and tested using Cisco Packet Tracer.

---

# 2. Network Architecture

## 2.1 OSPF Areas

The network was divided into OSPF areas as required:

- **Area 0 (Backbone):** Inter-terminal routing
- **Area 5 (Terminal 5):** All internal VLANs of Terminal 5

OSPF router ID (Router T5):
```text
5.5.5.5
```

---

## 2.2 Terminal 5 VLANs

Based on the network addressing and sub-interfaces implemented:

| VLAN | Network | Purpose |
|------|--------|--------|
| T5_USERS (762) | 10.51.16.0/20 | General users |
| T5_WIFI (763) | 10.51.32.0/20 | Wireless clients |
| T5_VOIP (764) | 10.51.48.0/20 | IP telephony |
| T5_SERVERS (765)| 10.51.64.0/20 | Internal servers / DMZ |
| Management (749) | 10.51.2.0/24 | Device management |

---

# 3. Routing (OSPF)

Static routing was replaced by OSPF dynamic routing. To resolve Packet Tracer broadcast issues and ensure stable routing table convergence, OSPF Area 5 was explicitly configured directly inside each corresponding sub-interface:

```bash
router ospf 1
 router-id 5.5.5.5

interface FastEthernet0/1.749
 ip ospf 1 area 5
interface FastEthernet0/1.762
 ip ospf 1 area 5
interface FastEthernet0/1.763
 ip ospf 1 area 5
interface FastEthernet0/1.764
 ip ospf 1 area 5
interface FastEthernet0/1.765
 ip ospf 1 area 5
```

---

# 4. DHCPv4 Service

The router provides dynamic IPv4 configurations for the internal VLAN networks.

## 4.1 USERS DHCP Pool (VLAN 762)
The configuration ensures users receive the correct gateway and the internal DNS server address.

```bash
ip dhcp pool T5_USERS
 network 10.51.16.0 255.255.240.0
 default-router 10.51.16.1
 dns-server 10.51.64.2
 domain-name terminal-5.rcomp-25-26-cc-gn
```

---

# 5. DNS and HTTP/HTTPS Server

A dedicated node was deployed inside the Server/DMZ network subnet (VLAN 765) hosting the web services and resolving domain queries locally.

Server IP address:
```text
10.51.64.2
```

## 5.1 Service Status & DNS Records

The HTTP, HTTPS, and DNS services were enabled and verified.
Local DNS domain: `terminal-5.rcomp-25-26-cc-gn`

Configured resource records:

| Record | Type | Value |
|---|---|---|
| ns.terminal-5.rcomp-25-26-cc-gn | A | 10.51.64.2 |
| server1.terminal-5.rcomp-25-26-cc-gn | A | 10.51.64.2 |
| www.terminal-5.rcomp-25-26-cc-gn | CNAME | server1.terminal-5.rcomp-25-26-cc-gn |
| web.terminal-5.rcomp-25-26-cc-gn | CNAME | server1.terminal-5.rcomp-25-26-cc-gn |

---

# 6. VoIP Service

Cisco IP telephony endpoints were provisioned in VLAN 764. The Cisco Call Manager Express (CME) on Router T5 was configured with strict MAC address authentication. Unlisted MAC addresses are actively rejected by the router to prevent registration loops.

## 6.1 Authorized IP Phones

| Phone | MAC Address | Status |
|---|---|---|
| IP Phone 1 | 00D0.97DE.8D35 | Authorized (ephone 1) |
| IP Phone 2 | 0001.962E.4142 | Authorized (ephone 2) |

```bash
ephone 1
 mac-address 00D0.97DE.8D35
!
ephone 2
 mac-address 0001.962E.4142
```

---

# 7. Conclusion

Sprint 3 successfully expanded the network infrastructure of Terminal 5.

The implemented solution integrates:
- **OSPF** dynamic routing directly applied to sub-interfaces for absolute topology stability.
- **DHCPv4 & DNS** infrastructure resolving local names and domains perfectly.
- **HTTP/HTTPS** web availability matching required visibility guidelines.
- **VoIP** telephony infrastructure authenticated via static device mapping.

All services and the Host/DNS resolution pipeline were fully tested, verified, and are operational in Cisco Packet Tracer.