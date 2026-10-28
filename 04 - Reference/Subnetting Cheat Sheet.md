---
tags: [ccna, reference, subnetting, ipv4]
type: reference
---
# Subnetting Cheat Sheet

[[00 - CCNA Home|← Home]]

## Core Formulas

```text
Host bits H        = 32 - prefix
Total addresses    = 2^H
Normal usable      = 2^H - 2
Block size         = 256 - interesting mask octet
Borrowed bits S    = smallest S where 2^S >= required subnets
New prefix         = original prefix + S
```

## Prefix Table

| Prefix | Mask | Total | Normal usable | Block size in last octet* |
|---:|---|---:|---:|---:|
| /24 | 255.255.255.0 | 256 | 254 | 256 |
| /25 | 255.255.255.128 | 128 | 126 | 128 |
| /26 | 255.255.255.192 | 64 | 62 | 64 |
| /27 | 255.255.255.224 | 32 | 30 | 32 |
| /28 | 255.255.255.240 | 16 | 14 | 16 |
| /29 | 255.255.255.248 | 8 | 6 | 8 |
| /30 | 255.255.255.252 | 4 | 2 | 4 |
| /31 | 255.255.255.254 | 2 | P2P special case | 2 |
| /32 | 255.255.255.255 | 1 | one address | 1 |

`*` When the interesting octet is the fourth octet. The same subtraction method works in whichever octet is interesting.

## Find Network/Broadcast Fast

```text
1. Prefix → mask.
2. Find interesting octet.
3. Block size = 256 - mask value.
4. Write nearby multiples of block size.
5. Network = lower boundary.
6. Broadcast = next boundary - 1.
7. First = network + 1.
8. Last = broadcast - 1.
```

## Required Hosts → Prefix

```text
Hosts needed + 2
→ next power of 2
→ H host bits
→ prefix = 32-H
```

| Required hosts | Choose at least | Prefix |
|---:|---:|---:|
| 100 | 128 addresses | /25 |
| 50 | 64 | /26 |
| 25 | 32 | /27 |
| 10 | 16 | /28 |
| 5 | 8 | /29 |
| 2 | 4 | /30 |

## Example

`10.40.0.169/27`

```text
Mask:       255.255.255.224
Block size: 32
Boundaries: ...128,160,192...
Network:    10.40.0.160
Broadcast:  10.40.0.191
First:      10.40.0.161
Last:       10.40.0.190
```

## VLSM

> [!warning]
> Sort requirements **largest to smallest**, allocate the largest first, and ensure every subnet starts on a valid boundary for its own prefix.

Related: [[01 - Lessons/13 - Subnetting Part 1]] · [[01 - Lessons/14 - Subnetting Part 2]] · [[01 - Lessons/15 - Subnetting Part 3 - VLSM]]
