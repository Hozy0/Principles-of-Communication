## Links to subsections
- [[Central Routing]]
- Multicast Routing
- Routing in telephone networks
- Routing for mobile hosts

## What is routing?

Routing is the process of finding a path from sources to every destination of the network
## Basics

A [[Routing Protocol|routing protocol]] sets up a [[Routing Table|routing table]] in routers and switch controllers
## The key problem

- A network node has to make quick decisions based on local information ([[FIB]]) but also considers the broader, slower-changing characteristics of the entire network ([[RIB]]) when making these decisions. This is a common approach in routing algorithms, where nodes balance the need for fast decision-making with the requirement to adapt to network structure changes.

- So, how do we make correct local decisions? Every router needs to know about the global state, which is naturally characterised by its large, dynamic, and challenging-to-gather nature.

-  **A routing protocol must intelligently summarise relevant information**

## Requirements

A suitable routing protocol must meet these requirements:
- **Minimise routing table space**
	- **Fast to look up**: A smaller routing table typically contains fewer entries, making it faster to search through when a router needs to make routing decisions. With fewer entries, the lookup process is quicker because the router has to compare the destination address of an incoming packet with fewer entries in the routing table to find the best matching route.
	- **Less to exchange**: A smaller routing table means there is less routing information to exchange between routers in a network. When routers share routing updates, they transmit information about the routes they know. If the routing table is small and contains only essential routes, the amount of information that needs to be exchanged is reduced.
- **Minimise the number and frequency of control messages**.
- **Robustness** 
	- **Avoiding [[Black Holes]]**:  To maintain robustness, a network or routing protocol should be designed to prevent or quickly recover from black hole scenarios, ensuring that data packets reliably reach their destinations.
	- **Avoiding [[Loops]]**: Robust networking protocols are designed to detect and prevent routing loops, often through mechanisms like loop prevention algorithms or time-to-live (TTL) counters in packets.
	- **Avoiding [[Oscillations]]**: Robust routing protocols aim to minimise oscillations by employing stability mechanisms and route dampening techniques.
- **Use optimal path**

## Internet Routing Model

- The Internet is organised as "[[AS|AS]]"
	- AS are internally connected
- Features
	- Dynamic routing: Dynamic routing in the internet routing model refers to the use of routing protocols to automatically and adaptively determine the best paths for data to travel between AS based on real-time network conditions and policies. It enables efficient and flexible data routing across the global internet.
	- [[AS#Routing Policies|Intra- and Inter-AS routing]]: AS can route traffic within themselves and can be exchanged with other AS
	- AS = [[AS#Locus of admin control|locus of admin control]]: this concept emphasises that each autonomous system on the internet has its own independent control over its routing policies and network management. This autonomy allows organisations to make decisions that best suit their network's needs while participating in the global internet routing system.

### Requirements for Intra-AS Routing

- **Should scale for the size of an AS**
	- Low end: 10s of routers (small enterprise)
	- High end: 1000s of routers (large ISP)
-  **Different requirements on [[Definitions/Routing Convergence|routing convergence]] after topology changes**
	- Low end: can tolerate some connectivity disruptions
	- High end: fast convergence essential to business (making money on transport)
- **Operational/Admin/Management (OAM) Complexity**
	- Low end: simple, self-configuring
	- High end: Self-configuring, but operator hooks for control
- **Traffic engineering capabilities**
	- high end only

### Requirements for Inter-AS Routing

- **Should scale for the size of the global Internet**
	- Focus on reachability, not optimality
	- Use address aggregation techniques to minimise core routing table sizes and associated control traffic
	- At the same time, it should allow flexibility in topological structure (e.g. don’t restrict to trees, etc.)
- **Allow *policy-based routing* between AS**
	- Policy refers to an <u>arbitrary preference among a menu of available options</u> (based on options’ attributes)
	- In the case of routing, options include advertised AS-level routes to address prefixes
	- Fully distributed routing (as opposed to a signalled approach) is the only possibility
	- Extensible to meet the demands for newer policies.

### Intra-AS and Inter-AS Routing:  Example

![[Pasted image 20231012144631.png]]

## Basic Dynamic Routing Methods

- **[[Source-Based Routing]]**: The source gets a map of the network.
	- The source finds the route, and either
	- signals the route setup (e.g. ATM approach)
	- encodes the route into packets (inefficient)
- **[[Link State Routing]]**: per-link information.
	-  Get a map of the network (in terms of link states) at all nodes and find the [[Definitions/Next-hop|next-hops]] locally
	- Maps consistent => next-hops consistent
- **[[Distance Vector Routing]]**: per-node information.
	- At every node, set up distance signposts to destination nodes (a vector)
	- Set up this by peeking at neighbours’ signposts.

 These basic dynamic routing methods determine how data is routed through a network. Source-based routing places the routing decision at the source node, while link state routing and distance vector routing distribute routing information among routers to collectively make routing decisions based on either per-link or per-node information. Each method has advantages and use cases depending on the network's needs and complexity.

## Routing Choices


- **Centralised vs. Distributed Routing**:
	- *[[Central Routing|Centralised Routing]]*: In centralised routing, <u>routing decisions are made by a central controller or entity</u>. It is simpler to manage but can be vulnerable to failures and congestion at the central point. ^e57da0
	- *Distributed Routing*: Distributed routing spreads<u> routing decision-making across multiple routers or nodes in the network</u>. It can handle failures and congestion more effectively but may be more complex to configure and maintain.

- **Source-Based vs. Hop-by-Hop Routing**:
	- *Source-Based Routing*: In source-based routing, <u>the source node determines the complete path or route to the destination</u> and includes this information in the packet header. Intermediate routers follow the specified route. ^1f8797
	- *Hop-by-Hop Routing*: In hop-by-hop routing, <u>each router along the path makes its own independent routing decision</u> based on its local routing table. The packet header typically contains only the destination address, and routers determine the next hop based on this address.

- **Stochastic vs. Deterministic Routing**:
	- *Stochastic Routing*: Stochastic routing <u>introduces randomness</u> into routing decisions to spread the load and prevent oscillations in the network. However, it may occasionally misorder packets due to randomness.
	- *Deterministic Routing*: Deterministic routing <u>follows predefined rules or algorithms</u> for routing decisions. It ensures predictable routing but can lead to issues like routing loops in certain situations.

- **Single vs. Multiple Path Routing**:
	- *Single Path Routing*: Single path routing selects <u>one primary path</u> for data transmission. If that path fails, the network must recompute a new path, potentially causing delays.
	- *Multiple Path Routing*: Multiple path routing involves the use of <u>both primary and alternative paths</u>. If the primary path experiences issues, data can be rerouted via alternative paths, improving network fault tolerance. ^2183d8

- **State-Dependent vs. State-Independent Routing**:
	- *State-Dependent Routing*: State-dependent routing decisions are<u> influenced by the current network conditions</u>, such as delay or traffic load. Routes may change dynamically based on the real-time state of the network.
	- *State-Independent Routing*: State-independent routing decisions are made <u>without considering the current network conditions</u>. Routes are determined based on static or predetermined criteria and do not change dynamically based on network state.
