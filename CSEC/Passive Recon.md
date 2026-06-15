
Diffculty: Fundamental
Finished: Yes
Source: THM
Status: Learning

# Tools/Commands

### WHOIS

`whois DOMAIN_NAME`

- Search in the WHOIS server (Listens on tcp port 43) that acts as a directory database for domain names, IP address blocks, and Autonomous System Numbers (ASNs).
- Gives info for
    - Registrar
    - Contact info of registrant - *(unless made hidden via a privacy service)*
    - Creation, update, and expiration dates
    - Name Server

---

### Nslookup

`nslookup -type=<OPTIONS> DOMAIN_NAME SERVER` 

- Options:
    
    
    | A | IPv4 Addresses | Domain (Website) → IP (Server) |
    | --- | --- | --- |
    | AAAA | IPv6 Addresses | Domain (Website) → IP (Server) |
    | CNAME | Canonical Name | Cloud → Domain (Website) |
    | MX | Mail Servers | Mail (Email from the Domain) → Domain (Website) |
    | SOA | Start of Authority |  |
    | TXT | TXT Records |  |
- Server → Any local or public DNS server

---

### Dig

`dig @<server> DOMAIN_NAME TYPE`

- Same Type options as nslookup
- Returns more information than nslookup like TTL and etc.

---

# Websites

### DNSDumpster

[https://dnsdumpster.com/](https://dnsdumpster.com/)

### Shodan

[https://www.shodan.io/](https://www.shodan.io/)

you can use different services from [Shodan.io](http://shodan.io/) to learn about connected and exposed devices belonging to your organization.

[Shodan.io](http://shodan.io/) tries to connect to every device reachable online to build a search engine of connected “things” in contrast with a search engine for web pages. Once it gets a response, it collects all the information related to the service and saves it in the database to make it searchable.