#### VLANs
- LAN is a specific Broadcast Domain, Routers won't pass any Broadcast Frames so a It creates a closed **Broadcast domain** -a group of devices that receive a Broadcast Frame- that is referred to be a LAN
- VLANs are Configured on Switches and Operates at Layer 2 
- Subnetting of Layer 3 will divide LANs Logically -IP wise- only. Within a subnet only switch operates. but, when form a LAN to other, the packet with ==Dest. IP of **target** and Dest. MAC of the **router** -the sender's default gateway-== will be handled by the router as they are in different subnets and need logical routing. However if a Broadcast frame came -Identified by all 'f's MAC-, It will be forwarded to all disregarding subnetting.
- VLANs of Layer 2 will Isolates LANs Logically Physical. Within a VLAN only switch operates, but when a VLAN to other, the switch will pass the packet with ===Dest. IP of **target** and Dest. MAC of the **router** -the sender's default gateway-== will be handled by the router as the switch does not perform inter-VLAN routing. Also, if a Broadcast frame came, it will be be forwarded to only devices within that VLAN.
	- Keep in mind that **Layer 3 Switches (Multi-layer Switches)** _can_ perform inter-VLAN routing using SVIs (Switched Virtual Interfaces). On a Layer 3 switch, the "router" is built right into the switch hardware.
	- VLANs ensures Performance and Security

#### Trunking
- Switches will 'tag' all frames that they send over trunk link to allow the receiving switch to know which VLAN the frame belongs to
- There are 2 trunking protocols
	  1. ISL -> Legacy Cisco protocol 
	  2. EEE 802.1Q 'dot1q' -> Real-world
	     - VLAN 1 is the native VLAN on all trunk ports by default. It can be changed but it must match with other switches
	       -> the native VLAN frames are not tagged and receiver switch assumes any untagged is from the native VLAN
	     - Its tag (32bits) is inserted between Source MAC and type/length field in the Ethernet and the tag consists of 2 main fields
	     1. TPID: Tag Protocol Identifier (16bits)
		     - Always set to value of`0x8100`indicating dot1q tagging
	     2. TCI: Tag Control Information
	        That TCI consists of 3 sub-fields
	        1. PCP (3bits)
		        - Used for Class of Service CoS, to prioritize important traffic in congested networks
	        2. DEI (1bit)
			    - Used to indicate frames that can be dropped if the network is congested
	        **3. VID (12bits)**
			    - Identifies the VLAN the frame belongs to 
			    - 12bits, `2^12 =4096` total number of VLANs with range of 0-4095
				- 0 and 4095 are reserved and can not be used so the actual range is 1-4094
					  - Normal VLANs range: 1-1005
					  - Extended VLANs range: 1006-4094 *some Legacy devices can not use extended vlans*

### Cisco IOS CLI
-> `#show vlan breif` 
###### Default Config
- VLAN 1 is found and will be containing all interfaces by default
- Also there will be 4 1002:5 VLANs of legacy technologies
- All Default VLANs cannot be deleted 
###### Config 
1. Assigning interfaces
	 Interface to a VLAN
	   `(config)# interface <interface-type> <slot/port>` 
	   ->(config)#interface g1/0
	 Range of interfaces to a VLAN
	   `(config)#interface range <interface-type(g/f)> <slot/port> - <ending-port-number>`  
	   ->(config)#interface range g1/0 - 3 
2. Setting interfaces Port mode
	As an Access Port
	   - Access 'untagged' Port is a switch port that belongs to a single VLAN
	   1st:`(config-if(-range))#switchport mode access`
	   2nd:`(config-if(-range))#switchport access vlan <VLAN-id(ex.20)>`
	As a Trunking Port
	   - Trunking 'tagged' Port is a switch port that carry traffic from multiple VLANs over a single interface
	   1st:
	   2nd:
3. Setting VLAN Characteristics
	   1. `(config)# vlan <VLAN-id>`
	   2. `(config-vlan)#name <name>`
###### Config Notes
1. Assigning interfaces to a VLAN that is not created will create it automatically.
   VLANs Creation: `(config)# vlan <VLAN-id>`
2. Do not forget to add the interfaces of wires between switch and router to the VLAN serving each from the switch