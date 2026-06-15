
Diffculty: Fundamental
Tier: Tier 0
Finished: No
Source: HTB
Status: Learning

# Linux Structure

Everything is a file

### Components

| Bootloader | code that runs to guide the booting process |
| --- | --- |
| OS Kernel | manages the resources for system's I/O |
| Daemons |   • each daemon is a service, but not vie versa
  • daemon works in background, all time and without supervision
  • services only work when needed 
  • usually ends with …d
  • the daemon itself is just a brain without any limbs—it knows what it wants to do, but it doesn't have the tools to do it. |
| OS Shell | interface between the OS and the user. |
| Graphics server |  |
| Window Manager |  |
| Utilities |  |

### Linux Archi.

| Hardware |  |
| --- | --- |
| Kernel |  |
| Shell | CLI |
| System Utility |  |

### File System Hierarchy

| / |  • root 
 • contains all  files required to boot the operating system before other filesystems are mounted, as well as the files required to boot the other filesystems. After boot, all of the other filesystems are mounted at standard mount points as subdirectories of the root. | Mother |
| --- | --- | --- |
| /bin |   • command binaries (bash,ls, date, mkdir)
  • a sibling folder called /sbin for System or Superuser (reboot)
  •  /bin is often just a symbolic link to /usr/bin
 | Core |
| /sbin |  | Core |
| /boot | static bootloader, kernel executable, and files required to boot | Core |
| /dev |   • device files to facilitate access to every hardware device
—>Instead of requiring a programmer to write complex, hardware-specific code to talk to a "Kingston 512GB SSD," Linux provides a file like /dev/nvme0n1. If a program wants to save data, it simply "writes" to that file, and the Linux kernel translates that "write" into physical electrons moving on the disk.
  • Common Residents :
1-Storage Devices:  /dev/sda or /dev/nvme0n1 *main hard drive*
2-Terminals: /dev/tty *Represents the terminal the current process is using*
3-Human Interface: /dev/input/mouse0: *mouse movement*, /dev/input/eventX: *Keyboard strokes*
  • The Magic Files (logical tools):
1-/dev/null *the black hole*
2-/dev/zero *endless stream of null 0 bytes*
3-/dev/random *random numbers generated from system noise*
4- /dev/full *always returns er: Disk Full*
  • Permissions:
1- c —>unbuffered byte by byte that is used for live data
2- l —>pointer to another path
3- b —>block and buffered chunks of data used for drives | Devices |
| /etc |   • Editable Text Configurations: Human-Readable,
Static.. It does not contain "binaries" It only contains the "instructions" those programs read when they start up Programs often have their own folders inside ( /etc/ssh/ *Settings for remote login (the sshd daemon)*  )
  • mess up a configuration file, your system might not boot, and having that .bak file will save your life. | Config |
| /home |   • Isolated | User |
| /root | The home directory for the root user. | Core |
| /lib |   • Shared library files that are required for system boot.
  • The /lib directory is strictly for the libraries required by the binaries in /bin and /sbin
  • /lib/modules/ *containing Kernel Modules (drivers)*
  • many modern systems (like Arch or Fedora) now make /lib a symbolic link to /usr/lib | Core |
| /media |   • External removable media devices such as USB drives are mounted here.
  • The System (daemons like udisks) automatically.
  • How to use it 
1-  Create a spot: sudo mkdir /mnt/my_usb
2- Park the device: sudo mount /dev/sdb1 /mnt/my_usb
3- Leave: sudo umount /mnt/my_usb (Note: It is umount, not "unmount"!) | Devices |
| /mnt (mount) |   • Needs Admin
  • Manual/Static mounts
  • handled by “mount” cmd | Devices |
| /opt |   • a sandbox or private storage locker for 3rd party weren't built by Linux
  • It keeps everything—/bin binaries,/lib libraries, and /etc settings—inside its own single folder.
  • Since files in /opt are hidden in their own private lockers, the system doesn't "see" them automatically.
