# OSI Model
## Physical Layer:
- Actual Physical Connection
- Hubs/Cables
- ***PDU sent as: Information in Bits***

## Data Link Layer:
- Node to Node Delivery
- Switches
- ***PDU: Frames***

## Network Layer:
- Host to Host Delivery
- ***PDU: Packet***

## Transport Layer:
- Provide Network Layer Services to Application Layer
- Segment, transfer and reassemble data
- ***PDU: Segment***

## Session Layer:
- Establish Connections, Maintenance, Authentication and Security
- ***PDU: Data*** 

## Presentation Layer:
- Data From application layer is formatted and encoded for transmission
- ***PDU: Data***

## Application Layer:
- Helps in identifying the client and sync communication.
- ***PDU: Data***

---

# TCP/IP Model (ATIN)
## Application Layer:
- Represents data to user, encoding and dialog 
  control
- HTTPS, DNS, DHCP, FTP

## Transport Layer:
- Supports communication between various 
  devices across diverse networks
- TCP, UDP

## Internet Layer:
- Determine the best path through the network
- IPv4, IPv6

## Network Access Layer:
- Control the hardware devices and media that make up the network
- Ethernet, WLAN

---

# Comparison
- Now, both of these models are layered style models, and they certainly are interoperable.

In fact:

| OSI Reference Model (7 Layers) | TCP/IP Model (4 Layers) |
|:------------------------------:|:-----------------------:|
|          Application           |       Application       |
|          Presentation          |       Application       |
|            Session             |       Application       |
|           Transport            |        Transport        |
|            Network             |        Internet         |
|           Data Link            |     Network Access      |
|            Physical            |     Network Access      |



>[!NOTE]
>We can see there is a direct mapping between the two models

