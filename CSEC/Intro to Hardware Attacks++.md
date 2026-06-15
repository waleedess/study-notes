
Tier: Tier 0
Finished: No
Source: HTB
Status: Learning

# **Introduction to Bluetooth**

- The technology operates by establishing personal area networks (PANs) using radio frequencies in the Industrial, Scientific, Medical (ISM) band from (121mm)/2.402 GHz to (124mm)/2.480 GHz. Conceived as a wireless alternative to RS-232 data cables
    - Of Electromagnetic waves that travels -not in one direction- but in all direction and
    - Causing an Electrical Field and Magnetic Field
    - That wave length gives the info about frequency and length of that wave
    - That range 2.4 : 2.4835GHZ is split to 79 different channel with each having its specific wavelength for 1 and 0 within its individual channel range
        - Each communication only go through 1 channel at a time but hops between the 79 channels with a 1600hops/sec and for each hop it sends 1 full packet
        - The master device does not send the sequence outright as a list. Instead, both devices calculate the exact same pseudo-random sequence mathematically. They use the master device's MAC address and internal clock as the seed for the algorithm. Because they share the same seed, they hop in perfect synchronization without needing to continuously transmit the roadmap
        - Each channel can handle more than 1 communication as each communication is differentiated and synchronized by each 2 devices communicating by the access code located in the first 72bits of the packet then a 54bit header then a 136 : 8168 bits of payload, also it has a “i didn't receive this packet” TCP-like thing sent by receiver to sender to send the lost packet again
        - The basic 1,600 hops/sec mechanism works great, but what happens if a local Wi-Fi network is completely dominating Channels 20 through 30? Under pure random hopping, Bluetooth would still blindly hop into those jammed channels 
        To fix this, modern Bluetooth uses **Adaptive Frequency Hopping (AFH)**.
        During operation, the devices constantly monitor the signal-to-noise ratio and packet loss on every channel. If they notice that certain channels are consistently dropping packets due to interference, the master builds a **Channel Map**. It marks those congested frequencies as "bad" and shares this map with the receiver.
        The algorithm then dynamically adapts: when the math dictates a hop to a "bad" channel, it automatically remaps that hop to a known "good" channel instead.
        From a security perspective, this hopping makes capturing Bluetooth traffic mid-air incredibly difficult without specialized, expensive hardware that can sniff all 79 channels simultaneously.
    - The transition between frequencies is called Frequency Shift Keying to 0 and 1
        - Also there is a Carrier wave undergo Frequency modulation which that is shifted to a higher frequency when it wants to send a 1, and to lower for a zero

### Pairing

This involves two devices `discovering` each other and establishing a connection Through these phases:

1. `Discovery`: One device makes itself `discoverable`, broadcasting its presence to other Bluetooth devices within range. →
Slave enter a state called `INQUIRY SCAN`. The device listens on a specific subset of 32 dedicated "wake-up" channels. Every few seconds, it broadcasts an **EIR (Extended Inquiry Response)** packet. This packet contains its MAC address, its clock profile, its device class (e.g., audio device), and its human-readable name.
Master enters the `INQUIRY` state. It rapidly blasts out inquiries across those same wake-up channels, asking, *"Is anyone out there?"* Once your phone catches the earbuds' EIR packet, the earbuds appear on your screen.
2. `The Handshake` : Searcher enters PAGE state and targets the specific MAC it found in discovery and the other device enters PAGE SCAN state
→ This is the exact moment the master transmits its clock profile and the slave adjust its internal native clock to match the master’s to start synzing the hopping
3. `Pairing & Authentication` : 
    1. Step a: Before the devices exchange any security data, they need to know how they can interact with the human user. They exchange a quick packet stating their **Input/Output (IO) capabilities**
    2. Step b: The devices must create an encrypted tunnel before doing anything else. They use an algorithm called **ECDH (Elliptic Curve Diffie-Hellman).** Both devices generate a temporary pair of cryptographic keys: a **Private Key** (kept secret) and a **Public Key** (shared openly)
    3. Step c: Now that the tunnel is encrypted, the devices must prove they are actually talking to *each other* and that a hacker hasn't slipped into the middle of the connection. Depending on the IO capabilities from Step 1, they choose one of three flavors:
        1. Numeric Comparison
        2. Passkey Entry
        3. Automatic acceptance
    4. Once the authentication step is successful, the devices take that shared secret they made in Step 2 and convert it into a permanent cryptographic key called a **Link Key** (or **Long-Term Key** in Bluetooth Low Energy) and this key is saved directly into the secure hardware storage of both devices.

