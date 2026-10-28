---
aliases: ["08 - IPv4 Networks and Subnets"]
tags: ["ccna", "jeremys-it-lab", "ipv4", "ipv4", "addressing", "interfaces"]
day: "08"
order: 8
type: lecture
status: studied
mastery: developing
topic_group: "IPv4"
source_video: "https://www.youtube.com/watch?v=FiAatRd84XI"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/13"
---

# Day 08 — IPv4 Addressing Part 2

← [[01 - Lessons/07 - IPv4 Addressing Part 1|Day 07 — IPv4 Addressing Part 1]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/09 - Switch Interfaces|Day 09 — Switch Interfaces]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - Normal usable-host formula: **`2^H - 2`**.
> - `show ip interface brief`: **Status = L1**, **Protocol = L2**.
> - Router interfaces are **administratively down by default**; switch ports are not.
> - Configure IPv4 with `ip address <IP> <MASK>` and enable with `no shutdown`.

## Host Capacity

For the normal subnetting cases introduced here:

```text
Usable hosts = 2^H - 2
```

`H` = number of host bits. The subtraction accounts for the network and broadcast addresses.

Historical classful capacities from the course:

| Class | Default prefix | Networks in classful model | Usable hosts per network |
|---|---:|---:|---:|
| A | /8 | 128 | 16,777,214 |
| B | /16 | 16,384 | 65,534 |
| C | /24 | 2,097,152 | 254 |

> [!note]
> These classful counts are historical learning context. Modern addressing uses CIDR/VLSM.

## First and Last Usable Addresses

For a normal subnet:

```text
First usable = network + 1
Last usable  = broadcast - 1
```

Example:

```text
192.168.1.0/24
Network:      192.168.1.0
First usable: 192.168.1.1
Last usable:  192.168.1.254
Broadcast:    192.168.1.255
```

## Cisco Interface Status

The workhorse command:

```cisco
show ip interface brief
```

Interpret the two state columns separately:

| Field | Represents |
|---|---|
| **Status** | Layer 1 state |
| **Protocol** | Layer 2 line protocol state |

Common states:

```text
up/up                       working
administratively down/down  shutdown command applied
down/down                   no physical link / L1 failure
up/down                     L1 present, L2/protocol issue
```

### Router vs switch defaults

- Cisco **router interfaces** are administratively shut down by default in the lesson/platform context.
- Cisco **switch access ports** are not administratively shut down by default.

## Configuring an IPv4 Address on a Router Interface

```cisco
configure terminal
interface gigabitEthernet0/0
 description ## to LAN ##
 ip address 192.168.1.1 255.255.255.0
 no shutdown
```

Useful verification:

```cisco
show ip interface brief
show interfaces description
show running-config interface gigabitEthernet0/0
```

> [!example] Command context
> `ip address` and `description` are **interface configuration mode** commands.  
> `show ip interface brief` is a **privileged EXEC** command.

## End-Host Addressing Checklist

A host normally needs:

```text
IP address
Subnet mask/prefix
Default gateway (for remote networks)
DNS server (for name resolution)
```

An IP and mask can be perfectly valid while the default gateway is wrong, producing local connectivity but no routed connectivity.

## Active Recall

> [!question]- Check yourself
> 1. What is the normal usable-host formula?
> 2. In `show ip interface brief`, which column represents Layer 1?
> 3. What IOS command enables an administratively shut router interface?
> 4. Which command quickly lists IPs and interface states?
> 5. What is the last usable address of `192.168.1.0/24`?

> [!check]- Answers
> 1. `2^H - 2`.
> 2. Status.
> 3. `no shutdown`.
> 4. `show ip interface brief`.
> 5. `192.168.1.254`.

## Related Notes

- [[02 - Labs/08.02 - Configuring IP Addresses|Configuring IP Addresses Lab]]
- [[09 - Switch Interfaces]]
- [[13 - Subnetting Part 1]]
- [[04 - Reference/IOS Command Index|IOS Command Index]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=FiAatRd84XI)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/13)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
