# Azure Foundations

## Overview
Strong foundations are critical to the long term safety and stability of a building (such as a datacenter) and the cloud is no different.  This section provides an overview of some of the fundamental concepts that make up the foundations of an organizations Azure Estate.  This is not meant to replace official documentation, MS Learn trainings or professional services.  It is simply a high level overview of the concepts and some key best practices obnserved by Azure Cloud Solutions Architects over dozens of customers and several years.

## Sections
* [EA Portal](#ea-portal)
* [Management Groups](#management-groups)
* [Subscriptions](#subscriptions)
---
---
# EA Portal
## Summary
When securing an organizations Azure Estate, it all starts with the EA portal.  Most understand that the EA portal is a cost and billing function but what is often missed is that the EA Portal Administrator has the ability to modify account owners and thus subscription owners.  From the perspective of the organizations Azure estate the EA Administrator has full access.  This is a commonly misunderstood administrative access path.  Most organizations think of the EA portal as solely a cost and billing function and do not realize the "Shadow Admin" type of access it has.
## Key Points
* EA Portal is an Administrative function as well as Cost Management/Billing
## Best Practices
* Use Azure AD Authentication only (Work and School accounts) and avoid using Microsoft Live accounts
* For privileged roles, use shared accounts where credentials are secured in a password/credential/secret management system and email address is accessible to multiple individuals. (EA Admins, Account Owners, Department Admins)its
* Consider creating separate Azure Account for non-prod and production subscriptions to limit blast radius.
	* Account Owners are Owners of Subscriptions so having a single Account Owner over BOTH prod/non-prod subscriptions introduces the risk of accidental changes to production.
* Do not use the Account Owner ID for administration of Azure resources. 
	* Use separate accounts for EA Portal Administration vs Azure Portal administration vs Azure AD Administration
* Do not use the same accounts for Administrative access in multiple places (EA Portal, Azure Portal, Azure AD, M365)
* No account should be used in any two portals
## Checklist
- [ ] Who has permissions to the EA portal?
	* Have you documented the access model and approval process?
- [ ] How are you securing access to the EA portal and the EA accounts?
	* You should vault/secure the EA accounts
	* You should use privileged access service for access to these accounts
    * Are those Microsoft accounts or sourced from Azure AD
- [ ] Have you started creating Accounts yet?
	* Who are the owners of those accounts?
	* Are you using shared accounts?
- [ ] What is your process for creating subscriptions?
	* At the minimum you should have a documented process, even if it is manual to control the creation of subscriptions.
	* This helps prevent subscription bloat
	* Ensures proper governance, tagging, billing, ownership, administration etc
	* You can improve the process by tying into the API with your ITSM solution and automation.
- [ ] What are your processes for break glass, emergency access to the EA portal
	* Recommended that you have two cloud local accounts sourced from azure AD that are separate from the Azure AD global admins
## Links
* [Azure EA portal administration | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/ea-portal-administration)
* [Create Azure subscriptions programmatically | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/programmatically-create-subscription)
* [Get started with the Azure Enterprise portal | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/ea-portal-get-started)
* [Understand admin roles for Enterprise Agreements (EA) in Azure | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/understand-ea-roles)
* [Cloud-Architekt.net | Security considerations of Azure EA management and potential privilege escalation](https://www.cloud-architekt.net/azure-ea-management-security-considerations/)
## Learning
* Mslearn
	* [Build great solutions with the Microsoft Azure Well-Architected Framework - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/paths/azure-well-architected-framework/)
	* [Azure Fundamentals part 1: Describe core Azure concepts (AZ-900) - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/paths/az-900-describe-cloud-concepts/)
	* [Enterprise-scale architecture organizational design principles - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/enterprise-scale-organization/)
* Videos
	* [Full EA Portal Onboarding Session](https://www.youtube.com/watch?v=OiZ1GdBpo-I)
	* [EA Portal User Management](https://www.youtube.com/watch?v=621jVkvmwm8)
	* [EA Portal Usage Summary Video](https://www.youtube.com/watch?v=Cv2IZ9QCn9E)
## Premiere Workshops
* Activate Azure with Administration & Governance (https://datasheet.azureedge.net/offerings-datasheets/8230/EN.pdf)
* Modern Service Management Governance for Azure (https://datasheet.azureedge.net/offerings-datasheets/9005/EN.pdf)
---
---


# Management Groups
## Summary
Once an organization has settled on an access model for the EA portal, some basic R&R on Azure and a RACI of common tasks, the work can begin designing the organizations actual Azure Estate.  The first primitive is the management group structure.  Management groups are logical containers for subscriptions.  They are a construct where Azure RBAC (Permissions) and Azure Policy (Controls) can be applied with enforcement pushed down and inherited by child management groups and subscriptions.  There are a few common models for Management groups linked below but an organization should think about where lines are drawn with regards to access and controls as to how to formulate their structure.  For example, separating production vs non-production in order to apply differing permissions or separating public facing workloads vs internal facing workloads.
## Key Points
* List Key Points
* Not trying to recreate public documentation
* Just include the important gotchas
## Best Practices
* Keep the hierarchy flat and limited to 4 levels (6 levels hard cap)
* Always start with a single organizational Management Group under the root
* Tightly control access to MGs limiting it to non-human/automation accounts
* Create a default management group to apply bare minimum level of controls
* Use management groups for RBAC inheritance and governance (policy) inheritance 
* Apply Policies at the highest level possible but avoid applying at the root to avoid having to manage exclusions at inherited scopes
* Consider putting sandboxed workloads in a separate management group to allow exploration of new services
* Enable Azure RBAC for Management Groups [link](https://docs.microsoft.com/en-us/azure/governance/management-groups/how-to/protect-resource-hierarchy#setting---require-authorization)
* Examples
    * Prod/Non-Prod
    * Regional
    * By Regulatory Requirement
## Checklist
- [ ]Do you have a proposed architecture and design for Management Groups?
- [ ]What is the thought process around the design?
- [ ] Have the management groups been created?
- [ ]Have Azure Policies been applied to the management groups?
- [ ]Have subscriptions been moved to the appropriate management groups?
- [ ]Have you established a default management group
## Links
* [Management group and subscription organization - Cloud Adoption Framework | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/management-group-and-subscription-organization)
* [Azure management groups documentation | Microsoft Docs](https://docs.microsoft.com/en-us/azure/governance/management-groups/)
* [How to protect your resource hierarchy - Azure Governance - Azure governance | Microsoft Docs](https://docs.microsoft.com/en-us/azure/governance/management-groups/how-to/protect-resource-hierarchy#setting---require-authorization)
* https://docs.microsoft.com/en-us/azure/governance/management-groups/how-to/protect-resource-hierarchy#setting---default-management-group
## Learning
* Mslearn
	* [Enterprise-scale architecture organizational design principles - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/enterprise-scale-organization/)
	* [Describe core Azure architectural components - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/azure-architecture-fundamentals/)
* Videos
	* [Microsoft Azure Master Class Part 3 - Governance](https://www.youtube.com/watch?v=cIh_Nfl67T0)
	* [How to organize subscriptions with Management Groups - YouTube](https://www.youtube.com/watch?v=4v9_6duE25s)
	* [Azure Management Groups Overview 1/10/2019](https://www.youtube.com/watch?v=jOprhCxnEAg)
	* [How to organize subscriptions with Management Groups](https://www.youtube.com/watch?v=4v9_6duE25s)
	* [Exam AZ-900 Microsoft Azure Fundamentals Study Guide Episode 44 - Management Groups](https://www.youtube.com/watch?v=wY6dLkvcG4c)
## Premiere Workshops
* [Activate Azure with Administration & Governance](https://datasheet.azureedge.net/offerings-datasheets/8230/EN.pdf)
* [Modern Service Management Governance for Azure](https://datasheet.azureedge.net/offerings-datasheets/9005/EN.pdf)
---
---


# Subscriptions
## Summary
The next logical container below Management Groups are Subscriptions.  Subscriptions are created by Azure Accounts through the Enterprise Admin portal (or API).  They act as permissions, policy and billing boundaries.  For many organizations they are a major construct for delineation between business lines, apps of different risk profiles and even central IT groups.  The closest analogies to other clouds would be AWS Accounts or GCP Projects but with some significant differences to both.  Subscription strategy significantly impacts and is impacted by the organizational cloud strategy.  An organization that seeks to "democratize" the cloud may opt for a lot of Subscriptions, while an organization building a one off workload in the cloud may seek to minimize the number of subscriptions. 
## Key Points
* Limit Boundary (Azure Resource Limits)
    * These are real limits that need to be considered, for example 1000 VMs sounds like a lot but could easily be exceeded in large AVD deployments
* Some limits can be increased via support (such as VM cores)
* Authorization and Administrative Boundary (Azure RBAC), Blast Radius Boundary
* Compliance Boundary (Azure Policy)
* Cost Boundary
*  Provisioned by Azure Accounts in the EA Portal
* Azure Accounts from EA Portal also have Administrative permissions over the Subscriptions in the Azure Portal
* Subscriptions share the Identity boundary of the Azure AD Tenant they are joined to.
* Example Subscription Models
## Best Practices
* Establish formalized process for the creation of new subscriptions
* Separate Subscriptions for core infrastructure services vs workloads to limit blast radius
* Use Subscriptions as a boundary for workloads with specific governance requirements such as PCI
* Remember that resources within a subscription can only use a virtual network within the same subscription
* Separate Subscriptions for sandbox and non-prod workloads
* Leverage MSDN subscriptions for true sandbox purposes
* Avoid creating subscriptions and resources non-prod azure tenants
* Do not grant "Contributor" or "Owner" roles standing access to Subscriptions
    * Most access can be configured using built in Azure RBAC Roles or derivates of
* Monitor subscription resource limits via the Azure Advisor
## Checklist
- [ ]Have you settled on a subscription structure that builds on the Management Group Structure?
- [ ]Have you settled on a subscription provisioning process?
- [ ]Have you settled on an RBAC model for the subscriptions
- [ ]Have you created the initial subscriptions necessary to begin building out the Azure Estate
    * Alternatively have you built out brownfield or greenfield subscriptions
- [ ]Have you secured the "Owner" accounts for the subscription via shared vaulted credentials or application of organizational privileged access patterns
## Links
* [Azure Subscription Limits | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits)
* [Subscription Decision Guide | Cloud Adoption Framework](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/decision-guides/subscriptions/)
* [Manage Azure Subscription Policies | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/manage-azure-subscription-policy#subscriptions-entering-aad-directory)
* [Management group and subscription organization | Cloud Adoption Framework](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/enterprise-scale/management-group-and-subscription-organization)
* [Get Alerts as you approach your Azure resource quotas | Microsoft Docs](https://docs.microsoft.com/en-us/archive/blogs/tomholl/get-alerts-as-you-approach-your-azure-resource-quotas)
* [Sample Script to track Azure Resource Quotas in Azure Monitor | github](https://github.com/DaFitRobsta/PowerShell/tree/3008ebca44da79635785ddc33bbe348811986d6e/Monitoring/SubscriptionQuotas)
* [Sample Script and workbook to track Azure Resource Quotas in Azure Monitor | github](https://github.com/vanessabruwer/scripties/tree/master/Azure%20Subscription%20Limits)
## Learning
* Mslearn
	* [Enterprise-scale architecture organizational design principles - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/enterprise-scale-organization/)
	* [Describe core Azure architectural components - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/azure-architecture-fundamentals/)
* Videos
	* [Microsoft Azure Master Class Part 3 - Governance](https://www.youtube.com/watch?v=cIh_Nfl67T0)
	* [How to organize subscriptions with Management Groups - YouTube](https://www.youtube.com/watch?v=4v9_6duE25s)
	* [Azure Tutorial - Tenants, Subscriptions & Resource Groups Explained](https://www.youtube.com/watch?v=FAbqJqr93v8)
	* [Exploring the Real Relationship Between Azure AD and Azure Subscriptions](https://www.youtube.com/watch?v=sXurr46f3HA)
    * [Learn azure subscription types](https://www.youtube.com/watch?v=MgTUYIiPn2g)
## Premiere Workshops
* [Activate Azure with Administration & Governance](https://datasheet.azureedge.net/offerings-datasheets/8230/EN.pdf)
* [Modern Service Management Governance for Azure](https://datasheet.azureedge.net/offerings-datasheets/9005/EN.pdf)