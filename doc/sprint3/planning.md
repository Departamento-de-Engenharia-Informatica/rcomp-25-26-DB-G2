# COMP 2025-2026 Project 1 - Sprint 3 planning

### Sprint master: 1211920 ###

(This file is to be created/edited by the sprint master only)

---

# 1. Sprint's backlog #

Sprint 3 extends the Packet Tracer network simulation built in Sprint 2. The focus shifts from static routing to **OSPF dynamic routing**, and adds enterprise services on each terminal:

- **OSPF** — replace static routes; Area 0 on the campus backbone; one non-backbone area per terminal
- **DHCPv4** — dynamic addressing on user, Wi-Fi, and VoIP VLANs (not backbone or Switches DMZ)
- **DNS** — hierarchical naming under a team root domain; local authoritative server per terminal
- **HTTP/HTTPS** — web server in the terminal servers/DMZ network
- **VoIP** — Cisco Call Manager Express (CME) on the terminal router; Cisco 7960 phones
- **NAT** — static NAT on the backbone interface to publish HTTP/HTTPS to the DMZ server
- **ACL** — stateless firewall on the backbone-facing interface

Each team member updates the Packet Tracer simulation for the same terminal as in Sprint 2. Terminal 3 is responsible for integrating all terminals into **campus.pkt** (same as Sprint 2).

| Task ID | Task description | Member(s) |
|---------|------------------|-----------|
| T.3.1 | Terminal 2 — OSPF, DHCPv4, DNS, VoIP, HTTP/HTTPS, NAT, ACL; internet/default route | 1222215 & 1211369 |
| T.3.2 | Terminal 3 — OSPF, DHCPv4, DNS, VoIP, HTTP/HTTPS, NAT, ACL; **campus.pkt** integration | 1240729 |
| T.3.3 | Terminal 5 — OSPF, DHCPv4, DNS, VoIP, HTTP/HTTPS | 1211920 |
| T.3.4 | Terminal 4 — OSPF, DHCPv4, DNS, VoIP, HTTP/HTTPS, NAT, ACL | 1240751 |

---

# 2. Technical decisions and coordination #

Decisions below carry over from Sprint 2 unless noted. All members use **Cisco Packet Tracer 9.0.0**.

## Device naming convention

| Device Type | Format Example |
|-------------|----------------|
| Switch | SW-T4-F1 |
| Router | R-T4 |
| Access Point | AP-T4 |
| PC | PC-T4-USER |
| Server | SRV-T4-DMZ |

---

## Layer 2 (unchanged from Sprint 2)

- **VTP domain:** `rc2526dbg2`
- **VTP mode:** backbone/core switches → Server; other switches → Client
- **Trunking:** all inter-switch and switch–router links in trunk mode
- **Native VLAN:** 749 (SWITCH_DMZ)
- **STP:** enabled (default)
- **VLAN database:** VLANs 748–765 (see Sprint 2 `planning.md`)

---

## OSPF design

| Item | Decision |
|------|----------|
| Process ID | `1` on all terminal routers |
| Area 0 | Campus backbone `10.51.0.0/24` — all terminal routers participate |
| Terminal areas | One area per terminal for all local VLAN subnets (including Switches DMZ where advertised) |

| Terminal | OSPF area | Router ID |
|----------|-----------|-----------|
| Terminal 2 | Area 2 | 2.2.2.2 |
| Terminal 3 | Area 3 | 3.3.3.3 |
| Terminal 4 | Area 4 | 4.4.4.4 |
| Terminal 5 | Area 5 | 5.5.5.5 |

**Backbone router IPv4 addresses** (unchanged from Sprint 2):

| Terminal | Router IP (VLAN 748) |
|----------|----------------------|
| Terminal 2 | 10.51.0.2 |
| Terminal 3 | 10.51.0.3 |
| Terminal 4 | 10.51.0.1 |
| Terminal 5 | 10.51.0.5 |

Static routes from Sprint 2 are removed once OSPF is operational. Terminal 2 keeps the ISP default route (`0.0.0.0/0`) and may redistribute it into OSPF if required for campus-wide internet access.

**Example — Terminal 4 (`R-T4`):**

```text
router ospf 1
 router-id 4.4.4.4
 network 10.51.0.0 0.0.0.255 area 0
 network 10.51.48.0 0.0.7.255 area 4
 network 10.51.56.0 0.0.3.255 area 4
 network 10.51.60.0 0.0.1.255 area 4
 network 10.51.62.0 0.0.0.127 area 4
```

---

## DNS domain structure