If you install a program to /opt/mytool/bin/mytool, typing “mytool” in the terminal won't work unless you do **one of two** things:
1- Create a Symbolic Link (”ln -s <TARGET> <LINK_NAME>”) from /opt/mytool/bin/mytool to /usr/local/bin.
2- Add the /opt folder to your PATH variable. | Software |
| /usr |   • usr=Unix System Resources and it stores User Serviceable Read-only data
  • mirror some directories as /bin /sbin /lib
  • /usr/share: *This is for "architecture-independent" data*
some things like word lists and nmap scripts | Software |
| /tmp (temporary) |   • "public R&W" area where any user or program can scribble down notes and are deleted automatically when you reboot | Devices |
| /var (variant) |   • same as /tmp by persistent and survives a reboot | Config |
| /proc |   • stands for Process Information —>contains PIDs
  • does not exist on your hard drive. it is a virtual filesystem created by the Linux kernel in your RAM every boot. | Config |
| /sys  |   • does not exist on your hard drive. t is a virtual filesystem created by the Linux kernel in your RAM every boot.
  • clean up the mess in /proc by moving hardware-specific information into its own organized hierarchy
  • Many files are writable —> allows you to control hardware directly by just sending a number to a file |  |
| /srv |   • to keep the data you are "serving" to others separate from the "working data" the system needs to run
  • example directories /srv/www /srv/ftp
  • might be empty on PC but useful for multiusers and entrprises | Software |
| /run |   • reated in RAM immediately by the kernel, it is available from the very first second the computer turns on |  |

## Useful Comparison (colors show sensitive data risk ranking)

| /var | /tmp | /run | /proc | /dev/shm |
| --- | --- | --- | --- | --- |
| Disk  | Disk mostly or RAM | RAM | Virtual | RAM |
| Persistent | usually not | no | no | no |
|   • system must remember ex. (logs, mail, spool, cache, databases, backups) ex /var/log/auth.log |   • temporary object files go here of users and apps
 |   • 	Runtime state data (PIDs, sockets, locks)
 • very structured and handled mostly by the OS itself, not by you or your random apps. |   • Kernel is actually generating a report for you on the fly. It’s for information, not for storing your own data. |   • this "file" is actually just a block of RAM, they can both **read and write** to it at the speed of light without the "lag" of a hard drive.
 |
| some writable subdirs, Often writable by services | writable | Yes (root; some subdirs user-writable) | Mostly No, only some writable and by root only | writable |
| contain very sensitive data 
+ Most valuable target for attackers after /etc + critical for forensic investigations | contain very sensitive data 
+ Common exploitation area. | contain sensitive data | contain sensitive data + reconnaissance gold + process & kernel exposure | contain very sensitive data
+ Often used to evade 
disk-based detection. |
|  • Log tampering
 • Credential artifacts
 • Database storage
 • Webshell uploads
 • Backup leakage
 |  • Common attack target (symlink attacks, race conditions). 
• Malicious file replacement 
• Sensitive temp files left behind
 |  • Exposure of running service info  
 •  PID file manipulation (if misconfigured)
 |  • Process and environment leakage  
 • Kernel parameter tampering (root only)  |  • In-memory payload storage
 • Used in fileless malware
 • Race condition vulnerabilities
 |

# System Information

### some commands (in-red are the most important)

| Id | audit account permissions and group membership |
| --- | --- |
| Which bash/python/gcc/wget |  Which shell is specified for the user |
| uname -a | all information about the machine in a specific order: kernel name, hostname, the kernel release, kernel version, machine hardware name, and operating system |
| uname -r |  print out the kernel release as it an the processor type “-p” not included under the -a flag |
| ss | investigate sockets. (port no. + ip ex. 255.255.255.255:65035) |
| ps —aux | Shows process status. |
| who | Displays who is logged in. |
| env | Prints environment or sets and executes command |
| lsblk | Lists block devices. (disks, drives and all (un)mounted files)  |
| lsusb | Lists USB devices |
| lsof | Lists opened files. |
| lspci | Lists PCI devices |
| lscpu | Lists CPU info |
| mkdir -p /x/xy/z | it means create a new dir and if any parent is not found create it ,too |

### useful “find” coomand flags and options

