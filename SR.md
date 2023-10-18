**Segment Routing** (SR) is a relatively recent move to tidy up some ways to get different packet
treatments, but also to more cleanly integrate with traffic engineering and resource pooling.

In traditional IP networks, routing decisions are made based on destination addresses, and each router determines the next hop along the path. In segment routing, routing decisions are based on segments. A segment is a short, fixed-length identifier that represents a specific instruction or action in the network. Segments can include attributes like IP addresses, MPLS labels, or other relevant information.