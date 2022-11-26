>Chapter - [[EN 8.0 - Network Layer]]

Sep 14, 2022
Topics - 

# Network Layer
- IPv4 and IPv6 are the principle Layer 3 protocols
- Other protocols are :-
	- routing protocol - <u>Open Shortest Path First (OSPF)</u>
	- messaging protocol - <u>Internet Control Message Protocol (ICMP)</u>
- Layer 3 has four basic operations
	1. <u>Addressing end devices</u>
		- configuring end-devices with unique IP address for identification on the network
	2. <u>Encapsulation</u>
		- network layer encapsulates PDU from transport layer into a ***packet***
		- the process adds IP header info - IP address of source and destination
		- performed by source host
	3. <u>Routing</u>
		- direct the packets to a destination on <u>another network</u> 
		- packet must be processed by a router
		- routing - router selects the best path and directs the packets towards destination host
		- packet may cross many router to reach destination
		- each router a packet crosses to reach destination host is a ***hop***
	4. <u>De-encapsulation</u>
		- when packet arrives at destination host its IP address is checked with the host IP address
		- if it matches the IP header is removed from the packet
		- this is called de-encapsulation at Network Layer
		- the resulting PDU (transport layer segment) is passed to upper layer for further processing

![[Pasted image 20221126142542.png]]
![[Pasted image 20221126142718.png]]
![[Pasted image 20221126142734.png]]
![[Pasted image 20221126142801.png]]
![[Pasted image 20221126142818.png]]
![[Pasted image 20221126142836.png]]
![[Pasted image 20221126142850.png]]
![[Pasted image 20221126151058.png]]
![[Pasted image 20221126151306.png]]
![[Pasted image 20221126151320.png]]
![[Pasted image 20221126151332.png]]

---
# IP Encapsulation
- encapsulates transport layer segment by adding <u>IP header</u>
- IP header used to deliver packet to destination host
![[Pasted image 20221126151523.png]]

>[!NOTE]
>- Layer 3 device = routers and layer 3 switches
>- Layer 3 switches different from Layer 2 switches, not in syllabus, so no need to worry about it just mention and get tf out of there

IP address info (source and destination addresses) remain same in the packet throughout the journey from source host to destination host except when translated by a device performing Network Address Translation (NAT) for IPv4

--- 
# Characteristics of IP
- protocol with low overhead
- provides only the functions necessary to deliver a packet from source to a destination over a network
- NOT designed to track and manage the flow of packet
	- these are performed by other protocols at other layer (TCP at Layer 4)
- basic characteristics
	1. **Connectionless**
		- no dedicated end-to-end connection established before sending data
		- similar to sending a letter
	2. **Best Effort**
		- unreliable as no guarantee is provided
		- tho it reduces overhead
	3. **Media Independent**
		- works on any medium / channel

---
