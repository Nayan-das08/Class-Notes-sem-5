>Chapter - [[EN 3.0 - Protocols and Models]]

Aug 20, 2022
Topics - 

# Segmenting data
- data can be sent from sender to receiver in one uninterrupted stream of bits over the channel, but that is not feasible
- by doing so, we limit the usage of the particular connection/link to a particular transmission
- the transmission would be slow
- in case of any failure in network infrastructure, complete message will be lost

## Better Approach
- divide the data into smaller segments/pieces/packets before sending
- This process is called ***SEGMENTATION*** 
- These packets sent can be received from different paths, thus not dedicating a single link
- results in increased speed, efficiency reliability

---
# Sequencing
- segmenting adds complexity to the process
- **problem** - order of segments/packets
- **solution** - Protocol data units
	- holds meta data about packets

---
# Protocol Data Units
- **Encapsulation process** - as info is passed down from each layer of the network link, information gets added to the packet
- PDU - The piece of data which acts as metadata for each layer
- These are set as per the protocols used at each layer
- These have different names at different layers

![[Pasted image 20220828232940.png]]

| PDU     | Layer          |
| ------- | -------------- |
| Data    | Application    |
| Segment | Transport      |
| Packet  | Network        |
| Frame   | Data link      |
| Bits    | Physical Layer | 

![[Pasted image 20220828233232.png]]

>[!NOTE]
>Frame create a header and a trailer while the rest don't


>[!NOTE]
>encapsulation works in a top-down approach
>de-encapsulation works in a bottom-up approach

