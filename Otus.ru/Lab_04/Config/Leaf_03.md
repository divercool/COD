```python
route-map Leaf_peer permit 10
  match as-number 65001-65010 
vrf context management


interface Ethernet1/1
  no switchport
  ip address 10.100.254.10/30
  ip router ospf 1 area 0.0.0.3
  no shutdown

interface Ethernet1/2
  no switchport
  ip address 10.100.254.22/30
  ip router ospf 1 area 0.0.0.3
  no shutdown

  interface loopback0
  ip address 10.5.1.1/32
  ip router ospf 1 area 0.0.0.3
icam monitor scale

router ospf 1
  router-id 5.5.5.5

router bgp 65010
  router-id 5.5.5.5
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