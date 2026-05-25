# Linux Networking Lab

>English verion: [README.md](README.md)

Проект посвящён изучению сетевой подсистемы Linux на уровне настройки и диагностики. Включает работу с IP-адресацией, маршрутизацией, фильтрацией трафика и базовыми сетевыми сервисами.

## Содержание

Проект охватывает следующие темы:

* Работа с IP-адресацией и подсетями
* Использование утилиты `ipcalc` для анализа сетей
* Статическая маршрутизация между хостами и через маршрутизаторы
* Настройка сетевых интерфейсов через Netplan
* Анализ сетевого трафика (`tcpdump`, `traceroute`)
* Тестирование пропускной способности (`iperf3`)
* Настройка фильтрации трафика (`iptables`)
* Работа с сетевыми экранами (firewall)
* DHCP: динамическая выдача IP-адресов и резервации по MAC
* NAT (SNAT / DNAT)
* SSH-туннелирование (local / remote forwarding)

## Схема сети

Собранная топология лабораторного стенда (роутеры, рабочие станции, сегменты сети).

![Network topology](images/part5_network.png)

## Структура проекта

The project is divided into logical parts:

* [Part 1](docs/eng/Part1.md) — IP addressing and subnetting
* [Part 2](docs/eng/Part2.md) — Basic static routing between two machines
* [Part 3](docs/eng/Part3.md) — Network throughput testing (`iperf3`)
* [Part 4](docs/eng/Part4.md) — Basic firewall configuration (`iptables`) and port scanning (`nmap`)
* [Part 5](docs/eng/Part5.md) — Multi-node static routing
* [Part 6](docs/eng/Part6.md) — DHCP and automatic network configuration
* [Part 7](docs/eng/Part7.md) — NAT (SNAT / DNAT) and service access
* [Part 8](docs/eng/Part8.md) — SSH tunneling

## Структура репозитория

```text
.
├── docs/         # Основная документация проекта (пошаговые инструкции)
├── images/       # Схемы сети и скриншоты
├── notes/        # Дополнительные заметки и пояснения (необязательные материалы)
├── README_ru.md  # Описание проекта (русская версия)
└── README.md     # Описание проекта (английская версия)
```

## Используемые технологии

**1. Основные технологии**

- Linux networking stack
- Netplan
- iproute2
- iptables
- DHCP (isc-dhcp-server)
- NAT (SNAT / DNAT)
- SSH tunneling

**2. Инструменты диагностики**
- tcpdump
- traceroute
- iperf3
- nmap
- ip

## Особенности реализации

* Полная настройка сетевых интерфейсов без использования GUI инструментов
* Ручная конфигурация маршрутизации и DHCP
* Разделение ролей машин (workstations / routers)
* Проверка связности через ICMP и TCP
* Анализ поведения пакетов на уровне маршрутизаторов

## Требования

Для воспроизведения окружения:

* VirtualBox или аналог
* Ubuntu Server (рекомендуется 20.04+)
* root/sudo доступ
* минимум 5 виртуальных машин (для Part 5+)

## Цель проекта

Понимание того, как в Linux реализованы:

* маршрутизация IP-пакетов
* работа сетевых интерфейсов
* механизмы NAT и firewall
* автоматическая конфигурация сети (DHCP)
* диагностика сетевых проблем на уровне пакетов