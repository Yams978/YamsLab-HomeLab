# 🌐 YamsLab Networking

This section documents the networking architecture, configuration, troubleshooting, and future development of the YamsLab homelab.

The goal of this environment is to gain practical experience designing, operating, securing, and troubleshooting a multi-device network.

---

## Current Network

YamsLab currently uses Starlink as its Internet connection.

The lab includes multiple physical servers, virtual machines, Docker containers, infrastructure services, and client devices connected through the local network.

### Technologies & Concepts

- TCP/IP
- IPv4 addressing
- Static IP configuration
- DHCP
- DNS
- LAN/WAN networking
- Ethernet
- VPN connectivity
- Tailscale
- Network monitoring
- Service availability monitoring
- Linux networking
- SMB file sharing
- Network troubleshooting

---

## DNS

YamsLab uses AdGuard Home for network DNS filtering.

This project provided hands-on experience with:

- Configuring a DNS server
- Changing client/network DNS settings
- Testing DNS resolution
- Monitoring DNS queries
- Understanding DNS-based content filtering
- Troubleshooting DNS connectivity

---

## Secure Remote Access

Tailscale is used to provide secure remote connectivity to YamsLab services.

This allows authorized devices to access internal services without directly exposing those services to the public Internet.

Services accessed remotely include infrastructure management and self-hosted applications.

---

## Monitoring

Uptime Kuma is used to monitor YamsLab services and infrastructure.

Monitoring helps identify:

- Service outages
- Connectivity failures
- HTTP/HTTPS availability
- Infrastructure availability
- DNS/networking problems

---

## Troubleshooting Experience

Building YamsLab has required troubleshooting real networking issues, including:

- DNS resolution problems
- VPN connectivity
- Remote Jellyfin connectivity
- Service port accessibility
- Linux network configuration
- Docker container networking
- SMB network shares
- Hostname resolution
- Local vs. remote service access

Troubleshooting steps and solutions will be documented individually as the project develops.

---

## 🚧 Planned Network Architecture

The future YamsLab network will use a dedicated OPNsense firewall/router and managed multi-gigabit switching.

Planned topology:

Internet → OPNsense → Managed 2.5GbE Switch → YamsLab / Home Network

Planned improvements include:

- Dedicated OPNsense firewall/router
- 2.5GbE Ethernet
- 10Gb SFP+ uplinks
- Managed switching
- Cat6 structured cabling
- Central patch panel
- PoE wireless access points
- VLAN segmentation
- UPS-backed networking equipment

---

## Planned VLAN Design

| Network | Purpose |
|---|---|
| Main | Trusted computers, consoles, and personal devices |
| Server | Proxmox nodes, VMs, containers, NAS, and infrastructure |
| IoT | Smart-home and IoT devices |
| Guest | Isolated network for guest devices |

Firewall policies between these networks will follow least-privilege principles while allowing required services to communicate.

---

## Future Documentation

This section will eventually include:

- VLAN configuration
- OPNsense configuration
- Firewall policies
- DHCP configuration
- DNS architecture
- Switch configuration
- Physical network topology
- Wi-Fi architecture
- Troubleshooting case studies
