>Chapter - [[EN 7.0 - Ethernet Switching]]

#incomplete 
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

---
[^1]: [[EN 7.1 - Ethernet Frames#Ethernet Frame Fields]]