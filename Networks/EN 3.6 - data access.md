>Chapter - [[EN 3.0 - Protocols and Models]]

Aug 22, 2022
Topics - 


# addresses
- network and data link layers responsible for delivering data from source to destination

| layer              | function                            |
| ------------------ | ----------------------------------- |
| physical           | timing/sync the bits                |
| data link          | dest. and source phys addesses      |
| network            | dest. and source logical addesses   |
| transport          | dest. and source process no (ports) |
| rest (upper)layers | encoding app data                   |

>[!NOTE]
>both **data link** and **network** layers have dest and source addresses
>but they have different purposes

| layer     | address function                         |
| --------- | ---------------------------------------- |
| network   | for original source to final destination |
| data link | for one NIC to another                   |

---

# layer 3 (network/internet) logical address
## **IP packet** (PDU name) contains 2 addresses
1. original source IP address
2. final destination IP address

![[Pasted image 20220822095218.png]]

## address has two parts
1. **network part/prefix** 
	- left most part of address -> network group
	- common for all the devices on the network
2. **host part/Interface ID** 
	- remaining part of address -> for host/specific device
	- unique for each device on the network

>[!NOTE]
>***subnet mask/prefix length*** is used to identify network part and host part in an address

---
# on the same net

>[!NOTE]
>The data link is sent directly to the receiver when the devices are on the same network

- on ethernet network, data link addresses are known as Ethernet ***Media Access Control (MAC) Address***
- these are physically embedded on Ethernet NIC


![[Pasted image 20220822095623.png]]

>[!NOTE]
>multiple intermediary devices can be present in same link

---
# on remote network
![[Pasted image 20220828235736.png]]

- The **network layer address** remain unchanged
- The **data link addresses** change as the data moves from one intermediary device to another

![[Pasted image 20220828235920.png]]

- L3 is the **layer 3 (network layer) logical address**
- L2 is the **layer 2 (data link) address** that keeps changing

1. from HOST to ROUTER
	- layer 3 address remains same
	- layer 2 address 
		- source: PC1
		- destination: Router1
2. from ROUTER to ROUTER
	- layer 3 address remains same
	- layer 2 address 
		- source: Router1
		- destination: Router2
3. from ROUTER to HOST
	- layer 3 address remains same
	- layer 2 address 
		- source: router2
		- destination: PC2

