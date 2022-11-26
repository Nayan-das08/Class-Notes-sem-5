>Chapter - [[EN 8.0 - Network Layer]]

Nov 26, 2022
Topics - 

# IPv4 packets
purposes
- ensures packet is sent n the correct direction

---
# IPv4 packet header fields

![[Pasted image 20221126152642.png]]

## Version
- 4-bit value (set to 0100), identifies this as IPv4 packet

## Differentiated Service
- 8-bit value
- to determine priority of each packet
- 6 most significant bits - Differentiated Services Code Point (DSCP) bits
- last 2 bits - explicit congestion notification (ECN) bits

## TTL
- 8-bit value
- used to limit the lifetime of a packet
- source sets initial TTL value
- **decreased by one** after each hop
- when TTL zero, the packet is discarded and sends ICMP time exceeded message to source IP address
- since the value is changed after each hop, the Header checksum field is recalculated by router (similar to FCS in frames)

## Protocol
- 8-bit value
- identify next level protocol
- common values are
	- 1 - ICMP
	- 6 - TCP
	- 17 - UDP

## Header Checksum
- used to detect corruption of IPv4 header and validate the packet
- used along with another field called Internet Header Length (IHL)

## Source IPv4 address
- 32-bit value
- always a unicast address

## Destination IPv4 address
- 32-bit value
- can either be unicast, broadcast or multicast

