## Part 6. DHCP Dynamic IP Configuration

> [Russian version](../ru/Part6_ru.md)

`DHCP` (Dynamic Host Configuration Protocol) is used to automatically assign network parameters to clients, including IP addresses, subnet masks, default gateways, and DNS servers.

Virtual machines used in this section:

* `r1` and `r2` — routers;
* `ws11`, `ws21`, and `ws22` — workstations.

Install the DHCP server:

```bash
sudo apt install isc-dhcp-server
```

---

### 6.1. DHCP server configuration

On `r2`, configure the DHCP server in `/etc/dhcp/dhcpd.conf`.

![/etc/dhcp/dhcpd.conf](../../images/Part6/6.1_1.png)

To configure DNS resolution, add the following line to `/etc/resolv.conf`:

```text
nameserver 8.8.8.8
```

![/etc/resolv.conf](../../images/Part6/6.1_2.png)

Restart the service:

```bash
sudo systemctl restart isc-dhcp-server
```

![systemctl restart isc-dhcp-server](../../images/Part6/6.1_3.png)

Reboot `ws21` and verify DHCP address assignment:

```bash
ip a
```

Also check connectivity with `ws22`.

![reboot, ip a, ping](../../images/Part6/6.1_4.png)

The subnet `10.20.0.0/26` is configured as a DHCP pool with the address range `10.20.0.2`–`10.20.0.50`.

---

### 6.2. MAC-based address reservation

Configure `ws11` to receive a fixed IP address based on its MAC address.

In `/etc/netplan/00-installer-config.yaml`, specify the MAC address and enable DHCP:

```text
macaddress: 10:10:10:10:10:BA
dhcp4: true
```

![etc/netplan/00-installer-config.yaml](../../images/Part6/6.2_1.png)

Then shut down the virtual machine and set the same MAC address in VirtualBox settings:

```text
Network → Adapter 2 → Advanced → MAC Address
```

Value:

```text
1010101010BA
```

Configure the DHCP server on `r1` for MAC-based address assignment.

File `/etc/dhcp/dhcpd.conf`:

![/etc/dhcp/dhcpd.conf](../../images/Part6/6.2_2.png)

For DNS configuration, add to `/etc/resolv.conf`:

```text
nameserver 8.8.8.8
```

![/etc/resolv.conf](../../images/Part6/6.2_3.png)

Restart the DHCP server:

```bash
sudo systemctl restart isc-dhcp-server
```

![systemctl restart isc-dhcp-server](../../images/Part6/6.2_4.png)

Verify that `ws11` received an address and check connectivity to `ws22`:

![ip a, ping](../../images/Part6/6.2_5.png)

---

### 6.3. DHCP lease renewal

Enable DHCP on `ws21` and `ws22` via Netplan:

```text
dhcp4: true
```

Apply configuration changes:

```bash
sudo netplan apply
```

Check current IP address:

![ip a](../../images/Part6/6.3_1.png)

Release the current lease and request a new one from the DHCP server:

```bash
sudo dhclient -r
sudo dhclient
```

After obtaining a new lease, verify the IP address again:

![dhclient](../../images/Part6/6.3_2.png)

---

## Navigation

↑ [README](../../README.md)

← [Part 5. Static Network Routing](Part5.md)

→ [Part 7. NAT](Part7.md)

---