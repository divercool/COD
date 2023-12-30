# IP address
| Network IPv4         | Description    | device name&port           |
|----------------------|----------------|----------------------------|
| 10.100.254.0/23      | P2P Spine-Leaf |                            |
| 10.100.254.1-2/30    | P2P Spine-Leaf | Spine_01-E1/3 Leaf_01-E1/0 |
| 10.100.254.5-6/30    | P2P Spine-Leaf | Spine_01-E1/4 Leaf_02-E1/0 |
| 10.100.254.9-10/30   | P2P Spine-Leaf | Spine_01-E1/5 Leaf_03-E1/0 |
| 10.100.254.13-14/30  | P2P Spine-Leaf | Spine_02-E1/3 Leaf_01-E1/1 |
| 10.100.254.17-18/30  | P2P Spine-Leaf | Spine_02-E1/4 Leaf_02-E1/1 |
| 10.100.254.21-22/30  | P2P Spine-Leaf | Spine_02-E1/5 Leaf_03-E1/1 |
| 150.150.150.1-2/30   | P2P Leaf_02-Border| Leaf_02-E1/3 Border E1/3|
| 50.50.50.1-2/30      | P2P Leaf_03-Border| Leaf_03 E1/3 Border E1/1|

# Loopback0
```
Python
| Spine 1 | 10.1.1.1/32 |
| Spine 2 | 10.1.1.2/32 |
| Leaf 1  | 10.3.1.1/32 |
| Leaf 2  | 10.4.1.1/32 |
| Leaf 3  | 10.5.1.1/32 |


```
