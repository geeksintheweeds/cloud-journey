# Azure Foundations

## Overview
Establishing a strong foundation is critical to the success of cloud adoption.  This section provides an overview of the fundamental concepts that make up the foundations of an organization's Azure estate.  This is not meant to replace official documentation, MS Learn trainings, or professional services.  It is a high level overview of the concepts and key best practices observed by the authors over years of working with a wide range of customers across many industries.

## Sections
* [EA Portal](#ea-portal)
* [Management Groups](#management-groups)
* [Subscriptions](#subscriptions)
---
---
# EA Portal
## Summary
Securing an organization's Azure footprint begins with the EA (Enterprise Agreement) Portal.  Many organizations focus on the cost and billing function of the EA Portal and are unaware of the security risks the EA Portal can present to their Azure resources. In addition to cost and billing, the EA Portal is the administration point for Enterprise Enrollments and Azure Accounts. This capability makes it critically important to properly secure access to the EA Portal.
## Key Points
* EA Portal is used for administration in addition to cost and billing.
* EA Portal is used to manage access to Enterprise Enrollments and Azure Accounts.
* EA Portal supports authentication with both accounts sourced from Azure AD (referred to as Work and School accounts) and Microsoft Accounts.
* Administrators of an Enterprise Enrollment have full control of the Azure Accounts created under the enrollment.
* The individual(s) with control over the email address associated with an Azure Account Owner inherits the Azure RBAC Role of owner on any subscription created under or transferred to the Azure Account.
* The email address associated with an Azure Account must be a valid email address. This is because it is needed for communication from Microsoft.
* The audit logs for the EA Portal are only available by opening a support ticket with Microsoft.
* Enterprise enrollments can span Azure AD tenants allowing you to create subscriptions in multiple tenants all charging back to the same enterprise enrollment.
## Best Practices
* Use only Azure AD Authentication (Work and School accounts). 
* For privileged roles in the EA Portal such as enrollment or department administrator, look at applying existing privileged access patterns. For example, you could use shared accounts where the credentials are secured in a credential management system such as Thycotic or CyberArk.
* Grant business users, such as the accounting department, read-only roles.
* Consider creating separate Azure Account for non-prod and production subscriptions to limit blast radius.
* Do not use the Azure AD Identity with the email address associated with the Azure Account for administration of Azure resources. 
* Use separate identities for EA Portal Administration, Azure Administration, Azure AD Administration, and Microsoft 365 services.
## Checklist
- [ ] Is your instance of the EA Portal configured for both Azure AD and Microsoft account authentication? Check the [Auth level](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/ea-portal-troubleshoot#issues-adding-a-user-to-an-enrollment) in the EA Portal. 
- [ ] Have you documented who has access to the EA Portal and what they have permission to do?
- [ ] Have you implemented the best practices for the EA Portal that are referenced above?
- [ ] Have you created any Azure Accounts? How are you handling access to the email addresses associated with the Azure Accounts?
- [ ] Have you documented the processes for managing the lifecycle of Azure Accounts?
- [ ] What are your processes for break glass / emergency access to the EA portal?
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
* [Activate Azure with Administration & Governance](https://datasheet.azureedge.net/offerings-datasheets/8230/EN.pdf)
* [Modern Service Management Governance for Azure](https://datasheet.azureedge.net/offerings-datasheets/9005/EN.pdf)
---
---

# Management Groups
## Summary
Managing the access, security, and compliance of an organization's IT estate can be challenging.  Azure cloud introduces management groups which help to address these challenges. Management groups are logical containers for subscriptions which contain Azure resources.  They are a construct where Azure RBAC (Permissions) and Azure Policy (Controls) can be applied and enforced to child resources such as child management groups and subscriptions. Establishing a management structure that aligns with organizational goals is critical to the design of the foundation of the Azure platform. Included in this repository and the links below are some common management group patterns that the authors have seen implemented successfully across organizations.
## [Key Points](https://www.cloud-architekt.net/azure-ea-management-security-considerations/)
* Management groups are hiearcharal in nature and there can be multiple children to a parent but only a single parent to a child.
* Management groups can have child management groups and subscriptions.
* Subscriptions can be the child of a single management group.
* Each Azure AD tenant contains a root management group.
* Management groups can be nested underneath other management groups up to a hard limit of six levels.
* Management groups have their own [Activity Logs](https://docs.microsoft.com/en-us/azure/governance/management-groups/overview#audit-management-groups-using-activity-logs) separate from subscription.
## Best Practices
* Keep the hierarchy flat and limited to 4 levels (6 levels hard cap).
* Always start with a single organizational Management Group under the root management group.
* Tightly control access to management groups limiting it to non-human/automation accounts where possible.
* Create a [default management group](https://docs.microsoft.com/en-us/azure/governance/management-groups/how-to/protect-resource-hierarchy#setting---default-management-group) where newly create subscriptions that are not created with a parent management group are placed. The default management group should have a minimum set of access and security controls.
* Use management groups for Azure RBAC inheritance and Azure Policy inheritance.
* Apply Azure Policies at the highest level possible but avoid applying at the root management. This will avoid having to use exceptions and utilize highly privileged roles to administer it.
* Consider putting sandboxed workloads in a separate management group to allow exploration of new services.
* [Enable Azure RBAC for Management Groups](https://docs.microsoft.com/en-us/azure/governance/management-groups/how-to/protect-resource-hierarchy#setting---require-authorization) to limit who can create management groups.
* [Enable diagnostic logging for mangement group Activity Logs](https://docs.microsoft.com/en-us/rest/api/monitor/management-group-diagnostic-settings/create-or-update)
* Apply the [Azure Security Benchmarks initiative](https://docs.microsoft.com/en-us/azure/governance/policy/samples/azure-security-benchmark) in audit mode to the organizational top-level management under the root management group. This will provide a baseline as to the security posture of the Azure estate.
## Checklist
- [ ] Do you have a proposed architecture and design for management groups?
- [ ] What were the requirements that drove the design?
- [ ] Have the management groups been created?
- [ ] Have established a process for managing the lifecycle of management groups?
- [ ] Has Azure RBAC been applied to the management groups?
- [ ] Have Azure Policies been applied to the management groups?
- [ ] Have subscriptions been moved to the appropriate management groups?
- [ ] Have you established a default management group?
- [ ] Have you applied the Azure Security Benchmarks initiative in audit mode?
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
Subscriptions are logical containers for Azure resources and act as permissions, policy and billing boundary. Subscriptions are child objects of an Azure Account and can be created [in the Azure Portal](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/create-subscription) or the EA Portal if the Azure Account is associated with an Enterprise Enrollment. The [strategy around the usage of subscriptions](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/decision-guides/subscriptions/) is driven by the organization's cloud strategy. They may be organized based upon business unit, workload classification, geography, or a mix of each. Included in this repository and the links below are some common subscription strategies that the authors have seen implemented successfully across organizations.
## Key Points
* [Limited to a certain number of resources](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits) in order to accomodate the multi-tenant nature of the public cloud.
* Limits in a subscription are either soft limits or hard limits. Engage your Microsoft team when you have requirements to go beyond a limit.
* Blast radius where a user or group assigned the RBAC Owner role has full permissions on all resources within the subscription.
* Compliance boundary where Azure Policy can be applied to enforce organizational operations and security controls.
* Cost boundary which includes all resources in the subscription.
* Created either in the Azure Portal, EA Portal, or via [API](https://docs.microsoft.com/en-us/azure/cost-management-billing/manage/programmatically-create-subscription).
* The user or group who controls the Azure Account used to create the subscription has full control over the resources in the subscription. 
* Subscriptions must be associated to a single Azure AD tenant.
* Resources within a subscription can only be attached to Virtual Networks in the same subscription.
* Transferring subscriptions between Azure AD tenants will result in the loss of all Azure RBAC and Azure Policy assignments.
## Best Practices
* Subscriptions used by the organization for non-production and production should be created from an Enterprise Enrollment and should be associated to the production Azure AD tenant.
* Work with your Microsoft support team to block subscriptions that are not sourced from the Enterprise Enrollment. This would include subscriptions offers like Visual Studio and Pay-As-You-Go subscriptions.
* Subscriptions used by individual employees for the purposes of learning and experimentation should be Visual Studio Subscriptions and should not be associated to any of the organization's Azure AD tenants.
* Establish formalized process for the subscription lifecycle.
* Separate subscriptions for shared infrastructure services from subscriptions containing resources for specific workloads.
* Use separate subscriptions for non-production and production
* Use separate subscriptions as boundaries between workloads with differing compliance requirements.
* Avoid granting human users the Contributor or Owner role on a subscription. Consider using less-privileged [built-in Azure RBAC roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/built-in-roles) or creating [custom Azure RBAC roles](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles).
* Monitor subscription resource limits using Azure Advisor.
## Checklist
- [ ] Have you established process for managing the lifecycle of subscriptions? Does this take into account the management group design?
- [ ] Have you established a baseline configuration for both operations and security for new subscriptions?
- [ ] Have you established an RBAC model for the different types of subscriptions (shared services, identity, networking, workload, etc)?
- [ ] Have you created any subscriptions? Do you know which Azure Account the subscriptions are associated with?
- [ ] Have you secured the identities for owners of the Azure Accounts for each subscription?
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