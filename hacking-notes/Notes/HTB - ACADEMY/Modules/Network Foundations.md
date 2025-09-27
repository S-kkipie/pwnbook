---
tags:
  - "#MOC"
  - "#Module"
platform: "[[Hack The Box]]"
difficulty: Fundamental
tier: I
banner: "![[network_foundations_banner.webp]]"
status: Incomplete
---
2
> [!danger]- Associated Certs
> [[HTB CJCA|HTB Certified Junior Cybersecurity Associate]]
^faq

> [!faq]- Associated Paths
> [[Junior Cybersecurity Analyst]]
^faq

> [!summary] Network Foundations Summary
> This course is designed to introduce and reinforce the core aspects of networking, which are essential in today's digital world. The curriculum begins with the basics of network types and topologies, moves into the mechanics of data transmission across networks, and examines the critical components that ensure secure and efficient communication. By the end of this course, students will possess a thorough understanding of network infrastructure.
^summary

> [!FLag] In this module, we will cover:
> - Definition and Types of Networks
>- Networking Models
>- Types of Network Components and their Roles
>- MAC/IP Addresses and Ports
>- Address Resolution Protocol (ARP)
>- Network Data Flow Process
>- DHCP and DORA Process
>- Role of DHCP Server and Client
>- IP Address Leasing
>- IP Address Conservation
>- Types of NAT
>- Port Address Translation (PAT)
>- DNS and DNS Hierarchy
>- DNS Resolution Process
>- Internet Architectures
>- Wireless Networks and Communication Frequencies
>- Mobile Hotspot
>- CIA Triad
>- Role and Types of Firewalls
>- Intrusion Detection and Prevention

# Sections
## 1. Introduction to Networks
In this module we will focused on two primaries networks: *Local Area Networks(LAN)* and *Wide Area Networks(WAN)*

>[!info] What is a Network?
>A network is a collection of interconnected devices that can communicate.
>A device in a network is called a *Node*, however nodes alone do not comprise the entire network.


| **Concepts**   | **Description**                                                |
| -------------- | -------------------------------------------------------------- |
| `Nodes`        | Individual devices connected to a network.                     |
| `Links`        | Communication pathways that connect nodes (wired or wireless). |
| `Data Sharing` | The primary purpose of a network is to enable data exchange.   |
### Types of netowrks
#### LAN 
Local Area Networks connects devices in a short distance, like a house or a small company.

| **Characteristic**   | **Description**                                                 |
| -------------------- | --------------------------------------------------------------- |
| `Geographical Scope` | Covers a small area.                                            |
| `Ownership`          | Typically owned and managed by a single person or organization. |
| `Speed`              | High data transfer rates.                                       |
| `Media`              | Uses wired (Ethernet cables) or wireless (Wi-Fi) connections.   |

![[Pasted image 20250904153156.png]]
#### WAN
Wide Area Network spans a large area geographical area connecting multiple LANs.

| **Characteristic**   | **Description**                                                                 |
| -------------------- | ------------------------------------------------------------------------------- |
| `Geographical Scope` | Covers cities, countries, or continents.                                        |
| `Ownership`          | Often a collective or distributed ownership (e.g., internet service providers). |
| `Speed`              | Slower data transfer rates compared to LANs due to long-distance data travel.   |
| `Media`              | Utilizes fiber optics, satellite links, and leased telecommunication lines.     |

![[Pasted image 20250904153339.png]]

### Comparing LAN and WAN

|Aspect|LAN|WAN|
|---|---|---|
|`Size`|Small, localized area|Large, broad area|
|`Ownership`|Single person or organization|Multiple organizations/service providers|
|`Speed`|High|Lower compared to LAN|
|`Maintenance`|Easier and less expensive|Complex and costly|
|`Example`|Home or office network|The Internet|
###  How Do LANs and WANs Work Together?
A LAN connects to a WAN thorough a ISP(Internet Service Provider) which grants internet access to all devices within the LAN. In this setup, a device called modem (modulator-demodulator) plays a crucial role. The modem acts as a bridge between your home network and the internet. 

## 2. Network concepts
In this section we will cover concepts like OSI Model, TCP/IP Model , common network protocols and the various transmission methods.

### OSI Model
The Open Systems Information(OSI) model is a conceptual framework that standardizes the functions of a computing system or a telecommunication into seven abstract layers.
#### Physical layer (Layer 1)
This is the layer that transmits a bit stream over a physical medium like ethernet cables, hubs and repeaters.
#### Data Link Layer (Layer 2)
This layer communicates two or more devices through a direct link, ensuring synchronization, error handling and correction. Devices in this layer have a MAC (Media Access Control) addresses to identify, some devices that deals this communication are switches and bridges.
#### Network Later (Layer 3)



# References
- [[Hack The Box]]
- [[HTB Module]]
