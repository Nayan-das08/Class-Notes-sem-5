>Back: [[_Networks]]

# EN 9.0 - Address Resolution

## sub-chapters
```dataview
LIST
FROM [[EN 9.0 - Address Resolution]]
sort file.name asc
```
## summary
### 9.1 MAC and IP
- Layer 2 physical addresses (i.e., Ethernet MAC addresses) are used to deliver the data link frame with the encapsulated IP packet from one NIC to another NIC on the same network
- If the destination IP address is on the same network, the destination MAC address will be that of the destination device
- When the destination IP address (IPv4 or IPv6) is on a remote network, the destination MAC address will be the address of the host default gateway (i.e., the router interface)
- Along each link in a path, an IP packet is encapsulated in a frame
- The frame is specific to the data link technology associated that is associated with that link, such as Ethernet
- If the next-hop device is the final destination, the destination MAC address will be that of the device Ethernet NIC
- How are the IP addresses of the IP packets in a data flow associated with the MAC addresses on each link along the path to the destination? For IPv4 packets, this is done through a process called ARP
- For IPv6 packets, the process is ICMPv6 ND

### 9.2 ARP
- Every IP device on an Ethernet network has a unique Ethernet MAC address
- When a device sends an Ethernet Layer 2 frame, it contains these two addresses: destination MAC address and source MAC address
- A device uses ARP to determine the destination MAC address of a local device when it knows its IPv4 address
- ARP provides two basic functions: resolving IPv4 addresses to MAC addresses and maintaining a table of IPv4 to MAC address mappings
- The ARP request is encapsulated in an Ethernet frame using this header information: source and destination MAC addresses and type
- Only one device on the LAN will have an IPv4 address that matches the target IPv4 address in the ARP request
- All other devices will not reply
- The ARP reply contains the same header fields as the request
- Only the device that originally sent the ARP request will receive the unicast ARP reply
- After the ARP reply is received, the device will add the IPv4 address and the corresponding MAC address to its ARP table
- When the destination IPv4 address is not on the same network as the source IPv4 address, the source device needs to send the frame to its default gateway
- This is the interface of the local router
- For each device, an ARP cache timer removes ARP entries that have not been used for a specified period of time
- Commands may also be used to manually remove some or all of the entries in the ARP table
- As a broadcast frame, an ARP request is received and processed by every device on the local network, which could cause the network to slow down
- A threat actor can use ARP spoofing to perform an ARP poisoning attack

### 9.3 Neighbour Discovery
- IPv6 does not use ARP, it uses the ND protocol to resolve MAC addresses
- ND provides address resolution, router discovery, and redirection services for IPv6 using ICMPv6
- ICMPv6 ND uses five ICMPv6 messages to perform these services: neighbor solicitation, neighbor advertisement, router solicitation, router advertisement, and redirect
- Much like ARP for IPv4, IPv6 devices use IPv6 ND to resolve the MAC address of a device to a known IPv6 address