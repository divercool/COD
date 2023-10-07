Current configuration : 1328 bytes
!
! Last configuration change at 17:06:49 EET Fri Oct 6 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname Leaf_02
!
boot-start-marker
boot-end-marker
!
!
!
no aaa new-model
clock timezone EET 2 0
!
!
!
!         
!
!
!
!
no ip domain-lookup
ip cef
ipv6 multicast rpf use-bgp
no ipv6 cef
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
vlan internal allocation policy ascending
no cdp run
!
! 
!
!
!
!
!         
!
!
!
!
!
!
!
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
!
!
!         
!
!
control-plane
!
!
line con 0
 logging synchronous
line aux 0
line vty 0 4
 login
!
!
end