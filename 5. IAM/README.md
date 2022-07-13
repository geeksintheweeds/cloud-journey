# Azure RBAC
## Summary
Azure RBAC is the mechanism by which IAM policies can be configured and enforced on Azure resources.
## Key Points
* Azure AD is the shared identity boundary amongst all Azure Subscriptions in a tenant and all other Microsoft Cloud services using the Azure AD Tenant
* Azure RBAC roles are separate from Azure AD or EA Portal Roles
* Azure AD Global Admin role and Enterprise Administrator roles (Department Admin, Account Owner) present shadow admin paths to Azure Subscription Owner
* Azure Account Owners (EA Portal) are by default "Service Administrators" of the Azure Subscriptions under that Azure Account
* Azure RBAC = Principal + Role Definition + Assignment scope
* Roles can be assigned at the Management group, Subscription, Resource Group or even Resource level
* Managed Identities are a type of non-human principal stored in Azure AD for use within the Azure Control plane
* Service Principals are a type of non-human principal stored in Azure AD for use outside of the Azure Control Plane
* Azure Custom RBAC roles can be created at the subscription scope or tenant scope
* Azure RBAC roles can be used anywhere in the hierarchy under where they were created implicitly
* Azure RBAC roles created in a subscription can be used in other subscriptions explicitly through the use of the "Assignable Scope"
* Within Azure there are Management Plane permissions (actions) and Data Plane permissions (dataActions).
    * The ability to create a keyvault (Management Plane) vs the ability to create a key within a keyvault (data plane)
* The use of notActions and notDataActions within an RBAC role definition serve only to remove those permissions from a wildcarded permission set in the same RBAC Role definition.  They are NOT explicit denies.
* If a user has multiple RBAC roles assigned, the user has the aggregate permissions of all roles, and actions in one role will supercede notActions or notDataActions in another role.
* Deny assignments for Azure RBAC are only available as part of Blue Prints which are public preview (Not GA)
* Azure RBAC defines what access a user has to Azure resources where as Azure Policy defines what can and cannot be done with azure resources.  Azure Policies will trump Azure RBAC.
## Best Practices
* Use Built-In roles where possible
* When creating custom roles, start with a built-in role
* Store all custom roles at the tenant level or in an Identity Subscription
* Assign roles to Groups not users
* Use managed identities instead of service principals where possible
* Avoid assigning roles at the resource level where possible as it created excessive administrative overhead
* Utilize an external source of truth for tracking role assigment if possible (IGA)
* Monitor and Alert on use of subscription and management level privileged roles such as "Owner, Contributor, User Access Administrator"
* Consider restricting the use of Managed Identity, Service Principals in sandbox subscriptions
* Restrict the Azure RBAC Subscription Owner level roles to break glass accounts only
* When the need arises to create custom Azure RBAC roles, create reusable roles not one-off roles
## Checklist
- [ ] Review the organizations Management Group, Subscription and Resource Group structure and identify an Azure RBAC strategy
- [ ] Establish break glass Subscription Owner accounts
- [ ] Create Groups that align to Azure RBAC assignments
## Links
* [Azure Docs | Microsoft Docs](https://docs.microsoft.com/en-us/azure/role-based-access-control/overview)
* [Azure Docs | Microsoft Docs](https://docs.microsoft.com/en-us/azure/role-based-access-control/deny-assignments)
* [Service Principals vs Managed Identities | BLOG](https://www.007ffflearning.com/post/azure-spring-clean-demystifying-service-principal-and-managed-identities/)
## Learning
* Mslearn
	* [Secure your Azure resources with Azure RBAC | MS Learn](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/)
	* [Create custom roles for Azure Resources with RBAC | MS Learn](https://docs.microsoft.com/en-us/learn/modules/create-custom-azure-roles-with-rbac/)
* Videos
	* [Azure Role-Based Access Control Deep Dive](https://www.youtube.com/watch?v=qFoHDTxkQII)
	* [Azure Custom Roles](https://www.youtube.com/watch?v=29TPBeqrSSc)
	* [Azure Key Vault RBAC and Policy Deep Dive](https://www.youtube.com/watch?v=oYzFWOrZMKc)
## Premiere Workshops
* [WorkshopPLUS - Microsoft Azure: Identity 1 Day](https://datasheet.azureedge.net/offerings-datasheets/8230/EN.pdf)