```python

feature ospf
feature bgp
feature lacp
feature bfd

route-map Leaf_AS permit 10
  match as-number 65005-65010 
route-map Leaf_peer permit 10
  match interface loopback0 
  match as-number 65001-65010 
vrf context management


interface port-channel1
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
  ip address 10.100.0.2/30
  ip router ospf 1 area 0.0.0.0

interface Ethernet1/1
  no switchport
  channel-group 1 mode active
  no shutdown

interface Ethernet1/2
  no switchport
  channel-group 1 mode active
  no shutdown

interface Ethernet1/3
  no switchport
  ip address 10.100.254.13/30
  ip router ospf 1 area 0.0.0.1
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.254.17/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.254.21/30
  ip router ospf 1 area 0.0.0.3
  no shutdown

interface loopback0
  ip address 10.1.1.2/32
  ip router ospf 1 area 0.0.0.0

router ospf 1
  router-id 2.2.2.2

router bgp 65001
  router-id 2.2.2.2
  reconnect-interval 10
  log-neighbor-changes
  address-family ipv4 unicast
    redistribute direct route-map Leaf_peer
    maximum-paths 10
  neighbor 10.1.1.1
    bfd
    remote-as 65001
    update-source loopback0
    timers 15 20
    address-family ipv4 unicast
  neighbor 10.0.0.0/8 remote-as route-map Leaf_AS
    update-source loopback0
    address-family ipv4 unicast








```