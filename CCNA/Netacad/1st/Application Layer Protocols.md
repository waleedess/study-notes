![[Screenshot From 2026-06-02 22-45-08.png]]

#### Application Layer Protocols

1. **Name System**
	   1. DNS

2. **Host Configuration**
	   1. DHCPv4/6
	   2. SLAAC: *Stateless Address Auto-configuration* -> allows a device to obtain an IPv6 without DHCPv6

3. **Email**
	   1. SMTP: *Simple Mail Transfer Protocol* -> Send email to/from email servers
	   2. POP3: *Post Office Protocol v3* -> retrieve emails form mail servers and download the email to client local mail app
	   3. IMAP: *Internet Message Access Protocol* -> Access to email stored on a mail server as maintaining emails on the server

4. **File Transfer**
	   1. FTP -> Access and transfer files to/from another host over a network
		      - Reliable, Connection-Oriented and Acknowledge file delivery
	   2. SFTP: *Secure File Protocol* -> Extension to SSH
	   3. TFTP: *Trivial File Transfer Protocol* -> Simple, Connection-less and unacknowledged file delivery
		     - Less overhead than FTP/SFTP

5. **Web & Web Services**
	   1. HTTP
	   2. HTTPS
	   3. REST: *Representation State Transfer* -> Web service using APIs and HTTP to create web applications

#### Transport Layer

1. TCP -> Reliable Communication betn process on separate hosts and acknowledge transmission
2. UDP: *User Datagram Protocol* -> Only supports one to another host packets with unacknowledged transmission
   
#### Internet Layer 

2. **Internet Protocol**
	   1. IPv4/6
	   2. NAT: *Network Address translation* -> Translates IPv4 addresses from private to global unique public IPv4
3. **Messaging**
	   1. ICMPv4/6: *Internet Control Meassage Protocol* -> Feedback errors in packet delivery from destination to source
	   2. ICMPv6 ND: *ICMPv6 Neighbor Discovery* -> Includes 4 protocol messages that are used for address resolution and duplicate address detection

4. **Routing Protocols**
	   1. OSPF: *Open Shortest Path* -> Link-state routing protocol that uses hierarchical design based on areas
		      - Is an open standard ==Interior== Routing Protocol 
	   2. EIGRP: *Enhanced Interior Gateway Routing Protocol* -> uses a Composite metric on bandwidth, delay, load and reliability
		      - Is an open standard ==Interior== Routing Protocol
	   3. BGP: *Border Gateway Protocol* -> Used by ISPs with each other or with their large private clients to exchange routing information
		     - Is an open standard ==Exterior== Routing Protocol

#### Network Access Layer

1. **Address Resoultion**
	   1. ARP: *Address Resolution Protocol* -> Dynamic address mapping betn IPv4s and hardware access
2. **Data Link Protocols**
	   1. Ethernet-> Defines rules for wiring and signaling standards of the network access layer
	   2. WLAN: *Wireless Local Area Network* -> Defines rules for wireless signaling across the 2.4/5GHz radio frequencies 

---
## OSI ~ TCP/IP

| OSI             | TCP/IP            |
| --------------- | ----------------- |
| 7. Application  |                   |
| 6. Presentation | 4. Application    |
| 5. Session      |                   |
| 4. Transport    | 3. Transport      |
| 3. Network      | 2. Internet       |
| 2. Data Link    | 1. Network Access |
| 1. Physcial     |                   |
