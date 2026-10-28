---
aliases: ["13 - Subnetting Fundamentals"]
tags: ["ccna", "jeremys-it-lab", "subnetting", "subnetting", "cidr", "ipv4"]
day: "13"
order: 14
type: lecture
status: studied
mastery: developing
topic_group: "Subnetting"
source_video: "https://www.youtube.com/watch?v=bQ8sdpGQu8c"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/24"
---

# Day 13 — Subnetting Part 1

← [[01 - Lessons/12 - Life of a Packet|Day 12 — Life of a Packet]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/14 - Subnetting Part 2|Day 14 — Subnetting Part 2]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - CIDR replaced strict classful sizing.
> - **Host bits = `32 - prefix`**.
> - Normal usable hosts = **`2^H - 2`**.
> - Masks: `/25 .128`, `/26 .192`, `/27 .224`, `/28 .240`, `/29 .248`, `/30 .252`.
> - `/31` = point-to-point special case; `/32` = one address/host route.

## From Classful Networks to CIDR

Classful addressing forced networks into /8, /16, or /24 boundaries, which wastes addresses when an organization needs a different-sized network.

**CIDR — Classless Inter-Domain Routing** replaced the strict classful model and allows arbitrary prefix lengths.

Splitting a larger network into smaller networks creates **subnets**.

## Prefix Length and Host Bits

An IPv4 address contains 32 bits.

```text
Host bits H = 32 - prefix length
```

For normal LAN subnets:

```text
Total addresses = 2^H
Usable hosts    = 2^H - 2
```

## Prefix / Mask Table

| Prefix | Dotted-decimal mask | Total addresses | Normal usable |
|---:|---|---:|---:|
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /29 | 255.255.255.248 | 8 | 6 |
| /30 | 255.255.255.252 | 4 | 2 |
| /31 | 255.255.255.254 | 2 | special P2P use |
| /32 | 255.255.255.255 | 1 | one address |

## Splitting a /24

Example: divide `192.168.1.0/24` into four equal subnets.

Need 4 subnets:

```text
2^2 = 4 → borrow 2 bits
/24 + 2 = /26
```

A /26 has 64 addresses, so the subnets begin every 64:

```text
192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26
```

For the first subnet:

```text
Network:   192.168.1.0
First:     192.168.1.1
Last:      192.168.1.62
Broadcast: 192.168.1.63
```

## /31 and /32

### /31

A /31 has two addresses and is useful on certain **point-to-point** links where the traditional network/broadcast concept is not needed in the same way. Treat it as a special point-to-point case rather than applying `2^H - 2` mechanically.

### /32

Represents exactly one IPv4 address. Router local routes are commonly shown as /32s.

> [!danger] Exam trap
> `2^H - 2` is the normal LAN-host formula, not a universal rule for every prefix/application.

## Subnetting Workflow

```text
Prefix → host bits → block size → network boundary → broadcast → usable range
```

This becomes faster in [[14 - Subnetting Part 2]].

## Active Recall

> [!question]- Check yourself
> 1. What does CIDR stand for?
> 2. What mask is /27?
> 3. How many total addresses are in a /28?
> 4. How many normal usable host addresses are in a /30?
> 5. Why is /31 treated specially?

> [!check]- Answers
> 1. Classless Inter-Domain Routing.
> 2. 255.255.255.224.
> 3. 16.
> 4. 2.
> 5. It is used for point-to-point links where both addresses can be used under the special /31 behavior.

## Related Notes

- [[14 - Subnetting Part 2]]
- [[15 - Subnetting Part 3 - VLSM]]
- [[04 - Reference/Subnetting Cheat Sheet|Subnetting Cheat Sheet]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=bQ8sdpGQu8c)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/24)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
