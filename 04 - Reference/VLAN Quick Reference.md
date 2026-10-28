---
tags: [ccna, reference, vlan, 8021q, roas]
type: reference
---
# VLAN Quick Reference

[[00 - CCNA Home|← Home]]

## Mental Model

```text
Access port  = puts endpoint INTO one VLAN
Trunk        = MOVES multiple VLANs between devices
Router/L3    = ROUTES BETWEEN VLANs
```

## Access Port

```cisco
vlan 10
 name ADMIN

interface fa0/1
 switchport mode access
 switchport access vlan 10
```

## Trunk

```cisco
interface g0/1
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 switchport trunk native vlan 99
```

Modify allowed list:

```cisco
switchport trunk allowed vlan add 40
switchport trunk allowed vlan remove 20
```

Verify:

```cisco
show vlan brief
show interfaces trunk
show interfaces <interface> switchport
```

## 802.1Q Tag

```text
4 bytes inserted after Source MAC
TPID 16 bits = 0x8100
PCP   3 bits  = priority/CoS
DEI   1 bit   = drop eligible
VID  12 bits  = VLAN ID
```

VLAN IDs:

```text
0 and 4095 reserved
1-4094 usable
1-1005 normal
1006-4094 extended
```

## Native VLAN

Default = VLAN 1. Native traffic is normally untagged on the trunk. Untagged inbound trunk traffic is mapped to the native VLAN.

## Router-on-a-Stick

```cisco
interface g0/0/1
 no ip address
 no shutdown

interface g0/0/1.10
 encapsulation dot1q 10
 ip address <gateway> <mask>
```

## Troubleshooting

```text
VLAN exists
→ endpoint access mode/VLAN correct
→ trunk up
→ VLAN allowed
→ native VLAN compatible
→ router parent up
→ dot1Q ID correct
→ gateway IP/mask correct
```

Related: [[01 - Lessons/16 - VLANs Part 1]] · [[01 - Lessons/17 - VLANs Part 2]]
