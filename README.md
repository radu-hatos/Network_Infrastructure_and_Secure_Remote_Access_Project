<h1 align="center">Network Infrastructure and Secure Remote Access Project</h1>

<p align="center">
  <b>[ EN ]</b> Static Routing, Network Services, and SSH/Telnet Administration Across Three LANs
</p>

<p align="center">
  📄 <b>Download PDF Documentation:</b><br>
  [ EN ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Network_Infrastructure_and_Secure_Remote_Access_Project.pdf"><b>[ English Version PDF ]</b></a><br>
  [ ES ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Proyecto_Infraestructura_de_Red_y_Acceso_Remoto_Seguro.pdf"><b>[ Versión en Español PDF ]</b></a>
</p>

<hr>

## 📋 Index

- [1. Introduction](#1-introduction)
- [2. Objective](#2-objective)
- [3. Network Topology](#3-network-topology)
- [4. Work Performed](#4-work-performed)
  - [4.1 Physical and Logical Cabling](#41-physical-and-logical-cabling)
  - [4.2 Host Configuration](#42-host-configuration)
  - [4.3 Switch Configuration](#43-switch-configuration)
  - [4.4 Router Configuration](#44-router-configuration)
  - [4.5 Network Services: DNS and HTTP](#45-network-services-dns-and-http)
  - [4.6 Interface and Link Verification](#46-interface-and-link-verification)
  - [4.7 Remote Administration: Telnet on BLUE1](#47-remote-administration-telnet-on-blue1)
  - [4.8 Remote Administration: SSH on RED1 and YELLOW1](#48-remote-administration-ssh-on-red1-and-yellow1)
  - [4.9 Static Routing Across the Mesh](#49-static-routing-across-the-mesh)
  - [4.10 End-to-End and Application-Layer Verification](#410-end-to-end-and-application-layer-verification)
- [5. Skills Demonstrated](#5-skills-demonstrated)
- [6. Tools Used](#6-tools-used)

---

## 1. Introduction

This is a multi-site network configuration exercise carried out independently, building on an earlier two-LAN static routing project. Here, a third network, network services, and secured remote access are added using Cisco Packet Tracer. It covers IP addressing, VLAN-based switch management, DNS and HTTP services, Telnet and SSH remote access, and static routing across a full mesh of routers.

---

## 2. Objective

Design, cable, and configure a three-site network (RED, BLUE, and YELLOW) in Cisco Packet Tracer, implementing IP addressing, VLAN-based switch management, DNS and HTTP services, secured remote access over Telnet and SSH, and static routing across a full mesh of routers. Then, verify both end-to-end connectivity and DNS/HTTP services across all three sites.

---

## 3. Network Topology

The network features three separate LANs, each connected to its own edge router. The three routers are joined in a full mesh—every router has a direct point-to-point link to each of the other two—so any site can reach any other site in a single hop.

- **RED LAN:** `172.16.0.0/24` (Gateway: `172.16.0.1`) — 2 PCs, 1 switch (`RED_SW1`), 1 router (`RED1`)
- **BLUE LAN:** `192.168.0.0/24` (Gateway: `192.168.0.1`) — 2 PCs, 1 switch (`BLUE_SW1`), 1 router (`BLUE1`)
- **YELLOW LAN:** `10.8.8.0/24` (Gateway: `10.8.8.1`) — DNS server (`10.8.8.8`), HTTP server (`10.8.8.9`), 1 switch, 1 router (`YELLOW1`)
- **Inter-router links (Full Mesh):**
  - `RED1 <-> BLUE1`: `89.12.0.0/24`
  - `RED1 <-> YELLOW1`: `89.13.0.0/24`
  - `YELLOW1 <-> BLUE1`: `89.32.0.0/24`

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%201.PNG" alt="Figure 1" width="100%">
</p>

---

## 4. Work Performed

### 4.1 Physical and Logical Cabling
All PCs, servers, switches, and routers were connected according to the topology, ensuring each cable connected to the correct interface and every link was active prior to configuration.

### 4.2 Host Configuration
Static IP addresses, subnet masks, and default gateways were assigned to every host to provide Layer 3 reachability within each LAN. The RED hosts use the `172.16.0.0/24` range, and BLUE hosts use the `192.168.0.0/24` range.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%202.PNG" alt="Figure 2" width="100%">
</p>

### 4.3 Switch Configuration
On each switch, a hostname and a management IP address on VLAN 1 were configured (`RED_SW1` at `172.16.0.2/24`, `BLUE_SW1` at `192.168.0.2/24`, and the YELLOW switch at `10.8.8.2/24`), along with each switch's default gateway, saving the running configuration.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%203.PNG" alt="Figure 3" width="100%">
</p>

### 4.4 Router Configuration
On each of the three routers, a hostname, an enable secret password, and a MOTD login banner were configured, bringing the LAN-facing interfaces up with `no shutdown`.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%204.PNG" alt="Figure 4" width="100%">
</p>

### 4.5 Network Services: DNS and HTTP
A DNS server (`10.8.8.8`) and an HTTP server (`10.8.8.9`) were added on the YELLOW network with static IP configurations to support domain name resolution and web hosting.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%205.PNG" alt="Figure 5" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%206.PNG" alt="Figure 6" width="100%">
</p>

### 4.6 Interface and Link Verification
Interface statuses were verified using `show ip interface brief` across all routers simultaneously, correcting any misconfigurations to ensure all links showed up/up.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%207.PNG" alt="Figure 7" width="100%">
</p>

### 4.7 Remote Administration: Telnet on BLUE1
Remote management over Telnet was set up on BLUE1 using a local user account, VTY authentication against the local database (`login local`), and permitted transport protocols.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%208.PNG" alt="Figure 8" width="100%">
</p>

### 4.8 Remote Administration: SSH on RED1 and YELLOW1
SSH version 2 was configured on RED1 and YELLOW1 by setting a local domain name, creating local user credentials, generating 1024-bit RSA keys, and restricting VTY lines to SSH-only.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%209.PNG" alt="Figure 9" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2010.PNG" alt="Figure 10" width="100%">
</p>

### 4.9 Static Routing Across the Mesh
Static routes (`ip route`) were configured across the full-mesh topology on all three routers so every LAN could seamlessly reach the other two without needing intermediate hops.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2011.PNG" alt="Figure 11" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2012.PNG" alt="Figure 12" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2013.PNG" alt="Figure 13" width="100%">
</p>

### 4.10 End-to-End and Application-Layer Verification
Connectivity was successfully tested using `ping` across all networks. Application-layer validation confirmed proper DNS resolution and HTTP web page loading for `www.google.ro` and `www.facebook.ro` from hosts on both the RED and BLUE networks.

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2014.PNG" alt="Figure 14" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2015.PNG" alt="Figure 15" width="100%">
</p>

---

## 5. Skills Demonstrated

- IP addressing and subnetting across multiple LANs and inter-router links.
- VLAN-based switch management interfaces.
- Router configuration: hostname, enable-secret, MOTD banners.
- Setting up DNS and HTTP network services.
- Telnet for remote CLI access.
- SSH version 2 for secured remote access, including RSA key generation.
- Static routing across a full-mesh topology.
- Interface troubleshooting with `show ip interface brief`.
- Understanding security trade-offs (Telnet vs. SSH) and network segmentation (DMZ).
- End-to-end and application-layer (DNS/HTTP) testing.
- Clear technical documentation of a multi-step network project.

---

## 6. Tools Used

- Cisco Packet Tracer

---

<p align="center">
  📄 <b>Download PDF Documentation:</b><br>
  [ EN ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Network_Infrastructure_and_Secure_Remote_Access_Project.pdf"><b>[ English Version PDF ]</b></a><br>
  [ ES ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Proyecto_Infraestructura_de_Red_y_Acceso_Remoto_Seguro.pdf"><b>[ Versión en Español PDF ]</b></a>
</p>
