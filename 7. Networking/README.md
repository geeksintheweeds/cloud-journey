# Azure Networking
## Overview
Networking within Azure provides the plumbing and backbone to make applications in the cloud work.  It is a very complex topic that generally requires a bit of discussion and exploration of an organizations requirements.  Much of the design and architecture of an organizations network is going to be driving by organizational requirements around things such as mediation, inspection and segmentation.  This section covers some of the common the primitives of the Azure Networking stack as well as some common patterns.

## Sections
* [Azure Networking Components](#azure-networking-components)
---
---
# Azure Networking Components
## Summary
There are a large variety of networking services and offerings in Azure to meet almost any enterprise usecase or scenario.  This section will not cover every component or service but rather the basic building blocks that an organization needs to be familiar with to begin building in azure.

## Primary Components
* Virtual Networks (VNET)
    * Isolated logical networking that provides connectivity for IaaS and PaaS services
    * RFC 1918 User defined address space (can be one or more ranges)
    * Address space assigned to VNET can be changed but doing so with peerings in place is only in (Preview)
    * Native connectivity for resources in the same VNET
    * VNET Peering
        * Provides Connectivity for resources in other VNETs in the same region (Local) or across regions (Global)
    * All resources have native connectivity to the internet
    * Scoped to a SINGLE region
    * Functional Limit of /16 CIDR block based on IP limits per vnet
    * DDoS protection at VNET scope
    * DNS servers set at the VNET scope
* Subnets
    * Range of IP addresses in a VNET
    * Can span only 1 range of contigous IP space
    * Similar to a traditional Layer 3 network segment
    * NSG scope for securing network traffic
    * Route Table Scope
    * Inherits system route table
    * Service Endpoint Scope (such as keyvault) [link](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-service-endpoints-overview)
    * Can be deleged to a PaaS service (such as Azure Bastion) [link](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-for-azure-services)
    * NAT Gateway Scope [link] (https://docs.microsoft.com/en-us/azure/virtual-network/nat-gateway)
 * Route Tables
    * Overrides automatically provisioned Azure routes.
    * Applied to subnet(s) to affect traffic leaving a subnet
    * Order of Preference
        * User Defined Routes
        * BGP learned routes
        * System Routes
    * Default System Routes [route-routes](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview#default)
        * Virtual network - Allows all subnets in a VNET to communicate with eachother
        * Internet - Allows all resources in VNET to communicate to the Internet
        * VNET Peering - Allows all resources in VNET to communicate with Peered VNETs
        * BGP - Allows all resources in VNET to communicate with BGP peered networks
        * None - Blackholes all RFC 1918 & RFC6598 traffic not defined in other routes
* Network Security Groups
    * Basic, stateful, packet filtering firewall that enables network access control based on 5-tuple rules (Source Address, Source Port, Destination Address, Destination Port, Protocol)
    * Can be combined with Service Tags and Application Security Groups to reduce overhead
    * Can be applied at the subnet or NIC
    * Can capture traffic between resources via NSG Flow logs
    * Only one NSG can be applied to a subnet
    * If NSG is assigned at both NIC and Subnet the aggregate least restrictive rules apply
    * Limit of 5,000 per region per subscription
* Application Security Groups
    * Groupings of resources that allow for simplified NSG rules
    * ASGs apply to the resource NOT the IP so no need to maintain IP lists
    * Similar to "Address Groups" on a traditional firewall
* Service Tags
    * Similar to Application Security Groups but maintained by Microsoft
    * Address Prefixes associated with a given Azure Service.
* Network Interface Cards
    * Connection between VM (or other resource) and Virtual Network
    * All VMs must have at least 1 NIC
    * Can have multiple IPs assigned
    * Must exist in the same region and subscription as the VNET and VM
    * Can change the Subnet 
    * CANNOT change the VNET ofa  nic
    * Can have static or Dynamic IP assignment
    * Can have public or private IP assignment (or both)
    * Can have explicit DNS Servers defined (override inherited from VNET)
* DNS Resolver
    * DNS provided in every VNET by default via the static IP 168.63.129.16
    * Can only resolve records in VNET, Attached Private Zones, and Public records
    * Only accessible within the VNET
    * Does not support forwarders of any type including conditional forwarders
    * All recursive queries use Microsoft public DNS servers
    * Does not support query logging
* Azure Private DNS Zones
    * Provides DNS zones available only within internal VNET where linked
    * Can be linked to multiple VNETs
    * Primarily used for Private Endpoints
    * Can have the same zone defined and linked in multiple regions with different records
    * Azure Private DNS Zones are region specific
* Virtual Network Gateway (VNG)
    * Virtual Network Gateway goes into a VNET and provides network gateway services such as VPN and ExpressRoute connectivity.
    * Only one VPN type Virtual Network Gateway can exist in a VNET, but multiple VPN tunnels can terminate into a single VPN VNG
    * Must be deployled into a subnet named GatewaySubnet

## Best Practices
---
* # Azure Networking Resources

## Networking Patterns
[This repository](https://github.com/mattfeltonma/azure-networking-patterns) contains a collection of common Azure networking patterns. The patterns each include a write-up of how a packet flows through the architecture.

## Networking Labs
* [Azure Application Gateway and App Services with a Private Endpoint](https://github.com/mattfeltonma/azure-labs/tree/master/app-gw-app-service-pe)
* [Azure App Services with Forced Tunneling](https://github.com/mattfeltonma/azure-labs/tree/master/app-service-force-tunnel)
* [Azure Function App with Forced Tunneling](https://github.com/mattfeltonma/azure-labs/tree/master/function-app-force-tunnel)

    
---
---

