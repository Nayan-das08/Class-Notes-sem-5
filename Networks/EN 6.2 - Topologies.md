>Chapter - [[EN 6.0 - Data Link Layer]]

Aug 31, 2022
Topics - 

# types of topology for LAN & WAN
## 1. Logical Topology
![[Pasted image 20220913125206.png]]

## 2. Physical Topology
![[Pasted image 20220913125144.png]]

---
# WAN Topologies
1. **Point-to-Point** 
	- no intermediary devices
	- permanent link between to end-devices
	- ![[Pasted image 20220913125305.png]]
2. **Hub and spoke**
	- WAN version of star topology
	- the central hub acts as a single *point of failure*
	- data must go through central point for transmission from one branch to another
	- ![[Pasted image 20220913125323.png]]
3. **Mesh**
	- every device is connected to every other device
	- *always available* connections
	- *point of failure* is difficult to find
	- placed where failure is not an affordable/acceptable situation
	- each link is essentially a *point-to-point* link to the other node
	- ![[Pasted image 20221125173534.png]]

---
# LAN topologies
- nodes are interconnected using star or extended star topologies
- extended star is created by interconnecting multiple Ethernet switches
- easy to install
- very scalable

## legacy LAN topologies
1. **Bus**
	- all end-devices connected to each other and terminated in some form on each end
	- switches ad such devices are not needed to interconnect devices
	- often used co-axial cables as it was inexpensive and easy to set up
2. **Ring**
	- end-devices connected to their respective neighbour forming a ring
	- ring not terminated unlike bus
	- used by Fibre Distributed Data Interface and Token Ring networks

---
# Half and Full Duplex Communication
refers to the direction of data transmission between two devices
## Half duplex
- both devices can transmit and receive on the media/channel, ***but not simultaneously***
- WLANs and legacy bus topologies working with ethernet hubs use this mode

## Full duplex
- both devices can simultaneously transmit and receive on the shared media/channel
- ethernet switches operate in full duplex mode by default
- they can work in half duplex mode when connected to devices like ethernet hub

---
# Access Control Methods
Multi-access networks require rules to govern how devices share the physical media

Two types of methods are :-

## Contention based access
***compete*** for control of media

### 1. **carrier sense multiple access with collision detection (CSMA/CD)**
- for bus/legacy ethernet LANs
- half duplex
- the collision is detected here
- wait, then transmit again
- [[EN 3.1 - Rules|hidden terminal problem]]
- The detection of whether any device is transmitting on the medium is done by the NIC
- NIC checks before sending data on the shared medium
- If another device wants to send while another device is transmitting on the media, it will wait until the channel is clear
- the ethernet hub will relay the received frame to all connected devices as it is also known as a multiport repeater
- the device whose MAC address was in the frame header address space will accept and copy the frame, rest will ignore the frame
![[Pasted image 20221125200130.png]]

>[!Useless shit]
>- 1-persistent
>	- check every $t$ moment of time if the media is accessible
>	- if it finds it free: the access will be allowed
>- p-persistent
>	- wait for $p$ instant of time
>- n-persistent
>	- wait for $p\cdot n$ instances of time

### 2. **carrier sense multiple access with collision avoidance (CSMA/CA)**
- for WLANs
- half duplex
- [[EN 3.1 - Rules|exposed terminal problem]]
- try to avoid collision at any cost
	- attempts to avoid them before transmitting
- connections are not visible
	- wireless connections
- devices include the time needed for channel access while transmitting the frame
- others will wait for that period of time
- not scalable for heavy media use

>[!NOTE]
>- **Ethernet LANs using switches** (modern) don't use contention based system as switches are intelligent devices
>- switches and host NICs operate in full-duplex mode

## controlled access
***fixed strategy is used

- fixed deterministic access
- **drawback**: time wasted when a device is allotted time but it does not require it at all
- poor utilization of time
- used in legacy systems (Token ring, ARCNET)