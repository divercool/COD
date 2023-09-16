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