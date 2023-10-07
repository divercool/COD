```python

!Command: show running-config
!Running configuration last done at: Sat Oct  7 16:40:54 2023
!Time: Sat Oct  7 16:41:14 2023

version 9.3(10) Bios:version  
hostname Spine_03
vdc Spine_03 id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 128 maximum 128
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8

feature isis

no password strength-check
username admin password 5 $5$AJOPNO$luONer/miFmqDPFojPgL.jB7Bcsf6paK5sAQnsDVIJ3 
 role network-admin
no ip domain-lookup
copp profile strict
snmp-server user admin network-admin auth md5 165E7A19D13E031B0C0F195D78263862C3
0C priv 32385D28CB384F4D46234F3745E4F4BF1365 localizedV2key
rmon event 1 log trap public description FATAL(1) owner PMON@FATAL
rmon event 2 log trap public description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 log trap public description ERROR(3) owner PMON@ERROR
rmon event 4 log trap public description WARNING(4) owner PMON@WARNING
rmon event 5 log trap public description INFORMATION(5) owner PMON@INFO

ip route 0.0.0.0/0 10.200.0.2
vlan 1

vrf context management

interface Ethernet1/1
  no switchport
  ip address 10.200.0.1/30
  isis network point-to-point
  isis circuit-type level-2
  ip router isis 1
  no shutdown

interface Ethernet1/2
  no switchport
  ip address 10.200.1.1/30
  isis network point-to-point
  ip router isis 1
  no shutdown

line console
line vty
router isis 1
  net 49.0002.0002.0002.0002.00
  address-family ipv4 unicast
```