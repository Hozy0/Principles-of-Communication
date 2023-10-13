**Multi-protocol label switching** (MPLS) is a forwarding scheme designed to speed up IP packet forwarding. It was originally considered a possible replacement for the Internet Protocol but is now used as a substrate to enhance traffic engineering capabilities for ISPs (intra-AS) or data centres.

## The main idea

MPLS Is a good example of what is sometimes called a [[Shim Layer|shim layer]] which is inserted between the existing link layer (whichever one is in use) and the IP datagram layer (<u>MPLS supports any network layer protocol and link layer protocol</u>). The protocol adds fixed length (20-bit) labels in this layer, primarily to simplify hardware lookup of the next-hop.

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

**Forwarding Equivalence Class** (FEC) is a subset of packets that are all treated the same way by an [[Definitions/LSR|LSR]]. A packet is assigned to an FEC at the ingress of an MPLS domain.

A packet's FEC can be determined by one or more of the following:
- Source and/or address destination IP address
- Source and/or address destination port number
- Protocol ID
- Differentiated service code point
- Incoming interface

A particular [[PHB]] (scheduling and discard policy) can be defined for a given FEC.

## MPLS Operation

Here’s an overview of how MPLS operates:
- At ingress LSR of an MPLS domain, an MPLS header is inserted into a packet before forwarding. The label in the MPLS header is used to encode the packet's FEC.
- At subsequent LSRs, the label is used as an index into a [[Forwarding Table|forwarding table]] that specifies the [[Next-hop|next-hop]] and a new label.
- The old label is replaced with the new label, and the packet is forwarded to the next hop.
- Egress LSR strips the label and forwards the packet to the final destination based on the IP packet header.

![[Pasted image 20231013022327.png]]

## Label distribution

For each FEC, a specific path called[[LSP| Label Switching Path]] (LSP) is assigned and we need a label distribution protocol so that an LSR can inform others of the label/FEC binding it has made.

A forwarding table is constructed as the result of label distribution
![[Pasted image 20231013023601.png]]

## LSP route selection

- **Hop-by-hop routing**: 
	Use the route determined by the dynamic routing protocol
- **Explicit routing (ER)**: 
	The sender LSR can specify an <u>explicit route</u> (that can be selected ahead of time or dynamically) for the LSP

### Explicitly routed LSP

The advantages of ER are that we can establish LSP based on policy, QoS, etc and that we can have pre-established LSP in case of failures.

These mappings are established by signalling protocols such as **CR-LDP** and **RSVP-TE**.

## Diffserv-Aware MPLS

MPLS can be used together with [[DiffServ|Differentiated Services ]]to provide [[QoS]] (*More when discussing traffic management*).

Here LSP are configured between each ingress-egress pair, and there are 2 approaches:
- For each ingress-egress pair, a separate LSP can be created for each traffic class
- For each ingress-egress pair, c
