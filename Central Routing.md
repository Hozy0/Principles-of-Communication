Having touched on traffic engineering in the context of Inter-domain routing, let's look at
three more approaches to helping engineer paths traffic follows within a single routing
domain, namely [[Routing#^e57da0|centralised routing]] using [[Definitions/SDN|software-defined network]] (SDN) controls, multi
protocol label switching, and segment routing.

## Fibbing

SDN is the simplest technique to enhance a [[Link State Routing|link state routing]] system within a single [[AS|AS]] to
allow the operator to place some traffic on different paths than those computed by a shortest
path algorithm. The approach described here is based on a technique called **[[Fibbing]]** for
illustrative reasons - once one has SDN capability, many other similar tricks could be
deployed.

