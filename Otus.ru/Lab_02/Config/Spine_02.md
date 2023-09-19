interface port-channel1
  description to Spine_01
  no switchport
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
  
  router ospf 1
  router-id 2.2.2.2
