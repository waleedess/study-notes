

#### Intro

---
# Protocols' Foundations

#### NetBIOS: Network Basic Input/Output System

- Allows applications on separate computers to communicate and share resources within a LAN. 
- Operating Primarily at the Session Layer of OSI = Application Layer of TCP/IP -> NBT *NetBIOS over TCP/IP*
- Superseded by more ==secure & scalable== protocols like DNS & SMB
  
###### Ports and Usages

| Port   | Name                       | Usage                                                                                          | Notes                                                                         |
| ------ | -------------------------- | ---------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| U: 137 | NBNS: NetBIOS Name Service | Name Registration & Resolution                                                                 | - Primitive version of DNS<br>- Names are broadcasted to ensure no duplicates |
| U: 138 | NetBIOS Datagram Service   | Connection-less and Fast Communication                                                         | - Broadcasting and Windows Network Neighborhood discovery features            |
| T: 139 | NetBIOS Session Service    | Manages Connection-oriented, Reliable Communication for data transfer between 2 specific hosts | - Used to carry Leagcy SMB -*before SMB had its own port*-                    |
- **All of its ports and usages are considered as high-risk legacy protocols**
  
---
#### SMB

---
#### RPC

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
