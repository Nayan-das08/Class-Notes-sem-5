>Chapter - [[EN 7.0 - Ethernet Switching]]

Nov 26, 2022
Topics - 

# Frame Forwarding methods
methods for switching data between network ports are :-
- <u>Store and forward switching</u>
	- receives the entire frame and computes the CRC
	- CRC uses a mathematical formula based on number of bits in the frame
	- CRC determines whether the received frame has an error
	- if CRC valid, switch looks up the destination address thus determining outgoing interface
	- the frame then can be forwarded out of the correct port
	- if CRC is invalid, the frame is dropped
	- this reduces the amount of bandwidth consumed by corrupt data
	- required for Quality of Service (QoS) analysis
- <u>Cut through switching</u>
	- acts upon the data as soon as it is received, even if the transmission is not complete
	- buffers just enough of frame to read the destination MAC address 
	- so that it can be determined quickly to which port it should forward out the data
	- destination MAC address present in the first 6 bytes of the frame following the preamble[^1]
	- no error checking on the frame here
	- two variants of cut through switching
		- <u>fast forward switching</u>
			- offers lowest level of latency
			- immediately forwards a packet after reading the destination address
			- since forwarded before entire packet has been received, the packets may sometimes be relayed with errors (infrequently tho)
		- <u>fragment free switching</u>
			- switch stores 64 bits of frame before forwarding
			- compromise between *store and forward switching* and *fast forward switching* 
			- most network errors and collisions occur during the first 64 bytes 
			- performs small error check on the first 64 bytes of the frame to ensure that a collision has not occurred before forwarding the frame

>[!NOTE]
>- some switches configured to perform cut-through for certain ports until a threshold on errors is reached
>- after that it is changed to store-and-manage switching till the error rate falls below the threshold

---
# Memory Buffering on Switches
- buffering technique used to store frames before forwarding them
- also used when the destination port is busy because of congestion
- two types of methods for storing / buffering

## Port-based memory 
- frames are stored in queues linked to specific incoming and outgoing ports
- a frame is transmitted to outgoing port ONLY when all the frames ahead in the queue have been transmitted
- delays possible for busy destination port

## Shared memory
- deposits frame to common memory buffer shared by all switch ports
- amount of memory required by a port is dynamically allocated
- frames in buffer dynamically linked to destination port
- this means a port can receive a packet and can be sent to another port without moving it to a different queue
- ability to store larger frames with potentially fewer frame drop
- helps in asymmetric switching where connection to a 10Gbps port (server) and 1Gbps port (PCs) can be handled smoothly

---
# Duplex and Speed Settings
- these are two basic settings of a switch
- these two should match between switch port and connected devices
- <u>Duplex Settings</u>[^2]
	1. Half duplex
	2. Full Duplex
- <u>Auto-negotiation</u>
	- optional feature on most switches and NICs
	- enables two devices to automatically negotiate best speeds and duplex settings
	- ***duplex settings***: Full duplex chosen if both devices have the capabilities
	- ***speed settings***: highest common speed is chosen
- <u>Duplex mismatch</u> is one of the most common causes of performance issues
	- the network will continually experience collisions 

![[Pasted image 20221126135654.png]]

---
# Auto-MDIX[^3]
connections between different devices needs either straight-through or crossover cable

| devices          | connection       |
| ---------------- | ---------------- |
| different device | straight-through |
| similar device   | crossover        |

![[Pasted image 20221126140215.png]]

- Most switches use/support ***Automatic Medium-Dependent Interface Crossover (Auto-MDIX) feature*** 
- switch automatically detects the type of cable attached to the port and configures accordingly

>[!NOTE]
>command to re-enable this feature = `mdix auto`


---
[^1]: [[EN 7.1 - Ethernet Frames#Ethernet Frame Fields]]
[^2]: [[EN 6.2 - Topologies#Half and Full Duplex Communication]]
[^3]: [[EN 4.4 - UTP#Straight-through & crossover UTP]]