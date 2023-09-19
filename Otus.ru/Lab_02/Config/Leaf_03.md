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
!