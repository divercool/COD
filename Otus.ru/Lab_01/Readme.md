# Задачи лабы:
1) Распределение адресного пространства Underlay
2) Схема сети CLOS





# 1) Распределение адресного пространства Underlay
# IP address P2P Spine-Leaf

| Network IPv4         | Description    | device name&port           |
|----------------------|----------------|----------------------------|
| 10.100.254.0/23      | P2P Spine-Leaf |                            |
| 10.100.254.1-2/30    | P2P Spine-Leaf | Spine_01-E1/3 Leaf_01-E1/0 |
| 10.100.254.5-6/30    | P2P Spine-Leaf | Spine_01-E1/4 Leaf_02-E1/0 |
| 10.100.254.9-10/30   | P2P Spine-Leaf | Spine_01-E1/5 Leaf_03-E1/0 |
| 10.100.254.13-14/30  | P2P Spine-Leaf | Spine_02-E1/3 Leaf_01-E1/1 |
| 10.100.254.17-18/30  | P2P Spine-Leaf | Spine_02-E1/4 Leaf_02-E1/1 |
| 10.100.254.21-22/30  | P2P Spine-Leaf | Spine_02-E1/5 Leaf_03-E1/1 |

 # IP address P2P Spine-Spine

| Network IPv4    | Description     | device name&port            |
|---------------  |-----------------|-----------------------------|
| 10.100.0.0/24   | P2P Spine-Spine | 
| 10.100.0.1-2/30 | P2P Spine-Spine | Spine_01-PO1 - Spine_02-PO1 |

# IP address SVI Vlan Srv_farm_01 

| Network IPv4  | Description          | device name&port              |
|---------------|----------------------|-------------------------------|
| 10.100.1.0/24 | SVI Vlan Srv_farm_01 |                               |
| 10.100.1.1-2  | Vlan-10 Srv_farm_01  | Leaf_01-Vlan-10 - Srv_Farm_01 |

# IP address SVI Vlan Srv_Farm_02 

| Network IPv4  | Description          | device name&port              |
|---------------|----------------------|-------------------------------|
| 10.100.2.0/24 | SVI Vlan Srv_Farm_02 |                               |
| 10.100.2.1-2  | Vlan-20 Srv_farm_02  | Leaf_02-Vlan-20 - Srv_Farm_02 |

# IP address  SVI Vlan Srv_farm_03-4 

| Network IPv4  | Description            | device name&port              |
|---------------|------------------------|-------------------------------|
| 10.100.3.0/24 | SVI Vlan Srv_farm_03-4 |                               |
| 10.100.3.1-2  | Vlan-30 Srv_farm_03    | Leaf_03-Vlan-30 - Srv_Farm_03 |
| 10.100.3.1-3  | Vlan-30 Srv_farm_04    | Leaf_03-Vlan-30 - Srv_Farm_04 |

# 2) Схема сети CLOS

![image](https://github.com/divercool/COD/assets/39337787/8efca99e-beff-41dd-a4dd-92827892b1cb)


