---
aliases: ["15 - VLSM"]
tags: ["ccna", "jeremys-it-lab", "subnetting", "subnetting", "vlsm", "cidr"]
day: "15"
order: 16
type: lecture
status: studied
mastery: developing
topic_group: "Subnetting"
source_video: "https://www.youtube.com/watch?v=z-JqCedc9EI"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/26"
---

# Day 15 — Subnetting Part 3 - VLSM

← [[01 - Lessons/14 - Subnetting Part 2|Day 14 — Subnetting Part 2]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/16 - VLANs Part 1|Day 16 — VLANs Part 1]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - **FLSM** = every subnet same size; **VLSM** = subnet sizes can differ.
> - VLSM rule: **sort largest → smallest and allocate largest first**.
> - Host requirement → add 2 → next power of 2 → host bits → prefix.
> - Every subnet must begin on a boundary valid for **its own prefix**.
> - Verify: no overlaps, no gaps you did not intend, correct gateway/usable ranges.

## FLSM vs VLSM

**FLSM — Fixed Length Subnet Masking:** all subnets use the same prefix length. Simple, but can waste addresses.

**VLSM — Variable Length Subnet Masking:** different subnets use different prefixes according to their actual size requirements.

VLSM lets you fit networks efficiently inside a larger address block.

## Convert Host Requirements to Prefixes

For a normal LAN subnet:

```text
Required hosts + 2
→ round up to next power of 2
→ determine host bits H
→ prefix = 32 - H
```

Common examples:

| Hosts needed | Minimum total addresses | Prefix | Normal usable |
|---:|---:|---:|---:|
| 100 | 128 | /25 | 126 |
| 50 | 64 | /26 | 62 |
| 25 | 32 | /27 | 30 |
| 10 | 16 | /28 | 14 |
| 5 | 8 | /29 | 6 |
| 2 | 4 | /30 | 2 |

## The VLSM Allocation Algorithm

> [!success] Golden rule
> **Allocate the largest requirement first.**

Workflow:

```text
1. List all required networks and host counts.
2. Sort from largest host requirement to smallest.
3. Determine the smallest valid prefix for the largest.
4. Place it on a valid boundary.
5. Begin the next subnet immediately after the previous range.
6. Repeat with progressively smaller networks.
7. Verify boundaries, overlaps, usable ranges, and broadcasts.
```

### Example

Parent network:

```text
192.168.5.0/24
```

Requirements:

```text
LAN-A 100 hosts → /25
LAN-B 50 hosts  → /26
LAN-C 25 hosts  → /27
P2P   2 hosts   → /30
```

A valid largest-first allocation could begin:

```text
192.168.5.0/25      .0-.127
192.168.5.128/26    .128-.191
192.168.5.192/27    .192-.223
192.168.5.224/30    .224-.227
```

Unused space remains available after the final assigned block.

## Boundary Discipline

A subnet cannot begin just because an address is unused. It must begin on a **valid boundary for that prefix**.

Example: a /26 has a block size of 64, so last-octet /26 boundaries are:

```text
0, 64, 128, 192
```

Starting a /26 at `.160` would be invalid even if `.160` happened to be unused.

## Point-to-Point Links

The course VLSM exercises include sizing a point-to-point router link after the larger LANs. A traditional /30 provides exactly two normal usable host addresses and is a common training-lab choice. `/31` point-to-point behavior was introduced in Day 13 as a special case.

## VLSM Verification Checklist

For every subnet record:

```text
Purpose / VLAN
Network/prefix
Subnet mask
First usable
Last usable
Broadcast
Gateway convention
```

Then check:
- No ranges overlap.
- Parent network contains every subnet.
- Each subnet starts on a correct boundary.
- Each has enough usable addresses.

## Active Recall

> [!question]- Check yourself
> 1. Why allocate the largest VLSM subnet first?
> 2. What prefix normally supports 50 hosts?
> 3. Can a /26 begin at any unused address?
> 4. What is the difference between FLSM and VLSM?
> 5. What prefix normally supports a two-host P2P network in traditional subnetting exercises?

> [!check]- Answers
> 1. It prevents small allocations from fragmenting the space needed by large networks.
> 2. /26.
> 3. No; it must start on a valid /26 boundary.
> 4. FLSM uses one prefix size; VLSM uses different sizes according to need.
> 5. /30 (with /31 as a special modern P2P option).

## Related Notes

- [[02 - Labs/15.02 - VLSM Lab|VLSM Lab]]
- [[13 - Subnetting Part 1]]
- [[14 - Subnetting Part 2]]
- [[04 - Reference/Subnetting Cheat Sheet|Subnetting Cheat Sheet]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=z-JqCedc9EI)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/26)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
