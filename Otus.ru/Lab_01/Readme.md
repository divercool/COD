Задачи лабы:
1) Распределение адресного пространства Underlay
2) Схема сети CLOS
3) Настройка интерфейсов
4) Документирование


1) Распределение адресного пространства Underlay

# IP address P2P Spine-Leaf

| Network IPv4         | Description    | device name&port           |
|----------------------|----------------|----------------------------|
| 10.100.254.0/23      | P2P Spine-Leaf |                            |
| 10.100.254.1-2/30    | P2P Spine-Leaf | Spine_01-E1/3 Leaf_01-E1/0 |
| 10.100.254.5-6/30    | P2P Spine-Leaf | Spine_01-E1/4 Leaf_02-E1/0 |
| 10.100.254.9-10/30   | P2P Spine-Leaf | Spine_01-E1/5 Leaf_03-E1/0 |
| 10.100.254.13-14/30  | P2P Spine-Leaf | Spine_02-E1/3 Leaf_01-E1/1 |
| 10.100.254.17-18/30  | P2P Spine-Leaf | Spine_02-E1/4 Leaf_02-E1/1 |
| 10.100.254.21-22/30  | P2P Spine-Leaf | Spine_02-E1/5 Leaf_03-E1/1 |

 # IP address P2P Spine-Spine

| Network IPv4    | Description     | device name&port            |
|---------------  |-----------------|-----------------------------|
| 10.100.0.0/24   | P2P Spine-Spine | 
| 10.100.0.1-2/30 | P2P Spine-Spine | Spine_01-PO1 - Spine_02-PO1 |

# IP address SVI Vlan Srv_farm_01 

| Network IPv4  | Description          | device name&port              |
|---------------|----------------------|-------------------------------|
| 10.100.1.0/24 | SVI Vlan Srv_farm_01 |                               |
| 10.100.1.1-2  | Vlan-10 Srv_farm_01  | Leaf_01-Vlan-10 - Srv_Farm_01 |

# IP address SVI Vlan Srv_Farm_02 

| Network IPv4  | Description          | device name&port              |
|---------------|----------------------|-------------------------------|
| 10.100.2.0/24 | SVI Vlan Srv_Farm_02 |                               |
| 10.100.2.1-2  | Vlan-20 Srv_farm_02  | Leaf_02-Vlan-20 - Srv_Farm_02 |

# IP address  SVI Vlan Srv_farm_03-4 

| Network IPv4  | Description            | device name&port              |
|---------------|------------------------|-------------------------------|
| 10.100.3.0/24 | SVI Vlan Srv_farm_03-4 |                               |
| 10.100.3.1-2  | Vlan-30 Srv_farm_03    | Leaf_03-Vlan-30 - Srv_Farm_03 |
| 10.100.3.1-3  | Vlan-30 Srv_farm_04    | Leaf_03-Vlan-30 - Srv_Farm_04 |

2) Схема сети CLOS

![image](https://github.com/divercool/COD/assets/39337787/8efca99e-beff-41dd-a4dd-92827892b1cb)


3) Конфигурация интерфейсов

Leaf_01

interface Ethernet0/0
 no switchport
 ip address 10.100.254.2 255.255.255.252
!
interface Ethernet0/1
 no switchport
 ip address 10.100.254.14 255.255.255.252
 duplex auto
!
interface Ethernet0/2
 switchport trunk encapsulation dot1q
 switchport trunk native vlan 10
 switchport mode trunk
 duplex auto
!
interface Ethernet0/3
 duplex auto
!
interface Vlan10
 ip address 10.100.1.1 255.255.255.0

 Leaf_02

 interface Ethernet0/0
 no switchport
 ip address 10.100.254.6 255.255.255.252
 duplex auto
!
interface Ethernet0/1
 no switchport
 ip address 10.100.254.18 255.255.255.252
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

 Leaf_03

 interface Ethernet0/0
 no switchport
 ip address 10.100.254.10 255.255.255.252
 duplex auto
!
interface Ethernet0/1
 no switchport
 ip address 10.100.254.22 255.255.255.252
 duplex auto
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

Spine_01

interface port-channel1
  description to Spine_02
  no switchport
  ip address 10.100.0.1/30

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
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.254.5/30
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.254.9/30

  Spine_02

  interface port-channel1
  description to Spine_01
  no switchport
  ip address 10.100.0.2/30

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
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.254.17/30
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.254.21/30
  no shutdown

