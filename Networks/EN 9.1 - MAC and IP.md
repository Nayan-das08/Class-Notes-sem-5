>Chapter - [[EN 9.0 - Address Resolution]]

Oct 10, 2022
Topics - 

# Destination on same network
Address resolution is used to determine the MAC address using IPv4 address[^1]

a device has two addresses
- <u>physical address</u> - MAC Address
	- used for NIC to NIC communication on same ethernet network
- <u>logical address</u> - IP address
	- used to send packet from source host to destination host
	- destination host may or may not be on same network

![[Pasted image 20221126224513.png]]

---
# Destination on Remote Network
when destination IP address is on a remote network, we use host default gateway (router interface) as the destination MAC address

![[Pasted image 20221126224658.png]]

- the router will examine the destination IPv4 address to determine the best path to forward the packet
- after deciding where the next hop will be, the router re-encapsulates the packet into a frame for outgoing interface

![[Pasted image 20221126224916.png]]

- new destination MAC address would be of R2 G0/0/1 interface (determined from routing table)

![[Pasted image 20221126225109.png]]






---
[^1]: [[EN 7.2 - Ethernet MAC Address#finding destination MAC address using IP addresses]]