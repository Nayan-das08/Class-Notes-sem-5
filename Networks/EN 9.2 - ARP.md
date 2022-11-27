>Chapter - [[EN 9.0 - Address Resolution]]

Nov 26, 2022
Topics - 

# ARP Overview
- ARP maps IPv4 to MAC addresses for hosts
- To send a packet to another host in the same network segment, destination host MAC address must be known
- this is because Layer 2 ethernet switches use Layer 2 MAC addresses to make forwarding decisions
- ARP has two functions
	- resolving IPv4 addresses to MAC addresses
	- maintaining a table of IPv4 to MAC addresses

>[!NOTE]
>- ARP tables map a Layer 3 address to a Layer 2 address configuration
>- MAC tables map a Layer 2 address to a Layer 1 (physical layer) interface

---
# ARP functions
- when a packet is sent to data link layer to be encapsulated into a frame, device refers to a table in memory to find MAC address for destination IP address host
- this table is called ***ARP Table/Cache***
- stored temporarily in RAM
- how to search 
	- if destination IPv4 address of same local network, search for the device IPv4 address in ARP table, the map to its MAC address
	- if destination IPv4 address of remote network, search for default gateway IPv4 address in ARP table, the map to its MAC address
- if no entry is found, then device sends an <u>ARP Request</u>

![[Pasted image 20221127204121.png]]
![[Pasted image 20221127204131.png]]
![[Pasted image 20221127204142.png]]
![[Pasted image 20221127204154.png]]
![[Pasted image 20221127204204.png]]

---
# ARP Request
- request is sent when a device needs to know the MAC address of a device but cannot find it in ARP table
- ARP message encapsulated in a frame
- no IPv4 header
- header info in ARP request frame
	- destination MAC address
	- source MAC address
	- Type
		- `0x806` value
		- informs receiving NIC that data/payload of this frame needs to be passed to ARP process of the receiver
- **ARP requests are BROADCAST**
- all NICs on LAN receive the ARP request and deliver it to its OS for processing
- **Router will not forward BROADCAST messages (including ARP requests)**

![[Pasted image 20221127205029.png]]

|                 | field                   | description                               |
| --------------- | ----------------------- | ----------------------------------------- |
| ethernet header | destination MAC address | set to broadcast address                  |
| ethernet header | source MAC address      | set as the MAC address of requesting host |
| ARP request     | target IPv4 address     |                                           |
| ARP request     | target MAC address      | the required field, sent empty            | 

---
# ARP Reply
- only the device with matching target IPv4 address sends the ARP reply
- encapsulated in a frame
- info in frame
	- destination MAC address
	- source MAC address
	- Type
		- `0x806` value
		- informs receiving NIC to treat data/payload part of frame as ARP process
- after reply is received, the IPv4 address and MAC address is appended in the ARP table
- packets that were needed to be sent, can now be sent since all info needed for transmission (destination MAC address) is known
- entries in ARP table are timestamped
- if a device does not receive a frame from a particular device before the timestamp expires, the entry for the device is removed
- static ARP table entries do not expire, they need to be removed manually

>[!NOTE]
>- IPv6 uses a similar method
>- known as [[EN 9.3 - IPv6 Neighbour Discovery|Neighbour Discovery (ND)]]

![[Pasted image 20221127205029.png]]

![[Pasted image 20221127210025.png]]

| ARP Reply               | ARP Request                           |
| ----------------------- | ------------------------------------- |
| destination MAC address | source MAC address                    |
| source MAC address      | the field required in the first place |
| sender IPv4 address     | target IPv4 address                   |
| sender MAC address      | the field required in the first place | 

---
# ARP Role in Remote communication
- for remote network communications, the ARP request will be sent with *target IPv4 address* as the the default gateway
	- it would still be a broadcast message
- the router interface will receive the ARP request frame, process it and then send a unicast message - ARP reply with default gateway MAC address as *target MAC address*
- this reply will be added to the ARP table
- the next time packets for remote network need to be sent to the default gateway, its MAC address will be known

---
# Removing entries from ARP table
- entries that haven't been used for a long time are removed
- in Windows, entries are stored for 15-45 seconds
- entries can be manually removed as well

---
# ARP tables on devices
- `show ip arp` command used to display ARP table
- on Windows, its `arp -a`

---
# ARP issues
## performance issues
- broadcast flooding of ARP request may impact performance of network *significantly* if large number of devices are connected
- once devices send out initial ARP broadcast requests and learn necessary MAC addresses, any impact on the network would be minimized

## security issues
- a *threat actor* can use <u>ARP spoofing</u>, sending falsified ARP message over LAN 

![[Pasted image 20221127212437.png]]

wrong MAC address would be added to the ARP table and the malicious user would receive packets that are not meant for them

Enterprise level switches use mitigation technique called <u>Dynamic ARP Inspection (DAI)</u>

---
