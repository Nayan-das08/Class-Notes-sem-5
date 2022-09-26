# physical layer
- serves as the actual physical connection between nodes
- the information transmitted through this layer is in the form of bits

# data link
- responsible for NIC to NIC connection
- allows upper layer protocols to access the physical layer media/channel  
- encapsulates layer 3 packets (IP address of source and final destination) into layer 2 frames
- controls how data is placed on physical media
- error detection and rejects corrupted frames (CRC method)

# Network layer
- responsible for host to host delivery of packets/info
- contains the logical address of the original source and the final destination