>Chapter - [[EN 9.0 - Address Resolution]]

#incomplete 
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
