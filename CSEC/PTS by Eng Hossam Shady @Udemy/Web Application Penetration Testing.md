#### Web Servers Examples

| Ngnix |  |
| --- | --- |
| Apache | The most popular |
| IIS  | Windows only |

---

# Web Server Enumeration

Enumerate with `nmap` ports to know which ones got the web server 

Enumerate with `nmap` scripts to see easy wins

Enumerate website technologies and services using the extension called `Wappalyzer` gives web servers, frameworks, libraries and much more

---

# Fuzzing & BruteForcing

[**Attacking Web Applications with Ffuf**](Attacking%20Web%20Applications%20with%20Ffuf.md) 

Fuzzing using `Dirsearch - ffuf - gobuster` using seclists `-w /usr/share/SecLists/Discovery/Web-Content` best ones are the raft

Or using `Burpsuite’s intruder` Steps:

1. Send request to intruder and `Clear`
2. Select the needed variable and `Add` to load wordlists
3. Then Use `Sniper attack` 

---

# Subdomain Enumeration

Using on of these

| subfinder (t) 
*Passive Recon | `subfinder -d <website> -all`  | `--recursive` → to put them in hierarchy
  • recursion works best when you have multiple API keys configured (like Shodan, Chaos, or Virustotal) so the tool has enough "sources" to find those deeper layers. |
| --- | --- | --- |
| assetfinder (t)
*Passive Recon | `echo “<website>” | assetfinder -subs-only` |   • or have a list then `cat list.txt | ass-` 
  • Searches passively from *crt.sh* |
| ffuf (t)
*Active Recon | `ffuf -u <URL> -w wordlist.txt` | Two Types of flags (m → match, f → filterout)
  • `(f/m)c` → status code ex. 404,200
  • `(f/m)s` → size
  • `(f/m)w` → words
  • `(f/m)l` → lines |
| dnscan (t)
*Active Recon | `dnscan -d <website> -w <wordlist> -t <no. of threads>` | Asks a DNS Server if a record exists. If the server says "Yes, [example.com](http://dev.example.com/) is at 192.168.1.1," the job is done.
 • `-t` → threads (speed), range:1-32, def:8 
  • `-w` → wordlist
  • `-d`→ target domains separated by commas
  • `-l` → domain list (list of target domains) |
| amass (t)
*Active & Passive Recon | `amass enum -d <website> 2>/dev/null` |   • `-d` → domain
  • `-brute` → brute forcing
  • `-asn value` → ASNs separated by commas
  • `-active` → turn on active scan, def is pasive |
|  | `amass intel -active -cidr <ip>/<subnet>` | To search CIDR |
| [SecurityTrails](https://securitytrails.com/) (w) |  |  |
| [shrewdeye](https://shrewdeye.app/) (w) |  |  |
| [subdomianfinder](https://subdomainfinder.c99.nl/) (w) |  |  |

---

Now Using Passive ones to discover VHOST
VHOST idea: virtual host is hosting 2 or more websites or domains actually on the same server with the 
- Same IP → Name-Based VHOST (manipulate the host in the request header)
- Different IP → IP-Based VHOST (scan an IP range)

| ffuf | Only with Name-Based | `ffuf -u http(s)://<website/ip> -w wordlist.txt **-H “Host:FUZZ.mars.com”**` |
| --- | --- | --- |
| nmap | **Capable** with Name-Based **but** **Expert** in IP-Based |   • Name-Based: `nmap -p <ports> --script http-vhosts --script-args <URL> <IP>` 
  • IP-Based: `nmap -p <ports> <IP range>` |

If you Found one how to break into (Name-Based)

1. Get the IP of the main domain
2. Get the name of subdomain you can’t access
3. Edit in `/etc/hosts`  and write the IP from the main domain and the subdomain you can’t access
4. Open firefox and it will open

---

# DNS

Server responsible for translating : 

1. Domain (Website) → IP (Server) : Using “A” DNS Records
2. Cloud → Domain (Website) : Using “CNAME” DNS Records
3. Mail (Email from the Domain) → Domain (Website) : Using “MX” DNS Records

---

#### Dig Command

`dig <domain/subdomain>` → shows types of records used to link what from/to the domain

---

# Dirsearch

---

## XSS Cross Site Scripting

- Client-Side vulnerability
- Results in Cookie stealing

Got many types:

1. Reflected
2. Stored
3. File Upload
4. Dom-based XSS

Will be found in the html in 6 places:

1. Input (uname, passwd)
2. Parameters
3. Comments
4. Images
5. Redirection
6. Support messages

---

## CSRF Cross Site Request Forgery

---