- Network and Data-Link layers are responsible for felivering data so they have source and destination addresses
###### Network Layer Addresses
- Reponsible for IP packet
- Logical Addressing *-IP-*
- May be on same or remote network
###### Data Link Layer Addresses
- Responsible for data link frame
- Physical Addressing *-Mac-* on the NIC
- On Same network only
---
###### Situations
1. On the same network
   - **Mac**: Source -> Sending host
     Destination -> Receiving host
   - **IP**: Source -> Sending host
     Destination -> Receiving  host
   - **Way**: Sender -> Router -
1. On remote network
   - **Mac**: Source -> Sending host
     Destination -> ==Default Gateway== *-the mac of the router's interface it is conected to-* 
   - **IP**: Source -> Sending host
     Destination -> Receiving  host
  