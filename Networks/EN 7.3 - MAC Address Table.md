>Chapter - [[EN 7.0 - Ethernet Switching]]

Nov 26, 2022
Topics - 

# Switch Fundamentals
- if a switch forwarded every frame it received out to all ports, the network would be very congested and would probably come to a halt
- Layer 2 ethernet switches use Layer 2 MAC addresses to make forwarding decisions
- switch examines the MAC address table to make a forwarding decision ***for each frame***
![[Pasted image 20221126005436.png]]
when the switch MAC address table is empty

>[!NOTE]
>MAC address table also referred to as a content addressable memory (CAM) table

---
# Switch Learning and Forwarding
- switch dynamically builds the MAC address table by examining the <u>source MAC address of the frames</u> received on a port
- switch forwards frames by searching for a match between destination MAC address and MAC address table entries

## Learn (by examining the Source MAC Address)
- every frame that enters a switch is checked for new info
- does this by examining the source MAC address of the frame and the port number of the host
- if it does not exist, it is added. If it does, refreshes timer for that entry
- if the MAC address exists in the table but for a different port number, the switch treats it as a new entry and the current entry is replaced by the more current port number
- most switches keep an entry in the table for 5 mins 

![[Pasted image 20221126010416.png]]

## Forward (by finding the distination MAC address)
- if destination MAC address is a unicast address, switch will look for a match in table
- if found in the table it will forward the frame out to the specified port
- if not found, the switch will forward the frame out to all ports except incoming port - <u>Unknown Unicast</u>
- the same is done for broadcast and multicast

![[Pasted image 20221126011058.png]]

---
# Filtering Frames
this refers to the process of filtering out the matching MAC address from the table and sending information to corresponding port only

![[Pasted image 20221126013745.png]]
![[Pasted image 20221126013758.png]]
![[Pasted image 20221126013819.png]]