| Level | Domain |
|-------|--------|
| Team root | `rcomp-25-26-db-g2` |
| Terminal 2 | `terminal-2.rcomp-25-26-db-g2` |
| Terminal 3 | `terminal-3.rcomp-25-26-db-g2` |
| Terminal 4 | `terminal-4.rcomp-25-26-db-g2` |
| Terminal 5 | `terminal-5.rcomp-25-26-db-g2` |

Each terminal deploys an authoritative DNS server in its **servers/DMZ** VLAN. Minimum records per terminal:

| Record | Type | Purpose |
|--------|------|---------|
| `ns.<terminal-domain>` | A | Name server |
| `server1.<terminal-domain>` | A | Web/DNS host |
| `www.<terminal-domain>` | CNAME | → server1 |
| `web.<terminal-domain>` | CNAME | → server1 |
| `dns.<terminal-domain>` | CNAME | → ns |

---

## DNS server IPv4 addresses

| Terminal | DNS / web server IP | VLAN / network |
|----------|---------------------|----------------|
| Terminal 2 | 10.51.30.10 | T2_SERVERS `10.51.30.0/25` |
| Terminal 3 | 10.51.46.10 | T3_SERVERS `10.51.46.0/24` |
| Terminal 4 | 10.51.62.10 | T4_SERVERS `10.51.62.0/25` |
| Terminal 5 | 10.51.90.10 | T5_SERVERS `10.51.90.0/24` |

DHCP pools must point clients to the corresponding DNS server address above.

---

## VoIP numbering schema

CME runs on each terminal router. Extension numbers use the terminal digit as prefix:

| Terminal | VLAN | Router `ip source-address` | Extension range |
|----------|------|--------------------------|-----------------|
| Terminal 2 | 752 (T2_VOIP) | 10.51.28.1 | 2001–2010 |
| Terminal 3 | 756 (T3_VOIP) | 10.51.44.1 | 3001–3010 |
| Terminal 4 | 760 (T4_VOIP) | 10.51.60.1 | 4001–4002 |
| Terminal 5 | 764 (T5_VOIP) | 10.51.88.1 | 5001–5010 |

- Phone model: **Cisco 7960**
- VoIP DHCP pool: `option 150` → router VoIP address (TFTP/CME)
- Phones authorized by MAC on the router (`ephone` / `telephony-service`)

---

## DHCPv4

Provided by each terminal router for **Users**, **Wi-Fi**, and **VoIP** VLANs only.

- **Not used on:** VLAN 748 (backbone), VLAN 749 (Switches DMZ)
- Each pool: `default-router` = first usable IP of subnet; `dns-server` = terminal DNS IP; `domain-name` = terminal subdomain
- Exclude static infrastructure addresses (gateways, servers, switches) from pools

### Terminal 4 pools (reference)

| Pool | Network | Default gateway | DNS |
|------|---------|-----------------|-----|
| T4_USERS | 10.51.56.0/22 | 10.51.56.1 | 10.51.62.10 |
| T4_WIFI | 10.51.48.0/21 | 10.51.48.1 | 10.51.62.10 |
| T4_VOIP | 10.51.60.0/23 | 10.51.60.1 | option 150 → 10.51.60.1 |

---

## HTTP/HTTPS and NAT

- Web server in the terminal **servers** VLAN serves a simple page identifying the terminal.
- **Static NAT** on the backbone sub-interface maps public backbone IP:port → DMZ server:port.

| Terminal | NAT outside (backbone) | Inside server | Services |
|----------|------------------------|---------------|----------|
| Terminal 2 | 10.51.0.2 : 80 / 443 | 10.51.30.10 | HTTP, HTTPS |
| Terminal 3 | 10.51.0.3 : 80 / 443 | 10.51.46.10 | HTTP, HTTPS |
| Terminal 4 | 10.51.0.1 : 80 / 443 | 10.51.62.10 | HTTP, HTTPS |
| Terminal 5 | 10.51.0.5 : 80 / 443 | 10.51.90.10 | HTTP, HTTPS |

Example (Terminal 4):

```text
ip nat inside source static tcp 10.51.62.10 80 10.51.0.1 80
ip nat inside source static tcp 10.51.62.10 443 10.51.0.1 443
```

---

## ACL / firewall (backbone interface)

Applied **inbound** on the backbone sub-interface (`Fa0/0.748` or equivalent). Common policy:

1. Permit ICMP (ping / troubleshooting)
2. Permit TCP 80/443 to the terminal DMZ server
3. Permit DNS (UDP/TCP 53) to the DMZ server
4. Permit OSPF
5. Deny direct IP access to/from the DMZ subnet from other internal sources (anti-spoofing)
6. Permit remaining IP traffic

