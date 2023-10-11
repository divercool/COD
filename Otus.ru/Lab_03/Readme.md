# Настройка протокола IS-IS для сети Underlay

Схема сети IS-IS

![!\[Alt text\](image.png)](Network_Topology.png)
# Конфигурация интерфейсов Leaf_01

```python
interface Ethernet0/0
 no switchport
 ip address 10.100.1.2 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/1
 no switchport
 ip address 10.100.2.2 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 10
 switchport mode trunk
!
interface Vlan10
 ip address 192.168.0.1 255.255.254.0
 ip router isis 1
!
router isis 1
 net 49.0001.3333.3333.3333.00
 is-type level-1
!
ip route 0.0.0.0 0.0.0.0 10.100.1.1
```
# Конфигурация интерфейсов Leaf_02

```python
interface Ethernet0/0
 no switchport
 ip address 10.100.1.6 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/1
 no switchport
 ip address 10.100.2.6 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 10
 switchport mode trunk
!
interface Ethernet0/3
!
interface Vlan10
 ip address 10.10.0.1 255.255.254.0
 ip router isis 1
 isis network point-to-point 
!
router isis 1
 net 49.0001.4444.4444.4444.00
 is-type level-1
!
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 10.100.1.5
```

# Конфигурация интерфейсов Leaf_03

```python
interface Ethernet0/0
 no switchport
 ip address 10.100.1.10 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/1
 no switchport
 ip address 10.100.2.10 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 10
 switchport mode trunk
!
interface Ethernet0/3
!
interface Vlan10
 ip address 192.168.2.1 255.255.254.0
 ip router isis 1
!
router isis 1
 net 49.0001.5555.5555.5555.00
 is-type level-1
!
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 10.100.1.9
```

# Конфигурация интерфейсов Leaf_04
```python
interface Ethernet0/0
 no switchport
 ip address 10.200.1.2 255.255.255.252
 ip router isis 1
 duplex auto
 isis network point-to-point 
!
interface Ethernet0/1
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 10
 switchport mode trunk
!
interface Ethernet0/3
!
interface Vlan10
 ip address 172.30.0.1 255.255.254.0
 ip router isis 1
 isis network point-to-point 
!         
router isis 1
 net 49.0002.1235.1235.1235.00
 is-type level-1

```

# Конфигурация интерфейсов Spine_01


```python
interface port-channel1
  no switchport
  ip address 10.100.0.1/30
  ip router isis 1

interface Ethernet1/1
  no switchport
  channel-group 1 mode active
  no shutdown

interface Ethernet1/2
  no switchport
  channel-group 1 mode active
  no shutdown

interface Ethernet1/3
  no switchport
  ip address 10.100.1.1/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.1.5/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.1.9/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/6
  no switchport
  ip address 10.200.0.2/30
  isis network point-to-point
  ip router isis 1
  no shutdown  

router isis 1
  net 49.0001.1111.1111.1111.00
  address-family ipv4 unicast
    default-information originate

```


 # Конфигурация интерфейсов Spine_02

```python
interface port-channel1
  no switchport
  ip address 10.100.0.2/30
  ip router isis 1

interface Ethernet1/1
  no switchport
  channel-group 1 mode active
  no shutdown

interface Ethernet1/2
  no switchport
  channel-group 1 mode active
  no shutdown

interface Ethernet1/3
  no switchport
  ip address 10.100.2.1/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.2.5/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.2.9/30
  isis network point-to-point
  ip router isis 1
  no shutdown
  
router isis 1
  net 49.0001.2222.2222.2222.00

``````

# Конфигурация интерфейсов Spine_03

```python
interface Ethernet1/1
  no switchport
  ip address 10.200.0.1/30
  isis network point-to-point
  isis circuit-type level-2
  ip router isis 1
  no shutdown

interface Ethernet1/2
  no switchport
  ip address 10.200.1.1/30
  isis network point-to-point
  ip router isis 1
  no shutdown
  
router isis 1
  net 49.0002.0002.0002.0002.00
  address-family ipv4 unicast

