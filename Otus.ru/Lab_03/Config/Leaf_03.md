```python
Current configuration : 1338 bytes
!
! Last configuration change at 17:08:17 EET Fri Oct 6 2023
!
version 15.2
service timestamps debug datetime msec
service timestamps log datetime msec
no service password-encryption
service compress-config
!
hostname Leaf_03
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
ip forward-protocol nd
!
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 10.100.1.9
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
```
