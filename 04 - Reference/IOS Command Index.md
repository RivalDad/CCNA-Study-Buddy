---
tags: [ccna, reference, ios, commands]
type: reference
---
# IOS Command Index — Days 1-17

[[00 - CCNA Home|← Home]]

> [!tip]
> Learn the **mode** with the command. The same text copied at the wrong prompt is not a valid workflow.

## Navigation & Configuration

| Purpose | Command | Mode |
|---|---|---|
| Privileged EXEC | `enable` | User EXEC |
| Global config | `configure terminal` | Privileged EXEC |
| Back one level | `exit` | Any submode |
| Return to privileged EXEC | `end` | Config modes |
| Context help | `?` | Any |
| Run EXEC command from config mode | `do <command>` | Config modes |
| Remove/reverse config | `no <command>` | Matching config mode |

## Configuration Files

| Purpose | Command |
|---|---|
| Active config | `show running-config` |
| Saved boot config | `show startup-config` |
| Save | `copy running-config startup-config` |
| Save (legacy shortcut) | `write memory` |

## Basic Device Configuration

```cisco
hostname R1
enable password <password>
enable secret <secret>
service password-encryption
```

## Interfaces

```cisco
show ip interface brief
show interfaces
show interfaces status
show interfaces description
show interfaces counters errors
```

```cisco
interface <interface-id>
 description <text>
 ip address <ip> <mask>
 no shutdown
 speed <value>
 duplex <full|half|auto>
```

Multiple ports:

```cisco
interface range <range>
```

## MAC / ARP

```cisco
show mac address-table
clear mac address-table dynamic
clear mac address-table dynamic address <mac>
clear mac address-table dynamic interface <interface>
show arp
```

## Routing

```cisco
show ip route
ip route <network> <mask> <next-hop>
ip route <network> <mask> <exit-interface>
ip route <network> <mask> <exit-interface> <next-hop>
ip route 0.0.0.0 0.0.0.0 <next-hop>
```

## VLANs — Access Ports

```cisco
vlan 10
 name ADMIN

interface <interface>
 switchport mode access
 switchport access vlan 10
```

Verify:

```cisco
show vlan brief
```

## VLANs — Trunks

```cisco
interface <interface>
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 switchport trunk allowed vlan add 40
 switchport trunk allowed vlan remove 20
 switchport trunk native vlan 99
```

On platforms that expose it:

```cisco
switchport trunk encapsulation dot1q
```

Verify:

```cisco
show interfaces trunk
show interfaces <interface> switchport
```

## Router-on-a-Stick

```cisco
interface g0/0/1
 no ip address
 no shutdown

interface g0/0/1.10
 encapsulation dot1q 10
 ip address <gateway> <mask>
```

## Verification Philosophy

```text
Configure → show command → test traffic → inspect tables → save
```

Related: [[04 - Reference/Troubleshooting Index]] · [[04 - Reference/VLAN Quick Reference]]