Once the devices are paired, they remember each other's details and can automatically connect in the future without needing to go through the pairing process again.

### Piconet

A **Piconet** is the fundamental building block of Bluetooth networking. The moment a connection is established, an automatic hierarchy is created.

- Every piconet can have **only one** Main device. As you noted, it completely coordinates the communication. Returning to our discussion on the hopping sequence, the Main device is the one that provides its **MAC address** and **internal clock** to serve as the blueprint for the entire network. Every other device in the piconet must synchronize its clock to this Main device to know what channel to hop to next.
    - Clients never talk directly to each other; they only talk to the Main device. If Client A wants to send data to Client B, it must send it to the Main device first, which then routes it to Client B
    - In the Bluetooth packet header, there is a 3-bit field reserved for the "Active Member Address" (Logical Transport Address or LT_ADDR). Mathematically, 3 bits give you 2^3 = 8 possible combinations. Since address `000` is reserved for broadcasting messages to the entire network, that leaves exactly 7 unique addresses (`001` through `111`) to assign to active clients.
- A piconet can actually have up to 255 additional devices connected, but they must be placed in a **"Parked" or "Idle" state**. They give up their active 3-bit address, stop transmitting, and simply listen to the Main device's clock beacon until the Main device tells them to wake up and swap places with an active client.

### Scatternet

When you need to scale beyond 8 total devices, or connect distinct groups, piconets combine to form a **Scatternet**.
This configuration relies entirely on **Bridge Devices**. A bridge is a single piece of hardware that simultaneously participates in more than one piconet.

- A single radio chip cannot physically choose two different hopping sequences at the exact same microsecond. Therefore, a bridge device works by **time-multiplexing (time-sharing)**:
    1. For a few time slots, the bridge adjusts its clock to match *Piconet A* and acts as a client, receiving data from Piconet A's Main device.
    2. Then instantly caches that data, hops its radio clock over to match *Piconet B*, and transmits the data to Piconet B.
- A device can **never** be the Main device for two different piconets. If it tried, both piconets would share the exact same MAC address and clock seed, causing their hopping sequences to collide entirely, destroying the separate networks.
    - **Allowed Configurations:**
        - Client / Client Bridge: A device can be a client in Piconet A and a client in Piconet B
        - Main / Client Bridge: A device can be the Main coordinator of Piconet A, but only a client in Piconet B

### Linking Types

The primary device in the piconet dictates the schedule for packet transmission. The Bluetooth specification identifies two types of links for data transfer:

#### Synchronous Connection-Oriented (SCO) links

Primarily used for audio communication, these links *No matter how crowded the room gets* reserve slots at regular intervals for data transmission, guaranteeing steady, uninterrupted communication ideal for audio data

- SCO establishes a permanent, symmetric circuit between the Main device and a specific client. It locks down regular, repeating time slots.
- If a radio glitch hits an SCO slot and a packet gets corrupted, Bluetooth usually won't try to retransmit it.
- Maximum Priority
- Fixed Packet Size

#### Asynchronous Connection-Less (ACL) links

These links cater to transmitting all other types of data. Unlike SCO links, ACL links do not reserve slots but transmit data whenever bandwidth allows.

- ACL links use whatever bandwidth is left over after the SCO audio links have taken their reserved shares. If the network is idle, an ACL transfer can take up almost all the slots, even combining multiple slots together to blast a huge chunk of data at once.
- Unlike SCO, ACL links use the **retransmission system (ARQ)** we talked about earlier. If a packet of a file gets lost or corrupted, the receiver yells, the sender keeps retrying until it lands perfectly.
- Low Priority
- Dynamic Packet Size

