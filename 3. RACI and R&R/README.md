# Roles and Responsibilities and RACI Matrix
## Summary

Establishing roles and responsibilities is a critical step in the cloud adoption journey. Existing roles and responsibilities will evolve and new roles may need to be created. Identifying key decision makers both technical and non-technical questions that may arise is important to ensure the right people are involved in process and architectural decisions. The earlier the roles and responsibilties are agreed upon and documented, the more successful an organization will be in adopting the cloud. Holding off this conversation until after design and implementation results in poor architectural decisions which create technical debt, unaccounted for risks which can lead to audit findings, and expensive delays in implementation and operationalization. 

A RACI matrix is an effective tool in documenting roles and responsibilities.  RACI stands for responsible, accountable, consulted, and informed. The table below includes a description of each term.

| Term          | Number of Individuals | Definition  | 
| ------------- | ------------- |-------------|
| Accountable | 1 | This party is the decision maker and is answerable for the success or failure of the process. | 
| Responsible | Many | These parties play a role in the completion of the process but are not decision makers.  | 
| Consulting | Many | These parties should be solicited for best practices and feedback on the process but are not involved in the completion of the process and are not decision makers. |
| Informed | Many | These parties have an interest in the completion of the process but are not involved in feedback, completion of the tasks, or decision making. |

The purpose of the RACI matrix included in this module is to provide organizations who are planning to or have adopted Azure an understanding of the foundational processes and tasks necessary for successful cloud adoption. It includes processes and tasks for both the governance of cloud and operationalization of Microsoft Azure. The intent of this RACI matrix is to provide a starting point to understand and identify key teams that will be involved in architectural and process decisions during cloud adoption. It is not intended to replace a detailed RACI which could then be used to create custom Azure RBAC roles. Those types of RACIs can take weeks or months to create. This RACI can be completed in a one to two day workshop and will help to ensure the right teams are involved in future architectural and process based decisions during cloud adoption.

The roles included in the RACI should be treated as general buckets which may include multiple teams from the organization. For example, the Security Admin role may be a bucket which includes both Security Architecture and Security Engineering. Each role is described below.

| Role          | Description   | 
| ------------- |:-------------|
| **Cloud Service Owner**    | Individual who is accountable for the cloud program. This is often a role held by the CIO. The responsibility can be delegated to an architectural review board or CCoE.  | 
| **Workload Owner**    | Development team or primary support personnel for workload | 
| **Operations**    | Tier 2 day to day operation of the environment such as troubleshooting and incident management | 
| **Security Auditors**    | Tier 2 team responsible for validating security configuration for compliance | 
| **Systems Operators**     | Tier 3 team responsible for design, implementation, and configuration of compute resources (VMs, SQL, etc)     |   
| **Network Operators** | Tier 3 team responsible for design, implementation, and configuration of network resources (Vnet, routing tables, etc)   |   
| **Security Admins**    | Tier 3 team responsible for setting security policy and configuration of security solutions | 

## Key Points
* The workshop requires attendance of architecture, security, systems, networking, operations, and ideally one or two workload owners.
* The workshop typically takes one to two full days.
* The workshop should be conducted in partnership with the organization's Microsoft account team.
* Organizational decision makers around cloud adoption should be in attendance.

## Best Practices
* Establish roles and responsibilities before design and implementation. This will help to ensure requirements are not missed.
* Use the RACI matrix included in this module as a starting point and build it out as you move through your cloud adoption journey.
* If an existing RACI exists for on-premises make sure it is updated to include the cloud.
* Microsoft Azure shares an identity plane through Azure AD with Microsoft 365 services. Ensure the teams that administer Azure AD are included in the RACI conversations.

## Checklist
- [ ] Have you decided on roles and responsibilities for Azure?
- [ ] Have you documented roles and responsibilities for the cloud?
- [ ] Have you codified the roles in responsibilties into Azure RBAC Roles?
## Links
* [Aligning responsibilities across teams - Cloud Adoption Framework | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/organize/raci-alignment)
## Learning
* Mslearn
	* [Secure your Azure resources with Azure role-based access control (Azure RBAC) - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/)
	* [AZ-104: Manage identities and governance in Azure - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/paths/az-104-manage-identities-governance/)
	* [Enterprise-scale architecture organizational design principles - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/enterprise-scale-organization/)
* Videos
	* [AZ-900 Episode 28 | Azure Role-based Access Control (RBAC)](https://www.youtube.com/watch?v=4v7ffXxOnwU)
## Premiere Workshops
* [Modern Service Management Operational Roles and Tasks for Azure](https://datasheet.azureedge.net/offerings-datasheets/8513/EN.pdf)
* [Security: Identity Delegation – Fundamentals](https://datasheet.azureedge.net/offerings-datasheets/10924/EN.pdf)
* [WorkshopPLUS - Microsoft Azure: Security Best Practices - Closed Workshop](https://datasheet.azureedge.net/offerings-datasheets/6663/EN.pdf)
* [Activate Azure with Administration & Governance](https://datasheet.azureedge.net/offerings-datasheets/8230/EN.pdf)
* [Modern Service Management Governance for Azure](https://datasheet.azureedge.net/offerings-datasheets/9005/EN.pdf)