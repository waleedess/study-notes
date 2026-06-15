### Physical Layer Standards
- **Physical Layer Governing Organizations:**
Global and National: ISO, TIA/EIA, ITU, ANSI, and IEEE. Regulatory Authorities: FCC (USA) and ETSI (Europe). Regional Cabling Groups: CSA (Canada), CENELEC (Europe), and JSA/JIS (Japan).
- These standards address **three functional areas**:
	1. **Physical components**: Electronic hardware devices,cable materials & media, interfaces & connectors, NICs
	2. **Encoding**: Converts data bits into predictable bit groupings or patterns to represent digital information, similar to Morse code.
	   - Example: Manchester Encoding
	     It represents 0 bits by high-to-low voltage transitions and 1 bits by low-to-high voltage transitions occurring at the middle of each bit period. It is an older method used in 10 Mbps Ethernet standards like 10BASE-T.
	1. **Signaling**: Representing bits can be as simple as changing an electrical signal level or optical pulse duration, where a long pulse can mean a 1 and a short pulse can mean a 0.
---

## Bandwidth
Bandwidth is the data-carrying capacity of a physical medium, measuring the amount of data flowing from one place to another in a given time. It is typically measured in kbps, Mbps, or Gbps.
- Bandwidth is incorrectly thought of as bit travel speed. Bits travel at the same physical speed (e.g., speed of electricity in 10Mbps and 100Mbps Ethernet), but higher bandwidth means more bits are transmitted per second.
- Determinants of Bandwidth:
	   1. Physical media properties
	   2. Technologies chosen for signaling and detecting signals, and the laws of physics.
###### Bandwidth Terminology
1. **Latency**: Amount of time -including delays- for data to travel from a point to other
2. **Throughput**: Transfer of bits over a given period of time
	- Throughput is usually lower than the bandwidth because of these factors:
		  1. Amount of traffic
		  2. Type of traffic
		  3. Latency created by number of devices encounter betn. src. and dest.
3. **Goodput**: Usable data transferred over a given period of time
	- Goodput is Throughput minus Traffic overhead *establishing sessions, acknowledgments, encapsulation, retransmission*
---
- In Networks with multible segments, throughput cannot be faster than the slowest link in the path from src. to dest., even if all segments have high bandwidth a slow 
  *-for whatever the reason, legacy, config, etc.-* will create a bottleneck inthe entire network
---

## Copper Cabling

Data is transmitted on copeer cables as electrical pulses.
- Detector in the NIC of dest. must receive a signal that can be successfully decoded to match signal sent. However, the farther the signal travels, the more it deteriorates.
- Timing and Voltage values of those electrical pulses can be interfered from 2 sources
	  1. Electromagnetic interference EMI & Radio frequency interference: Can distort and corrupt data signals
	  2. Crosstalk: 
	     - Caused bu electric/magnetic field of a signal on an adjacent wire specially when electric current flows as it creates a small circular magnetic field.
	     - Can result in hearing part of another -for ex.- voice conversation of an adjacent circuit

#### Copper wire types
###### Unshielded twisted-pair *UTP*
- Consists of ==4 pairs== of color-coded wires twisted together  ==*+varying the number of twits per pair, each color has a different number*== then encased in a flexible ==plastic sheath== that protects minor physical damage
- The most common networkin media
- Terminated with RJ-35 connectors
- Used betn. hosts and intermediary networking devices *switches & routers*
---
###### shielded twisted-pair *STP*
- Consists of ==4 pairs== of color-coded wires, each pair twisted and wrapped in a ==foil== shield then the 4 pairs combined are wrapped in an overall metallic ==foil== braid
- That ==shield can backfire== may act as an antenna to pick up unwanted signals if grounded improperly 
- The most common networkin media
- Terminated with RJ-35 connectors
- Used betn. hosts and intermediary networking devices *switches & routers*
- ==More expensive and difficult to install==
---
###### Coaxial
- Consists of copper conductor that is covered and insulated by a flexible plastic layer, the insulating layer is surrounded then by a woven copper braid or metallic foil *-acting as a sheild and an interference preventor-* then the entire cable is covered with a cable jacket to prevent minor damages
- Has different types of connectors as BNC, N type, F type
- UTP replaces Coaxial but it is used in some situations:
	- **Wireless installations** by attaching antennas as it carries radio frequency energy between antennas and radio equipment
	- **Cable internet installations** by replacing portions of coaxial and supporting amplification elements with fiber-optic cable. still named Coaxial tho.
---

| Criteria\Type | Copper                                                                                                                                                                                                                       | Fiber-optic | Wireless |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | -------- |
| Pros          | - Inexpensive<br>- Easy to install<br>- Low electric resistance                                                                                                                                                              |             |          |
| Cons          | - Signal Attenuation: Deteriorate with distance<br>- Interference by EMI & RMI * *1*<br>- Crosstalk by Electical/Magnetic fields * *2*                                                                                       |             |          |
| Notes         | *1.* Some Copper wires are wrapped in metallic shielding and require proper ground connection to **counter EMI & RFI**<br>*2.* Some Copper wires have opposing circuit wire, pairs twisted together to **counter Crosstalk** |             |          |

