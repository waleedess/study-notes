
| Knowledge Priority | Classs                     | Range in Decimal                | Prefix | Primary Use                                           |
| :----------------: | -------------------------- | ------------------------------- | ------ | ----------------------------------------------------- |
|         1          | This Host / Network        | 0.0.0.0~0.255.255.255           | /8     | Source address during DHCP initialization             |
|         0          | Shared Address Space       | 100.64.0.0~100.127.255.255      | /10    | Carrier-Grade NAT (CGNAT) service providers           |
|         1          | Loopback Address Space     | 127.0.0.0~127.255.255.255       | /8     | Localhost diagnostic testing                          |
|         1          | Link-Local (APIPA)         | 169.254.0.0~169.254.255.255     | /16    | Auto-configuration when DHCP is unreachable           |
|         0          | IETF Protocol Assignments  | 192.0.0.0~192.0.0.255           | /24    | Specialized protocol headers / DS-Lite                |
|         0          | Documentation (TEST-NET-1) | 192.0.2.0~192.0.2.255           | /24    | Textbook examples and technical guides                |
|         0          | 6to4 Relay Anycast         | 192.88.99.0~192.88.99.255       | /24    | Deprecated IPv6-to-IPv4 relay gateway                 |
|         0          | Benchmark Testing          | 198.18.0.0~198.19.255.255       | /15    | Lab performance and stress-testing equipment          |
|         0          | Documentation (TEST-NET-2) | 198.51.100.0~198.51.100.255     | /24    | Textbook examples and technical guides                |
|         0          | Documentation (TEST-NET-3) | 203.0.113.0~203.0.113.255       | /24    | Textbook examples and technical guides                |
|         1          | D                          | 224.0.0.0~239.255.255.255       | /4     | One-to-many communication (e.g., OSPF, video streams) |
|         1          | E                          | 240.0.0.0~255.255.255.254       | /4     | Reserved for future use / system drops                |
|         1          | Limited Broadcast          | 255.255.255.255~255.255.255.255 | /32    | Floods immediate local broadcast domain               |
