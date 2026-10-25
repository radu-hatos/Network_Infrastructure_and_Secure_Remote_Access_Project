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

This is a multi-site network configuration exercise that I carried out on my own, building on an earlier two-LAN static routing project[cite: 22]. Here I add a third network, some network services and secured remote access[cite: 22]. I did it in Cisco Packet Tracer, and it covers IP addressing, VLAN-based switch management, DNS and HTTP services, Telnet and SSH remote access, and static routing across a full mesh of routers[cite: 22]. The screenshots below show the main steps rather than every single one[cite: 22].

---

## 2. Objective

Design, cable and configure a three-site network (RED, BLUE and YELLOW) in Cisco Packet Tracer, with IP addressing, VLAN-based switch management, DNS and HTTP services, secured remote access over Telnet and SSH, and static routing across a full mesh of routers[cite: 22]. Then check both end-to-end connectivity and the DNS/HTTP services across all three sites[cite: 22].

---

## 3. Network Topology

The network has three separate LANs, each connected to its own edge router[cite: 22]. The three routers are joined in a full mesh — every router has a direct point-to-point link to each of the other two — so any site can reach any other site in a single hop[cite: 22].

- **RED:** `172.16.0.0/24` (Gateway: `172.16.0.1`) — 2 PCs, 1 switch, 1 router (`RED1`)[cite: 22]
- **BLUE:** `192.168.0.0/24` (Gateway: `192.168.0.1`) — 2 PCs, 1 switch, 1 router (`BLUE1`)[cite: 22]
- **YELLOW:** `10.8.8.0/24` (Gateway: `10.8.8.1`) — DNS server (`.8`), HTTP server (`.9`), 1 switch, 1 router (`YELLOW1`)[cite: 22]
- **Inter-router links (mesh):**
  - `RED1 <-> BLUE1`: `89.12.0.0/24`[cite: 22]
  - `RED1 <-> YELLOW1`: `89.13.0.0/24`[cite: 22]
  - `YELLOW1 <-> BLUE1`: `89.32.0.0/24`[cite: 22]

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%201.PNG" alt="Figure 1" width="100%">
</p>

---

## 4. Work Performed

### 4.1 Physical and Logical Cabling
I connected all the PCs, servers, switches and routers according to the topology, checking that each cable went to the correct interface and that every link was active before starting the configuration[cite: 24].

### 4.2 Host Configuration
I assigned a static IP address to every host — giving Layer 3 IP address, subnet mask and default gateway reachability inside each LAN[cite: 24]. The screenshots show the RED hosts; the BLUE hosts (`BLUE_PC1`, `BLUE_PC2`) were configured the same way, with addresses in the `192.168.0.0/24` range[cite: 24].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%202.PNG" alt="Figure 2" width="100%">
</p>

### 4.3 Switch Configuration
On each switch I set a hostname and a management IP address on VLAN 1, then set the switch's default gateway and saved the running configuration so it survives a reload[cite: 25]. The screenshot shows `RED_SW1` (management IP `172.16.0.2/24`); `BLUE_SW1` (`192.168.0.2/24`) and the YELLOW switch (`10.8.8.2/24`) were configured identically, each with its own gateway[cite: 25].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%203.PNG" alt="Figure 3" width="100%">
</p>

### 4.4 Router Configuration
On each of the three routers I set a hostname, an enable secret password and a MOTD (message-of-the-day) login banner, then gave the LAN-facing interface its IP address and brought it up with no shutdown[cite: 25]. The screenshot shows `RED1`; `BLUE1` and `YELLOW1` were done the same way on their own LAN interfaces[cite: 25].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%204.PNG" alt="Figure 4" width="100%">
</p>

### 4.5 Network Services: DNS and HTTP
I added a DNS server and an HTTP server on the YELLOW network, each with its own static IP address, subnet mask and default gateway[cite: 26]. The DNS server resolves the domain names used in the browser tests in Section 4.10, and the HTTP server hosts the web pages the client PCs request[cite: 26].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%205.PNG" alt="Figure 5" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%206.PNG" alt="Figure 6" width="100%">
</p>

### 4.6 Interface and Link Verification
After addressing all three routers, I checked the interface status with `show ip interface brief` on `RED1`, `YELLOW1` and `BLUE1` at the same time[cite: 28]. One interface was in the wrong state, so I reviewed and fixed the connection and its configuration[cite: 28]. After the fix, every interface on all three routers showed up/up and all the links in the topology were active (green)[cite: 28].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%207.PNG" alt="Figure 7" width="100%">
</p>

