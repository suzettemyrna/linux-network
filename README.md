# Linux Networking Lab

>Russian version: [README_ru.md](README_ru.md)

This project focuses on exploring the Linux networking subsystem at the level of configuration and diagnostics. It covers IP addressing, routing, traffic filtering, and basic network services.

## Contents

The project covers the following topics:

* IP addressing and subnetting
* Using `ipcalc` for network analysis
* Static routing between hosts and across routers
* Network interface configuration using Netplan
* Network traffic analysis (`tcpdump`, `traceroute`)
* Network throughput testing (`iperf3`)
* Traffic filtering with `iptables`
* Firewall configuration and packet filtering
* DHCP: dynamic IP assignment and MAC-based reservations
* NAT (SNAT / DNAT)
* SSH tunneling (local / remote forwarding)

## Network topology

The project is based on a custom lab topology including routers, workstations, and multiple isolated network segments.

![Network topology](images/network.png)

## Project structure

The project is divided into logical parts:

* [Part 1](docs/eng/Part1.md) — IP addressing and subnetting
* [Part 2](docs/eng/Part2.md) — Basic static routing between two hosts
* [Part 3](docs/eng/Part3.md) — Network throughput testing (iperf3)
* [Part 4](docs/eng/Part4.md) — Basic firewall configuration (iptables) and port scanning (nmap)
* [Part 5](docs/eng/Part5.md) — Multi-node static routing
* [Part 6](docs/eng/Part6.md) — DHCP and automatic network configuration
* [Part 7](docs/eng/Part7.md) — NAT (SNAT / DNAT) and service access
* [Part 8](docs/eng/Part8.md) — SSH tunneling

## Repository structure

```text
.
├── docs/         # Main project documentation (step-by-step instructions)
├── images/       # Network diagrams and screenshots
├── notes/        # Additional notes and explanations (optional materials)
├── README_ru.md  # Project overview (russian version)
└── README.md     # Project overview (english version)
```

## Technologies used

**1. Core technologies**

* Linux networking stack
* Netplan
* iproute2
* iptables
* DHCP (isc-dhcp-server)
* NAT (SNAT / DNAT)
* SSH tunneling

**2. Diagnostic tools**

* tcpdump
* traceroute
* iperf3
* nmap
* ip

## Implementation highlights

* Full manual network interface configuration without GUI tools
* Static routing and DHCP configuration from scratch
* Separation of roles (workstations and routers)
* Connectivity validation using ICMP and TCP
* Packet-level analysis on routers

## Requirements

To reproduce the environment:

* VirtualBox or equivalent virtualization software
* Ubuntu Server (recommended 20.04+)
* root/sudo privileges
* at least 5 virtual machines (for Part 5 and beyond)

## Project goal

To understand how Linux implements:

* IP packet routing
* network interface management
* NAT and firewall mechanisms
* dynamic network configuration (DHCP)
* network troubleshooting at packet level