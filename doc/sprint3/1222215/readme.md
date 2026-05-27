# Terminal 2 (1222215) Implementation Summary - Sprint 3
**Team:** 2DB
**Terminal:** 2
**Status:** Completed, Secured & Verified (Isolated Implementation)

---

## 1. OSPF Dynamic Routing Architecture
Static routing configurations from the previous sprint were completely deprecated and replaced with an automated, dynamic routing infrastructure.

* **Table Cleansing**: All pre-existing static routes directing traffic to other terminals were completely removed from the routing table.
* **Default Route Retention**: The static default route (`ip route 0.0.0.0 0.0.0.0 89.73.67.33`) pointing to the ISP was explicitly preserved, as Terminal 2 serves as the primary internet gateway for the campus.
* **OSPF Process Initiation**: Activated OSPF Process 1 on the `R-T2` router.
* **Area Assignments**:
    * **Area 0 (Backbone)**: The core backbone network link (VLAN 748, `10.51.0.0/24`) was assigned directly to Area 0.
    * **Area 2 (Internal Terminal)**: All internal Terminal 2 network subnets (VLANs 749, 750, 751, 752, and 753) were grouped inside Area 2.
* **Default Route Propagation**: Enforced the `default-information originate` command under the OSPF routing daemon, ensuring that Terminal 2 automatically injects and advertises the default gateway path to all other downstream terminals across the OSPF domain.

---

## 2. Infrastructure Services Deployment: DHCPv4 & VoIP
Automated network configuration profiles and local IP telephony systems were introduced to scale the terminal deployment.

### DHCPv4 Service Configuration
The `R-T2` router was designated as the local DHCPv4 server to dynamically manage IP allocations across user and media pools.
* **Address Exclusions**: For safety, the first 25 usable IPv4 addresses (`.1` through `.25`) of each scope were strictly excluded from the dynamic assignment lists to preserve room for structural hardware and gateways.
* **Pool Standardization**: Implemented dynamic allocations for `T2_USERS` (VLAN 750) and `T2_WIFI` (VLAN 751), seamlessly pushing lease attributes including subnet masks, default gateways (`10.51.24.1` / `10.51.16.1`), local DNS server targets (`10.51.30.10`), and the default domain name string `terminal-2.rcomp-25-26-cc-gn`.
* **VoIP Pool Requirements**: The voice pool allocation (`T2_VOIP`, VLAN 752) was explicitly built to include **Option 150**, pointing directly to the router's voice gateway IP (`10.51.28.1`) to supply the TFTP server address to booting IP telephony units.

### VoIP Infrastructure Implementation
* **Hardware Integration**: Deployed and powered multiple physical Cisco 7960 IP Phone modules to facilitate local and inter-terminal voice stress testing.
* **Layer 2 Switchport Modifications**: Ports linking directly to the Cisco 7960 phone endpoints were transitioned to strip standard data traffic. Commanded `switchport voice vlan 752` and issued `no switchport access vlan` to explicitly lock those interfaces down for voice packets only.
* **Cisco Telephony Service Execution**: Activated basic call processing functionality on the `R-T2` router with an active socket listening on port 2000 (`ip source-address 10.51.28.1 port 2000`).
* **Directory Number Layout**: Registered operational extensions mapping to Team 2's dial prefix criteria: Extension 2001 (`ephone-dn 2`) and Extension 2002 (`ephone-dn 1`).
* **Cross-Terminal Call Forwarding**: Programmed explicit dial-peer voice matching patterns (`destination-pattern 3...`, `4...`, and `5...`) to route calls traversing the backbone directly to the target terminal telephony services running on neighboring routers.

---

## 3. DMZ Expansion: HTTP Server & Hierarchical DNS Tree
The local DMZ subnet (VLAN 753) was expanded with dedicated web applications and the root-level directory authority for the team repository.

### HTTP Server (`server1`) Addition
* **Hardware Provisioning**: Added a second standalone server hardware node to the server DMZ network lane (`10.51.30.0/25`), labeled as `server1-T2`.
* **Addressing Matrix**: Configured manual static parameters using IP address `10.51.30.11`, Subnet Mask `255.255.255.128`, Default Gateway `10.51.30.1`, and pointed its lookups to the local DNS authority at `10.51.30.10`.
* **Web Directory Customization**: Modified the baseline `index.html` file within the HTTP/HTTPS service daemons to cleanly present a Terminal 2 identification index.