### 4.7 Remote Administration: Telnet on BLUE1
I set up remote access to `BLUE1` over Telnet: I created a local user account, set the VTY lines to authenticate against the local user database (`login local`), and allowed Telnet as the transport protocol[cite: 28]. I then checked it by connecting to `BLUE1` over Telnet from a client PC and logging in with those credentials[cite: 28]. Note that Telnet sends everything, including the username and password, in cleartext[cite: 28]. I used it here because the exercise asked for it, but SSH (set up in Section 4.8) is the right choice for managing any network that untrusted users can reach[cite: 28].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%208.PNG" alt="Figure 8" width="100%">
</p>

### 4.8 Remote Administration: SSH on RED1 and YELLOW1
I set up SSH version 2 on `RED1` and `YELLOW1` for secured remote access: I set a local domain name, created a local user with a secret password, generated an RSA key pair (1024-bit) to turn SSH on, and limited the VTY lines to SSH-only, authenticated against the local user database[cite: 29]. I checked it with `show ip ssh`, which confirmed SSH version 2 was enabled on both routers[cite: 29]. Two choices here are fine for a lab but not for production: the 1024-bit RSA key is below the 2048-bit minimum recommended today, and I reused the same username and password on both devices for simplicity[cite: 29]. On a real network each device would have unique credentials and a longer key, ideally with central authentication such as AAA (RADIUS/TACACS+)[cite: 29].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%209.PNG" alt="Figure 9" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2010.PNG" alt="Figure 10" width="100%">
</p>

### 4.9 Static Routing Across the Mesh
Because `RED1`, `BLUE1` and `YELLOW1` are all directly connected in a full mesh, each router needs only one static route per remote network, pointing straight at its neighbour — there is no need to route through the third router[cite: 30]. I configured static routes (`ip route`) on all three routers so every LAN can reach the other two[cite: 30]. One trade-off is worth noting: with full-mesh reachability, the DNS and HTTP servers on the YELLOW network are directly reachable from both RED and BLUE, with no filtering in between[cite: 30]. On a real network, servers like these would usually sit in a separate, access-controlled segment (a DMZ) instead of being open to every client LAN[cite: 30].

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
I tested connectivity between all three LANs with `ping`, which confirmed that the static routes forwarded traffic correctly in both directions[cite: 32]. The very first packets to a new destination were sometimes lost — this is normal, because ARP needs one exchange to learn the address before it is cached — and after that there was 0% loss[cite: 32]. I also tested DNS and HTTP at the application layer: once the DNS server address was set on the client PCs, the names `www.google.ro` and `www.facebook.ro` resolved correctly and their pages loaded in the browser from hosts on both the RED and BLUE networks[cite: 32]. This confirmed that name resolution and web access worked across the whole network[cite: 32].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2014.PNG" alt="Figure 14" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2015.PNG" alt="Figure 15" width="100%">
</p>

---

## 5. Skills Demonstrated

- IP addressing and subnetting across multiple LANs and inter-router links[cite: 33]
- VLAN-based switch management interfaces[cite: 33]
- Router configuration: hostname, enable-secret, MOTD banners[cite: 33]
- Setting up DNS and HTTP network services[cite: 33]
- Telnet for remote CLI access[cite: 33]
- SSH version 2 for secured remote access, including RSA key generation[cite: 33]
- Static routing across a full-mesh topology[cite: 33]
- Interface troubleshooting with `show ip interface brief`[cite: 33]
- Awareness of remote-access security trade-offs (Telnet vs. SSH, key length, reused credentials) and basic network segmentation (DMZ)[cite: 33]
- End-to-end and application-layer (DNS/HTTP) testing[cite: 33]
- Clear technical documentation of a multi-step network project[cite: 33]

---

## 6. Tools Used

- Cisco Packet Tracer[cite: 33]

---

<p align="center">
  📄 <b>Download PDF Documentation:</b><br>
  [ EN ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Network_Infrastructure_and_Secure_Remote_Access_Project.pdf"><b>[ English Version PDF ]</b></a><br>
  [ ES ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Proyecto_Infraestructura_de_Red_y_Acceso_Remoto_Seguro.pdf"><b>[ Versión en Español PDF ]</b></a>
</p>
