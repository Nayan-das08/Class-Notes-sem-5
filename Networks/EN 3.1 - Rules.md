>Chapter - [[EN 3.0 - Protocols and Models]]

Aug 9, 2022
Topics - 

# 1 Communication Fundamentals
- a sender/source
- a receiver/destination
- a media/channel

# 2 Process of communication in computer networks
message source -> transmitter -> transmission medium -> receiver ->message destination

>[!NOTE]
>All communications are governed by ***protocols***

Protocols = rules

# 3 Rule Establishment
establishing the rules before communicating

## 3.1 Protocols must account following
- identified sender and receiver
- common language and grammar (rules of language)
	- if not present we need an interpreter
- speed and timing of delivery
- confirmation/acknowledgement  

# 4 Protocol Requirement
## 4.1 message encoding
process of converting info into another ***acceptable*** form of transmission
decoding reverses the process to interpret the message

message source -> **encoder** -> transmitter -> transmission medium -> receiver -> **decoder** -> message destination

## 4.2 message formatting and encapsulation
message must have a proper format/structure
the format depends on the type of message

## 4.3 message size
the message sent is broken into small packets of fixed size
thus, size is an important factor
the msg must meet minimum and max size requirements
when pinging, we have an MTU i.e. Max Transmission Unit, which if exceeded by the message it is broken into parts

## 4.4 message timing
- **flow control** - manage the rate of data transmission, defines how much info can be sent, speed at which it can be sent

- **response timeout** - manages how long a device  waits for a response/reply from the destination

- **Access method** - when can someone send a msg, NIC needs to ensure whether the medium is available for access and collision would not occur

this is handled by protocols
2 types - proactive and reactive

### proactive  - prevents collision
**hidden terminal problem**
being proactive fails when the devices sending msg to a single receiver are outside the range of each other 

**exposed terminal problem**
even after being in network/communication range, if second sender isn't sending to the common receiver, first sender wont send coz it won't know whom the second one is sending to. It would inly know that the other sender device is going to send (where, it wouldn't know)

>[!NOTE]
>the devices will check the availability of channel after every equal intervals (pre initialized)

### reactive - establishes recovery method after collision

## 4.5 message delivery options
for IPv4
- unicast - one to one comm
- multicast - one to many comm
- broadcast - one to all possible recipients comm
	- it becomes anycast in IPv6

![[Pasted image 20220810124111.png]]