```


# Соседство IS-IS Leaf_01 - 4

```python
Leaf_01#sh isis ne
Tag 1:
System Id      Type Interface   IP Address      State Holdtime Circuit Id
Spine_01       L1   Et0/0       10.100.1.1      UP    24       01
Spine_02       L1   Et0/1       10.100.2.1      UP    27       01

Leaf_02#sh isis ne

Tag 1:
System Id      Type Interface   IP Address      State Holdtime Circuit Id
Spine_01       L1   Et0/0       10.100.1.5      UP    27       01
Spine_02       L1   Et0/1       10.100.2.5      UP    27       01

Leaf_03#sh isis ne

Tag 1:
System Id      Type Interface   IP Address      State Holdtime Circuit Id
Spine_01       L1   Et0/0       10.100.1.9      UP    21       01
Spine_02       L1   Et0/1       10.100.2.9      UP    22       01

Leaf_04#sh isis ne

Tag 1:
System Id      Type Interface   IP Address      State Holdtime Circuit Id
Spine_03       L1   Et0/0       10.200.1.1      UP    24       01


```

#Таблица маршрутизации Leaf_01

```python
S*    0.0.0.0/0 [1/0] via 10.100.1.1
      10.0.0.0/8 is variably subnetted, 4 subnets, 2 masks
C        10.100.1.0/30 is directly connected, Ethernet0/0
L        10.100.1.2/32 is directly connected, Ethernet0/0
C        10.100.2.0/30 is directly connected, Ethernet0/1
L        10.100.2.2/32 is directly connected, Ethernet0/1
C     192.168.0.0/23 is directly connected, Vlan10
      192.168.0.0/32 is subnetted, 1 subnets
L        192.168.0.1 is directly connected, Vlan10

```
# Таблица маршрутизации Leaf_02

```python
 S*    0.0.0.0/0 [1/0] via 10.100.1.5
      10.0.0.0/8 is variably subnetted, 6 subnets, 3 masks
C        10.10.0.0/23 is directly connected, Vlan10
L        10.10.0.1/32 is directly connected, Vlan10
C        10.100.1.4/30 is directly connected, Ethernet0/0
L        10.100.1.6/32 is directly connected, Ethernet0/0
C        10.100.2.4/30 is directly connected, Ethernet0/1
L        10.100.2.6/32 is directly connected, Ethernet0/1
```
# Таблица маршрутизации Leaf_03

```python
S*    0.0.0.0/0 [1/0] via 10.100.1.9
      10.0.0.0/8 is variably subnetted, 4 subnets, 2 masks
C        10.100.1.8/30 is directly connected, Ethernet0/0
L        10.100.1.10/32 is directly connected, Ethernet0/0
C        10.100.2.8/30 is directly connected, Ethernet0/1
L        10.100.2.10/32 is directly connected, Ethernet0/1
C     192.168.2.0/23 is directly connected, Vlan10
      192.168.2.0/32 is subnetted, 1 subnets
L        192.168.2.1 is directly connected, Vlan10

```
# Таблица маршрутизации Leaf_04
```python

S*    0.0.0.0/0 [1/0] via 10.200.1.1
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.200.1.0/30 is directly connected, Ethernet0/0
L        10.200.1.2/32 is directly connected, Ethernet0/0
      172.30.0.0/16 is variably subnetted, 2 subnets, 2 masks
C        172.30.0.0/23 is directly connected, Vlan10
L        172.30.0.1/32 is directly connected, Vlan10

```

# Таблица маршрутизации Spine_01

```python
10.10.0.0/23, ubest/mbest: 1/0
    *via 10.100.1.6, Eth1/4, [115/50], 00:32:51, isis-1, L1
10.10.10.0/30, ubest/mbest: 1/0, attached
    *via 10.10.10.2, Eth1/7, [0/0], 00:32:51, direct
10.10.10.2/32, ubest/mbest: 1/0, attached
    *via 10.10.10.2, Eth1/7, [0/0], 00:32:51, local
10.100.0.0/30, ubest/mbest: 1/0, attached
    *via 10.100.0.1, Po1, [0/0], 00:34:08, direct
