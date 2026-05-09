RCOMP 2025-2026 Project 1 - Sprint 3 - Member 1240729 folder
===========================================
(This folder is to be created/edited by the team member 2222222 only)

#### This is just an example for a team member with number 1240729 ####
### Each member should create a folder similar to this, matching his/her number. ###
The owner of this folder (member number 1240729) will commit here all the outcomes (results/artifacts/products)		       of his/her work during sprint 3. This may encompass any kind of standard file types.


# 1. Introduction

This report describes the implementation of **Sprint 3** of the RCOMP project for **Terminal 3**, focusing on the migration from static routing to **OSPF dynamic routing**, and the integration of additional network services including **DHCPv4, DNS, VoIP, HTTP/HTTPS, NAT, and ACL-based firewall policies**.

The configuration was implemented and tested using Cisco Packet Tracer.

---

# 2. Network Architecture

## 2.1 OSPF Areas

The network was divided into OSPF areas as required:

- **Area 0 (Backbone):** 10.51.0.0/24  
- **Area 3 (Terminal 3):** All internal VLANs of Terminal 3  

OSPF router ID:

---

## 2.2 Terminal 3 VLANs

| VLAN | Network | Purpose |
|------|--------|--------|
| T3_WIFI | 10.51.32.0/21 | Wireless clients |
| T3_USERS | 10.51.40.0/22 | General users |
| T3_VOIP | 10.51.44.0/23 | IP telephony |
| T3_SERVERS (DMZ) | 10.51.46.0/24 | Servers |

---

## 2.3 Backbone and Management

| VLAN | Network | Purpose |
|------|--------|--------|
| Backbone | 10.51.0.0/24 | Inter-terminal routing |
| Management | 10.51.2.0/23 | Device management |

---

# 3. Routing (OSPF)

Static routing was replaced by OSPF:
router ospf 1
router-id 3.3.3.3
network 10.51.0.0 0.0.0.255 area 0
network 10.51.2.0 0.0.1.255 area 3
network 10.51.32.0 0.0.7.255 area 3
network 10.51.40.0 0.0.3.255 area 3
network 10.51.44.0 0.0.1.255 area 3
network 10.51.46.0 0.0.0.255 area 3

---

# 4. DHCPv4 Service

The router provides DHCP for all internal VLANs except DMZ and backbone.

## 4.1 VOIP DHCP 
ip dhcp pool T3_VOIP
network 10.51.44.0 255.255.254.0
default-router 10.51.44.1
option 150 ip 10.51.44.1


## 4.2 User and WiFi Pools

DHCP pools were created for:
- T3_USERS
- T3_WIFI

Static addresses were excluded for infrastructure devices.

---

# 5. VoIP Configuration

Cisco Call Manager Express was configured on the router.

## 5.1 Telephony Service
telephony-service
max-ephones 10
max-dn 10
ip source-address 10.51.44.1 port 2000
auto assign 1 to 10

## 5.2 IP Phone Configuration

- Phone model: Cisco 7960
- MAC address: 0060.3E3D.4AAA
- Extension: 3001

ephone-dn 1
number 3001

ephone 1
mac-address 0060.3E3D.4AAA
button 1:1


---

# 6. DNS Configuration

A hierarchical DNS structure was implemented.

## 6.1 Domain Structure

- Root domain: `rcomp-25-26--db-g2`
- Terminal 3 subdomain: `terminal-3.rcomp-25-26-db-g2`

Name server:
ns.terminal-3.rcomp-25-26-db-g2


---

## 6.2 DNS Records

| Type | Name | Value |
|------|------|-------|
| A | ns | 10.51.46.10 |
| A | server1 | 10.51.46.10 |
| CNAME | www | server1 |
| CNAME | web | server1 |
| CNAME | dns | ns |

---

# 7. HTTP/HTTPS Service (DMZ)

A server was deployed in the DMZ:

- IP: 10.51.46.10
- HTTP service enabled
- HTTPS service enabled
- Custom HTML page identifying Terminal 3

---

# 8. NAT Configuration

Static NAT was configured to allow external access to the DMZ server:
ip nat inside source static tcp 10.51.46.10 80 10.51.0.3 80
ip nat inside source static tcp 10.51.46.10 443 10.51.0.3 443


This enables HTTP/HTTPS redirection from the backbone interface to the DMZ server.

---

# 9. Firewall (ACL Configuration)

A stateless ACL was implemented on the backbone interface.

## 9.1 ACL Rules

- Allow ICMP (ping)
- Allow HTTP/HTTPS to DMZ server
- Allow DNS traffic
- Block DMZ access from internal networks (spoofing protection)
- Allow remaining traffic


access-list 100 permit icmp any any

access-list 100 permit tcp any host 10.51.46.10 eq 80
access-list 100 permit tcp any host 10.51.46.10 eq 443
access-list 100 permit udp any host 10.51.46.10 eq 53
access-list 100 permit tcp any host 10.51.46.10 eq 53

access-list 100 deny ip 10.51.46.0 0.0.0.255 any
access-list 100 deny ip any 10.51.46.0 0.0.0.255

access-list 100 permit ip any any


Applied to backbone interface:

interface FastEthernet0/0.748
ip access-group 100 in


---

# 10. Conclusion

Terminal 3 was successfully configured with:

- OSPF dynamic routing
- DHCP for all internal networks
- VoIP service with Cisco 7960 phone
- DNS hierarchical domain structure
- HTTP/HTTPS server in DMZ
- NAT static redirection
- ACL-based firewall security policies

All required Sprint 3 objectives were implemented and validated in Cisco Packet Tracer.

---