| /xx/xy/xyz |  | path |
| --- | --- | --- |
| -type  | f | files |
| -name | xxx or *.conf | name or asterisk=all |
| -user | root |  |
| -size | +20k | all above 20KB |
| -newermt | 2020-03-03 | all newer than this date |
| -exec _____ \; | ls -al | خد النتايج واعملها ls -la |
| -exec _____ + | ls -al | difference betn it and the \; is that the \; executes the cmd each time put the plus only once |
| 2> | /dev/null | take all errors to the specified path |
- File Descriptors (the ID numbers the system gives to data streams): 
0: standard input
1: standard output
2: standard output error
- “findcommand” | wc -l —> count lines ie. results
- “findcommand” > results.txt  —> put results in this file
- “findcommand” 2>err.txt 1>out.txt —> error ro err.txt, results to out.txt

### Filter Contents

| (| more) <path> | prints in fragments and the whole will still be seen after end | quit with q |
| --- | --- | --- |
| (| less) <path> | same as more put once you quit or end it will only display the terminal with the command no prints | quit with q |
| (| head) <path> | prints the first 10 lines |  |
| (| tail) <path> | prints the last 10 lines |  |
| (| sort) <path> | sorts acc to flag |   • -f —> ignore case
  • -M —>monthly sort
  • -n —> numeric
  • --sort=WORD
sort according to WORD: general-numeric  -g,  human-numeric  -h,
month -M, numeric -n, random -R, version -V
  • -V —> version sort |
| grep (will be studied in detail) |  |  |
| (| cut) <path> | extract specific vertical columns |   • -z —> no line delimiter; not a newline
  • --output-delimiter=STRING
use  STRING  as  the  output delimiter
  • -s —> print lines delimited
  • -d —> use delimiter |
| (| Tr) <path> | replace certain characters from a line with characters defined | ex. tr “:”  “ ”
: —>   |
| (| column) <path>  | display such results in tabular form | -t |
| (| Awk) <path> ‘{print $1, $NF}’ | display output of specific column |   • $1 —> 1st field or coulmn
  • $NF —> last 
NF indicates the field number by dollar sign it means the last |
| Sed (will be studied in detail) | stream editor |  |
| (| Wc)  | counts acc to flag |   • -L —> count lines |

### RegEx

| (a) |  | Within round brackets, you can define further patterns which should be processed together. |
| --- | --- | --- |
| [a-z] |  | Inside square brackets, you can specify a list of characters to search for. |
| {1,10} |  | Inside curly brackets, you can specify a number or a range that indicates how often a previous pattern should be repeated. |
| | |  (my|false) | OR operator and shows results when one of the two expressions matches |
| .* | (my.*false)  | AND operator by displaying results only when both expressions are present and match in the specified order |

# Permissions

(xxxx) —> (special (s/t), owner, group, others)

| r | 4 |  |
| --- | --- | --- |
| w | 2 |  |
| x | 1 | For apps → can’t execute
For directories → can’t opened |
| s | 4: run as owner
2: run as group | Special Permissions known as SetUID (Set User ID) and SetGID (Set Group ID). |
| t —>sticky bit is active but dir is not exec.
T —>sticky bit is active but dir is not exec. | 1 | only file owner -beside the root- can delete/rename even if others have access |

```
Sticky Bit + Full Permissions: chmod 1777 /my_folder (Results in rwxrwxrwt)

Sticky Bit + No Public Execute: chmod 1776 /my_folder (Results in rwxrwxrwT)
```

### chmod

| owner | u | +/- (r/w/x) |
| --- | --- | --- |
| group | g | +/- (r/w/x) |
| others | o | +/- (r/w/x) |
| all | a | +/- (r/w/x) |

### chown

<user>:<group> <file/directory>

### User Management

| sudo su | su utility requests appropriate user credentials, the default user is the superuser, a shell is executed |
| --- | --- |
| useradd |  |
| userdel |  |
| usermod |  |
| addgroup |  |
| delgroup |  |
| passwd |  |

# Packages

A package is an archive file containing multiple .rpm, .deb, etc.

### package management programs

| dpkg | install, build, remove, and manage Debian packages  |
| --- | --- |
| apt | high-level command-line interface 
• APT uses a database called the APT cache. This is used to provide information about packages installed on our system offline ex. ‘apt-cache search impacket’ & ’apt-cache show <Impacket name> & apt list --installed
 |
