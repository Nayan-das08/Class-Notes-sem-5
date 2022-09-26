>Chapter - [[EN 3.0 - Protocols and Models]]

Aug 20, 2022
Topics - 

# Benefits of using Layered model
- used to modularize the operations of a network into manageable layers
- assists in protocol designing

---

# OSI Reference Model
- **7 Layers**
- describes how interaction takes place between each layer

## layers
| Sno | Layer        | Description                                                                                                        |
| --- | ------------ | ------------------------------------------------------------------------------------------------------------------ |
| 7   | Application  | protocols for process-to-process communications                                                                    | 
| 6   | Presentation | provides common representation of data transferred b/w layer 7 services                                            |
| 5   | Session      | to organize its dialogue and to manage data exchange done in layer 6                                               |
| 4   | Transport    | segment, transfer and reassemble data ([[EN 3.5 - data encapsulation]])                                            |
| 3   | Network      | exchange individual pieces of data over the network b/w identified users                                           |
| 2   | Data link    | describe methods for exchanging data frames ([[EN 3.5 - data encapsulation]]) over common media                    |
| 1   | Physical     | describe mechanical, electrical, functional, and procedural means to (de)activate and maintain physical connection |

Data link
- works on MAC
- sharing common channel without interference

Physical
- responsible for actual connection

>[!NOTE]
>half duplex - either send or receive, only one way communication
>full duplex - 2 way communication


---

# TCP/IP Model
- also referred to as the ***Internet Model***

| Sno | Layer          | Description                                    |
| --- | -------------- | ---------------------------------------------- |
| 4   | Application    | encoding the data at software/app level        |
| 3   | Transport      | establishes connection between various devices |
| 2   | Internet       | Determines the best path through the Network   |
| 1   | Network Access | control the hardware and the channel of the network                                               |


# Comparison of the models
![[Pasted image 20220820141832.png]]
