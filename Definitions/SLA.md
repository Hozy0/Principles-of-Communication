**Service Level Agreements** (SLA) provide a simple mechanism for allocating blocks of a particular service to specific customers. This facilitates long-term bandwidth reservation for organisations or users but doesn't constrain the allocation to specific flows. An SLA is valid for flows within a single trust region.
Once an SLA has been established, portions of this service can be assigned to specific flows.

The SLA includes the following information:
- Customer Identification
- Service Type
- Service Type Parameters
- Service Restrictions

The [[Bandwidth Broker]] ensures that the total SLA obligations for any service do not exceed the amount of that service available in the trust region.