# Risks of Bluetooth

risk can be defined as any potential event that exploits the Bluetooth connection to `compromise` data or systems' `confidentiality`, `integrity`, or `availability`. Bluetooth risks often emanate from the wireless nature of the technology that allows for `remote, unauthorised access` to a device

#### Unauthorized Access

Unauthorized entities gaining unsolicited access to Bluetooth-enabled devices. Attackers can exploit vulnerabilities to take control of the device or eavesdrop on data exchanges

#### Data Theft

Bluetooth-enabled devices store and transmit vast amounts of personal and sensitive data that may include: contact lists, messages, passwords, financial details, or other confidential data

#### Interference

Disrupt or corrupt Bluetooth communication *the 2.4 GHz band*. Intentional interference can lead to data loss, connection instability, or other disruptions in device functionality

#### Denial of Service

Overwhelming with an excessive volume of requests or by exploiting vulnerabilities in Bluetooth protocols. This can result in the targeted device becoming unresponsive, rendering it unable to perform its intended functions

#### Device Tracking

Bluetooth technology relies on radio signals to establish connections between devices. Attackers can exploit this characteristic to track the physical location of Bluetooth-enabled devices

# **Bluetooth Attacks**

Bluetooth attacks have been identified, each with its unique characteristics and potential risks.

#### Bluejacking

Relatively harmless type of Bluetooth hacking where an attacker `sends unsolicited messages` or business cards to a device. Although it doesn't pose a direct threat, it can infringe on privacy and be a nuisance to the device owner.

- Bluejacking relies on a legitimate protocol within the Bluetooth suite called **OBEX (Object Exchange)**. OBEX was designed to let devices easily swap files, calendar events, and electronic business cards (**vCards**) without needing a complicated pairing handshake *before a formal pairing link key is created*. Bluejacking is executed using these steps:
    1. **The Scan:** The attacker goes to a crowded public space (like an airport or a university campus) and sets their phone to search for nearby Bluetooth devices. They are looking for any device currently in the `INQUIRY SCAN` (discoverable) state.
    2. **The Tricked Contact:** Instead of creating a regular contact file with their real name, the attacker creates a new contact on their phone and types a message into the "Name" field (for example: *"Look behind you, you've been bluejacked!"* or *"Your shoes are untied"*).
    3. **The Push:** The attacker selects that contact and hits "Send via Bluetooth" to a discovered device.

#### Bluesnarfing

 Entails `unauthorised access to a Bluetooth-enabled device's data`, such as contacts, messages, or calendar entries. Attackers exploit vulnerabilities to retrieve sensitive information without the device owner's knowledge or consent. This could lead to privacy violations and potential misuse of personal data.

- Just like Bluejacking, Bluesnarfing exploits the **OBEX (Object Exchange)** protocol. However, it specifically targets a massive oversight in how older Bluetooth firmware implemented the **IrMC (Infrared Mobile Communications)** synchronization service. IrMC service port is completely open and accessible *before* the device required any authentication or pairing to sync calendars and contact lists with mobile phones easily in **Old Bluetooth versions**. Bluesnarfing attack follows this workflow:
    1. **Targeting an Open Port:** The attacker uses a specialized Bluetooth scanning tool (like `hciconfig` and `hcitool` in Kali Linux) to find a target device.
    2. **Service Discovery:** They run a Service Discovery Protocol (SDP) search on the target's MAC address to map out its open channels. They are specifically looking for the RFCOMM channel running the OBEX/IrMC sync service.
    3. **Bypassing the Lock:** Instead of initiating a standard pairing request (which would trigger a PIN popup on your screen), the attacker forces a raw connection directly to that specific unauthenticated channel.
    4. **The Data Pull:** Once connected, the attacker sends standard **OBEX GET requests** or legacy AT commands (the same commands used to control old modems). The vulnerable Bluetooth chip simply obeys the command, treating the hacker like a trusted backup software, and starts dumping files over the air.