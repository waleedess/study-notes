- **Shell**: The user interface that allows users to request specific tasks from the computer. These requests can be made either through the CLI or GUI interfaces
- **Kernel**: Communicates between the hardware and software of a computer and manages how hardware resources are used to meet software requirements
- **Hardware**: The physical part of a computer including underlying electronics.
#### Access Methods
1. Console: Physical management port. *Do Not require prior networking services*
2. SSH: Remote secure connection via virtual interface. *Require prior networking services*
3. Telnet: Remote insecure connection. *Require prior networking services*
4. Aux: Legacy auxiliary port. *Do Not require prior networking services*

#### Terminal Emulators
1. PuTTY
2. TeraTerm
3. SecureCRT

#### Cisco IOS
###### Command Modes
1. User Exec Mode -> *Device>*
	   - Limited/ViewOnly
2. Privileged Exec Mode -> *Device#*
	   - Full Access
---
- User -> Privileged: enable
###### Configuration Modes
1. Global Configuration Mode -> *Device(config)#*
	 From global config mode, user can enter different sub-config modes each has its own particular function:
	1. Line Configuration Mode -> *Device(config-line)#*
		   - Used to Configure Console, AUX and VTYs: Virtual Terminals (ssh,telnet)
	2. Interface Configuration Mode -> *Device(config-if)#*
		   - Used to Configure a switch port or router network interface
---
- Privileged -> Global Configuration: `conf t`
- Global -> Line: `line <Connectiontype> <id>`  as  `line console 0`
- Global -> Interface: `interface <interface-type(g/f)> <slot/port>`

#### Basic Device Configuration
1. Device Names
	   - Set Name: `device(config)#hostname <name>`
	   - Unset Name: `device(config)#no hostname`
2. Passwords
	 1. Console - *that secures the User Exec Mode*
		    - Set Password: `Device(config-line)#password <passwd>`
		    - Enabling Password for User Exec: `Device(config-line)#login`
	 2. Secure the Privileged Exec Mode
		    - Set Password: `Device(config)#enable secret <passwd>`
	 3. Secure the VTYs
		    - Set Password: `Device(config-line)#password <passwd>`
		    - Enable Password for VTY: `Device(config-line)#login`
3. Encrypt Passwords
	   - Set Weak Encryption: `Device(config)#service password-encryption`
			- Only encrypts passwords in configuration files not over network
			- Startup-config and running-config display most passwords in plaintext by default
4. Banner Messages
	   - Setting Banner: `Device(config)#banner motd <delimiter.ex:#> <BannerMessage> <same delimiter:#>`

#### Storage

###### Config Files
1. Startup Configuration
	   - Stored in the NVRAM
	     - NVRAM: *Combines best of both worlds by having RAM speed but not being volatile* 
	     - `Device#Show startup-config`
2. Running configuration
	   - Stored in the RAM
	   - `Device#Show running-config` 
---
- To save Running to Startup -> `Device#copy running-config startup-config`
- `Device#reload` -> To disregard unsaved changes made to running config
	  - Causes Network Downtime as it switch the device offline for a brief amount of time
	  - To discard the changes, enter `n` or `no`.
- To Erase Startup -> `Device#erase startup-config` , Then `Device#reload` to remove it form RAM, too.
- To view Directories of config files -> `Device#Directory of <nvram/ram>:/` 