---
aliases: ["10 - IPv4 Header"]
tags: ["ccna", "jeremys-it-lab", "ipv4", "ipv4", "header", "fragmentation"]
day: "10"
order: 10
type: lecture
status: studied
mastery: developing
topic_group: "IPv4"
source_video: "https://www.youtube.com/watch?v=aQB22y4liXA"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/17"
---

# Day 10 — IPv4 Header

← [[01 - Lessons/09 - Switch Interfaces|Day 09 — Switch Interfaces]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/11A - Routing Fundamentals|Day 11A — Routing Fundamentals]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - Field-size memory pattern: **`4 4 6 2 16 / 16 3 13 / 8 8 16 / 32 / 32`**.
> - IHL counts **32-bit (4-byte) words**: min 5 = 20 B, max 15 = 60 B.
> - **TTL decrements at every router**; packet is dropped at 0.
> - Protocol numbers: **ICMP 1, TCP 6, UDP 17, OSPF 89**.
> - Fragmentation fields: **Identification + Flags (DF/MF) + Fragment Offset**.

## IPv4 Header Layout

| Field | Bits | What it tells us |
|---|---:|---|
| Version | 4 | IP version (`4` for IPv4) |
| IHL | 4 | Header length in 32-bit words |
| DSCP | 6 | QoS / traffic treatment |
| ECN | 2 | Explicit congestion notification |
| Total Length | 16 | Entire IPv4 packet length |
| Identification | 16 | Associates fragments with original packet |
| Flags | 3 | Fragmentation controls/status |
| Fragment Offset | 13 | Fragment position in original packet |
| TTL | 8 | Loop prevention / hop limit behavior |
| Protocol | 8 | Encapsulated next-layer protocol |
| Header Checksum | 16 | Error check for IPv4 header |
| Source IP | 32 | Original source IPv4 address |
| Destination IP | 32 | Final destination IPv4 address |
| Options | 0-320 | Optional header data; padded to 32-bit boundary |

### Field-size memory pattern

```text
4 4 6 2 16
16 3 13
8 8 16
32
32
Options 0-320 bits
```

## Version and IHL

**Version:** 4-bit field. IPv4 value = decimal 4 / binary `0100`.

**IHL (Internet Header Length):** 4 bits, measured in **4-byte (32-bit) units**.

```text
IHL 5  = 20 bytes (minimum IPv4 header)
IHL 6  = 24 bytes
IHL 15 = 60 bytes (maximum header)
```

## DSCP and ECN

**DSCP — Differentiated Services Code Point (6 bits):** used for QoS classification/priority treatment, especially for delay-sensitive traffic.

**ECN — Explicit Congestion Notification (2 bits):** supports end-to-end signaling of congestion without necessarily relying only on packet loss.

## Total Length

16 bits; indicates the complete IPv4 packet size, header plus payload.

```text
Minimum: 20 bytes
Maximum: 65,535 bytes
```

## Fragmentation Fields

IPv4 fragmentation can occur when a packet is larger than the outgoing interface's **MTU (Maximum Transmission Unit)**. The course uses **1500 bytes** as the common Ethernet MTU figure.

### Identification — 16 bits

Fragments created from the same original packet use the same Identification value so the destination can associate them.

### Flags — 3 bits

```text
Bit 0 = Reserved (0)
Bit 1 = DF — Don't Fragment
Bit 2 = MF — More Fragments
```

An unfragmented packet has **MF = 0**.

### Fragment Offset — 13 bits

Identifies where a fragment belongs in the original packet. The offset is measured in **8-byte units**.

> [!danger] Exam trap
> Fragment Offset is a position, not simply “fragment number 1, 2, 3…”.

## TTL — Time to Live

8 bits. Each router that forwards an IPv4 packet decreases TTL. If TTL reaches 0, the router drops the packet. This prevents a routing loop from circulating a packet indefinitely.

Course-recommended/default study value:

```text
64
```

## Protocol — 8 bits

Identifies the protocol carried in the IPv4 payload.

| Value | Protocol |
|---:|---|
| 1 | ICMP |
| 6 | TCP |
| 17 | UDP |
| 89 | OSPF |

## Header Checksum — 16 bits

Checks the **IPv4 header only**, not the payload. Because a router changes TTL, the header checksum must be updated as the packet is routed.

## Source and Destination IP

Both fields are **32 bits**.

During normal routing (no NAT discussed here):

```text
Source IP       normally stays the same end-to-end
Destination IP  normally stays the same end-to-end
Layer-2 MACs    change hop-by-hop
TTL             changes at routers
Header checksum changes when header changes
```

## Wireshark Reading Strategy

When examining an IPv4 header, do not memorize a screen position. Read the fields in a consistent order:

```text
Version/IHL → DSCP/ECN → Length
→ Identification/Flags/Offset
→ TTL/Protocol/Checksum
→ Source/Destination → Options
```

## Active Recall

> [!question]- Check yourself
> 1. How many bits is IHL and what unit does it count?
> 2. What are the four protocol numbers we are memorizing?
> 3. Which three fields matter most for fragmentation?
> 4. Why does a router update the IPv4 header checksum?
> 5. What happens when TTL reaches 0?

> [!check]- Answers
> 1. 4 bits; 32-bit/4-byte words.
> 2. ICMP 1, TCP 6, UDP 17, OSPF 89.
> 3. Identification, Flags, Fragment Offset.
> 4. The router changes TTL, so the header contents changed.
> 5. The router drops the packet.

## Related Notes

- [[03 - TCP-IP and OSI Models]]
- [[12 - Life of a Packet]]
- [[04 - Reference/Packet Walks|Packet Walks]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=aQB22y4liXA)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/17)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
