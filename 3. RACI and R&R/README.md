# Roles and Responsibilities + RACI
## Summary
As soon as an organization starts to secure the EA portal access, they arrive at the question of "Who should have access?".  This leads to the next logical discussion which is around Roles and Responsibilities.  This section is not about IAM or Azure RBAC specifically, as those come later but rather about organizational roles, responsibilities and RACI.  Every org should have a clear RACI and R&R chart.  It will not be possible to classify EVERYTHING but there are certain functions that are critical up front and if they are appropriately defined it at least provides a starting point for future discussions.  It is common for organizations who are already mature in other clouds to assume that this step can be skipped but it is important to understand that Azure works differently in certain critical areas to other clouds and especially on prem so even if a mature RACI and R&R exists, it should be revisited with a Microsoft CSA for alignment to Azure.  The most obvious difference is the Identity plane.  Azure is one big shared Identity boundary.  All subscriptions associated with an Azure AD tenant share that Azure AD tenant as an Identity and Authentication boundary.  Individual subscriptions are an Authorization boundary.  This is good and bad, it allows Microsoft to leverage incredibly powerful features of Azure AD like conditional access, HOWEVER it necessitates that a bit more planning and governance go into building out an organizations Azure estate before turning the dev community loose.  In other clouds, a sandbox environment can be stood up that is completely isolated from the larger enterprise where there is near 0 risk to the org.  In Azure that is a bit more difficult since even sandbox environments share the Identity plane.

## Key Points
* List Key Points
* Not trying to recreate public documentation
* Just include the important gotchas
## Best Practices
* Establish Roles and Responsibilities up front before starting to build.  You will likely have to change it but provides a starting point
* Start with a baseline RACI as you start to outline high level tasks and activities for Azure
* Even if you have mature R&R & RACI, be sure to revisit through the context of Azure
* Be sure to include all important and relevant parties, Azure AD is a shared Identity plane across all Microsoft clouds so include the relevant parties
## Checklist
- [ ] Have you decided on roles and responsibilities for Azure
- [ ] Have you translated those roles and responsibilities to actual permissions within azure and builtin or custom RBAC roles?
- [ ] Have you outlined common tasks and activities in azure in the form of a RACI (Use the RACI Toolkit as an example)
## Links
* [Aligning responsibilities across teams - Cloud Adoption Framework | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/organize/raci-alignment)
* [Azure RACI-Toolkit: Toolkit to help operationalize Microsoft Azure (github.com)](https://github.com/mattfeltonma/Azure-RACI-Toolkit)
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