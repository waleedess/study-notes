
Diffculty: Easy
Tier: Tier 0
Finished: Yes
Source: HTB
Status: Reviewing

# Flags

#### -ic

Ignore wordlist comments -seclists’ copyrights- (default: false)

---

#### -c

colored output

---

#### -v

verbose to show the full URLs 

---

#### -w

Wordlist location flag

---

#### -u

URL flag. IP → use http:// not https

---

#### -H

`-H ’Host: FUZZ.website’` → without manually adding the entire wordlist to our `/etc/hosts`, we will be fuzzing HTTP headers with the `-H Host:` to specify a header

`-H 'Content-Type: application/x-www-form-urlencoded’` → to add a custom specific Header that tells the server the "format" of the data in the request body.**`application/x-www-form-urlencoded`**→the standard format used by HTML forms. When you click "Submit" on a login page, your browser automatically uses this format.

---

#### -t

Number of threads with default of 40 and maximum of 200 *it may disrupt it, and cause a `Denial of Service`, or bring down your internet connection in severe cases.*

---

#### -rate

`-rate <number>` → Limit the rate of req/sec

---

#### -p

`-p 0.1-0.5`→ Limit the rate of req/sec

---

#### -e

`-e  .<ext1>,.<ext2>` → to specify the extension

---

#### -s

 to activate the silent mode

---

#### -X

 `-X <HTTPREQUEST>`→to set the method 

it is GET by default

---

#### -d

`-d 'FUZZ=key’` → This is the **Data** flag. Fuzzing the *parameter name*. Asking the server

---

#### Filtering

Two Types of flags (m → match, f → filterout)

| `-(f/m)c` | status code ex. 404,200 |
| --- | --- |
| `-(f/m)l` | size |
| `-(f/m)w` | words |
| `-(f/m)l` | lines |

#### REGEX filtering

`-fr '<regex>'` 
`-fr '/\..*’` → to get hidden files

---

# Page Fuzzing

`ffuf -u <URL/FUZZ> -w <Wordlistofdir>`
And Filter with wanted status codes 
Then filter-out with the most common like if the size is 900 for most but only a few with 300, the 300s are the most likely  

---

# Extension Fuzzing

One common way to identify that is by finding the server type through the HTTP response headers and guessing the extension. For example, if the server is `apache`, then it may be `.php`, or if it was `IIS`, then it could be `.asp` or `.aspx`, and so on. This method is not very practical

To fuzz the extension, similar to how we fuzzed for directories. Instead of placing the `FUZZ` keyword where the directory name would be, we would place it where the extension would be `.FUZZ`, and use a wordlist for common extensions.

`ffuf -w <wordlistofext:(.)FUZZ> -u <URL/FUZZ>`

---

# Mass Fuzzing

Page X Extension Fuzzing search for every extension under each directory searched

`ffuf -u <URL/FUZZ1.FUZZ2> -w <Wordlistofdir:FUZZ1> -w <Wordlistofext:FUZZ2>`

| dir.FUZZ | Very Fast | Accurate | Identifying the tech stack (PHP vs ASP). |
| --- | --- | --- | --- |
| FUZZ.ext | Fast | Accurate | Finding specific files once you know the language. |
| FUZZ1.FUZZ2 | Slow | Very Accurate | Exhaustive search when you have no clues.
*If you have 1,000 filenames and 50 extensions, the tool has to make **50,000 requests*** |

It is better to search for a dir `/FUZZ` first then the technology in a must-have dir like `/index.*` so you will get the technology for example `.ext` now search for dir again with the extention `FUZZ.ext`

---

# **Recursive** Fuzzing

`-recursion-depth <number>`

If not using recursion the default is `-recursion-depth 1` → will only fuzz the main directories and their direct sub-directories.

---

# **DNS Records**

Browsers only understand how to go to IPs, and if we provide them with a URL, they try to map the URL to an IP so it looks into the local `/etc/hosts` file and doesn't find any mention of it. It asks the public DNS `Domain Name System`. If the URL is not in either, it would not know how to connect to it.

---

# **Sub-domain Fuzzing**

`ffuf -u <FUZZ.website> -w <Wordlistofdir>`

A sub-domain (`*.website.com`) is any website underlying another domain. For example, `https://photos.google.com` is the `photos` sub-domain of `google.com`.

---

# **Vhost Fuzzing**

Fuzzing sub-domains that do not have a public DNS record or sub-domains under websites that are not public the key difference between VHosts and sub-domains is that a VHost is basically a 'sub-domain' served on the same server and has the same IP, such that a single IP could be serving two or more different websites. *VHosts may or may not have public DNS records.*

`ffuf -w <Wordlisofsubdomains> -u <URL:**PORT**>/ -H 'Host: FUZZ.<Website>'`

---

# HTTP Requests Fuzzing

## GET

`ffuf -w <Parameterwordlist:FUZZ> -u <URL>?FUZZ=key` 
Enumerate parameters. With fuzzing for `GET` requests, which are usually passed right after the URL, with a `?` → `<website>?parameter=key`

---

## POST

`POST` requests are not passed with the URL and cannot simply be appended after a `?` symbol. `POST` requests are passed in the `data` field within the HTTP request.

We need to use special 3 flags:

1. `-X POST` → to set the method to POST
2. `-d 'FUZZ=key’` → requests are passed in the data to the server's internal logic and triggers a **variable check**.
3. `-H 'Content-Type: application/x-www-form-urlencoded’` →  In PHP, "POST" data "content-type" can only accept "application/x-www-form-urlencoded". So, we can set that in "ffuf" with "-H 'Content-Type: application/x-www-form-urlencoded'".

`ffuf -w <Parameterwordlist:FUZZ> -u <URL> -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded'`

---

# **Value Fuzzing**

After fuzzing a working parameter, we now have to fuzz the correct value that would return the content we need. 

`ffuf -w <Parameterwisewordlist:FUZZ> -u <URL> -X POST -d '<workingparameter>=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded'` 

- Parameter wise means for ids its most likely numbers so we can make up a list from 0→1000 for ex. parameter wise means that i put the right format to the working parameter i found

---

# Finalizing with CURL

`curl <URL> -X POST -d '<workingparameter>=<correct value>' -H 'Content-Type: application/x-www-form-urlencoded'`

---

# Proxying

#### Full Traffic Proxying

`-x <http:proxyip:8080>` 
Requests going to the proxy first, Slow but, Giving 2 advantages: 

1. Using Burpsuite things
2. Network Pivoting → If you are on a penetration test and the target is inside an internal network you can't reach directly, you might use a SOCKS5 proxy (via SSH tunneling) to "hop" through a compromised machine to reach the target.

---

#### Selective Replaying

`-replay-proxy <http:proxyip:8080>` 
Requests goes to ffuf first and the only successful will be passed to the proxy