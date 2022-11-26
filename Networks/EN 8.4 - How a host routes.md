>Chapter - [[EN 8.0 - Network Layer]]

Sep 27, 2022
Topics - 

# Host Forwarding Decision
Host can send a packet to
1. <u>Itself</u>
	- to address `127.0.0.1` or `::1` i.e. the ***loopback address***
	- used to test the TCP/IP protocol stack on the host
2. <u>Local Host</u>
	- destination host is in the same network
	- both source and destination host share the same network address
3. <u>Remote Host</u>
	- destination host on remote network
	- network addresses of source and destination hosts are different

>[!NOTE]
>Network address = (IP address) && (Subnet Mask)

![[Pasted image 20221126183444.png]]

Determining whether packet is destined for <u>local host</u> or <u>remote host</u>
| IP version | method                                                                                             |
| ---------- | -------------------------------------------------------------------------------------------------- |
| in IPv4    | source device uses its subnet mask with its own <u>IPv4 address</u> and <u>destination address</u> |
| in IPv6    | local router advertises the local network address (prefix) to all devices on the network           |

---
# Default Gateway
- network device (router or Layer 3 switch) that can route traffic to other networks
- <u>has a local IP address</u> in the same address range as other hosts on the local network
- can accept data into the local network and <u>forward data out of the local network</u>
- routes traffic to other networks

>[!NOTE]
>if default gateway is down, traffic cannot be routed out of the local network

---
# A host routes to the default gateway
- default gateway IP address can be configured either manually, or dynamically via DHCP
- having a default gateway configured creates a <u>default route</u> in the <u>routing table</u> of the PC
- default route is the path taken when a host tries to contact (send or receive from) a remote network

---
# Host Routing Tables
- Routing table contains a list of all known network addresses (prefixes) and where to forward the packet
- these entries are called <u>route entries</u> or <u>routes</u>
- On windows, the command `route print` or `netstat -r` is used to display host <u>routing table</u>
- three sections are displayed in this command
	1. interface list
		- lists the MAC address and assigned interface number of all interfaces on the host
		- includes ethernet, wifi, bluetooth adapters
	2. IPv4 Route Table
		- lists all known IPv4 routes
		- includes direct connections, local network and local default routes
	3. IPv6 Route Table
		- same thing, just for IPv6 

