```python



!Command: show running-config
!Running configuration last done at: Sat Oct 28 20:04:28 2023
!Time: Sat Oct 28 20:04:28 2023

version 9.3(8) Bios:version  
hostname Leaf_03
vdc Leaf_03 id 1
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
feature interface-vlan
feature vn-segment-vlan-based
feature bfd
feature nv overlay

no password strength-check
username admin password 5 $5$HKAJHM$Ub5WyOf1girq5aoRbIHOBJRPhbKtIuqKNG0AzPQKnw6  role network-admin
ip domain-lookup
copp profile strict
rmon event 1 log trap public description FATAL(1) owner PMON@FATAL
rmon event 2 log trap public description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 log trap public description ERROR(3) owner PMON@ERROR
rmon event 4 log trap public description WARNING(4) owner PMON@WARNING
rmon event 5 log trap public description INFORMATION(5) owner PMON@INFO

fabric forwarding anycast-gateway-mac 0000.1111.2222
vlan 1,20,222
vlan 20
  name VLAN_20
  vn-segment 10020
vlan 222
  vn-segment 100222

route-map Leaf_peer permit 10
  match interface loopback0 
vrf context CCCP
  vni 100222
  rd auto
  address-family ipv4 unicast
    route-target both auto
vrf context management


interface Vlan1

interface Vlan20
  no shutdown
  vrf member CCCP
  ip address 20.20.20.20/24
  fabric forwarding mode anycast-gateway

interface Vlan222
  no shutdown
  vrf member CCCP
  ip forward

interface nve1
  no shutdown
  host-reachability protocol bgp
  source-interface loopback100
  member vni 10020
    ingress-replication protocol bgp
  member vni 100222 associate-vrf

interface Ethernet1/1
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
  ip address 10.100.254.10/30
  ip router ospf 1 area 0.0.0.3
  no shutdown

interface Ethernet1/2
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
  ip address 10.100.254.22/30
  ip router ospf 1 area 0.0.0.3
  no shutdown

interface Ethernet1/3
  switchport access vlan 20


interface mgmt0
  vrf member management

interface loopback0
  ip address 10.5.1.1/32
  ip router ospf 1 area 0.0.0.3

interface loopback100
  ip address 100.100.100.3/32
  ip router ospf 1 area 0.0.0.3
icam monitor scale

cli alias name wr copy run start
line console
line vty
router ospf 1
  router-id 5.5.5.5
router bgp 65001
  router-id 5.5.5.5
  timers bgp 3 9
  reconnect-interval 10
  log-neighbor-changes
  address-family l2vpn evpn
    maximum-paths 10
  template peer SPINES
    bfd
    remote-as 65001
    update-source loopback0
    timers 6 9
    address-family l2vpn evpn
      send-community
      send-community extended
  neighbor 10.1.1.1
    inherit peer SPINES
  neighbor 10.1.1.2
    inherit peer SPINES
evpn
  vni 10020 l2
    rd auto
    route-target import auto
    route-target export auto
  vni 100222 l2
    rd auto
    route-target import auto
    route-target export auto


!


!end
!end

```