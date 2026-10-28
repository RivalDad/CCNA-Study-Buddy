---
aliases: ["14 - Subnetting Practice"]
tags: ["ccna", "jeremys-it-lab", "subnetting", "subnetting", "binary", "cidr"]
day: "14"
order: 15
type: lecture
status: studied
mastery: developing
topic_group: "Subnetting"
source_video: "https://www.youtube.com/watch?v=IGhd-0di0Qo"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/25"
---

# Day 14 — Subnetting Part 2

← [[01 - Lessons/13 - Subnetting Part 1|Day 13 — Subnetting Part 1]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/15 - Subnetting Part 3 - VLSM|Day 15 — Subnetting Part 3 - VLSM]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - **Block size / subnet increment = `256 - interesting mask octet`**.
> - Find containing range first; **broadcast = next network - 1**.
> - Required subnets: find `S` where **`2^S ≥ number needed`**.
> - New prefix = **original prefix + borrowed bits**.
> - Write boundaries when tired; it prevents off-by-one mistakes.

## The Subnet Increment Shortcut

When a mask has a partially filled octet, identify that **interesting octet** and calculate:

```text
Block size = 256 - mask value
```

Example `/27`:

```text
Mask = 255.255.255.224
256 - 224 = 32
```

Subnet boundaries in the last octet:

```text
0, 32, 64, 96, 128, 160, 192, 224
```

## Find the Subnet Containing a Host

Example:

```text
10.40.0.169/27
```

The /27 increment is 32. Nearby boundaries:

```text
160 ... 191
192 ...
```

Therefore:

```text
Network:   10.40.0.160
Broadcast: 10.40.0.191
First:     10.40.0.161
Last:      10.40.0.190
```

> [!success] Fast rule
> **Network = lower boundary. Broadcast = next network - 1. First/last usable are one inside those boundaries.**

## Borrowing Bits for a Required Number of Subnets

If starting from a larger parent network, borrow `S` host bits until:

```text
2^S ≥ required subnets
```

Then:

```text
New prefix = original prefix + S
```

Example: Need at least 6 equal subnets from a /24.

```text
2^2 = 4  not enough
2^3 = 8  enough
New prefix = /24 + 3 = /27
```

## Class C and Class B Practice

The method does not change when the interesting octet moves.

Example `/20` mask:

```text
255.255.240.0
```

Interesting octet = third octet.

```text
256 - 240 = 16
```

Third-octet boundaries:

```text
0,16,32,48,64,80,96,112,128,144,160,176,192,208,224,240
```

You then find which third-octet block contains the host.

## Fast Prefix Table

| Prefix | Interesting mask | Block size | Total addresses |
|---:|---:|---:|---:|
| /25 | 128 | 128 | 128 |
| /26 | 192 | 64 | 64 |
| /27 | 224 | 32 | 32 |
| /28 | 240 | 16 | 16 |
| /29 | 248 | 8 | 8 |
| /30 | 252 | 4 | 4 |

## The No-Mistakes Workflow

```text
1. Write prefix and mask.
2. Find the interesting octet.
3. Calculate block size.
4. Write the nearby boundaries.
5. Find the containing block.
6. Network = lower boundary.
7. Broadcast = next boundary - 1.
8. First/last = network+1 / broadcast-1.
```

> [!danger] Common mistake
> Do not count forward from the host address. Find the **boundary** first.

## Active Recall

> [!question]- Check yourself
> 1. What is the block size for mask 255.255.255.224?
> 2. Which /27 subnet contains 10.40.0.169?
> 3. How many bits must be borrowed to make at least 8 equal subnets?
> 4. What is the first step after finding the interesting octet?
> 5. How do you get the broadcast address quickly?

> [!check]- Answers
> 1. 32.
> 2. 10.40.0.160/27.
> 3. 3 bits.
> 4. `256 - mask value` to get the block size.
> 5. One less than the next subnet/network boundary.

## Related Notes

- [[13 - Subnetting Part 1]]
- [[15 - Subnetting Part 3 - VLSM]]
- [[04 - Reference/Subnetting Cheat Sheet|Subnetting Cheat Sheet]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=IGhd-0di0Qo)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/25)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
