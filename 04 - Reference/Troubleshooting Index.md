---
tags: [ccna, reference, troubleshooting]
type: reference
---
# Troubleshooting Index

[[00 - CCNA Home|← Home]]

## Start With Scope

Write one precise statement:

```text
Source X cannot reach Destination Y using Protocol/Test Z.
```

Then find the **first boundary that fails** instead of changing random configuration.

## Layered Workflow

### Layer 1 — Physical

- Correct device/port?
- Cable/optic supported?
- Interface shutdown?
- `show ip interface brief`
- `show interfaces status`

### Layer 2 — Ethernet/VLAN

- Correct access VLAN?
- VLAN exists?
- Trunk operational?
- VLAN allowed across trunk?
- Native VLAN compatible?
- MAC being learned?

```cisco
show vlan brief
show interfaces trunk
show mac address-table
```

### ARP

- Does the sender consider destination local or remote?
- Correct subnet mask?
- Correct default gateway?
- ARP entry present?

```cisco
show arp
```

### Layer 3 — IPv4/Routing

- Correct IP/mask?
- Connected/local routes present?
- Static route network/mask correct?
- Next hop reachable?
- Longest-prefix route expected?
- Return path present?

```cisco
show ip route
ping <next-hop>
traceroute <destination>
```

## Common Packet Tracer Traps

- Correct config placed on the **wrong physical interface**.
- Endpoint port accidentally configured as **trunk** instead of access.
- VLAN missing from trunk's **allowed list**.
- Router parent interface still shutdown, leaving subinterfaces down.
- Correct forward static route but no return route.
- Wrong subnet mask causing incorrect local/remote decision.
- DHCP pool overlaps statically assigned infrastructure addresses.

## One-Change Rule

> [!tip]
> Change one thing, rerun the same test, and record what changed. This preserves evidence and teaches you which configuration actually controls the behavior.
