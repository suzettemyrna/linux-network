## Part 5. Static Network Routing

> [Russian version](../ru/Part5_ru.md)

Virtual machines used in this section:

* `r1` and `r2` — routers;
* `ws11`, `ws21`, and `ws22` — workstations.

### 5.1. Network configuration

Configure network interfaces according to the network topology:

![network](../../images/network.png)

Before configuring the network, create internal VirtualBox networks and connect virtual machine adapters to them.

* `ws11`:

  1. **NAT** type for external connectivity.
  2. **Internal Network** for connection with `r1`. Name: `Network1`.

* `ws21` and `ws22`:

  1. **NAT** type for external connectivity.
  2. **Internal Network** for connection with `r2`. Name: `Network3`.

* `r1`:

  1. **NAT** type for external connectivity.
  2. **Internal Network** for connection with `ws11`. Name: `Network1`.
  3. **Internal Network** for connection with `r2`. Name: `Network2`.

* `r2`:

  1. **NAT** type for external connectivity.
  2. **Internal Network** for connection with `ws21` and `ws22`. Name: `Network3`.
  3. **Internal Network** for connection with `r1`. Name: `Network2`.

Configure network interfaces using Netplan:

* `ws11`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_ws11.png)

* `ws21`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_ws21.png)

* `ws22`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_ws22.png)

* `r1`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_r1.png)

* `r2`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_r2.png)

Apply changes:

```bash
sudo netplan apply
```

Check IP configuration:

```bash
ip -4 a
```

* `ws11`:

  ![ip -4 a](../../images/Part5/5.1_2_ws11.png)

* `ws21`:

  ![ip -4 a](../../images/Part5/5.1_2_ws21.png)

* `ws22`:

  ![ip -4 a](../../images/Part5/5.1_2_ws22.png)

* `r1`:

  ![ip -4 a](../../images/Part5/5.1_2_r1.png)

* `r2`:

  ![ip -4 a](../../images/Part5/5.1_2_r2.png)

Check connectivity between nodes:

* `ws22 → ws21`:

  ![ping ws22 → ws21](../../images/Part5/5.1_3_ws22.png)

* `r1 → ws11`:

  ![ping r1 → ws11](../../images/Part5/5.1_3_r1.png)

---

### 5.2. Enabling IP forwarding

Routers must forward packets between interfaces.

Temporarily enable forwarding:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

* `r1`:

  ![sysctl -w net.ipv4.ip\_forward=1](../../images/Part5/5.2_1_r1.png)

* `r2`:

  ![sysctl -w net.ipv4.ip\_forward=1](../../images/Part5/5.2_1_r2.png)

To persist the setting after reboot, add it to `/etc/sysctl.conf`:

```text
net.ipv4.ip_forward = 1
```

* `r1`:

  ![/etc/sysctl.conf](../../images/Part5/5.2_2_r1.png)

* `r2`:

  ![/etc/sysctl.conf](../../images/Part5/5.2_2_r2.png)

---

### 5.3. Default route configuration

Configure default routes on workstations using Netplan.

Add the following route to `/etc/netplan/00-installer-config.yaml`:

```yaml
routes:
  - to: default
    via: <gateway IP>
```

* `ws11`:

  ![routes: \n to: default \n via: \<gateway IP>](../../images/Part5/5.3_1_ws11.png)

* `ws21`:

  ![routes: \n to: default \n via: \<gateway IP>](../../images/Part5/5.3_1_ws21.png)

* `ws22`:

  ![routes: \n to: default \n via: \<gateway IP>](../../images/Part5/5.3_1_ws22.png)

Apply changes:

```bash
sudo netplan apply
```

Check routing tables:

```bash
ip r
```

* `ws11`:

  ![ip r](../../images/Part5/5.3_2_ws11.png)

* `ws21`:

  ![ip r](../../images/Part5/5.3_2_ws21.png)

* `ws22`:

  ![ip r](../../images/Part5/5.3_2_ws22.png)

Check traffic flow through routers:

```bash
ping 10.100.0.12
```

where `10.100.0.12` is the address of `r2`.

![ping](../../images/Part5/5.3_3.png)

To capture and analyze traffic, use `tcpdump`.

On `r2`, start packet capture:

```bash
sudo tcpdump -tn -i enp0s9
```

After repeating the ping from `ws11`, packets appear in tcpdump output, confirming that traffic passes through the router.

![tcpdump -tn -i enp0s9](../../images/Part5/5.3_4.png)

---

### 5.4. Static routes

Static routes between networks are configured in Netplan on routers `r1` and `r2`.

* `r1`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_r1.png)

* `r2`:

  ![etc/netplan/00-installer-config.yaml](../../images/Part5/5.1_1_r2.png)

Check routing tables:

```bash
ip r
```

* `r1`:

  ![ip r](../../images/Part5/5.4_2_r1.png)

* `r2`:

  ![ip r](../../images/Part5/5.4_2_r2.png)

Check the route selection for the network `10.10.0.0/18` and the default route:

```bash
ip r list 10.10.0.0/18
ip r list 0.0.0.0/0
```

![ip r list](../../images/Part5/5.4_3.png)

A more specific route is used for `10.10.0.0/18`. The default route is used only when no more specific match exists.

---

### 5.5. Router path tracing

On `r1`, start packet capture:

```bash
tcpdump -tnv -i enp0s8
```

At the same time, from `ws11`, send packets to `ws21`:

```bash
ping 10.20.0.10
```

  ![tcpdump](../../images/Part5/5.5_1_r1.png)

  ![ping](../../images/Part5/5.5_1_ws11.png)

Build the route from `ws11` to `ws21` using `traceroute`:

```bash
sudo traceroute 10.20.0.10
```

![traceroute](../../images/Part5/5.5_2.png)

`Traceroute` works by increasing TTL: each router decreases TTL by 1 and returns ICMP "Time Exceeded" when TTL reaches zero.

---

### 5.6. ICMP in routing diagnostics

Start ICMP capture on `r1`:

```bash
tcpdump -n -i enp0s8 icmp
```

From `ws11`, send a packet to a non-existent address:

```bash
ping 10.30.0.111
```

![tcpdump](../../images/Part5/5.6_1_r1.png)

![ping](../../images/Part5/5.6_1_ws11.png)

An ICMP "Destination Unreachable" message is returned, demonstrating ICMP usage for network diagnostics.

---

## Navigation

↑ [README](../../README.md)

← [Part 4. Firewall](Part4.md)

→ [Part 6. DHCP Dynamic IP Configuration](Part6.md)

---