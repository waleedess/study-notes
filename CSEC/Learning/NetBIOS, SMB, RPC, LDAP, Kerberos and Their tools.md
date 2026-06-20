

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
#### RPC: Remote Procedure Call

- Allows programs to **execute** a subroutine or procedure on another computer over network as if it was a local function call
- Client-Server Inter-Process Communication
  
###### Ports and Usages

| Port                                        | Name                                            | OSI Layers                                          | TCP/IP Layers | Usage                                                                                                                                                                     |
| ------------------------------------------- | -------------------------------------- | --------------------------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| T/U: 135                                    | R                                               | Layer 5: Session                                    | 4             | - Registers, tracks and looks up endpoints<br>- Handle initial handshake client -> server                                                                                 |
| T/U: 49152 – 65535 Dynamic RPC Workers / Ephemeral Ports  ts  ts  ts  ts  ts  ts  ts  ts  ts  | Layer 4: Transport<br>(*Carrying Layer 7 payloads*) | 3             | - Actual data transmission and function execution                                                                                                                         |
| T: 445                                                                                        | Layer 7: Application                                | 4             | - Relies on SMB to handle application-layer authentication and transport encapsulation                                                                                    |
| T: 80/443                                      | M  dern  RPC<  r>(g  PC /  RPC   ver   TTP)  | Layer 7: Application<br>Layer 6: Presentation       | 4             | - Payloads serialized using (JSOM or Protocol Buffers) and sent natively inside HTTP/S application streams<br>- Serialization/NDR Network Data Representation are Layer 6 |
- **Due to RPC's dynamic nature it is difficult to firewall due to Dynamic worker ephemeral ports** -> To have some security force RPC to use tightly controlled, static range of ports and restrict the port 135 **TCP & UDP**

---
#### LDAP: Lightweight Directory Access Protocol

- Used for Querying and managing distributed directory information services over an IP network
- Organizes data such as user credentials, groups, accounts, organizational units into tree-like structure called **Directory Information Tree - DIT** 
- LDAP servers are engine for centralized identity and access management (IAM) as it utilizes **read-heavy** architecture that allows clients applications to rapidly search, authenticate and authorize users across enterprise networks
- Operates at the Application layer of Both OSI & TCP/IP

###### Ports and Usages

| Port     | Name                           | OSI Layers            | TCP/IP Layers | Usage                                                                                                                                                  | Notes                                                                                                               |
| -------- | ------------------------------ | --------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| T/U: 389 | Standard LDAP                  | Layer 7: Application  | 4             | - Standard directory queries, modifications, and authentication requests.                                                                              | - **Cleartext** *(unencrypted)* by default<br>- Frequently upgraded to an encrypted TLS session using **StartTLS**. |
| T: 636   | LDAPS<br>*(LDAP over SSL/TLS)* | Layer 6: Presentation | 4             | - It serves the exact same purpose as port 389 (searching, binding, altering directory objects), but it mandates encryption from the very first packet |                                                                                                                     |
| T: 3268  | Global Catalog LDAP            | Layer 7: Application  | 4             | - Used to query the Global Catalog with Active Directory                                                                                               |                                                                                                                     |
| T: 3269  | Global Catalog LDAPS           | Layer 6: Presentation | 4             | - Used to query the Global Catalog with Active Directory                                                                                               |                                                                                                                     |


---
#### Kerberos Protocol

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
