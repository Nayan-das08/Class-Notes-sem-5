>Chapter - [[EN 7.0 - Ethernet Switching]]

Nov 25, 2022
Topics - 

# Ethernet MAC Address
- used to identify physical source and destination devices on the local network segment
- it is a **48 bit address** 
	- 12 hex digits
![[Pasted image 20221125235351.png]]

## Organizationally Unique Identifier (OUI)
- all MAC addresses are unique
- devices registered with IEEE to obtain a **24-bit or 3-byte** unique hex code called OUI
- vendor assigns first 6 hex digits as the OUI
- unique value in the last 6 hex digits

>[!NOTE]
>- for new MAC address, we need new NIC, or can make modifications via software
>- MAC Address also referred to as a **burned-in address**
>- address is hard coded into ROM on the NIC

---
# Unicast MAC Address
- different Layer 2 address for unicast, broadcast and multicast communications

![[Pasted image 20221125235856.png]]

## finding destination MAC address using IP addresses
| IP address version | Process name                      |
| ------------------ | --------------------------------- |
| IPv4               | Address Resolution Protocol (ARP) |
| IPv6               | Neighbour Discovery (ND)          | 

---
# Broadcast MAC Address
- ethernet broadcast frame is received and processed by every device on the ethernet LAN
- destination MAC address = FF-FF-FF-FF-FF-FF
- sent out to all switch ports except the incoming port
- **NOT FORWARDED BY A ROUTER**

![[Pasted image 20221126003514.png]]
The destination IPv4 address in the Packet PDU is the broadcast address for the network

>[!NOTE]
>- DHCP for IPv4 uses IPv4 broadcast address
>- ARP Requests do not use IPv4, but the ARP message is sent as an Ethernet broadcast

---
# Multicast MAC Address
- a multicast frame is received and processed by a group of devices on the LAN that belong to the same multicast group
- Features of Ethernet multicast
	- destination MAC Address when encapsulated data is IPv4 multicast packet - **01-00-5E**
	- destination MAC Address when encapsulated data is IPv6 multicast packet - **33-33**
	- other reserved multicast destination MAC addresses when encapsulated data is not IP, such as 
		- Spanning Tree Protocol (STP)
		- Discovery Protocol (LLDP)
	- flooded out on all switch ports except incoming port
	- **NOT FORWARDED BY A ROUTER**, unless configured
	- if encapsulated IP packet is a **multicast packet**, the devices that belong to a multicast group are assign a multicast group IP address
	- IPv4 multicast address range - `224.0.0.0` to `255.255.255.255`
	- IPv6 multicast address range - ff00::/8

![[Pasted image 20221126005011.png]]
