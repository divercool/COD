```python
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