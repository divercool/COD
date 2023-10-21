```python

route-map Leaf_peer permit 10
  match interface loopback0 
vrf context management


interface Vlan1

interface Vlan10
  ip address 192.168.10.1/24

interface Ethernet1/1
  no switchport
  bfd interval 100 min_rx 100 multiplier 2
  ip address 10.100.254.2/30
  ip router ospf 1 area 0.0.0.1
  no shutdown

interface Ethernet1/2
  no switchport
  ip address 10.100.254.14/30
  ip router ospf 1 area 0.0.0.1
  no shutdown

interface loopback0
  ip address 10.3.1.1/32
  ip router ospf 1 area 0.0.0.1

router ospf 1
  router-id 3.3.3.3
  
router bgp 65008
  router-id 3.3.3.3
  reconnect-interval 10
  log-neighbor-changes
  address-family ipv4 unicast
    redistribute direct route-map Leaf_peer
    maximum-paths 10
  template peer SPINES
    remote-as 65001
    update-source loopback0
    ebgp-multihop 3
    timers 6 9
    address-family ipv4 unicast
  neighbor 10.1.1.1
    inherit peer SPINES
  neighbor 10.1.1.2
    inherit peer SPINES
```