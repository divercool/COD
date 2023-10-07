!Running configuration last done at: Fri Oct  6 13:51:45 2023
!Time: Sat Oct  7 14:42:13 2023

version 9.3(10) Bios:version  
hostname Spine_02
vdc Spine_02 id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 128 maximum 128
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8

feature isis
feature lacp

no password strength-check
username admin password 5 $5$LAFMGC$.o7EDHC9gbsMuUMS4NcxtqlXbgFC9L76BPdL95kbFvC 
 role network-admin
no ip domain-lookup
copp profile strict
snmp-server user admin network-admin auth md5 056AB029D8C9D291C7DDD6F878C3FE3C77
A5 priv 056FF824DA9DF8DB86F583B366C8F0276184 localizedV2key
rmon event 1 log trap public description FATAL(1) owner PMON@FATAL
rmon event 2 log trap public description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 log trap public description ERROR(3) owner PMON@ERROR
rmon event 4 log trap public description WARNING(4) owner PMON@WARNING
rmon event 5 log trap public description INFORMATION(5) owner PMON@INFO

vlan 1

vrf context management

interface port-channel1
  no switchport
  ip address 10.100.0.2/30
  ip router isis 1

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
  ip address 10.100.2.1/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/4
  no switchport
  ip address 10.100.2.5/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface Ethernet1/5
  no switchport
  ip address 10.100.2.9/30
  isis network point-to-point
  ip router isis 1
  no shutdown

interface mgmt0
  vrf member management
icam monitor scale

line console
line vty
router isis 1
  net 49.0001.2222.2222.2222.00