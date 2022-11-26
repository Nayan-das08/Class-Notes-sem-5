>Chapter - [[EN 8.0 - Network Layer]]

Nov 26, 2022
Topics - 

# Router Packet Forwarding Decision
When a packet arrives on a router interface
- router examines the destination IP address of the packet
- searches its routing table to determine where to forward
- router will forward the packet using best (longest) matching route entry

![[Pasted image 20221126190213.png]]
![[Pasted image 20221126190300.png]]

the router notices in the router table that for the best matching route entry (10.1.1.0/24) we need to forward the packet to R2

---
# IP Router Routing Table
Routing table has three types of route entries
1. <u>Directly connected networks</u>
	- active router interfaces
	- routers add a *directly connected route* when an interface is configured with an IP address and is activated
	- each router interface is connected to a different network segment
2. <u>remote networks</u>
	- entries connected to other routers
	- routers learn about remote networks by 
		- being explicitly configured by admin
		- exchanging route info using dynamic routing protocol
3. <u>default route</u>
	- used when there is no better (longer) match in the IP routing table

![[Pasted image 20221126201706.png]]
here the default route in R1 IPv4 routing table would be R2

Router can learn about remote networks in two ways
1. Manually - remote networks entered into the route table using **static routes**
2. Dynamically - Remote routes are automatically learned using **dynamic routing protocol**

---
# Static Routing
route entries that are manually configured

![[Pasted image 20221126201958.png]]

this instructs the router to forward packets to R2 if their destination IPv4 address is of the remote network 10.1.1.0/24

![[Pasted image 20221126202221.png]]

static route is appropriate for a small network and when there are few or no redundant links

---
# Dynamic Routing
dynamic routing protocols include <u>OSPF</u> and Enhanced Interior Gateway Routing Protocol <u>(EIGRP)</u> 

![[Pasted image 20221126203208.png]]

dynamic routing protocol can
- discover remote networks
- maintain up-to-date routing info
- choose the best path to destination network
- find new path if old path is no longer available

![[Pasted image 20221126203400.png]]

>[!NOTE]
>it is common for some routers to use combination of static and dynamic routing protocols

---
# IPv4 Routing Table

![[Pasted image 20221126203517.png]]

R2 connected to internet. Hence, in R1 we have configured a default route to R2 for when there is no specific entry in routing table for the destination IP address

`show ip route` command shows IPv4 routing table on a Cisco IOS router

common route sources include

| code | description                                   |
| ---- | --------------------------------------------- |
| L    | directly connected local interface ip address |
| C    | directly connected network                    |
| S    | static route                                  |
| O    | OSPF                                          |
| D    | EIGRP                                         |

directly connected routes automatically added when IP address is configured and router is activated. Thus R1 learns about networks <u>192.168.10.0</u>/24 and <u>209.165.200.224</u>/30 

R1 and R2 also learn about remote networks using OSPF protocol. Thus R1 learns about <u>10.1.1.0</u>/24 as well from R2

Static route is denoted with S* and here it is set to R2 (209.165.200.226) for 0.0.0.0, i.e. for a network which does not match at all