Example (Terminal 3, DMZ `10.51.46.0/24`):

```text
access-list 100 permit icmp any any
access-list 100 permit tcp any host 10.51.46.10 eq 80
access-list 100 permit tcp any host 10.51.46.10 eq 443
access-list 100 permit udp any host 10.51.46.10 eq 53
access-list 100 permit tcp any host 10.51.46.10 eq 53
access-list 100 permit ospf any any
access-list 100 deny ip 10.51.46.0 0.0.0.255 any
access-list 100 deny ip any 10.51.46.0 0.0.0.255
access-list 100 permit ip any any
```

---

## IPv4 addressing (unchanged from Sprint 2)

All Sprint 3 services use the networks defined in `doc/sprint2/planning.md`:

- **Team block:** 10.51.0.0/17
- **Backbone:** 10.51.0.0/24
- **Switches DMZ:** 10.51.2.0/23
- **Per-terminal VLAN networks:** see Sprint 2 sections 3.3 (T2–T5 tables)

---

## Technical decisions summary

- Static routing replaced by **OSPF** (Area 0 + per-terminal area)
- **DHCPv4** on user-facing VLANs; static config only for backbone, Switches DMZ, and infrastructure
- **Hierarchical DNS** under `rcomp-25-26-db-g2`
- **CME VoIP** with terminal-specific extension prefixes
- **HTTP/HTTPS** in servers VLAN; published via **static NAT** on backbone IP
- **ACL 100** (or equivalent) on backbone interface for basic firewalling
- Configuration dumps exported regularly (same practice as Sprint 2)

---

# 3. Subtasks assignment #

### Terminal 2 – T.3.1 (1222215 & 1211369)

- Migrate static routes to OSPF (Area 0 + Area 2)
- Configure DHCPv4 for T2_USERS, T2_WIFI, T2_VOIP
- Deploy DNS/HTTP/HTTPS server in T2_SERVERS
- Configure CME and IP phones (extensions 2001+)
- Static NAT for web services on backbone IP 10.51.0.2
- ACL on backbone interface
- Maintain internet connectivity (ISP / default route)

---

### Terminal 3 – T.3.2 (1240729 — Rita Oliveira)

- OSPF Area 0 + Area 3 (`router-id 3.3.3.3`)
- DHCPv4 for T3_USERS, T3_WIFI, T3_VOIP
- DNS server at 10.51.46.10 (`terminal-3.rcomp-25-26-db-g2`)
- HTTP/HTTPS on DMZ server
- VoIP: CME, extension 3001 (and additional phones as needed)
- Static NAT: 10.51.0.3 → 10.51.46.10 (ports 80/443)
- ACL on backbone interface

**Additional responsibilities:**

- Integrate all terminal simulations into **campus.pkt**
- Rebuild backbone links between terminal main switches
- Verify OSPF adjacency and end-to-end reachability across campus

---

### Terminal 4 – T.3.4 (1240751 — Afonso Simões)

- OSPF Area 0 + Area 4 (`router-id 4.4.4.4`)
- DHCPv4 for T4_USERS, T4_WIFI, T4_VOIP
- DNS/HTTP/HTTPS server at 10.51.62.10 (`terminal-4.rcomp-25-26-db-g2`)
- VoIP: extensions 4001, 4002
- Static NAT: 10.51.0.1 → 10.51.62.10 (ports 80/443)
- ACL on backbone interface

---

### Terminal 5 – T.3.3 (1211920 — Gonçalo Silva)

- OSPF Area 0 + Area 5 (`router-id 5.5.5.5`)
- OSPF may be enabled per sub-interface if needed for Packet Tracer stability
- DHCPv4 for T5_USERS, T5_WIFI, T5_VOIP
- DNS/HTTP/HTTPS server at 10.51.90.10 (`terminal-5.rcomp-25-26-db-g2`)
- VoIP: CME with MAC-based `ephone` authorization
- Static NAT: 10.51.0.5 → 10.51.90.10 (ports 80/443)
- ACL on backbone interface (if required by implementation)

---

## Notes

- Sprint 3 builds on Sprint 2 topologies; do not change VLAN IDs or team address plan without team agreement.
- DNS domain in member reports must match **`rcomp-25-26-db-g2`** (not alternate suffixes).
- Terminal 2 is the only terminal with internet; coordinate default-route propagation with the team.
- Commit `TerminalN.pkt`, configuration dumps, and sprint report/README per member folder.
