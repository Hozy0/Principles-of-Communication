**Multi-protocol label switching** (MPLS) is a forwarding scheme designed to speed up IP packet forwarding. It was originally considered a possible replacement for the Internet Protocol but is now used as a substrate to enhance traffic engineering capabilities for ISPs (intra-AS) or data centres.

## The main idea

MPLS Is a good example of what is sometimes called a [[Shim Layer|shim layer]] which is inserted between the existing link layer (whichever one is in use) and the IP datagram layer (<u>MPLS supports any network layer protocol and link layer protocol</u>). The protocol simply adds fixed length (20-bit) labels in this layer, primarily to simplify hardware lookup of the next-hop.

## MPLS Header Format

![[Pasted image 20231013014745.png]]

- **Label**: 20-bit label value
- **Exp**: experimental use
	- Can indicate class of service
- **S**: bottom of stack indicator
	- 1 for the bottom label, 0 otherwise
- **TTL**: time to live
	- Helps remove looping packets.

## Forwarding Equivalence Class

**Forwarding Equivalence Class** (FEC) is a subset of packets that are all treated the same way by an [[Link State Routing|LSR]]