## What is an AS

An **Autonomous System** (AS) can be thought of as an independent network entity that is responsible for routing IP traffic within its own network. It can be a single organisation, such as a large corporation, a university, an internet service provider (ISP), or any entity that manages a network infrastructure.

## Routing Policies

Each AS has its own routing policy, which dictates how traffic should be forwarded within the AS and how it should be exchanged with other AS. This policy includes decisions about which routes to accept, which routes to advertise to neighbouring AS, and how to prioritise or manipulate traffic.

We use [[Definitions/IGP|IGP]] within AS (intra-) and [[Definitions/EGP|EGP]] for AS to AS routing.



## Locus of admin control

The "*locus of admin control*" refers to the point within an AS where the decisions regarding routing policies are made and implemented. This is typically under the control of network administrators or engineers responsible for managing the AS's network infrastructure.

In practical terms, the locus of admin control within an AS involves:

- **Configuring Routers:** Network administrators configure routers within the AS to implement the desired routing policies. This includes defining which routes are preferred, setting up filters to control which routes are accepted from neighbouring AS, and managing traffic engineering.

- **Monitoring and Troubleshooting:** The administrators are responsible for monitoring network traffic, identifying issues, and making adjustments to routing policies as needed to ensure efficient and reliable network operation.
 
- **Interacting with Other AS:** AS need to negotiate and exchange routing information with neighbouring AS, and the locus of admin control determines how these interactions occur and which routes are advertised or accepted.