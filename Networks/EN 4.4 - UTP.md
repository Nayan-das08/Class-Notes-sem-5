>Chapter - [[EN 4.0 - Physical Layer]]

Sep 9, 2022
Topics - 

# Reducing crosstalk without shielding
1. cancellation of interfering signals using twisting
2. varying number of twists per wire pair
	- each coloured pair has different number of twist per meter

---
# UTP cabling and connectors standards
- cabling standards given by TIA/EIA-568 (for LAN installations)
- they define
	- cable types
	- lengths
	- connectors
	- cable termination
	- methods of testing cable

- electrical characteristics defined by IEEE
	- they are rated and placed into categories based on their ability to carry bandwidth rates

| name        | role                                                                  |
| ----------- | --------------------------------------------------------------------- |
| Category 3  | originally for voice comm., later for data transmission               |
| Category 5  | for data transmission, supports 100Mbps                               |
| Category 5e | 1000Mbps                                                              |
| Category 6  | has added separators between each wire pair for higher speeds, 10Gbps | 
| Category 7  | 10Gbps                                                                |
| Category 8  | 40gbps                                                                |

>[!NOTE]
>Category 6 = STP

---
# Straight-through & crossover UTP
- different situations need UTP to be wired accordingly
- concerns the orders of individual wires connected in pins of RJ-45 connector
- two conventions:
	- **Ethernet Straight-through**
		- most common type
		- host-switch, switch-router
	- **Ethernet Crossover**
		- interconnect similar devices
		- switch-switch, router-router, host-host
		- considered legacy now
			- NIC use medium dependent interface crossover (auto-MDIX)
			- automatically detect the cable type
			- make internal connection accordingly
		- **Rollover**
			- Cisco proprietary
			- workstation-router or workstation-switch console port

| type                      | ends                       | role                                                  |
| ------------------------- | -------------------------- | ----------------------------------------------------- |
| Ethernet Straight-through | both ends T568A or T568B   | host-switch, switch-router                            |
| Ethernet Crossover        | one end T568A, other T568B | switch-switch, router-router, host-host               |
| Rollover                  | Cisco proprietary          | workstation-router or workstation-switch console port |

![[Pasted image 20220909005906.png]]

---
