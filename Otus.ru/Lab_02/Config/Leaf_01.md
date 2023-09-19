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