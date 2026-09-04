# TechNova Enterprise Network

A Cisco Packet Tracer enterprise networking project that simulates a small company with a Head Office, Branch Office, internal servers, guest wireless access, and a simulated Internet connection.

## Project Goal

The goal of this lab is to practice designing, configuring, securing, and troubleshooting an enterprise-style IPv4 network using Cisco routing and switching technologies.

## Technologies Implemented

- VLAN segmentation
- 802.1Q trunking
- Router-on-a-Stick inter-VLAN routing
- OSPF dynamic routing
- DHCP
- NAT/PAT
- Extended ACLs
- SSH device management
- Switch port security
- Spanning Tree Protocol (STP)
- LACP EtherChannel
- DNS, Web, and FTP services
- Guest wireless network

## Network Overview

The network is divided into a Head Office and Branch Office. An edge router connects the internal network to a simulated ISP. The Head Office contains multiple departmental VLANs, internal servers, network-management infrastructure, and guest wireless access. The Branch Office contains separate Sales, IT, and Guest VLANs.

## IPv4 Addressing Plan

### Head Office

| VLAN | Purpose | Network | Default Gateway |
|---:|---|---|---|
| 10 | HR | `192.168.10.0/24` | `192.168.10.1` |
| 20 | IT | `192.168.20.0/24` | `192.168.20.1` |
| 30 | Sales | `192.168.30.0/24` | `192.168.30.1` |
| 40 | Management | `192.168.40.0/24` | `192.168.40.1` |
| 50 | Servers | `192.168.50.0/24` | `192.168.50.1` |
| 60 | Guest | `192.168.60.0/24` | `192.168.60.1` |
| 99 | Network Management | `192.168.99.0/24` | `192.168.99.1` |

### Branch Office

| VLAN | Purpose | Network | Default Gateway |
|---:|---|---|---|
| 10 | Sales | `172.16.10.0/24` | `172.16.10.1` |
| 20 | IT | `172.16.20.0/24` | `172.16.20.1` |
| 30 | Guest | `172.16.30.0/24` | `172.16.30.1` |

### WAN / Transit Networks

| Connection | Network |
|---|---|
| ISP ↔ Edge | `10.0.0.0/30` |
| Edge ↔ HQ | `10.0.0.4/30` |
| Edge ↔ Branch | `10.0.0.8/30` |
| Simulated Internet | `203.0.113.0/24` |

## Routing and Network Services

OSPF is used between the Edge, HQ, and Branch routers so internal routes are learned dynamically. The Edge router advertises a default route toward the internal network and uses PAT to provide simulated Internet connectivity.

R2-HQ provides DHCP for HQ user VLANs, while R3-BRANCH provides DHCP for Branch user VLANs. Infrastructure devices and servers use static addressing. Internal DNS is hosted at `192.168.50.10` using the `technova.local` domain.

## Security Controls

The project includes ACL-based segmentation, guest-network isolation, restricted Sales access to server resources, SSH-only remote device administration from the Management VLAN, and switch port security using sticky MAC learning with shutdown on violations.

## Switching Resiliency

The HQ switches use STP and an LACP EtherChannel between SW1-HQ and SW2-HQ. Two FastEthernet links are bundled into Port-Channel 1 to demonstrate link aggregation and redundancy.

## Validation

The final lab is tested for:

- DHCP address assignment
- Inter-VLAN communication
- HQ-to-Branch routing
- OSPF neighbor formation and learned routes
- DNS resolution and internal Web access
- NAT/PAT Internet connectivity
- ACL allow/deny behavior
- SSH management access
- Port-security behavior
- STP and EtherChannel operation

Evidence screenshots will be added under the `screenshots/` directory.

## Repository Structure

```text
TechNova-Enterprise-Network/
├── README.md
├── packet-tracer/
├── topology/
├── screenshots/
└── configs/
```

The Cisco Packet Tracer `.pkt` file, final topology image, selected verification screenshots, and device configurations will be added as the project documentation is completed.

## Disclaimer

This is a fictional lab environment created for learning and portfolio purposes. Any credentials used during lab configuration are demo-only and should not be reused in real environments.
