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

This is a multi-site network configuration exercise carried out independently, building on an earlier two-LAN static routing project[cite: 9]. Here, a third network, network services, and secured remote access are added using Cisco Packet Tracer[cite: 9]. It covers IP addressing, VLAN-based switch management, DNS and HTTP services, Telnet and SSH remote access, and static routing across a full mesh of routers[cite: 9].

---

## 2. Objective

Design, cable, and configure a three-site network (RED, BLUE, and YELLOW) in Cisco Packet Tracer, implementing IP addressing, VLAN-based switch management, DNS and HTTP services, secured remote access over Telnet and SSH, and static routing across a full mesh of routers[cite: 9]. Then, verify both end-to-end connectivity and DNS/HTTP services across all three sites[cite: 9].

---

## 3. Network Topology

The network features three separate LANs, each connected to its own edge router[cite: 9]. The three routers are joined in a full mesh—every router has a direct point-to-point link to each of the other two—so any site can reach any other site in a single hop[cite: 9].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%201.PNG" alt="Figure 1" width="100%">
</p>

---

## 4. Work Performed

### 4.1 Physical and Logical Cabling
All PCs, servers, switches, and routers were connected according to the topology, ensuring each cable connected to the correct interface and every link was active prior to configuration[cite: 10].

### 4.2 Host Configuration
Static IP addresses, subnet masks, and default gateways were assigned to every host to provide Layer 3 reachability within each LAN[cite: 10]. 

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%202.PNG" alt="Figure 2" width="100%">
</p>

### 4.3 Switch Configuration
On each switch, a hostname and a management IP address on VLAN 1 were configured, along with the switch's default gateway, saving the running configuration[cite: 11].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%203.PNG" alt="Figure 3" width="100%">
</p>

### 4.4 Router Configuration
On each of the three routers, a hostname, an enable secret password, and a MOTD login banner were configured, bringing the LAN-facing interfaces up with `no shutdown`[cite: 11, 12].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%204.PNG" alt="Figure 4" width="100%">
</p>

### 4.5 Network Services: DNS and HTTP
A DNS server and an HTTP server were added on the YELLOW network with static IP configurations to support domain resolution and web hosting[cite: 12, 13].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%205.PNG" alt="Figure 5" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%206.PNG" alt="Figure 6" width="100%">
</p>

### 4.6 Interface and Link Verification
Interface statuses were verified using `show ip interface brief` across all routers, correcting any misconfigurations to ensure all links showed up/up[cite: 14].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%207.PNG" alt="Figure 7" width="100%">
</p>

### 4.7 Remote Administration: Telnet on BLUE1
Remote management over Telnet was set up on BLUE1 using local user authentication and VTY configuration[cite: 14].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%208.PNG" alt="Figure 8" width="100%">
</p>

### 4.8 Remote Administration: SSH on RED1 and YELLOW1
SSH version 2 was configured on RED1 and YELLOW1 by setting a domain name, creating local users, generating 1024-bit RSA keys, and restricting VTY lines to SSH[cite: 15, 16].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%209.PNG" alt="Figure 9" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2010.PNG" alt="Figure 10" width="100%">
</p>

### 4.9 Static Routing Across the Mesh
Static routes (`ip route`) were configured across the full-mesh topology so every LAN could seamlessly reach the other two[cite: 16, 17, 18].

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
Connectivity was successfully tested using `ping`, and application-layer validation confirmed proper DNS resolution and HTTP web page loading across networks[cite: 18, 19, 20].

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2014.PNG" alt="Figure 14" width="100%">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/main/Figure%2015.PNG" alt="Figure 15" width="100%">
</p>

---

## 5. Skills Demonstrated

- IP addressing and subnetting across multiple LANs and inter-router links[cite: 20].
- VLAN-based switch management interfaces[cite: 20].
- Router configuration: hostname, enable-secret, MOTD banners[cite: 20].
- Setting up DNS and HTTP network services[cite: 20].
- Telnet for remote CLI access[cite: 20].
- SSH version 2 for secured remote access, including RSA key generation[cite: 20].
- Static routing across a full-mesh topology[cite: 20].
- Interface troubleshooting with `show ip interface brief`[cite: 20].
- Understanding security trade-offs (Telnet vs. SSH) and network segmentation[cite: 20].
- End-to-end and application-layer (DNS/HTTP) testing[cite: 20].
- Clear technical documentation of a multi-step network project[cite: 20].

---

## 6. Tools Used

- Cisco Packet Tracer[cite: 20]

---

<p align="center">
  📄 <b>Download PDF Documentation:</b><br>
  [ EN ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Network_Infrastructure_and_Secure_Remote_Access_Project.pdf"><b>[ English Version PDF ]</b></a><br>
  [ ES ] <a href="https://github.com/radu-hatos/Network_Infrastructure_and_Secure_Remote_Access_Project/blob/main/Proyecto_Infraestructura_de_Red_y_Acceso_Remoto_Seguro.pdf"><b>[ Versión en Español PDF ]</b></a>
</p>
