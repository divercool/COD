```python
route-map Leaf_peer permit 10
  match interface loopback0 
vrf context management


interface Ethernet1/1
  no switchport
  ip address 10.100.254.6/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

interface Ethernet1/2
  no switchport
  ip address 10.100.254.18/30
  ip router ospf 1 area 0.0.0.2
  no shutdown

  interface loopback0
  ip address 10.4.1.1/32
  ip router ospf 1 area 0.0.0.2
icam monitor scale

cli alias name wr copy run start
line console
line vty
router ospf 1
  router-id 4.4.4.
  
router bgp 65009
  router-id 4.4.4.4
  reconnect-interval 10
  log-neighbor-changes
  address-family ipv4 unicast
    redistribute direct route-map Leaf_peer
    maximum-paths 10
  template peer SPINES
    remote-as 65001
    ebgp-multihop 3
    timers 6 9
    address-family ipv4 unicast
  neighbor 10.1.1.1
    inherit peer SPINES
  neighbor 10.1.1.2
    inherit peer SPINES


```