- Usable address = `2^n - 2`, `n = Number of Host Bits` ,
  `Host Bits = 32-/Prefix` 
- `/31` -> Can be used in *Point to Point* Connection i.e.. router to router
---
#### FLSM
- All subnets must be of the same prefix length
- Received network like 192.168.255.0/24 -> Cannot be subnetted as we can not change the bits of network portion so we will have to borrow form the host portion as much as we need
- The number subnets we need will give us a hint to the number of bits we need to borrow, by using the formula `2^x = Number of subnets` , where 
  `x = Number of borrowed bits` 
---
#### VLSM
- Subnets can be of different sizes to be more efficient
- Start Subnetting from the largest -> smallest