10.100.0.1/32, ubest/mbest: 1/0, attached
    *via 10.100.0.1, Po1, [0/0], 00:34:08, local
10.100.1.0/30, ubest/mbest: 1/0, attached
    *via 10.100.1.1, Eth1/3, [0/0], 00:34:13, direct
10.100.1.1/32, ubest/mbest: 1/0, attached
    *via 10.100.1.1, Eth1/3, [0/0], 00:34:13, local
10.100.1.4/30, ubest/mbest: 1/0, attached
    *via 10.100.1.5, Eth1/4, [0/0], 00:34:13, direct
10.100.1.5/32, ubest/mbest: 1/0, attached
    *via 10.100.1.5, Eth1/4, [0/0], 00:34:13, local
10.100.1.8/30, ubest/mbest: 1/0, attached
    *via 10.100.1.9, Eth1/5, [0/0], 00:34:13, direct
10.100.1.9/32, ubest/mbest: 1/0, attached
    *via 10.100.1.9, Eth1/5, [0/0], 00:34:13, local
10.100.2.0/30, ubest/mbest: 1/0
    *via 10.100.1.2, Eth1/3, [115/50], 00:32:51, isis-1, L1
10.100.2.4/30, ubest/mbest: 1/0
    *via 10.100.1.6, Eth1/4, [115/50], 00:32:51, isis-1, L1
10.100.2.8/30, ubest/mbest: 1/0
    *via 10.100.1.10, Eth1/5, [115/50], 00:32:51, isis-1, L1
10.200.0.0/30, ubest/mbest: 1/0, attached
    *via 10.200.0.2, Eth1/6, [0/0], 00:34:13, direct
10.200.0.2/32, ubest/mbest: 1/0, attached
    *via 10.200.0.2, Eth1/6, [0/0], 00:34:13, local
192.168.0.0/23, ubest/mbest: 1/0
    *via 10.100.1.2, Eth1/3, [115/50], 00:32:51, isis-1, L1
192.168.2.0/23, ubest/mbest: 1/0
    *via 10.100.1.10, Eth1/5, [115/50], 00:32:51, isis-1, L1
```

# Таблица маршрутизации Spine_02

```python
10.10.0.0/23, ubest/mbest: 1/0
    *via 10.100.2.6, Eth1/4, [115/50], 00:34:29, isis-1, L1
10.10.10.0/30, ubest/mbest: 1/0
    *via 10.100.0.1, Po1, [115/60], 00:33:11, isis-1, L1
10.100.0.0/30, ubest/mbest: 1/0, attached
    *via 10.100.0.2, Po1, [0/0], 00:34:29, direct
10.100.0.2/32, ubest/mbest: 1/0, attached
    *via 10.100.0.2, Po1, [0/0], 00:34:29, local
10.100.1.0/30, ubest/mbest: 1/0
    *via 10.100.2.2, Eth1/3, [115/50], 00:34:29, isis-1, L1
10.100.1.4/30, ubest/mbest: 1/0
    *via 10.100.2.6, Eth1/4, [115/50], 00:34:29, isis-1, L1
10.100.1.8/30, ubest/mbest: 1/0
    *via 10.100.2.10, Eth1/5, [115/50], 00:34:29, isis-1, L1
10.100.2.0/30, ubest/mbest: 1/0, attached
    *via 10.100.2.1, Eth1/3, [0/0], 1d02h, direct
10.100.2.1/32, ubest/mbest: 1/0, attached
    *via 10.100.2.1, Eth1/3, [0/0], 1d02h, local
10.100.2.4/30, ubest/mbest: 1/0, attached
    *via 10.100.2.5, Eth1/4, [0/0], 1d02h, direct
10.100.2.5/32, ubest/mbest: 1/0, attached
    *via 10.100.2.5, Eth1/4, [0/0], 1d02h, local
10.100.2.8/30, ubest/mbest: 1/0, attached
    *via 10.100.2.9, Eth1/5, [0/0], 1d02h, direct
10.100.2.9/32, ubest/mbest: 1/0, attached
    *via 10.100.2.9, Eth1/5, [0/0], 1d02h, local
