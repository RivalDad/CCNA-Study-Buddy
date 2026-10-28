---
aliases: []
tags: ["ccna", "jeremys-it-lab", "routing", "routing", "static-routes", "default-route"]
day: "11B"
order: 12
type: lecture
status: studied
mastery: developing
topic_group: "Routing"
source_video: "https://www.youtube.com/watch?v=YCv4-_sMvYE"
source_transcript: "https://ccna-study-guide.vercel.app/course/jitl/19"
---

# Day 11B — Static Routing

← [[01 - Lessons/11A - Routing Fundamentals|Day 11A — Routing Fundamentals]] · [[00 - CCNA Home|CCNA Home]] · [[01 - Lessons/12 - Life of a Packet|Day 12 — Life of a Packet]] →


## Notebook Highlights

> [!summary] What belongs in the paper notebook
> - Static route: `ip route DESTINATION MASK NEXT-HOP`.
> - Default route = **`0.0.0.0/0`**, least-specific route.
> - `S` = static; `*` marks a candidate default.
> - A router needs a route to the **destination network**, not a route for every intermediate network.
> - **Return path matters**: ping needs routing in both directions.

## Default Gateways and Routed Traffic

An end host that needs to reach a remote network sends the packet to its **default gateway**. The host still keeps the remote endpoint's IP as the **destination IP**; the gateway's MAC is used as the Layer-2 destination for the first hop.

See [[12 - Life of a Packet]] for the complete walk.

## Static Routes

A **static route** is manually configured by an administrator.

### Next-hop form

```cisco
ip route <destination-network> <subnet-mask> <next-hop-ip>
```

Example:

```cisco
ip route 10.40.1.0 255.255.255.192 10.40.3.2
```

### Exit-interface form

```cisco
ip route <destination-network> <subnet-mask> <exit-interface>
```

### Fully specified form

```cisco
ip route <destination-network> <subnet-mask> <exit-interface> <next-hop-ip>
```

Static routes appear with route code:

```text
S
```

The course notes that an exit-interface-only static route can appear as **directly connected** in the route output.

## Default Route

A default route matches when no more-specific route exists.

```text
0.0.0.0/0
```

Configure with a next hop:

```cisco
ip route 0.0.0.0 0.0.0.0 <next-hop-ip>
```

In `show ip route`:

```text
S* 0.0.0.0/0 ...
```

`*` indicates a **candidate default route**.

If IOS displays:

```text
Gateway of last resort is not set
```

there is no active default route selected.

> [!success] Specific beats default
> `0.0.0.0/0` is the least-specific possible IPv4 route. Any more-specific match wins because of longest-prefix matching.

## Router-to-Router Forwarding

A router does **not** need a route to every network link along the path. It needs a route matching the **packet's destination network** and a resolvable way to reach the next hop/exit interface.

At each routed hop:

1. Receive a frame.
2. Remove the old Layer-2 encapsulation.
3. Look up the destination IP.
4. Select next hop/exit interface.
5. Resolve needed Layer-2 address.
6. Build a new Layer-2 frame.
7. Forward.

## The Return-Path Rule

> [!danger] One of the most important troubleshooting rules
> **A working forward route is only half of a conversation.** The destination or downstream router must also know how to route the reply back to the source.

For ping:

```text
Echo Request: source → destination
Echo Reply:   destination → source
```

A packet capture or Packet Tracer simulation may show the request reach the far side while the reply fails because a return route is missing.

## Static Route Troubleshooting

Check in this order:

```text
1. Destination network/mask correct?
2. Next-hop IP correct and reachable?
3. Exit interface correct/up?
4. More-specific route unexpectedly winning?
5. Return route present?
6. Host default gateway correct?
```

Verification:

```cisco
show ip route
show running-config | include ^ip route
ping <next-hop>
traceroute <destination>
```

## Active Recall

> [!question]- Check yourself
> 1. What is the default IPv4 route?
> 2. What route code indicates a static route?
> 3. What does `*` indicate in the routing table?
> 4. Does a router need routes to every intermediate network in a path?
> 5. Why can a one-way route break ping?

> [!check]- Answers
> 1. `0.0.0.0/0`.
> 2. `S`.
> 3. Candidate default route.
> 4. No; it needs a route matching the destination and reachability to the next hop.
> 5. The Echo Reply needs a return path to the source.

## Related Notes

- [[02 - Labs/11.03 - Configuring Static Routes|Static Route Configuration Lab]]
- [[02 - Labs/11.04 - Troubleshooting Static Routes|Static Route Troubleshooting Lab]]
- [[11A - Routing Fundamentals]]
- [[12 - Life of a Packet]]
- [[04 - Reference/Troubleshooting Index|Troubleshooting Index]]


## Sources

- [Jeremy's IT Lab video](https://www.youtube.com/watch?v=YCv4-_sMvYE)
- [Synchronized course transcript / chapter index](https://ccna-study-guide.vercel.app/course/jitl/19)

> [!note] Source fidelity
> These are original study notes organized from the course material, not a transcript. Course-era terminology, figures, and IOS behavior are preserved where they matter for the lesson. Platform/version-specific behavior should be verified on the device you are operating.
