>Chapter - [[EN 8.0 - Network Layer]]

Nov 26, 2022
Topics - 

# Limitations of IPv4
- **IPv4 address depletion**
	- $2^{32}$ ~ 4 billion IPv4 addresses, not enough
- **lack of end-to-end connectivity**
	- NAT provides a way for multiple devices to share a single public IPv4 address
	- since the public address is shared, IPv4 address of an internal network host is hidden
	- this can be problematic for tech that require end-to-end connectivity
- **increased network complexity**
	- NAT may have expanded the lifespan of IPv4
	- but it was meant as a transition to IPv6
	- NAT increases complexity in the network
	- creates latency

---
# IPv6 improvements
- **increased address space**
	- $2^{128}$ ~ 340 undecillion addresses
- **improved packet handling**
	- fewer fields in IP header
- **eliminates the need for NAT**
	- NAT between private IPv4 and public IPv4 addresses not needed anymore coz large number of IPv6 addresses available

---
# IPv6 Packet Header

![[Pasted image 20221126155617.png]]

## Version
- 4 bit value 
- set to 0110 to identify IPv6 packet 

## Traffic Class
- 8-bit value
- equivalent to IPv4 DS field

## Flow Label
- 20-bit value
- all packets with same flow label receive same type of handling by routers

## Payload Length
- 16-bit field
- length of data portion in the packet
- does not include length of IPv6 header (40-byte header)

## Hop Limit
- 8-bit value
- replaces IPv4 TTL
- when zero, ICMPv6 Time Exceeded message is forwarded to source IP address
- does not include IPv6 Header Checksum
	- this function is performed at both lower and upper layers
	- reduces this redundancy
	- improves performance

## Source IPv6 Address
- 128-bit value

## Destination IPv6 Address
128-bit value

Other fields are
- Extension Headers (EH)
	- provide optional network layer info
	- placed between IPv6 header and payload
	- used for fragmentation, security n shit

---