10.200.0.0/30, ubest/mbest: 1/0
    *via 10.100.0.1, Po1, [115/60], 00:34:27, isis-1, L1
192.168.0.0/23, ubest/mbest: 1/0
    *via 10.100.2.2, Eth1/3, [115/50], 00:34:29, isis-1, L1
192.168.2.0/23, ubest/mbest: 1/0
    *via 10.100.2.10, Eth1/5, [115/50], 00:34:29, isis-1, L1
```
# Таблица маршрутизации Spine_03

```python

0.0.0.0/0, ubest/mbest: 1/0
    *via 10.200.0.2, [1/0], 00:18:29, static
10.100.0.0/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/60], 00:20:08, isis-1, L2
10.100.1.0/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/80], 00:20:08, isis-1, L2
10.100.1.4/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/80], 00:20:08, isis-1, L2
10.100.1.8/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/80], 00:20:08, isis-1, L2
10.100.2.0/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/100], 00:20:06, isis-1, L2
10.100.2.4/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/100], 00:20:06, isis-1, L2
10.100.2.8/30, ubest/mbest: 1/0
    *via 10.200.0.2, Eth1/1, [115/100], 00:20:06, isis-1, L2
10.200.0.0/30, ubest/mbest: 1/0, attached
    *via 10.200.0.1, Eth1/1, [0/0], 01:17:19, direct
10.200.0.1/32, ubest/mbest: 1/0, attached
    *via 10.200.0.1, Eth1/1, [0/0], 01:17:19, local
10.200.1.0/30, ubest/mbest: 1/0, attached
    *via 10.200.1.1, Eth1/2, [0/0], 01:17:19, direct
10.200.1.1/32, ubest/mbest: 1/0, attached
    *via 10.200.1.1, Eth1/2, [0/0], 01:17:19, local
172.30.0.0/23, ubest/mbest: 1/0
    *via 10.200.1.2, Eth1/2, [115/50], 00:20:07, isis-1, L1
```
# IS-IS Topology Spine_01

```python
IS-IS Level-1 IS routing table
Spine_02.00, Instance 0x0000001B
   *via Spine_02, port-channel1, metric 20
Leaf_01.00, Instance 0x0000001B
   *via Leaf_01, Ethernet1/3, metric 40
Leaf_02.00, Instance 0x0000001B
   *via Leaf_02, Ethernet1/4, metric 40
Leaf_03.00, Instance 0x0000001B
   *via Leaf_03, Ethernet1/5, metric 40

IS-IS Level-2 IS routing table
Spine_03.00, Instance 0x00000051
   *via Spine_03, Ethernet1/6, metric 40
Spine_02.00, Instance 0x00000051
   *via Spine_02, port-channel1, metric 20
```
# IS-IS Topology Spine_02
```python
IS-IS Level-1 IS routing table
Spine_01.00, Instance 0x00000071
   *via Spine_01, port-channel1, metric 20
Leaf_01.00, Instance 0x00000071
   *via Leaf_01, Ethernet1/3, metric 40
Leaf_02.00, Instance 0x00000071
   *via Leaf_02, Ethernet1/4, metric 40
Leaf_03.00, Instance 0x00000071
   *via Leaf_03, Ethernet1/5, metric 40

IS-IS Level-2 IS routing table
Spine_03.00, Instance 0x0000004F
   *via Spine_01, port-channel1, metric 60
Spine_01.00, Instance 0x0000004F
   *via Spine_01, port-channel1, metric 20
```
# IS-IS Topology Spine_03

```python
IS-IS Level-1 IS routing table
Leaf_04.00, Instance 0x0000001D
   *via Leaf_04, Ethernet1/2, metric 40

IS-IS Level-2 IS routing table
Spine_01.00, Instance 0x00000023
   *via Spine_01, Ethernet1/1, metric 40
Spine_02.00, Instance 0x00000023
   *via Spine_01, Ethernet1/1, metric 60
Spine_02.01, Instance 0x00000023
   *via Spine_01, Ethernet1/1, metric 60

```
