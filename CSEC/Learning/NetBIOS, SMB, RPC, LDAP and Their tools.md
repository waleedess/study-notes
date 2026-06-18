

#### Intro

---
# Protocols' Foundations

#### NetBIOS: Network Basic Input/Output System

- Allows applications on separate computers to communicate and share resources within a LAN. 
- Designed fundemntally as Peer-to-Peer
- Operating Primarily at the **Session Layer of OSI** = **Application Layer of TCP/IP** -> NBT *NetBIOS over TCP/IP*
- Superseded by more **secure & scalable** protocols like DNS & SMB
  
###### Ports and Usages

| Port   | Name                       | Usage                                                                                          | Notes                                                                         |
| ------ | -------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| U: 137 | NBNS: NetBIOS Name Service | Name Registration & Resolution                                                                 | - Primitive version of DNS<br>- Names are broadcasted to ensure no duplicates |
| U: 138 | NetBIOS Datagram Service   | Connection-less and Fast Communication                                                         | - Broadcasting and Windows Network Neighborhood discovery features            |
| T: 139 | NetBIOS Session Service    | Manages Connection-oriented, Reliable Communication for data transfer between 2 specific hosts | - Used to carry Leagcy SMB -*before SMB had its own T: 445 port*-             |
- **All of its ports and usages are considered as high-risk legacy protocols**
  
---
#### SMB: Server Message Block

- Enabling applications on a computer to **Read/Write** to files, also request services from server programs in the network 
- Client-Server Communication

###### versions

| Version | Windows Version | Port              | OSI Layers                                                                                     | TCP Layers | Notes                                                           |
| ------- | --------------- | ----------------- | ---------------------------------------------------------------------------------------------- | ---------- | --------------------------------------------------------------- |
| SMBv1   |                 | T: 139 of NetBIOS | 7: SMB<br>->6: NetBIOS Session Service<br>>5: NetBIOS Session Service                          | 4          | - Responsible for the 2 massive attacks: Eternal Blue, WannaCry |
| SMBv2   | Visita          | T: 445            | 7->4<br>- Hands requests straight down to TCP Layer, **Completely Skipping** the middle layers | 4,3        |                                                                 |
| SMBv2.1 | 7               | T: 445            | 7->4<br>- Hands requests straight down to TCP Layer, **Completely Skipping** the middle layers | 4,3        |                                                                 |
| SMBv3   | 8               | T: 445            | 7->4<br>- Hands requests straight down to TCP Layer, **Completely Skipping** the middle layers | 4,3        |                                                                 |
| SMBv3.1 | 10              | T: 445            | 7->4<br>- Hands requests straight down to TCP Layer, **Completely Skipping** the middle layers | 4,3        |                                                                 |



---
#### RPC

- Allows programs to execute a subroutine or procedure on another computer over network as if it was a local function call
  
  
---
#### LDAP

---
###### Comparison 

---
# Enumeration Tools

#### nbtscan

---
#### smbclient & smbmap

---
#### enum4linux/-ng

---
######  Usage Guide
