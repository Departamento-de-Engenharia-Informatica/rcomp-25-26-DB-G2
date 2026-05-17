# RCOMP 2025-2026 Project 1 - Sprint 3 - Member 1240751 folder

(This folder is to be created/edited by the team member 1240751 only)

#### This is the Sprint 3 folder for Terminal 4 ####

The owner of this folder will commit here all the outcomes (results/artifacts/products) of his/her work during sprint 3.

---

# 1. Introduction

This report describes the implementation of **Sprint 3** of the RCOMP project for **Terminal 4**, focusing on the migration from static routing to **OSPF dynamic routing**, and the integration of additional network services including **DHCPv4, DNS, VoIP, HTTP/HTTPS, NAT, and ACL-based firewall policies**.

The configuration was implemented and tested using Cisco Packet Tracer.

---

# 2. Network Architecture

## 2.1 OSPF Areas

The network was divided into OSPF areas as required:

- **Area 0 (Backbone):** 10.51.0.0/24
- **Area 4 (Terminal 4):** All internal VLANs of Terminal 4

OSPF router ID:

```text
4.4.4.4
```

---

## 2.2 Terminal 4 VLANs

| VLAN | Network | Purpose |
|------|--------|--------|
| T4_WIFI | 10.51.48.0/21 | Wireless clients |
| T4_USERS | 10.51.56.0/22 | General users |
| T4_VOIP | 10.51.60.0/23 | IP telephony |
| T4_SERVERS | 10.51.62.0/25 | Internal servers |
| SWITCH_DMZ | 10.51.2.0/23 | Management and DMZ |

---

## 2.3 Backbone and Management

| VLAN | Network | Purpose |
|------|--------|--------|
| Backbone | 10.51.0.0/24 | Inter-terminal routing |
| Management / DMZ | 10.51.2.0/23 | Device management and DMZ |

---

# 3. Routing (OSPF)

Static routing was replaced by OSPF dynamic routing.

```bash
router ospf 1
router-id 4.4.4.4
network 10.51.0.0 0.0.0.255 area 0
network 10.51.48.0 0.0.7.255 area 4
network 10.51.56.0 0.0.3.255 area 4
network 10.51.60.0 0.0.1.255 area 4
network 10.51.62.0 0.0.0.127 area 4
```

---

# 4. DHCPv4 Service

The router provides DHCPv4 service for all internal VLANs except the backbone and DMZ networks.

## 4.1 USERS DHCP Pool

```bash
ip dhcp pool T4_USERS
network 10.51.56.0 255.255.252.0
default-router 10.51.56.1
dns-server 10.51.2.40
domain-name terminal-4.rcomp-25-26-cc-gn
```

---

## 4.2 WIFI DHCP Pool

```bash
ip dhcp pool T4_WIFI
network 10.51.48.0 255.255.248.0
default-router 10.51.48.1
dns-server 10.51.2.40
domain-name terminal-4.rcomp-25-26-cc-gn
```

---

## 4.3 VOIP DHCP Pool

```bash
ip dhcp pool T4_VOIP
network 10.51.60.0 255.255.254.0
default-router 10.51.60.1
option 150 ip 10.51.2.40
```

---

# 5. HTTP/HTTPS and DNS Server

A second server was added to the DMZ network.

Server configuration:

| Service | Status |
|---|---|
| HTTP | Enabled |
| HTTPS | Enabled |
| DNS | Enabled |

Server IP address:

```text
10.51.2.40
```

The HTTP server hosts a simple webpage identifying Terminal 4.

---

# 6. DNS Configuration

Local DNS domain:

```text
terminal-4.rcomp-25-26-cc-gn
```

Configured DNS records:

| Record | Type | Value |
|---|---|---|
| ns.terminal-4.rcomp-25-26-cc-gn | A | 10.51.2.40 |
| server1.terminal-4.rcomp-25-26-cc-gn | A | 10.51.2.40 |
| www.terminal-4.rcomp-25-26-cc-gn | CNAME | server1.terminal-4.rcomp-25-26-cc-gn |
| web.terminal-4.rcomp-25-26-cc-gn | CNAME | server1.terminal-4.rcomp-25-26-cc-gn |
| dns.terminal-4.rcomp-25-26-cc-gn | CNAME | ns.terminal-4.rcomp-25-26-cc-gn |

---

# 7. VoIP Service

Two Cisco 7960 IP phones were configured in VLAN T4_VOIP.

Telephony service configuration:

```bash
telephony-service
max-ephones 2
max-dn 2
ip source-address 10.51.60.1 port 2000
auto assign 1 to 2
```

Configured phone numbers:

| Phone | Extension |
|---|---|
| IP Phone 1 | 4001 |
| IP Phone 2 | 4002 |

---

# 8. NAT Configuration

Static NAT rules were configured to redirect HTTP and HTTPS traffic received on the backbone interface to the DMZ HTTP server.

```bash
ip nat inside source static tcp 10.51.2.40 80 10.51.0.1 80
ip nat inside source static tcp 10.51.2.40 443 10.51.0.1 443
```

---

# 9. ACL / Firewall Rules

Basic ACL rules were implemented to:

- Allow ICMP traffic
- Allow HTTP/HTTPS access to the DMZ server
- Allow DNS traffic
- Allow OSPF traffic
- Restrict direct access to the DMZ network

Example ACL:

```bash
access-list 100 permit icmp any any
access-list 100 permit tcp any host 10.51.2.40 eq 80
access-list 100 permit tcp any host 10.51.2.40 eq 443
access-list 100 permit udp any any eq domain
access-list 100 permit ospf any any
access-list 100 deny ip any 10.51.2.0 0.0.1.255
access-list 100 permit ip any any
```

---

# 10. Conclusion

Sprint 3 successfully extended the previous network implementation by integrating dynamic routing and multiple enterprise network services.

The implemented solution includes:

- OSPF dynamic routing
- DHCPv4 services
- DNS services
- HTTP/HTTPS services
- VoIP telephony
- NAT
- ACL-based firewall protection

All configurations were implemented and tested in Cisco Packet Tracer.