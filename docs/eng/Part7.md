## Part 7. NAT

> [Russian version](../ru/Part7_ru.md)

`NAT` (Network Address Translation) modifies IP addresses and ports of packets as they pass through a router. Two variants are used: `SNAT` for outgoing connections and `DNAT` for redirecting incoming connections.

Virtual machines used in this section: `r1`, `r2`, and `ws22`.

`Apache` is a web server that handles HTTP requests and serves web pages over a network.

Install it on each machine:

```bash
sudo apt install apache2
```

---

### 7.1. Web server setup

On `ws22` and `r1`, edit `/etc/apache2/ports.conf` by replacing:

```text
Listen 80
```

with:

```text
Listen 0.0.0.0:80
```

`ws22`:

![/etc/apache2/ports.conf](../../images/Part7/7.1_1_ws22.png)

`r1`:

![/etc/apache2/ports.conf](../../images/Part7/7.1_1_r1.png)

Start `Apache`:

```bash
sudo service apache2 start
```

`ws22`:

![service apache2 start](../../images/Part7/7.1_2_ws22.png)

`r1`:

![service apache2 start](../../images/Part7/7.1_2_r1.png)

---

### 7.2. Basic traffic filtering

On `r2`, create `/etc/firewall.sh` and configure the following rules:

* clear `filter` table;
* clear `nat` table;
* set `FORWARD DROP` policy.

Run the script:

```bash
sudo chmod +x /etc/firewall.sh
sudo /etc/firewall.sh
```

![/etc/firewall.sh](../../images/Part7/7.2_1.png)

Check connectivity between `ws22` and `r1`:

![ping](../../images/Part7/7.2_2.png)

After disabling packet forwarding, communication between nodes is blocked.

---

### 7.3. Allowing ICMP

Add a rule that allows ICMP packet forwarding.

![firewall.sh](../../images/Part7/7.3_1.png)

Restart the script and repeat the test:

![ping](../../images/Part7/7.3_2.png)

After adding the rule, ICMP echo requests are again forwarded through `r2`.

---

### 7.4. SNAT and DNAT configuration

Add the following rules to `r2` configuration:

* SNAT for network `10.20.0.0`;
* DNAT for redirecting port `8080` traffic to the web server on `ws22`.

![firewall.sh](../../images/Part7/7.4_1.png)

Test SNAT by connecting from `ws22` to the web server on `r1`:

```bash
telnet <r1-ip> 80
```

![telnet \<address> \<port>](../../images/Part7/7.4_2.png)

Test DNAT by connecting from `r1` to `r2` on port `8080`:

```bash
telnet <r2-ip> 8080
```

![telnet \<address> \<port>](../../images/Part7/7.4_3.png)

Connection is successfully redirected to the `ws22` web server.

---

## Navigation

↑ [README](../../README.md)

← [Part 6. DHCP Dynamic IP Configuration](Part6_ru.md)

→ [Part 8. SSH Tunnels](Part8_ru.md)

---