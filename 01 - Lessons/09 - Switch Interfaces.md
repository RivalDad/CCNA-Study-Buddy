---
aliases: ["09 - Switch Interfaces"]
tags: ["ccna", "jeremys-it-lab", "ethernet", "switching", "interfaces", "duplex"]
day: "09"
order: 9
type: lecture
status: studied
mastery: developing
topic_group: "Ethernet"
source_video: "https://www.youtube.com/watch?v=cCqluocfQe0"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/15"
---

# Day 09 — Switch Interfaces

← [[01 - Lessons/08 - IPv4 Addressing Part 2|Day 08 — IPv4 Addressing Part 2]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/10 - IPv4 Header|Day 10 — IPv4 Header]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - `show ip interface brief` gives a fast **up/down** picture.
> - Speed and duplex default to **auto** in the lesson.
> - **Full duplex** = send/receive simultaneously; **half duplex** = one direction at a time.
> - **Hub = one collision domain, Layer 1, half duplex**.
> - Error counters: **runts, giants, CRC, frame, input errors, output errors**.

## Default Interface States

Typical course/platform behavior:

```text
Router interface, default: administratively down/down
Connected switch port:      up/up
Unconnected switch port:    down/down
```

Use:

```cisco
show ip interface brief
show interfaces status
```

## Speed and Duplex

Default configuration in the lesson:

```text
speed  = auto
duplex = auto
```

Manual configuration examples:

```cisco
interface gigabitEthernet0/1
 speed 100
 duplex full
```

Configure multiple interfaces:

```cisco
interface range fastEthernet0/1 - 4
```

> [!warning] Behavior / rule
> Manual speed/duplex settings must be compatible at both ends. Auto-negotiation is intended to select compatible link parameters automatically.

## Full vs Half Duplex

**Full duplex:** device can transmit and receive simultaneously.

**Half duplex:** device cannot transmit and receive simultaneously; collisions can occur on shared Ethernet media.

### Ethernet hubs and collision domains

A hub:
- Operates at **Layer 1**.
- Repeats incoming signals to other ports.
- Places attached devices in one shared **collision domain**.
- Requires half-duplex behavior.

A switch:
- Gives each switch port its own collision domain.
- Supports full-duplex links.

### CSMA/CD

**Carrier Sense Multiple Access with Collision Detection** is used to manage collisions on half-duplex shared Ethernet.

In modern switched full-duplex Ethernet, collisions should not be normal.

## Interface Error Counters

Inspect detailed statistics:

```cisco
show interfaces
```

Important counters from the course:

| Counter | Meaning |
|---|---|
| **runts** | Frames smaller than 64 bytes |
| **giants** | Frames larger than the course's normal max frame size (1518 bytes) |
| **CRC** | Frames failing FCS/CRC validation |
| **frame** | Frames with invalid/illegal formatting/alignment |
| **input errors** | Aggregate receive-side errors |
| **output errors** | Frames the device attempted but failed to transmit properly |

> [!danger] Troubleshooting lesson
> Do not begin by changing configuration. Check **physical connection → correct interface → status → speed/duplex → error counters → Layer-2 configuration**.

## Useful Interface Configuration Pattern

```cisco
configure terminal
interface gigabitEthernet0/1
 description ## Uplink to SW2 ##
 no shutdown
```

Disable unused interfaces when appropriate:

```cisco
interface range fastEthernet0/10 - 24
 shutdown
```

Verify:

```cisco
show interfaces description
show interfaces status
show interfaces counters errors
show ip interface brief
```

## Active Recall

> [!question]- Check yourself
> 1. What is the difference between full and half duplex?
> 2. Which Layer does an Ethernet hub operate at?
> 3. What does a CRC counter suggest?
> 4. What are the default speed and duplex settings in the lesson?
> 5. What command configures several interfaces at once?

> [!check]- Answers
> 1. Full duplex can send and receive simultaneously; half duplex cannot.
> 2. Layer 1.
> 3. Ethernet frames failing their FCS/CRC check; investigate media/link quality and duplex issues.
> 4. Auto/auto.
> 5. `interface range`.

## Related Notes

- [[02 - Labs/09.02 - Configuring Interfaces|Configuring Interfaces Lab]]
- [[02 - Interfaces and Cables]]
- [[05 - Ethernet LAN Switching Part 1]]
- [[04 - Reference/Troubleshooting Index|Troubleshooting Index]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=cCqluocfQe0)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/15)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
