# Part 1. ipcalc Utility

> [Russian version](../ru/Part1_ru.md)

The examples in this section use the virtual machine `ws1`.

### 1.1. Networks and Masks

#### 1. Determining the Network Address

The network address can be determined using `ipcalc`:

```bash
ipcalc 192.167.38.54/13 | grep Network
```

Result:

```text
Network:   192.160.0.0/13
```

Therefore, the network address is `192.160.0.0`.

![ipcalc output](../../images/Part1/1.1_1.png)

#### 2. Converting Subnet Masks

Subnet masks can be converted using `ipcalc`:

```bash
ipcalc <mask> | grep Netmask
```

* Mask `/15`:

  * Dotted-decimal notation: 255.254.0.0

  * Binary notation: 11111111.11111110.00000000.00000000

  ![Mask /15 in dotted-decimal and binary notation](../../images/Part1/1.1_2.png)

* Mask `255.255.255.0`:

  * Prefix notation: `/24`

  * Binary notation: `11111111.11111111.11111111.00000000`

  ![Mask 255.255.255.0 in prefix and binary notation](../../images/Part1/1.1_3.png)

#### 3. Minimum and Maximum Host Addresses

Determine the minimum and maximum host addresses for `12.167.38.4` using different subnet masks:

```bash
ipcalc <IP-address>/<mask> | grep -e Min -e Max
```

| Mask  | Minimum Address | Maximum Address  |
| ----- | --------------- | ---------------- |
| `/8`  | `12.0.0.1`      | `12.255.255.254` |
| `/16` | `12.167.0.1`    | `12.167.255.254` |
| `/23` | `12.167.38.1`   | `12.167.39.254`  |
| `/4`  | `0.0.0.1`       | `15.255.255.254` |

![Minimum and maximum host addresses](../../images/Part1/1.1_4.png)

---

### 1.2. localhost

Addresses from the `127.0.0.0/8` range are reserved for the loopback interface (`localhost`).

Access to localhost is only possible from addresses within the `127.0.0.0/8` range.

| IP Address      | Access to localhost |
| --------------- | ------------------- |
| `194.34.23.100` | No                  |
| `127.0.0.2`     | Yes                 |
| `127.1.0.1`     | Yes                 |
| `128.0.0.1`     | No                  |

---

### 1.3. Network Ranges and Segments

#### 1. Public and Private IP Addresses

Determine which of the following addresses are private and which are public using:

```bash
ipcalc <IP-address> | grep Hosts
```

`ipcalc` indicates whether an address belongs to a `private network`.

IP address classification:

| Private IP Addresses | Public IP Addresses |
| -------------------- | ------------------- |
| `10.0.0.45`          | `134.43.0.2`        |
| `192.168.4.2`        | `172.0.2.1`         |
| `172.20.250.4`       | `192.172.0.1`       |
| `172.16.255.255`     | `172.68.0.2`        |
| `10.10.10.10`        | `192.169.168.1`     |

![Public and private IP addresses](../../images/Part1/1.3_1.png)

#### 2. Possible Gateway Addresses for a Network

Determine the address range of the `10.10.0.0/18` network:

```bash
ipcalc 10.10.0.0/18 | grep Broadcast
```

Output:

```text
Broadcast: 10.10.63.255     00001010.00001010.00 111111.11111111
```

![Network address range](../../images/Part1/1.3_2.png)

Valid host addresses are in the range:

* from `10.10.0.1`
* to `10.10.63.254`

Therefore, the following addresses can be used as a gateway:

* `10.10.0.2`
* `10.10.10.10`
* `10.10.1.255`

The following addresses cannot be used:

* `10.0.0.1`
* `10.10.100.1`

---

## Navigation

↑ [README](../../README.md)

→ [Part 2. Static Routing Between Two Machines](Part2.md)

---