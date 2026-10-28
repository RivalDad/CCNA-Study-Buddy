---
tags: [ccna, reference, packet-walk, routing, arp]
type: reference
---
# Packet Walks

[[00 - CCNA Home|← Home]]

## The One-Sentence Model

> [!summary]
> **IP addresses identify the end-to-end Layer-3 conversation; MAC addresses deliver the frame over the current Layer-2 hop.**

## Same-Subnet Walk

```text
PC-A checks mask → destination is local
↓
ARP for PC-B IP if MAC unknown
↓
ARP Reply provides PC-B MAC
↓
Ethernet frame:
  Src MAC = PC-A
  Dst MAC = PC-B
  Src IP  = PC-A
  Dst IP  = PC-B
↓
Switch forwards frame
```

## Remote-Subnet Walk

```text
PC-A checks mask → destination is remote
↓
ARP for DEFAULT GATEWAY IP
↓
Frame 1:
  Src MAC = PC-A
  Dst MAC = R1 LAN interface
  Src IP  = PC-A
  Dst IP  = PC-B
↓
R1 removes L2 header/trailer
↓
R1 routes based on Dst IP
↓
R1 ARPs for next hop if needed
↓
R1 creates NEW frame
↓
Repeat at each router
```

## What Changes at a Router?

| Item | Changes? |
|---|---|
| Source IP | Normally no |
| Destination IP | Normally no |
| Source MAC | Yes |
| Destination MAC | Yes |
| TTL | Yes — decreases |
| IPv4 header checksum | Yes when header changes |

## VLAN-to-VLAN Walk (ROAS)

```text
PC VLAN10
→ access port (untagged)
→ switch trunk (802.1Q VLAN10)
→ router .10 subinterface
→ route to VLAN20
→ router .20 subinterface
→ switch trunk (802.1Q VLAN20)
→ access port (untagged)
→ PC VLAN20
```

## Packet-Walk Questions

At every hop answer:

1. Destination IP?
2. Local or remote from the sender's perspective?
3. Which MAC is needed for this link?
4. Is ARP required?
5. What will the switch do with the destination MAC?
6. Which route wins by longest-prefix match?
7. Is the return path valid?

Related: [[01 - Lessons/06 - Ethernet LAN Switching Part 2 and ARP]] · [[01 - Lessons/11A - Routing Fundamentals]] · [[01 - Lessons/12 - Life of a Packet]]
