>Chapter - [[EN 3.0 - Protocols and Models]]

Aug 20, 2022
Topics - 

# Segmenting data
- data can be sent from sender to receiver in one uninterrupted stream of bits over the channel, but that is not feasible
- by doing so, we limit the usage of the particular connection/link to a particular transmission
- the transmission would be slow
- in case of any failure in network infrastructure, complete message will be lost

## Better Approach
- divide the data into smaller segments/pieces/packets before sending
- This process is called ***SEGMENTATION*** 
- These packets sent can be received from different paths, thus not dedicating a single link
- results in increased speed, efficiency reliability
- 