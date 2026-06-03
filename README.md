# Linux Networking Lab

> Russian version: [README_ru.md](README_ru.md)

Practical laboratory project focused on exploring the Linux networking subsystem.

The project involves manually configuring a network of multiple virtual machines and systematically studying core Linux networking concepts, including IP addressing, routing, DHCP, NAT, firewall configuration, network diagnostics, and SSH tunneling.

All configuration is performed using Linux command-line tools without relying on graphical interfaces.

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

## Learning Outcomes

After completing all laboratory exercises the user will be able to:

* calculate IPv4 network and subnet parameters;
* configure Linux network interfaces;
* create static routes;
* diagnose network connectivity issues;
* measure network throughput;
* configure a DHCP server;
* configure NAT and traffic filtering rules;
* use SSH tunnels to access remote services.

## Network topology

Laboratory network topology:

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

## Quick start 

For the laboratory exercises, the following are required:

* VirtualBox or a similar virtualization platform;
* Ubuntu Server 20.04 or newer;
* root/sudo privileges;
* at least five virtual machines.

It is recommended to complete the laboratory exercises sequentially, starting with [Part 1](docs/ru/Part1_ru.md).

## Repository structure

```text
.
├── docs/         # Main project documentation (step-by-step instructions)
│   ├── ru/
│   └── eng/
├── images/       # Network diagrams and screenshots
├── README_ru.md  # Project overview (russian version)
└── README.md     # Project overview (english version)
```

## Tools used

* Netplan
* iproute2
* iptables
* isc-dhcp-server
* OpenSSH
* tcpdump
* traceroute
* iperf3
* nmap
* ip