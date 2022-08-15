>Chapter - [[EN 3.0 - Protocols and Models]]

Aug 10, 2022
Topics - 

Net protocols define common set of rules

# types of protocols
| type                   | desc                                                                           | example       |
| ---------------------- | ------------------------------------------------------------------------------ | ------------- |
| Network communications | enables 2 or more devices to communicate over one or more network              | IP, TCP, HTTP |
| Network security       | secure data, provide authenticatn, data integrity                              | SSG, SSL, TLS |
| Routing                | select best path by enabling routers to exchange route info, compare path info | OSPF, BGP     |
| Service discovery      | for auto detection of devices/services                                         | DHCP, DNS     |

>[!NOTE]
>### (Dynamic Host Config Protocol) DHCP 
>discovers services for IP address allocation
>### (Domain Name System) DNS
>name to IP address translation

---

# Network protocol function
one protocol may have more than one function
devices must agree upon the protocols to communicate

>[!NOTE]
>raw data can't be sent, some meta-data is reqd

## functions
- ### addressing
	- identify sender and receiver
	- IPv4 and IPv6, Ethernet
- ### reliability
	- provides *guaranteed delivery* mechanisms 
	- TCP
- ### flow control
	- ensure data flows at efficient rate
	- TCP
- ### sequencing
	- uniquely labels each transmitted segment of data (when broken down)
- ### error detection
	- check integrity of data (corrupted or not)
- ### application interface
	- process to process communication

---

# Protocol Interaction
how multiple protocols interact
protocols must be compatible w/ each other

## http
- governs the way web server interacts with web client

## TCP
- manages individual conversations
- provides guaranteed delivery
- manages flow control

## IP
delivers messages globally from sender to receiver

## ethernet
delivery of messages from one NIC to another NIC
