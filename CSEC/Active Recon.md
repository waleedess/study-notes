
Diffculty: Fundamental
Finished: Yes
Source: THM
Status: Learning

# Ping

- Some useful flags
    - `-c`: On Linux, Mac → Count
    `-n` : On WIN → Count
    - `-s` → size
- MS Windows Firewall block ping by default

---

# Traceroute

Traces the route taken by the packets from your system to another host to find the IP addresses of the routers or hops that a packet traverses as it goes, also reveals the number of routers between the two systems. It is helpful as it indicates the number of hops (routers) in between

`traceroute <IP/Website>` : On Linux, Mac
`tracert <IP/Website>` : On windows

We rely on ICMP to “trick” the routers into revealing their IP addresses. We can accomplish this by using a small Time To Live (TTL) in the IP header field. 

Although the T in TTL stands for time, TTL indicates the maximum number of routers/hops that a packet can pass through before being dropped; TTL is not a maximum number of time units. When a router receives a packet, it decrements the TTL by one before passing it to the next router.

On Linux, traceroute will start by sending UDP datagrams within IP packets of TTL being 1. Thus, it causes the first router to encounter a TTL=0 and send an ICMP Time-to-Live exceeded back. Hence, a TTL of 1 will reveal the IP address of the first router to you. Then it will send another packet with TTL=2; this packet will be dropped at the second router. And so on.

---

# Telnet (Teletype Network)

`telnet <IP> <Port>`
For ex. i can connect on the port 80 for HTTP and send this `GET / HTTP/1.1` if it has a webpage it will send it with some interesting info, and so on.

---

# NetCat

`nc <IP> <Port>` 

- Some flags:
    - -l → Listen mode
    - -p → Specify the Port number
    - -n → Numeric only; no resolution of hostnames via DNS
    - -v → Verbose output (optional, yet useful to discover any bugs)
    - -vv → Very Verbose
    - -k → Keep listening after client disconnects
        - `nc -lvnp <Port>`