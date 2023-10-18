## What is it

In **Segment Routing** (SR), routing decisions are based on segments. A segment is a short, fixed-length identifier representing a specific network instruction or action. 
SR is a relatively recent move to tidy up some ways to get different packet treatments, but also to more cleanly integrate with traffic engineering and resource pooling so let's see where it fits in.

## SR: MPLS vs IPv6

One clear place is mapping from SR to [[MPLS]], which is almost direct (segment id lists are just label stacks). The other is an innovative way to put segment list information in the IPv6 segment list (routing extension) header, successively copying segment off into the IPv6 destination field (=pop).

![[Pasted image 20231018171030.png]]

We can also see how the control planes map for each type:
- **SR and MPLS**
	![[Pasted image 20231018171212.png]]
	
	The **SRGB** is a specific range of labels used for segment routing in the MPLS label stack. These labels fall within a well-defined block or range, typically allocated at the network level, to ensure consistency and avoid conflicts.


- **SR and IPv6**
	![[Pasted image 20231018171239.png]]

## What can you do with SR?

- As with MPLS, SR provides a form of loose [[Routing#^1f8797|source routing]] 
- **Path resilience**:  It allows for [[Routing#^2183d8|multi-path]] ECMP (Equal-Cost Multi-Path) and MPTCP (Multi-path TCP) and fast recovery.
- One can also involve arbitrary packet processing by targeting the right segment routing nodes by combining it with [[Definitions/NFV|NFV]], where specific segments in the SR network can be associated with virtualised network functions (VNFs). For example, a particular segment might be linked to a VNF that acts as a firewall.
- The integration of SR in [[IGP]] is very neat; the Segment ID information is just advertised as additional data in [[LInk State Routing|link state]] advertisements.



