>Chapter - [[EN 7.0 - Ethernet Switching]]

Nov 25, 2022
Topics - 

# Ethernet Encapsulation
- Ethernet operates in Data Link layer and Physical layer
- family of networking technologies defined in the IEEE 802.2 and 802.3 standards
- supports bandwidths of
	- 10 Mbps
	- 100 Mbps
	- 1000 Mbps (1 Gbps)
	- 10,000 Mbps (10 Gbps)
	- 40,000 Mbps (40 Gbps)
	- 100,000 Mbps (100 Gbps)
![[Pasted image 20221125214453.png]]

>[!NOTE]
>Ethernet defined by data link and physical layer protocols

---
# Data Link Sublayers
read from [[EN 6.1 - Purpose of Data Link Layer#IEEE 802 LAN/MAN Data Link sublayers|EN 6.1 - Purpose of Data Link Layer]]

---
# MAC Sublayer
responsible for data encapsulation and accessing the media

Data encapsulation includes
- ethernet frame
	- the PDU
- ethernet addressing
	- Layer 2 address of source and destination NICs
- ethernet error detection
	- [[EN 6.3 - Data Link Frame#error detection|frame check sequence (FCS)]] 

![[Pasted image 20221125215257.png]]

>[!NOTE]
>modern ethernets using switches work on [[EN 6.2 - Topologies#Full duplex|Full Duplex Mode]]

---
# Ethernet Frame Fields
- minimum ethernet frame size = 64 bytes
- expected max = 1518 bytes
- from destination MAC address field through FCS field
- any frame less than 64 bytes in length is considered a *collision fragment* or a *runt frame* and is discarded by receiving device
- frames of more than 1500 bytes are considered *jumbo* or *baby giant frames*
- dropped frames are likely to be the result of collisions or other unwanted signals
- these are considered invalid
- jumbo frames supported by most Fast Ethernet and Gigabit Ethernet switches and NICs

![[Pasted image 20221125220031.png]]

| field                                     | function                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Preamble and Start Frame Delimiter Fields | The Preamble (7 bytes) and Start Frame Delimiter (SFD), also called the Start of Frame (1 byte), fields are used for synchronization between the sending and receiving devices. These first eight bytes of the frame are used to get the attention of the receiving nodes. Essentially, the first few bytes tell the receivers to get ready to receive a new frame                                                                                                                                                                                                  |
| Destination MAC Address Field             | This 6-byte field is the identifier for the intended recipient. As you will recall, this address is used by Layer 2 to assist devices in determining if a frame is addressed to them. The address in the frame is compared to the MAC address in the device. If there is a match, the device accepts the frame. Can be a unicast, multicast or broadcast address.                                                                                                                                                                                                   |
| Source MAC Address Field                  | This 6-byte field identifies the originating NIC or interface of the frame.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| Type / Length                             | This 2-byte field identifies the upper layer protocol encapsulated in the Ethernet frame. Common values are, in hexadecimal, 0x800 for IPv4, 0x86DD for IPv6 and 0x806 for ARP.                                                                                                                                                                                                                                                                                                                                                                                     |
| Data Field                                | This field (46 - 1500 bytes) contains the encapsulated data from a higher layer, which is a generic Layer 3 PDU, or more commonly, an IPv4 packet. All frames must be at least 64 bytes long. If a small packet is encapsulated, additional bits called a pad are used to increase the size of the frame to this minimum size.                                                                                                                                                                                                                                      |
| Frame Check Sequence Field                | The Frame Check Sequence (FCS) field (4 bytes) is used to detect errors in a frame. It uses a cyclic redundancy check (CRC). The sending device includes the results of a CRC in the FCS field of the frame. The receiving device receives the frame and generates a CRC to look for errors. If the calculations match, no error occurred. Calculations that do not match are an indication that the data has changed; therefore, the frame is dropped. A change in the data could be the result of a disruption of the electrical signals that represent the bits. |

