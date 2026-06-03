# Part 3. `iperf3` Utility

> [Russian version](../ru/Part3_ru.md)

The examples in this section use the virtual machines `ws1` and `ws2`.

`iperf3` is used to measure network connection throughput.

Install `iperf3` on both virtual machines:

```bash
sudo apt install iperf3
```

Start the server on `ws1`:

```bash
iperf3 -s
```

By default, the server listens on TCP port `5201`.

![Starting the iperf3 server](../../images/Part3/3_1.png)

Start the client on `ws2` and connect to the server:

```bash
iperf3 -c 192.168.100.10
```

where `192.168.100.10` is the IP address of `ws1`.

![Starting the iperf3 client](../../images/Part3/3_2.png)

Main output fields:

| Field     | Description                          |
| --------- | ------------------------------------ |
| Transfer  | Amount of transmitted data           |
| Bandwidth | Average throughput                   |
| Retr      | Number of TCP packet retransmissions |
| Cwnd      | TCP congestion window size           |

According to the test results, the average throughput was **1.39 Gbit/s**.

---

## Navigation

↑ [README](../../README.md)

← [Part 2. Static Routing Between Two Machines](Part2.md)

→ [Part 4. Firewall](Part4.md)

---