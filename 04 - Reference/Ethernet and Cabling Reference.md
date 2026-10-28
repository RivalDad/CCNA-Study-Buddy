---
tags: [ccna, reference, ethernet, cabling]
type: reference
---
# Ethernet & Cabling Reference

[[00 - CCNA Home|← Home]]

## Copper

| Standard | IEEE | Speed | Pairs | Distance |
|---|---|---:|---:|---:|
| 10BASE-T | 802.3i | 10 Mb/s | 2 | 100 m |
| 100BASE-TX | 802.3u | 100 Mb/s | 2 | 100 m |
| 1000BASE-T | 802.3ab | 1 Gb/s | 4 | 100 m |
| 10GBASE-T | 802.3an | 10 Gb/s | 4 | 100 m |

RJ-45 = **8 pins**. UTP = **Unshielded Twisted Pair**.

### 10/100 pin-role memory

```text
PC/router/firewall: Tx 1-2, Rx 3-6
Switch:             opposite
```

Without Auto MDI-X:

```text
Different device types → straight-through
Same device types      → crossover
```

## Fiber

| Standard | IEEE | Fiber | Course distance |
|---|---|---|---:|
| 1000BASE-LX | 802.3z | MMF | ~550 m |
| 1000BASE-LX | 802.3z | SMF | ~5 km |
| 10GBASE-SR | 802.3ae | MMF | ~400 m |
| 10GBASE-LR | 802.3ae | SMF | ~10 km |
| 10GBASE-ER | 802.3ae | SMF | ~30 km course figure |

## Ethernet Frame Fields

```text
Preamble 7 | SFD 1 | Dst MAC 6 | Src MAC 6 | Type/Length 2 | Payload | FCS 4
```

Important EtherTypes:

```text
IPv4 0x0800
ARP  0x0806
IPv6 0x86DD
```

Minimum frame excluding Preamble/SFD = **64 bytes**. Minimum payload = **46 bytes**.

Related: [[01 - Lessons/02 - Interfaces and Cables]] · [[01 - Lessons/05 - Ethernet LAN Switching Part 1]] · [[01 - Lessons/06 - Ethernet LAN Switching Part 2 and ARP]]
