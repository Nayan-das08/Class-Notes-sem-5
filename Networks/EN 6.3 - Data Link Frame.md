>Chapter - [[EN 6.0 - Data Link Layer]]

Sep 5, 2022
Topics - 

# Frame
has 3 basic parts
- header
- data
- trailer

---
# Frame Fields

![[Pasted image 20221125201109.png]]

| fields               | function                                                     |
| -------------------- | ------------------------------------------------------------ |
| frame start and stop | identify beginning and end limits of frame                   |
| addressing           | holds source and destination addresses of nodes in the media |
| type                 | identifies **layer 3** protocols being used                  |
| control              | identifies special services (like VoIP, etc.)                |
| Data                 | frame payload (packet header, segment header, data)          |
| error detection      | included after data to form the trailer                      |

## error detection
- determines if the frame arrived without any error
- places a logical or mathematical summary of frame bits in the trailer
- any interference or distortion or loss would substantially change the bit values
- logical summary - **cyclic redundancy check** (CRC) value
- placed in **frame check sequence** (FCS) field in trailer, represents the contents of the frame

---
# Layer 2 Address

- address at this layer is called ***physical address***
- placed in beginning of the frame so that an NIC can check if it matches its own Layer 2 address (MAC Address)
- These address do not indicate on what network the device is located (unlike Layer 3 addresses)

![[Pasted image 20221125202831.png]]
![[Pasted image 20221125202851.png]]
![[Pasted image 20221125202905.png]]

- Layer 2 addresses are used only for local delivery
- no meaning beyond local network
- for inter-network transmission we need an intermediary device such as a **router**.
	- when it receives a frame, it de-encapsulates it to examine Layer 3 address
	- using this router can determine the network location of destination device
	- router creates a new frame and sends it to the next network segment

---
# LAN and WAN frames
WANS traditionally used 
- Point-to-Point Protocol (PPP)
- High-Level Data Link Control (HDLC)
- Frame Relay
- Asynchronous Transfer Mode (ATM)
- X.25

These are replaced by Ethernet protocols
- Ethernet
- 802.11 Wireless
- Point-to-Point Protocol (PPP)
- High-Level Data Link Control (HDLC)
- Frame Relay

## Layer 2 protocols functions
- In a TCP/IP network Layer 2 protocols used depends on the logical topology and the physical media
- the Layer 2 protocol used for a particular network topology is determined by the technology used to implement the topology (which is determined by the size of network, number of hosts, physical scope, types of services provided, etc.)

![[Pasted image 20221125212657.png]]
![[Pasted image 20221125212713.png]]
![[Pasted image 20221125212729.png]]
![[Pasted image 20221125212744.png]]
![[Pasted image 20221125212806.png]]
