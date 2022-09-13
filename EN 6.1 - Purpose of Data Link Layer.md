>Chapter - [[EN 6.0 - Data Link Layer]]

#Unlinked 
#incomplete 
Aug 31, 2022
Topics - 

# Data link layer purpose
- NIC to NIC connection
- allows upper layer protocols to access the physical layer media/channel  
- encapsulates layer 3 packets (IP address of source and final destination) into layer 2 frames
- controls how data is placed on physical media
- error detection and rejects corrupted frames (CRC method)

---
# IEEE 802 LAN/MAN Data Link sublayers
- these standards are specific to ethernet LANs, WLANs, WPANs and other MANs
- there are two sublayers :-

## LLC (Logical Link Control) Sublayer
- communicates between networking software at the upper layers and device at lower levels
- places info regarding the layer 3 protocols in the frame 
- thus layer 3 protocols - IPv4, IPv6, etc. can use the same network interface and the network media/channel

## MAC (Media Access Control) Sublayer
- implements IEEE 802.3, 802.11, 802.15 in hardware
- responsible for data encapsulation and ***media access control***
- responsibilities shared between Data link layer and physical layer
- controls the NIC and other hardware for transmission
- provides data encapsulation for
	- **frame delimiting**
		- provides delimiters to identify fields within a frame
		- provides synchronization between nodes
	- **Addressing**
		- [[EN 3.6 - data access|layer 2 addresses]] for source and destination NICs
	- **error detection**
		- includes a trailer to detect transmission errors
- provides media access control, thus allowing multiple devices to communicate over a shared (half-duplex) channel

>[!NOTE]
>full duplex communication does not require medium access control

![[Pasted image 20220912225202.png]]

---
# Providing access to media
at each hop (from one NIC to another) the router performs these ***Lyer 2 tasks***
1. accept the frame from a medium
2. de-encapsulate the frame
3. re-encapsulate the packet into a new frame
4. forward the new frame on appropriate medium to the next device

The Frame PDUs (header and trailer) change as per the medium being used

---
# Data link layer standards
- Data link protocols are not defined by RFC unlike upper layer protocols of TCP/IP suite
- IETF doesn't define the functions and operations of Network Access Layer ([[EN 3.4 - layered models (OSI and TCP-IP)]])

>[!RFC - Request For Comments]
>- a formal document drafted by IETF ([[EN 3.7 - standard org]])
>- describes the specifications for some tech
>- example: FTP protocol was ratified as RFC 114 in April 1971, later replaced by RFC 765 in 1980 and then again by RFC 959 


The protocols for Network Access Layer are :-
- IEEE
- ITU
- ISO
- ANSI