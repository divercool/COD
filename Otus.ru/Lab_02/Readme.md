# Настройка протокола OSPF IPv4 для сети Underlay

Схема сети OSPF
![image](https://github.com/divercool/COD/assets/39337787/8b962df2-cf2f-468b-947e-e916ab9913a6)

# Конфигурация интерфейсов Leaf_01

```console
interface Ethernet0/0
 no switchport
 ip address 10.100.254.2 255.255.255.252
 ip ospf 1 area 1
!
interface Ethernet0/1
 no switchport
 ip address 10.100.254.14 255.255.255.252
 ip ospf 1 area 1
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 10
 switchport trunk allowed vlan 10
 switchport mode trunk
!
interface Ethernet0/3
!
interface Vlan10
 ip address 10.100.1.1 255.255.255.0
!
router ospf 1
 router-id 3.3.3.3
 network 10.100.1.0 0.0.0.255 area 1
```
# Конфигурация интерфейсов Leaf_02

```console
interface Ethernet0/0
 no switchport
 ip address 10.100.254.6 255.255.255.252
 ip ospf 1 area 2
!
interface Ethernet0/1
 no switchport
 ip address 10.100.254.18 255.255.255.252
 ip ospf 1 area 2
 duplex auto
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 20
 switchport mode trunk
 duplex auto
!
interface Ethernet0/3
 duplex auto
!         
interface Vlan20
 ip address 10.100.2.1 255.255.255.0
!
router ospf 1
 router-id 4.4.4.4
 network 10.100.2.0 0.0.0.255 area 2
```

# Конфигурация интерфейсов Leaf_03

```console
interface Ethernet0/0
 no switchport
 ip address 10.100.254.10 255.255.255.252
 ip ospf 1 area 3
!
interface Ethernet0/1
 no switchport
 ip address 10.100.254.22 255.255.255.252
 ip ospf 1 area 3
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 30
 switchport mode trunk
 duplex auto
!
interface Ethernet0/3
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 30
 switchport mode trunk
 duplex auto
!
interface Vlan30
 ip address 10.100.3.1 255.255.255.0
!
router ospf 1
 router-id 5.5.5.5
 network 10.100.3.0 0.0.0.255 area 3
```

# Конфигурация интерфейсов Spine_01


```console
interface port-channel1
  description to Spine_02
  no switchport
  ip address 10.100.0.1/30
  ip router ospf 1 area 0.0.0.0

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
  ip address 10.100.254.1/30
  ip router ospf 1 area 0.0.0.1
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.254.5/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.254.9/30
  ip router ospf 1 area 0.0.0.3
  no shutdown
  
router ospf 1
  router-id 1.1.1.1
  default-information originate
```


 # Конфигурация интерфейсов Spine_02

```console
interface port-channel1
  description to Spine_01
  no switchport
  ip address 10.100.0.2/30
  ip router ospf 1 area 0.0.0.0

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
  ip address 10.100.254.13/30
  ip router ospf 1 area 0.0.0.1
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.254.17/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.254.21/30
  ip router ospf 1 area 0.0.0.3
  no shutdown
  
  router ospf 1
  router-id 2.2.2.2

```

# Таблица маршрутизации Leaf_01

```python
10.0.0.0/8 is variably subnetted, 13 subnets, 3 masks
O IA     10.100.0.0/30 [110/30] via 10.100.254.13, 03:49:35, Ethernet0/1
                       [110/30] via 10.100.254.1, 03:58:41, Ethernet0/0
C        10.100.1.0/24 is directly connected, Vlan10
L        10.100.1.1/32 is directly connected, Vlan10
O IA     10.100.2.0/24 [110/51] via 10.100.254.13, 03:31:19, Ethernet0/1
                       [110/51] via 10.100.254.1, 03:31:14, Ethernet0/0
O IA     10.100.3.0/24 [110/51] via 10.100.254.13, 03:49:35, Ethernet0/1
                       [110/51] via 10.100.254.1, 03:51:20, Ethernet0/0
C        10.100.254.0/30 is directly connected, Ethernet0/0
L        10.100.254.2/32 is directly connected, Ethernet0/0
O IA     10.100.254.4/30 [110/50] via 10.100.254.1, 03:58:41, Ethernet0/0
O IA     10.100.254.8/30 [110/50] via 10.100.254.1, 03:58:41, Ethernet0/0
C        10.100.254.12/30 is directly connected, Ethernet0/1
L        10.100.254.14/32 is directly connected, Ethernet0/1
O IA     10.100.254.16/30 [110/50] via 10.100.254.13, 03:49:35, Ethernet0/1
O IA     10.100.254.20/30 [110/50] via 10.100.254.13, 03:49:35, Ethernet0/1
```
# Таблица маршрутизации Leaf_02

```python
 10.0.0.0/8 is variably subnetted, 13 subnets, 3 masks
O IA     10.100.0.0/30 [110/30] via 10.100.254.17, 03:32:09, Ethernet0/1
                       [110/30] via 10.100.254.5, 03:32:09, Ethernet0/0
O IA     10.100.1.0/24 [110/51] via 10.100.254.17, 03:32:09, Ethernet0/1
                       [110/51] via 10.100.254.5, 03:32:09, Ethernet0/0
C        10.100.2.0/24 is directly connected, Vlan20
L        10.100.2.1/32 is directly connected, Vlan20
O IA     10.100.3.0/24 [110/51] via 10.100.254.17, 03:32:09, Ethernet0/1
                       [110/51] via 10.100.254.5, 03:32:09, Ethernet0/0
O IA     10.100.254.0/30 [110/50] via 10.100.254.5, 03:32:09, Ethernet0/0
C        10.100.254.4/30 is directly connected, Ethernet0/0
L        10.100.254.6/32 is directly connected, Ethernet0/0
O IA     10.100.254.8/30 [110/50] via 10.100.254.5, 03:32:09, Ethernet0/0
O IA     10.100.254.12/30 [110/50] via 10.100.254.17, 03:32:09, Ethernet0/1
C        10.100.254.16/30 is directly connected, Ethernet0/1
L        10.100.254.18/32 is directly connected, Ethernet0/1
O IA     10.100.254.20/30 [110/50] via 10.100.254.17, 03:32:09, Ethernet0/1
```
# Таблица маршрутизации Leaf_03

```python
10.0.0.0/8 is variably subnetted, 13 subnets, 3 masks
O IA     10.100.0.0/30 [110/30] via 10.100.254.21, 03:52:30, Ethernet0/1
                       [110/30] via 10.100.254.9, 03:52:35, Ethernet0/0
O IA     10.100.1.0/24 [110/51] via 10.100.254.21, 03:50:54, Ethernet0/1
                       [110/51] via 10.100.254.9, 03:52:35, Ethernet0/0
O IA     10.100.2.0/24 [110/51] via 10.100.254.21, 03:32:37, Ethernet0/1
                       [110/51] via 10.100.254.9, 03:32:31, Ethernet0/0
C        10.100.3.0/24 is directly connected, Vlan30
L        10.100.3.1/32 is directly connected, Vlan30
O IA     10.100.254.0/30 [110/50] via 10.100.254.9, 03:52:35, Ethernet0/0
O IA     10.100.254.4/30 [110/50] via 10.100.254.9, 03:52:35, Ethernet0/0
C        10.100.254.8/30 is directly connected, Ethernet0/0
L        10.100.254.10/32 is directly connected, Ethernet0/0
O IA     10.100.254.12/30 [110/50] via 10.100.254.21, 03:52:30, Ethernet0/1
O IA     10.100.254.16/30 [110/50] via 10.100.254.21, 03:52:30, Ethernet0/1
C        10.100.254.20/30 is directly connected, Ethernet0/1
L        10.100.254.22/32 is directly connected, Ethernet0/1
```

# Таблица маршрутизации Spine_01

```python
10.100.0.0/30, ubest/mbest: 1/0, attached
    *via 10.100.0.1, Po1, [0/0], 04:32:39, direct
10.100.0.1/32, ubest/mbest: 1/0, attached
    *via 10.100.0.1, Po1, [0/0], 04:32:39, local
10.100.1.0/24, ubest/mbest: 1/0
    *via 10.100.254.2, Eth1/3, [110/41], 03:56:48, ospf-1, intra
10.100.2.0/24, ubest/mbest: 1/0
    *via 10.100.254.6, Eth1/4, [110/41], 03:29:25, ospf-1, intra
10.100.3.0/24, ubest/mbest: 1/0
    *via 10.100.254.10, Eth1/5, [110/41], 03:49:28, ospf-1, intra
10.100.254.0/30, ubest/mbest: 1/0, attached
    *via 10.100.254.1, Eth1/3, [0/0], 04:32:43, direct
10.100.254.1/32, ubest/mbest: 1/0, attached
    *via 10.100.254.1, Eth1/3, [0/0], 04:32:43, local
10.100.254.4/30, ubest/mbest: 1/0, attached
    *via 10.100.254.5, Eth1/4, [0/0], 04:32:43, direct
10.100.254.5/32, ubest/mbest: 1/0, attached
    *via 10.100.254.5, Eth1/4, [0/0], 04:32:43, local
10.100.254.8/30, ubest/mbest: 1/0, attached
    *via 10.100.254.9, Eth1/5, [0/0], 04:20:31, direct
10.100.254.9/32, ubest/mbest: 1/0, attached
    *via 10.100.254.9, Eth1/5, [0/0], 04:20:31, local
10.100.254.12/30, ubest/mbest: 1/0
    *via 10.100.254.2, Eth1/3, [110/50], 03:47:57, ospf-1, intra
10.100.254.16/30, ubest/mbest: 1/0
    *via 10.100.254.6, Eth1/4, [110/50], 03:29:25, ospf-1, intra
10.100.254.20/30, ubest/mbest: 1/0
    *via 10.100.254.10, Eth1/5, [110/50], 03:49:23, ospf-1, intra
```

# Таблица маршрутизации Spine_02

```python

10.100.0.0/30, ubest/mbest: 1/0, attached
    *via 10.100.0.2, Po1, [0/0], 04:34:03, direct
10.100.0.2/32, ubest/mbest: 1/0, attached
    *via 10.100.0.2, Po1, [0/0], 04:34:03, local
10.100.1.0/24, ubest/mbest: 1/0
    *via 10.100.254.14, Eth1/3, [110/41], 03:49:08, ospf-1, intra
10.100.2.0/24, ubest/mbest: 1/0
    *via 10.100.254.18, Eth1/4, [110/41], 03:30:51, ospf-1, intra
10.100.3.0/24, ubest/mbest: 1/0
    *via 10.100.254.22, Eth1/5, [110/41], 03:50:47, ospf-1, intra
10.100.254.0/30, ubest/mbest: 1/0
    *via 10.100.254.14, Eth1/3, [110/50], 03:49:08, ospf-1, intra
10.100.254.4/30, ubest/mbest: 1/0
    *via 10.100.254.18, Eth1/4, [110/50], 03:30:51, ospf-1, intra
10.100.254.8/30, ubest/mbest: 1/0
    *via 10.100.254.22, Eth1/5, [110/50], 03:50:47, ospf-1, intra
10.100.254.12/30, ubest/mbest: 1/0, attached
    *via 10.100.254.13, Eth1/3, [0/0], 04:35:30, direct
10.100.254.13/32, ubest/mbest: 1/0, attached
    *via 10.100.254.13, Eth1/3, [0/0], 04:35:30, local
10.100.254.16/30, ubest/mbest: 1/0, attached
    *via 10.100.254.17, Eth1/4, [0/0], 04:35:30, direct
10.100.254.17/32, ubest/mbest: 1/0, attached
    *via 10.100.254.17, Eth1/4, [0/0], 04:35:30, local
10.100.254.20/30, ubest/mbest: 1/0, attached
    *via 10.100.254.21, Eth1/5, [0/0], 04:35:30, direct
10.100.254.21/32, ubest/mbest: 1/0, attached
    *via 10.100.254.21, Eth1/5, [0/0], 04:35:30, local
```