### DNS Tree Hierarchical Setup
Terminal 2 acts as the absolute root zone authority for the entire team project space (`rcomp-25-26-cc-gn`).
* **Local Identity Mapping**: Populated Fully Qualified Domain Names (FQDNs) for local internal assets, including the core namespace record (`ns.rcomp-25-26-cc-gn` -> `10.51.30.10`) and web host records (`server1.rcomp-25-26-cc-gn` -> `10.51.30.11`).
* **CNAME Architecture**: Structured formal aliases map definitions including `www` and `web` pointing back to `server1`, and a `dns` alias pointing cleanly to `ns`.
* **Subdomain Delegation Glue Records**: As the highest-level authoritative domain platform, Name Server (NS) records and explicit matching Glue A records were added to link the server to downstream subdomains (`terminal-3`, `terminal-4`, and `terminal-5`) administered by colleagues.
---

## 4. Edge Translation: Static NAT Port Forwarding
Static Destination Network Address Translation rules were implemented on the edge routing limits to gracefully expose core DMZ portals to external networks.

* **Interface Demarcation**: Tagged the external backbone interface (`Fa0/0.748`) as `ip nat outside` and the internal DMZ server interface (`Fa0/0.753`) as `ip nat inside`.
* **Port-Forwarding Enforcement**: Hardcoded static TCP port rules mapping inbound requests hitting the public backbone address (`10.51.0.2`) on port 80 (HTTP) and port 443 (HTTPS) directly to the private internal address of the primary DNS server host (`10.51.30.10`).
* **Backup Web Portal**: Activated HTTP/HTTPS engines directly inside the DNS server (`10.51.30.10`) running an explicitly labeled NAT portal splash screen.

---

## 5. Network Hardening: Extended Inbound Static Firewalls
A stateless, top-down security boundary was implemented using Cisco Extended Access Control Lists (ACLs) to validate packet parameters at the router boundaries.

### Outside Perimeter Access List (`BACKBONE_IN`)
Applied inbound at `FastEthernet 0/0.748` to police packets coming from the external backbone.
1. **Spoofing Eradication**: Drops any inbound external packet claiming to originate from within the internal campus space (`10.51.0.0/17`).
2. **Diagnostic Clearway**: Universally allows all ICMP echo requests and replies for campus troubleshooting.
3. **NAT Exception Passage**: Explicitly permits TCP traffic targeting port 80 and 443 at host IP `10.51.0.2` to allow public translation rules to pass through safely.
4. **Routing Admittance**: Allows OSPF protocol traffic to permit dynamic convergence tracking.
5. **Router Termination Lockdown**: Restricts all remaining unapproved packets addressed directly to the router's backbone interface IP.
6. **DMZ Shielding**: Drops any external attempt to directly browse or scan the private DMZ subnet address pool (`10.51.30.0/25`) unless matching the port-forwarded exceptions.
7. **Transit Clearway**: Passes remaining legitimate transit data streams heading to other terminals.

### Core Internal Access List (`INTERNAL_IN`)
Applied inbound across all user, wireless, and media sub-interfaces (`Fa0/0.750`, `.751`, and `.752`) to isolate internal networks.
1. **ICMP Admittance**: Permits diagnostic ping capabilities.
2. **DMZ Service Whitelisting**: Selectively opens paths exclusively for UDP/TCP port 53 (DNS lookup traffic) to the DNS host (`10.51.30.10`), alongside TCP ports 80/443 directly to web nodes `.10` and `.11`.
3. **General DMZ Blockade**: Denies all other internal cross-VLAN traffic from entering the secure DMZ perimeter.
4. **Control Plane Exceptions**: Opens structural holes for bootps/bootpc (DHCP negotiation), TFTP (IP phone startup configs), and skinny port 2000 (Cisco Call Manager registration control).
5. **Gateway Protection**: Rejects all other traffic addressed directly to the internal virtual gateway IPs of the router to isolate the system brain.
6. **Transit Clearway**: Permits all remaining valid cross-VLAN communication.

---

## 6. Verification & Telemetry Output Logs

### DNS Name Resolution Verification (`nslookup`)
Executing a verification test from `PC-T2-USER` against the standardized web server alias yields an instant, valid mapping response:
```cmd
C:\>nslookup www.rcomp-25-26-cc-gn

Server: [10.51.30.10]
Address:  10.51.30.10

Non-authoritative answer:
Name:   server1.rcomp-25-26-cc-gn
Address:   10.51.30.11
           
Aliases:   server1.rcomp-25-26-cc-gn