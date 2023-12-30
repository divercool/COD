```python



!Command: show running-config
!Running configuration last done at: Wed Dec 27 09:14:08 2023
!Time: Wed Dec 27 09:39:58 2023

version 9.3(8) Bios:version  
system memory-thresholds minor 88 severe 90 critical 93

hostname Leaf_02
vdc Leaf_02 id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 128 maximum 128
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8

cfs eth distribute
nv overlay evpn
feature ospf
feature bgp
feature interface-vlan
feature vn-segment-vlan-based
feature lacp
feature vpc
feature bfd
feature nv overlay

no password strength-check
username admin password 5 $5$HKAJHM$Ub5WyOf1girq5aoRbIHOBJRPhbKtIuqKNG0AzPQKnw6 
 role network-admin
ip domain-lookup
copp profile strict
rmon event 1 log trap public description FATAL(1) owner PMON@FATAL
rmon event 2 log trap public description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 log trap public description ERROR(3) owner PMON@ERROR
rmon event 4 log trap public description WARNING(4) owner PMON@WARNING
rmon event 5 log trap public description INFORMATION(5) owner PMON@INFO

fabric forwarding anycast-gateway-mac 0000.1111.2222
ip route 55.55.55.0/24 150.150.150.1
ip route 55.55.55.55/32 150.150.150.1
vlan 1,10,20,30,222
vlan 10
  name VLAN_10
  vn-segment 10010
vlan 20
  name VLAN_20
  vn-segment 10020
vlan 30
  name VLAN_30
  vn-segment 10030
vlan 222
  vn-segment 100222

spanning-tree vlan 1-200 priority 4096
route-map Leaf_peer permit 10
  match interface loopback0 
vrf context CCCP
  vni 10222
  rd auto
  address-family ipv4 unicast
    route-target both auto
vrf context VPC
vrf context management
vpc domain 1
  peer-switch
  role priority 5
  peer-keepalive destination 1.1.1.1 source 1.1.1.2 vrf VPC
  delay restore 10
  peer-gateway
  ip arp synchronize


interface Vlan1
  no ip redirects
  no ipv6 redirects

interface Vlan10
  no shutdown
  vrf member CCCP
  no ip redirects
  ip address 10.10.10.10/24
  no ipv6 redirects
  fabric forwarding mode anycast-gateway

interface Vlan20
  no shutdown
  vrf member CCCP
  no ip redirects
  ip address 20.20.20.20/24
  no ipv6 redirects
  fabric forwarding mode anycast-gateway

interface Vlan30
  no shutdown
  vrf member CCCP
  no ip redirects
  ip address 30.30.30.30/24
  no ipv6 redirects
  fabric forwarding mode anycast-gateway

interface Vlan222
  no shutdown
  vrf member CCCP
  no ip redirects
  ip forward
  no ipv6 redirects

interface port-channel1
  switchport mode trunk
  switchport trunk native vlan 10
  mtu 9216
  vpc 1

interface port-channel2
  switchport mode trunk
  spanning-tree port type network
  vpc peer-link

interface nve1
  no shutdown
  host-reachability protocol bgp
  source-interface loopback100
  member vni 10010
    ingress-replication protocol bgp
  member vni 10020
    ingress-replication protocol bgp
  member vni 10030
    ingress-replication protocol bgp
  member vni 100222 associate-vrf

interface Ethernet1/1
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
  ip address 10.100.254.6/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

interface Ethernet1/2
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
  ip address 10.100.254.18/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

interface Ethernet1/3
  no switchport
  vrf member CCCP
  ip address 150.150.150.2/30
  no shutdown

interface Ethernet1/4
  no switchport
  vrf member VPC
  ip address 1.1.1.2/30
  no shutdown

interface Ethernet1/5
  switchport mode trunk
  channel-group 2 mode active

interface Ethernet1/6
  switchport mode trunk
  channel-group 2 mode active

interface Ethernet1/7

interface Ethernet1/8
  switchport mode trunk
  switchport trunk native vlan 10
  mtu 9216
  channel-group 1 mode active

interface mgmt0
  vrf member management

interface loopback0
  ip address 10.4.1.1/32
  ip router ospf 1 area 0.0.0.2

interface loopback100
  ip address 100.100.100.2/32
  ip address 100.100.100.23/32 secondary
  ip router ospf 1 area 0.0.0.2
icam monitor scale

cli alias name wr copy run start
line console
line vty
router ospf 1
  router-id 4.4.4.4
router bgp 65001
  router-id 4.4.4.4
  timers bgp 3 9
  reconnect-interval 10
  log-neighbor-changes
  address-family ipv4 unicast
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
  neighbor 150.150.150.1
    remote-as 2000
    address-family ipv4 unicast
  vrf CCCP
    timers bgp 3 9
    address-family ipv4 unicast
      export-gateway-ip
    neighbor 150.150.150.1
      remote-as 2000
      address-family ipv4 unicast
evpn
  vni 10010 l2
    rd auto
    route-target import auto
    route-target export auto
  vni 10020 l2
    rd auto
    route-target import auto
    route-target export auto
  vni 10030 l2
    rd auto
    route-target import auto
    route-target export auto
  vni 100222 l2
    rd auto
    route-target import auto
    route-target export auto

```