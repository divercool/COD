


```python


!Command: show running-config
!Running configuration last done at: Wed Dec 27 09:59:41 2023
!Time: Wed Dec 27 12:06:58 2023

version 9.3(8) Bios:version  
vdc switch id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 248 maximum 248
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8
feature bgp

no password strength-check
username admin password 5 !  role network-admin
ip domain-lookup
copp profile strict
rmon event 1 log trap public description FATAL(1) owner PMON@FATAL
rmon event 2 log trap public description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 log trap public description ERROR(3) owner PMON@ERROR
rmon event 4 log trap public description WARNING(4) owner PMON@WARNING
rmon event 5 log trap public description INFORMATION(5) owner PMON@INFO

vlan 1

vrf context management

interface Ethernet1/1
  no switchport
  ip address 50.50.50.1/30
  no shutdown

interface Ethernet1/2

interface Ethernet1/3
  no switchport
  ip address 150.150.150.1/30
  no shutdown

interface loopback0
  ip address 8.8.8.8/32
icam monitor scale

line console
line vty
router bgp 2000
  router-id 50.50.50.50
  timers bgp 3 9
  reconnect-interval 10
  log-neighbor-changes
  address-family ipv4 unicast
    network 8.8.8.8/32
  neighbor 50.50.50.2
    remote-as 65001
    address-family ipv4 unicast
  neighbor 150.150.150.2
    remote-as 65001
    address-family ipv4 unicast
```