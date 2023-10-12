Having touched on traffic engineering in the context of Inter-domain routing, let's look at
three more approaches to helping engineer paths traffic follows within a single routing
domain, namely [[Routing#^e57da0|centralised routing]] using [[SDN]] controls, multi protocol label switching, and segment routing.

## Central control over distributed routing

The approach described here is the simplest technique to enhance a [[Link State Routing|link state routing]] system within a single [[AS|AS]] to allow the operator to place some traffic on different paths than those computed by a shortest path algorithm. It is based on a technique called **[[Fibbing]]**, but once one has SDN capability, many other similar tricks could be deployed.

Here, we illustrate how a central node can provide a host-specific (or perhaps prefix-specific) route across a simple topology. The requirement is to separate traffic for destination two, way from the default shortest path computed by everyone, which would clearly go via the C-X link (weight 3) rather than the C-A-B-X link, which is 10+1+1 or weight 12.

Considering this simple network:
	![[Pasted image 20231012211747.png]]

An [[IGP]] control-plane computes shortest paths on a shared weighted topology, and then these shortest paths are translated into forwarding paths on the data-plane.
	![[Pasted image 20231012212047.png]]

In Fibbing, operators can ask the controller to modify the forwarding paths. The Fibbing controller injects information on fake nodes and links to the IGP control-plane to achieve the desired result.
	![[Pasted image 20231012212512.png]]

Informations are flooded to all IGP routers in the network, and the Fibbing messages augment the topology seen by all IGP routers.
	![[Pasted image 20231012212727.png]]

Augmented topologies translate into new control-pane and data-pane paths.
	![[Pasted image 20231012212908.png]]

By achieving full per-destination control, Fibbing is highly flexible. 
Indeed, <u>any set of forwarding DAGs can be enforced by Fibbing</u>. 
Here's how Fibbing's flexibility and ability to enforce various forwarding DAGs helps in different scenarios:

- **[[Fine-Grained Traffic Steering]] (Middleboxing)**
   - With Fibbing, network administrators can define forwarding DAGs that route specific traffic flows to the appropriate middleboxes within the network. This ensures that packets follow precise paths that include these intermediate services.

- **[[Per-Destination Load Balancing]] (Traffic Engineering)**
   - Fibbing allows network administrators to create forwarding DAGs that implement per-destination load balancing. It can enforce routing decisions that evenly distribute traffic across various paths to specific destinations, enhancing network efficiency.

- **[[Backup Paths Provisioning]] (Failure Recovery)**
   - Fibbing's flexibility enables administrators to configure forwarding DAGs that include backup paths. Fibbing can quickly reroute traffic along these pre-established backup paths when network issues occur, ensuring reliable failure recovery and network resilience.
