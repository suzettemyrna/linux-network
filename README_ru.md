# Linux Networking Lab

> English version: [README.md](README.md)

Лабораторный проект по изучению сетевой подсистемы Linux.

В проекте вручную настраиваются:

* IP-адресация и маршрутизация
* DHCP и NAT
* firewall и фильтрация трафика
* SSH-туннелирование
* диагностика сетевых соединений

Все настройки выполняются через консольные инструменты Linux без использования GUI.

## Темы проекта

* IP-адресация и подсети
* `ipcalc`
* статическая маршрутизация
* Netplan
* `tcpdump`, `traceroute`
* `iperf3`
* `iptables`
* DHCP
* NAT (SNAT / DNAT)
* SSH tunneling

## Схема сети

Топология лабораторного стенда:

![Network topology](images/part5_network.png)

## Структура проекта

* [Part 1](docs/ru/Part1_ru.md) — IP-адресация и подсети
* [Part 2](docs/ru/Part2_ru.md) — Статическая маршрутизация между двумя машинами
* [Part 3](docs/ru/Part3_ru.md) — Тестирование пропускной способности сети (`iperf3`)
* [Part 4](docs/ru/Part4_ru.md) — Настройка `iptables` и сканирование портов (`nmap`)
* [Part 5](docs/ru/Part5_ru.md) — Маршрутизация между несколькими сетями
* [Part 6](docs/ru/Part6_ru.md) — DHCP и автоматическая настройка сети
* [Part 7](docs/ru/Part7_ru.md) — NAT (SNAT / DNAT)
* [Part 8](docs/ru/Part8_ru.md) — SSH-туннелирование

## Структура репозитория

```text
.
├── docs/         # Основная документация
├── images/       # Схемы и скриншоты
├── notes/        # Дополнительные заметки
├── README_ru.md  # Русская версия README
└── README.md     # English README
```

## Используемые технологии

### Сетевые инструменты

* Netplan
* iproute2
* iptables
* isc-dhcp-server
* OpenSSH

### Диагностика сети

* tcpdump
* traceroute
* iperf3
* nmap
* ip

## Требования

* VirtualBox или аналог
* Ubuntu Server 20.04+
* root/sudo доступ
* минимум 5 виртуальных машин

## Цель проекта

Практическое изучение:

* маршрутизации IP-пакетов
* настройки сетевых интерфейсов
* работы NAT и firewall
* DHCP
* диагностики сетевых проблем