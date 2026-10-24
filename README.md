# Enterprise Campus Network Design (Apex Dynamics)

A high-availability multi-VLAN campus network built in Cisco Packet Tracer demonstrating enterprise design principles including redundant gateways, centralized services, and access control.

## Project Overview

This lab implements a collapsed-core campus network for a mid-sized headquarters (~300 users) with departmental segmentation, gateway redundancy, and guest isolation.

**Key Features**
- Multi-VLAN segmentation (Management, Servers, Engineering, Finance, Sales, Guest)
- HSRP gateway redundancy with load balancing
- Inter-VLAN routing on Layer 3 core switches
- Centralized DHCP and internal DNS
- Dual-homed access layer with EtherChannel between cores
- Guest isolation via extended ACLs
- Port security, PortFast, and BPDU Guard on access ports

## Topology

- **Core Layer**: 2× Cisco 3650 (CORE1, CORE2) running HSRP
- **Access Layer**: 5× Cisco 2960 (AS-ENG, AS-SALES, AS-FINANCE, AS-SERVERS, AS-GUEST)
- **Edge**: Cisco 2911 router for transit/default route
- **Services**: Dedicated DHCP and DNS servers
- **Clients**: PCs in Engineering, Sales, Finance, and Guest VLANs

## VLAN & IP Plan

| VLAN | Name     | Subnet         | HSRP VIP     | Active Core |
|------|----------|----------------|--------------|-------------|
| 10   | MGMT     | 10.10.10.0/24  | 10.10.10.1   | CORE1       |
| 20   | SERVERS  | 10.10.20.0/24  | 10.10.20.1   | CORE2       |
| 30   | ENG      | 10.10.30.0/24  | 10.10.30.1   | CORE1       |
| 40   | FINANCE  | 10.10.40.0/24  | 10.10.40.1   | CORE2       |
| 50   | SALES    | 10.10.50.0/24  | 10.10.50.1   | CORE1       |
| 60   | GUEST    | 10.10.60.0/24  | 10.10.60.1   | CORE2       |
| 99   | NATIVE   | —              | —            | —           |

## Technologies Used

- VLANs & 802.1Q Trunking
- HSRP (Hot Standby Router Protocol) v2
- EtherChannel (LACP)
- DHCP (with relay / ip helper-address)
- DNS
- Extended ACLs
- Port Security, PortFast, BPDU Guard
- Static routing

## Verification Highlights

- HSRP active/standby roles correctly distributed and preempt
- Clients receive DHCP addresses with correct gateway and DNS
- Internal name resolution works (e.g. `dhcp.apexdynamics.local`)
- Guest VLAN blocked from all internal subnets via ACL
- Inter-VLAN routing functional for permitted traffic
- EtherChannel and trunks verified

## Files

- `Apex-Dynamics-Campus.pkt` — Packet Tracer topology file
- `configs/` — (Optional) Sanitized device configurations
- `docs/` — Design documentation

## How to Use

1. Open `Apex-Dynamics-Campus.pkt` in Cisco Packet Tracer.
2. Verify HSRP with `show standby brief` on CORE1 and CORE2.
3. Test DHCP by setting a PC to DHCP.
4. Confirm guest isolation by pinging internal addresses from a Guest PC.
5. Test failover by shutting a VLAN interface on the Active core.

## Author

Todd Ethersee

## License

This project is for educational and portfolio purposes.