| aptitude | alternative to apt and is a high-level interface + a friendly front end than dpkg |
| snap | Install, configure, refresh, and remove snap packages. Snaps enable the secure distribution of the latest apps and utilities for the cloud, servers, desktops, and the IoT |
| gem | standard package manager for RubyGems |
| pip | Python package installer, can work with version control repositories (currently only Git, Mercurial, and Bazaar repositories), prevents partial installs by downloading all requirements before starting installation. |
| git | fast, scalable, distributed revision control system, provides both high-level operations and full access to internals
  • `git clone <githublink> ~/<foldername>` |

### wget

- stands for **World Wide Web Get**. It is a command-line utility used to retrieve content from web servers via HTTP, HTTPS, and FTP protocols, It can recursively download every page of a site for offline viewing.
- `wget -c` can pick up right where it was paused

# **Service and Process Management**

### Daemons (services)

- As mentioned earlier there names end with d ex. sshd
- have 2 types: 
1-System Services: required during system startup and perform essential hardware-related tasks and initialize system components
2-User-Installed Services: added by users and typically include server applications and other background processes
- `systemd` is the initialization system (init system),  first process that starts during the boot process
- Process are assigned a `PID` and can be viewed under the `/proc/` directory, which contains information about each process. Processes may also have a Parent Process ID (`PPID`), indicating that they were started by another process.

### **Systemctl & journalctl**

systemctl <option> <process>

| `systemctl start` |  |
| --- | --- |
| `systemctl status` |  |
| `systemctl enable` | add the selected service to the sysV service script to run this service early after the startup |
| `systemctl list-units --type=service` |  to list all services |

| `journalctl -u <servicename.service> --no-pager` | to view the logs |
| --- | --- |

### Process states

| Running |  |
| --- | --- |
| Waiting | for event or resource |
| Stopped |  |
| Zombie | stopped but still has an entry in the process table |

### Process control

can be controlled using `kill`, `pkill`, `pgrep`, and `killall`. To interact with a process, we must send a signal to it.

### Kill

Kill <type of signal by numbers below> <PID>

| `SIGHUP` | 1 | sent to a process when the terminal that controls it is closed. |
| --- | --- | --- |
| `SIGINT` | 2 | user presses `[Ctrl] + C` in the controlling terminal to interrupt a process |
| `SIGQUIT` | 3 | user presses `[Ctrl] + D` to quit.  |
| `SIGKILL` | 9 |  Immediately kill a process with no clean-up operations |
| `SIGTERM` | 15 | termination |
| `SIGSTOP` | 19 | Stop the program. It cannot be handled anymore |
| `SIGTSTP` | 20 | user presses `[Ctrl] + Z` to request for a service to suspend. The user can handle it afterward |

### Back/Foreground process

| `bg` | put the process in the background, will display return when it finishes |
| --- | --- |
| `<command> &` | put the process in the background, will display return when it finishes |
| `jobs` | all background processes (not a sys or journal command) identified with a number to order |
| `fg <bg process number>` |  |

# **Multiple Commands exec.**

| ; | executes the commands by ignoring previous commands' results and errors |
| --- | --- |
| && | executes the commands by ignoring previous commands' results but not errors |
| | | executes the commands by considering both previous commands' results and errors |

# **Task Scheduling**

### **systemd**

- Systemd is a service used in Linux systems
- we need to take some steps and precautions before our scripts or processes are automatically executed by the system
1. Create a timer (schedules when your `mytimer.service` should run)
2. Create a service (executes the commands or script)
3. Activate the timer

**1. Create a Timer**

- To create a timer for systemd, we need to create a directory where the timer script will be stored. : `sudo mkdir /mytimer.timer.d`
- Next, we need to create a script that configures the timer. The script must contain the following options:

```
[Unit]
Description=My Timer

[Timer]
OnBootSec=3min
OnUnitActiveSec=1hour

[Install]
WantedBy=timers.target
```

| Unit | option specifies a description for the timer |
| --- | --- |
| Timer | option specifies when to start the timer and when to activate it
  • OnBootSec —> to run only once after boot
  • OnUnitActiveSec —> to run at regular intervals |
| Install | specifies where to install the timer. |

2. **Create a Service**

