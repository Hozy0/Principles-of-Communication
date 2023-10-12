**Fibbing**, short for "[[FIB]]-based forwarding," is a network routing technique used to optimise the efficiency of routing tables and improve network scalability. It is typically used in [[SDN|SDNs]] and data centre environments.

## Why is it used?

[[Routing#^e57da0|Centralisation]] <u>improves network management but sacrifices the robustness</u> of distributed protocols. 
![[Pasted image 20231012185905.png]]

Therefore, we propose **Fibbing**, a hybrid SDN architecture which *combines* the advantages of SDN and traditional networking.
![[Pasted image 20231012192413.png]]
![[Pasted image 20231012192455.png]]

## How does it work?

The English definition of fibbing is: "the act of telling a lie, typically an unimportant one." which helps understanding and remembering how it works.

Here's an overview:

- SDN achieves high manageability by centralising both computation and installation.
	![[Pasted image 20231012193309.png]]
- Fibbing is as manageable as SDN, but centralises only high-level decisions (which are strategic or abstract routing choices made at the network level), leaving the detailed, low-level, day-to-day routing decisions to the network devices themselves.
	![[Pasted image 20231012195056.png]]
- Fibbing keeps installation distributed, meaning the process of configuring and managing network routing tables remains decentralised and distributed across network devices, relying on distributed protocols.
	![[Pasted image 20231012195151.png]]
- Distributed installation is controlled by injecting carefully-computed information. Instead of talking to the routers, the controller talks to the protocol by cleverly generating fake protocol messages
	![[Pasted image 20231012204507.png]]
- We study which messages to inject for controlling intra-domain routing protocols. The output of the controlled protocol is specified by the operators' requirements.
	![[Pasted image 20231012205200.png]]
- To control [[IGP]] output, the Fibbing controllers invert the shortest-path function
	![[Pasted image 20231012205321.png]]

## Implementing a Fibbing controller

Here's an implementation of a Fibbing controller. We propose algorithms that should run in sequence to compute augmented topologies of limited size.
	![[Pasted image 20231012214922.png]]

The controller can be changed to also listen to OSPF and 
### Simple and Merger

Consider the following example, with a drastic forwarding path change.
	![[Pasted image 20231012215600.png]]

Simple adds one fake node for every router that has to change [[Next-hop|next-hop]].
	![[Pasted image 20231012215704.png]]

Merger iteratively merges fake nodes (Starting from Simple's output).
	![[Pasted image 20231012215905.png]]

This way, Merger programs multiple next-hop changes with a single fake node. Previous SDN solutions <u>CANNOT</u> do the same.
	![[Pasted image 20231012215954.png]]

Simple and Merger achieve different trade-offs in terms of time and optimisation efficiency. Running experiments on Rocketfuel topologies, with at least 25% of nodes changing next-hops these are the observations: 
- Simple runs in milliseconds and Merger takes 0.1 seconds
- Merger reduces fake nodes by up to 50% and up to 90% with cross-destination optimisation.


