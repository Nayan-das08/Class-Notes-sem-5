>Chapter - [[]]

#Unlinked 
#incomplete 
Aug 31, 2022
Topics - 

# types of topology
logical and physical

# WAN Topologies
1. Point-to-Point 
	- no intermediary devices
	- permanent link between to end-devices
2. Hub and spoke
	- similar to star topology
	- the central hub acts as a single point of failure
3. Mesh
	- every device is connected to every other device
	- always available connections
	- point of failure is difficult to find
	- placed where failure is not an affordable/acceptable situation

# LAN topologies
1. Bus
2. Ring
3. Extended Star (Bus + Star)
4. Star

# Access Control Methods
## Contention based access
***compete for control of media

1. **carrier sense multiple access with collision detection (CSMA/CD)**
	- for bus/legacy ethernet LANs
	- half duplex
	- the collision is detected here
	- wait, then transmit again
	- hidden terminal problem
	- 1-persistent
		- check every $t$ moment of time if the media is accessible
		- if it finds it free: the access will be allowed
	- p-persistent
		- wait for $p$ instant of time
	- n-persistent
		- wait for $p\cdot n$ instances of time

1. **carrier sense multiple access with collision avoidance (CSMA/CA)**
	- for WLANs
	- exposed terminal problem
	- try to avoid collision at any cost
	- connections are not visible
	- half duplex
	- devices include the time needed for channel access
	- others will wait for that period of time

## controlled access
***fixed strategy is used

fixed deterministic access

**drawback**: time wasted when a device is allotted time but it does not require it at all

poor utilization of time

used in legacy systems (Token ring, ARCNET)