- To create a service for systemd, `sudo vim /etc/systemd/system/mytimer.service`

```
[Unit]
Description=My Service

[Service]
ExecStart=/full/path/to/my/script.sh

[Install]
WantedBy=multi-user.target
```

| Unit |  |
| --- | --- |
| **Service** |  |
| Install |   • [multi-user.target](http://multi-user.target) —>  normal multi-user mode |

**3. Reload Systemd**

`sudo systemctl daemon-reload`

**4. Start the Timer & Service**

```bash
sudo systemctl start mytimer.timer --> to start the service manually
sudo systemctl enable mytimer.timer --> enable the autostart
```

### **Cron**

- Tasks are stored at /crontab

‘#Backups
0 */6 * * 7 /path’ ←example command
Cron have 5 astrisks each tells smth starting from the left
*               *               *                *              *

mins        hrs          day(m)      mon       day(w) 

---

for that*/6:—*→every, /6→specifies the increment
(0,30)—(,)→Used for lists
(9-17)—(-)→Used for ranges

---

The day of the week (0–7, where 0 and 7 are both Sunday) & 0 for hrs means midnight.

| Minutes (0-59) |
| --- |
| Hours (0-23) |
| Days of month (1-31) |
| Months (1-12) |
| Days of the week (0-7) |

### **Systemd vs. Cron**

The key difference between these two tools is how they are configured. With Systemd, you need to create a timer and services script that tells the operating system when to run the tasks. On the other hand, with Cron, you need to create a `crontab` file that tells the cron daemon when to run the tasks.

# Network Services

### SSH

- OpenSSH is a free, opensource implementation of SSH

‘sudo apt install openssh-server -y’ → to install OpenSSH

‘systemctl status ssh’ → to check the server status

- OpenSSH can be configured and customized [max no. of conn., passowrds, keys, host key check, etc.] by editing the file `/etc/ssh/sshd_config` using a text editor

### NFS

- Stands for Network File System
- there are several NFS servers, including NFS-UTILS (`Ubuntu`), NFS-Ganesha (`Solaris`), and OpenNFS (`Redhat Linux`).
- It enables easy and efficient management of files across networks, It can also be used to share and manage resources efficiently, also offers features such as access controls, real-time file transfer, and support for multiple users accessing data simultaneously. We can use this service just like FTP.

‘sudo apt install nfs-kernel-server -y’ → to install NFS

‘ systemctl status nfs-kernel-server’ → to check the server’s status

- configure NFS via the configuration [speed, use of encryption] by editing file `/etc/exports` ,This file specifies which directories should be shared and the access rights for users and systems

| rw | users and systems read and write permissions |
| --- | --- |
| ro | users and systems read-only access |
| no_root_squash | Prevents the root user on the client from being restricted to a normal user |
| root_squash | Restricts the rights of the root user |
| sync | ensure that changes are only transferred after they have been saved |
| async | transfer faster, but may cause inconsistencies in the file system |
- to create a NFS 
’echo  ‘/<dir to be shared> hostname(rw,sync,no_root_squash)' >> /etc/exports’
- we have to mount it to work with it on the target system
’mount <target ip>:/home/john/dev_scripts ~/target_nfs’

### **Web Server**

- Among the most widely used web servers on Linux platforms are Apache, Nginx, Lighttpd, and Caddy, with Apache being particularly popular due to its broad compatibility with operating systems including Ubuntu, Solaris, and Red Hat Linux.

‘sudo apt install apache2 -y’ → to install apache web server

‘sudo systemctl start apache2’ → to start the apache

- For Apache2, to specify which folders can be accessed and what actions can be performed, we can edit the file `/etc/apache2/apache2.conf` with a text editor.
- the default `/var/www/html` folder is accessible, that users can use the `Indexes` and `FollowSymLinks` options, that changes to files in this directory can be overridden with `AllowOverride All`, and that `Require all granted` grants all users access to this directory. For example, if we want to transfer files to one of our target systems using a web server, we can put the appropriate files in the `/var/www/html` folder and use `wget` or `curl` or other applications to download these files on the target system.
- It is also possible to customize individual settings at the directory level by using the `.htaccess` file, which we can create in the directory in question. This file allows us to configure certain directory-level settings, such as access controls, without having to customize the Apache configuration file. We can also add modules to get features like `mod_security`, `mod_ssl` acts like a lockbox, securing the communication between the browser and the web server by encrypting the data,`mod_proxy` traffic controller, directing requests to the correct destination,`mod_headers + mod_rewrite` traffic controller, directing requests to the correct destination. and that help us improve the security of our web application.
- navigate using our browser to the default page ([http://localhost](http://localhost/)). By default, Apache will serve on HTTP port 80, and your browser will default to this port as well whenever you enter an HTTP [URI](https://clouddocs.f5.com/api/irules/HTTP__uri.html)
- To set an alternate port for our web server, we can edit the `/etc/apache2/ports.conf` then restart Apache and instead browse to `http://localhost:8080`, or could use a command line tool such as `curl` to verify: ‘curl -I [http://localhost:8080](http://localhost:8080/)’

‘python3 -m http.server’ → to install python web server 

- Python Web Server will be started on the `TCP/8000` port, and we can access the folder we are currently in. We can also host another folder using ‘python3 -m http.server --directory /target_files’
- ‘python3 -m http.server 443’ → to change port to 443

### **VPN**

- Among the most widely used VPN solutions for Linux servers are OpenVPN, L2TP/IPsec, PPTP, SSTP, and SoftEther. OpenVPN stands out as a popular open-source option compatible with various operating systems, including Ubuntu, Solaris, and Red Hat Linux.

‘sudo apt install openvpn -y’ → to install  OpenVPN

- OpenVPN can be customized and configured [encryption, tunneling, traffic shaping, etc.] by editing the configuration file `/etc/openvpn/server.conf`

‘sudo openvpn --config internal.ovpn’ → connect to vpn

# communication with a web server

### cURL

`cURL` is a tool that allows us to transfer files from the shell over protocols like `HTTP`, `HTTPS`, `FTP`, `SFTP`, `FTPS`, or `SCP`, and in general, gives us the possibility to control and test websites remotely via command line. 

### wget

An alternative to curl is the tool `wget`. With this tool, we can download files from FTP or HTTP servers directly from the terminal,  website content is downloaded and stored locally.

### **Python 3**

Another option that is often used when it comes to data transfer is the use of Python 3. In this case, the web server's root directory is where the command is executed to start the server. For this example, we are in a directory where WordPress is installed

# **Backup and Restore**

### Rsync

open-source tool that allows for fast and secure backups, whether locally or to a remote location. One of its key advantages is that it only transfers the portions of files that have changed, making it highly efficient when dealing with large amounts of data. Rsync is particularly useful for network transfers, such as syncing files between servers or creating incremental backups over the internet.
”sudo apt install rsync -y” → install rsync
”rsync -av /path/to/mydirectory” → To backup an entire directory using **Backup-Server**

| -a | archive. used to preserve the original file attributes, such as permissions, timestamps, etc. |
| --- | --- |
| -v | verbose |
| -z | enabled compression, for faster transfers |
| --backup | option creates incremental backups in the directory |
| --delete |  removes files from the remote host that is no longer present in the source directory. |
| -e | specify the **remote shell program** you want `rsync` to use to communicate with the other machine.
for ex “ -e ssh “ → By using SSH, we are able to encrypt our data as it is being transferred, The encryption key itself is also safeguarded by a comprehensive set of security protocols |

“rsync -av user@remote_host:/path/to/backup/directory” → restore our directory from our backup server to our local directory

```bash

```

### Duplicity

builds on Rsync, but adds encryption features to protect the backups. It allows you to encrypt your backup copies, ensuring that sensitive data remains secure even if stored on remote servers, FTP sites, or cloud services like Amazon S3. Duplicity provides an extra layer of security while maintaining Rsync's efficient data transfer capabilities.

### Deja Dup

simple, more user-friendly offering a graphical interface, accessible, safe and anyone can operate, it also uses Rsync, while still offering the same level of Duplicity’s protection. Encrypting your backups adds an additional lock on your safe, ensuring that even if someone finds it, they can't get inside.

---

- On Ubuntu systems, you can use additional encryption tools like GnuPG, eCryptfs, or LUKS to add another layer of protection to your backups.