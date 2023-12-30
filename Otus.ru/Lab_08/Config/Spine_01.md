```python


!Command: show running-config
!Running configuration last done at: Sat Oct 28 20:04:42 2023
!Time: Sat Oct 28 20:04:43 2023

version 9.3(8) Bios:version  
hostname Spine_01
vdc Spine_01 id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 128 maximum 128
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8

nv overlay evpn
feature ospf
feature bgp
feature lacp
feature bfd
feature nv overlay

no password strength-check
username admin password 5 $5$ZEZH5HAr$RH/DgUpKgo2AYptGopI9Pe/3hBYSbRnopDYxyY9DZ07  role network-admin
no ip domain-lookup
copp profile strict
snmp-server user admin network-admin auth md5 0x1ad8959fb9e18714faffbb6d6861a939 priv 0x1ad8959fb9e18714faffbb6d6861a939 localizedkey
rmon event 1 description FATAL(1) owner PMON@FATAL
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 description ERROR(3) owner PMON@ERROR
rmon event 4 description WARNING(4) owner PMON@WARNING
rmon event 5 description INFORMATION(5) owner PMON@INFO

vlan 1

route-map Leaf_AS permit 10
  match interface loopback0 
  match as-number 65005-65010 
route-map Leaf_peer permit 10
  match as-number 65001-65010 
route-map NH_UNCHANGED permit 10
  set ip next-hop unchanged
vrf context management


interface Ethernet1/1
  no switchport
  no shutdown

interface Ethernet1/2
  no switchport
  no shutdown

interface Ethernet1/3
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
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



interface mgmt0
  vrf member management

interface loopback0
  ip address 10.1.1.1/32
  ip router ospf 1 area 0.0.0.0

interface loopback1
  ip address 10.10.1.1/32
icam monitor scale

cli alias name wr copy run start
line console
line vty
no feature signature-verification
router ospf 1
  router-id 1.1.1.1
  default-information originate
router bgp 65001
  router-id 1.1.1.1
  timers bgp 3 9
  reconnect-interval 10
  log-neighbor-changes
  address-family l2vpn evpn
    maximum-paths 10
  neighbor 10.3.1.1
    remote-as 65001
    update-source loopback0
    timers 6 9
    address-family l2vpn evpn
      send-community
      send-community extended
      route-reflector-client
  neighbor 10.4.1.1
    remote-as 65001
    update-source loopback0
    timers 6 9
    address-family l2vpn evpn
      send-community
      send-community extended
      route-reflector-client
  neighbor 10.5.1.1
    remote-as 65001
    update-source loopback0
    timers 6 9
    address-family l2vpn evpn
      send-community
      send-community extended
      route-reflector-client


!


!end
!end

```