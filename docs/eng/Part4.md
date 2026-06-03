# Part 4. Firewall

> [Русская версия](../ru/Part4_ru.md)

The examples in this section use the virtual machines `ws1` and `ws2`.

### 4.1. iptables Utility

`iptables` is used to configure network traffic filtering rules in Linux.

To create a firewall on both machines, create the file `/etc/firewall.sh` on each machine and configure it as follows:

* For `ws1`:

  ![/etc/firewall.sh](../../images/Part4/4.1_1_ws1.png)

* For `ws2`:

  ![/etc/firewall.sh](../../images/Part4/4.1_1_ws2.png)

**Scripts explanation:**

1. `iptables -F` — clears existing rules.

2. `iptables -X` — removes user-defined chains.

3. `iptables -A INPUT -p TCP --dport=22 -j ACCEPT` — allows incoming SSH connections (port 22).

4. `iptables -A INPUT -p TCP --dport=80 -j ACCEPT` — allows incoming HTTP connections (port 80).

5. `iptables -A OUTPUT -p ICMP --icmp-type echo-reply -j DROP` — blocks outgoing ICMP echo-reply packets.

6. `iptables -A OUTPUT -p ICMP --icmp-type echo-reply -j ACCEPT` — allows outgoing ICMP echo-reply packets.

Make the script executable and run it on both machines:

```bash
sudo chmod +x /etc/firewall.sh
sudo /etc/firewall.sh
```

![sudo /etc/firewall.sh](../../images/Part4/4.1_2_ws1.png)
![sudo /etc/firewall.sh](../../images/Part4/4.1_2_ws2.png)

**Configuration differences:**

On `ws1`, outgoing ICMP echo-reply packets are blocked, so the machine does not respond to ping requests.

On `ws2`, outgoing ICMP echo-reply packets are allowed, so the machine responds to ping requests.

---

### 4.2. nmap Utility

`nmap` is used to verify host availability.

On `ws2`, ICMP replies are allowed:

![ping ws2](../../images/Part4/4.2_1_ws1.png)

On `ws1`, ICMP replies are blocked:

![ping ws1](../../images/Part4/4.2_1_ws2.png)

Despite not responding to ping requests, an `nmap` scan shows that `ws1` is reachable.

![nmap](../../images/Part4/4.2_2.png)

---

## Navigation

↑ [README](../../README.md)

← [Part 3. iperf3 Utility](Part3.md)

→ [Part 5. Static Network Routing](Part5.md)

---