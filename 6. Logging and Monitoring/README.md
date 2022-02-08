# Azure Logging and Monitoring

## Overview
Logging and monitoring represent the foundational primitives of Operationalization and Security within the Azure estate.  They should be some of the first considerations beyond IAM, even before networking as it is critical to have insights into everything that happens within the environment from day 1

## Sections
* [Logging](#logging)
* [Monitoring](#monitoring)
---
---

# Logging
## Summary
As an organization starts to think about their Governance requirements and where to start with Azure Policy, the first logical step is logging.  Every organization has logging requirements of some kind and generally they are pretty straight forward with regards to collection, retention, access.  Where things can sometimes get complicated is when Application teams, Operation teams and Security teams have different requirements.  Historically this has led to fragmented logging strategies at many organizations which leads to overhead in the forms of cost, maintenance and complexity.  Not to mention it reduces the effectiveness of logs when there is not a single pane of glass for all logs.  This can sometimes get further complicated in hybrid and multi-cloud enterprises as organizations attempt to balance the various requirements new requirements around cost and desires to use cloud native tools.  It is important for organizations to carefully plan out their logging strategy as an organization wholistically first then apply those principals to the cloud.  Many organizations will end up with hybrid strategies where they send logs to multiple places to balance requirements.  For example, an organization may send all logs to an Azure Event Hub which is integrated with their enterprise SIEM for security insights, but also send logs to an Azure Log Analytics Workspace for their operations teams but maintain shorter retention to minimize costs.
## Key Points
* Types of Azure Logs
	* Platform - Provide information about Azure Resource Manager Create, Update, Delete (CRUD) operations
		* Subscriptions and Management Groups
		    * Azure Activity Log (ex: Creation of a Keyvault)
	* Tenant
		* Azure AD Logs
			* Sign-Ins - Who is logging in and how
			* Audit - Changes to the tenant
			* Provisioning - Provisioning and Changes to integrated SaaS solutions like workday or service now
	* Resource - Provide information about events raised as part of Azure Resource Usage
		* Diagnostic Settings - Information about activities within the resource
			* Example: Modification of secrets in keyvault
		* Metrics - Summarized information about usage and performance of the resource
			* Example - # of access attempts per hour for secret in a keyvault
		* Process - Events as a result of custom processing like alerts
	* OS - OS logs can be captured via agents
	* Custom - Custom logs can be ingested to Log analytics via API
	* Application
		* Application Insights 
* Destinations
	* Event Hub - To integrate with 3rd party SIEM
	* Storage Account - Long term storage and 3rd party integration
    * Log Analytics Workspace - Operational Use within Azure and 3rd party integration
## Best Practices
* Use as few Log Analytics Workspaces as possible to achieve best price and performance as well as provide single pane of glass
*  Use as few Event Hubs as possible to minimize operational overhead/complexity
* Separate Event Hub use cases might be region specific or separate log criteria for different siems
* Export logs to Azure Storage if they are required to be kept for long term retention
* Establish up front the networking patterns for log data.  This is important as changes to the networking pattern for logging with the use of Private Endpoints can have global impact across a customer's azure estate
* Be selective of the types of logs sent to Azure Log Analytics to minimize costs
* Diagnostic and Audit logs should be enabled and should all go to the central LAW or Central Event Hub
* Use azure policy to enforce logging configuration
* Azure Storage Immutable storage with WORM (Write Once, Read Many) can be used to make data non-erasable, no-modifiable
* Use Traffic Analytics within Azure Network Watcher to parse NSG flow logs for easier consumption
* Use table level retention to minimize costs on data that is not required for long periods
* Use table level RBAC to restrict sensitive logs
* Even when a 3rd party SIEM is used, consider native cloud tooling (Azure Log Analytics) for operational purposes
## Checklist
- [ ] Does your existing SIEM have a standardized integration pattern
- [ ] Do you require Private Endpoints (private Ips to send log data to)
- [ ] Have you documented organizational logging requirements
	* Security Logging
    	* Storage - Where do you plan to store it
    	* Retention - How long do you need to keep it
    	* Logging Level - What do you need to capture
    	* Presentation - How do you plan to consume the logs
    	* Alerting - How do you plan to generate alerts
    	* Integration - What integrations are required
    	* Access - Who needs access to what logs, how will that access be granted
	    * Responsibilities - Who is responsible for capture, configuration, review, 
	* Operational Logging
		* Storage - Where do you plan to store it
		* Retention - How long do you need to keep it
		* Logging Level - What do you need to capture
		* Presentation - How do you plan to consume the logs
		* Alerting - How do you plan to generate alerts
		* Integration - What integrations are required
		* Access - Who needs access to what logs, how will that access be granted
        * Responsibilities - Who is responsible for capture, configuration, review, 
## Links
* [Overview of Azure platform logs - Azure Monitor | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/platform-logs-overview)
* [Logging and reporting decision guide - Cloud Adoption Framework | Microsoft Docs](https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/decision-guides/logging-and-reporting/)
* [Create diagnostic settings to send platform logs and metrics to different destinations - Azure Monitor | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings?tabs=CMD)
* [Tutorial - Stream logs to an Azure event hub | Microsoft Docs](https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/tutorial-azure-monitor-stream-logs-to-event-hub)
* [Configure the log analytics wizard in Azure AD | Microsoft Docs](https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/tutorial-log-analytics-wizard)
* [Analyze activity logs using Azure Monitor logs | Microsoft Docs](https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/howto-analyze-activity-logs-log-analytics)
* [Audit Management Groups using activity logs | Microsoft Docs](https://docs.microsoft.com/en-us/azure/governance/management-groups/manage#audit-management-groups-using-activity-logs)
* [Introduction to flow logging for NSGs - Azure Network Watcher | Microsoft Docs](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)
* [Azure traffic analytics | Microsoft Docs](https://docs.microsoft.com/en-us/azure/network-watcher/traffic-analytics)
* [Monitor VM Diagnostic Logs using Azure Event Hub | by Aditya Vishwekar | Medium](https://medium.com/@adityavishwekar/monitor-vm-diagnostic-logs-using-azure-event-hub-573e5dffef3e)
* [3rd Party SIEM Examples | Splunk Add-on for Microsoft Cloud Services | Splunkbase](https://splunkbase.splunk.com/app/3110/#/overview)
* [3rd Party SIEM Examples | Splunking Microsoft Azure Monitor Data – Part 1 – Azure Setup | Splunk](https://www.splunk.com/en_us/blog/tips-and-tricks/splunking-microsoft-azure-monitor-data-part-1-azure-setup.html)
* [3rd Party SIEM Examples | Splunking Microsoft Azure Network Watcher Data | Splunk](https://www.splunk.com/en_us/blog/tips-and-tricks/splunking-microsoft-azure-network-watcher-data.html)
## Learning
* Mslearn
	* [AZ-104: Monitor and back up Azure resources - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/paths/az-104-monitor-backup-resources/)
	* [Configure Log Analytics - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/configure-log-analytics/)
	* [Configure and manage Azure Monitor - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/azure-monitor/)
	* [Analyze your Azure infrastructure by using Azure Monitor logs - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/analyze-infrastructure-with-azure-monitor-logs/)
	* [Introduction to Event Hubs - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/modules/intro-to-event-hubs/)
	* [Overview of Azure platform logs - Azure Monitor | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/platform-logs-overview)
* Videos
	* [Microsoft Azure Master Class Part 9 - Monitoring and Security](https://www.youtube.com/watch?v=hTS8jXEX_88)
	* [What is Azure Monitor?](https://www.youtube.com/watch?v=eSutaPE80PM)
## Premiere Workshops
* [Activate Azure with Azure Monitor](https://datasheet.azureedge.net/offerings-datasheets/9080/EN.pdf)
* [WorkshopPLUS - Azure: Modern Monitoring and Management](https://datasheet.azureedge.net/offerings-datasheets/8786/EN.pdf)  
* [WorkshopPLUS - Microsoft Azure: Application, Monitoring and Diagnostics for IT Professionals](https://datasheet.azureedge.net/offerings-datasheets/4270/EN.pdf) 
* [WorkshopPLUS - Microsoft Azure: Azure Monitor Introduction 1 day](https://datasheet.azureedge.net/offerings-datasheets/9484/EN.pdf)
* [WorkshopPLUS - Microsoft Azure: Azure Monitor Visualization 1 day](https://datasheet.azureedge.net/offerings-datasheets/9487/EN.pdf)

---
---
# Monitoring
## Summary
The logical progression from Logging is Monitoring.  Where logging is the collection of important/relevant data about the environment, monitoring is what to do with that data.  In addition, logging topics tend to focus on activity log, audit logs etc.  Whereas monitoring focuses on the collection of telemetry and performance data and metrics.  Historically in the enterprise, this was often multiple separate product suites, but increasingly over the years these capabilities have been converging such that we now see most vendors in the space offering both sides of the coin.  This is no different in Azure where Azure Monitor offers full stack monitoring capabilities.  The Azure Monitor service offering is a collection of services, agents and integrations that together make up the full Azure Monitor suite.  Most organizations that adopt azure leverage Azure Monitor at least to some degree given the use of Azure PaaS services and the native capabilities Azure Monitor provides.
## Key Points
* List Key Points
* Not trying to recreate public documentation
* Just include the important gotchas
## Best Practices
* Establish monitoring requirements up front and prioritize
* Use alerts and notifications to bring attention to resources when necessary and move away from "dashboard watching"
* Utilize interactive dashboards and workbooks for exploration, review, deep dive and troubleshooting
* Utilize azure policy to enforce monitoring requirements (deployment of agents or collection of data)
* Empower app owners to manage their own application level monitoring
## Checklist
- [ ] Include Actionable tasks here that typically map back to key points or best practices.  They can be decision points or they can be actual tasks.  Point here is to give the practitioner actual work to pgoress the effort.
	* Have you decided on X vs Y vs Z?
- [ ] Now that you have decided, have you implemented?
	* What are the steps to implement?
	* Have you documented the decision as well as reasoning/justification?
    * Who is doing the work?
    * These can often be put into a project plan and deliverables by the project or program PM.  Dont get too specific, keep it high level but at the same time include the important points
## Links
* [Azure Docs | Microsoft Docs](https://docs.microsoft.com/en-us/azure/?product=popular)
* [Azure Docs | Microsoft Docs](https://docs.microsoft.com/en-us/azure/?product=popular)
* [Azure Inventory Dashboard | Blog](https://www.cloudsma.com/2020/10/ultimate-azure-inventory-dashboard/)
## Learning
* Mslearn
	* [Link MS Learn and other learning resources here | MS Learn](https://docs.microsoft.com/en-us/learn/)
	* [Microsoft Certified: Azure Fundamentals - Learn | Microsoft Docs](https://docs.microsoft.com/en-us/learn/certifications/azure-fundamentals/)
* Videos
	* [Full EA Portal Onboarding Session](https://www.youtube.com/watch?v=OiZ1GdBpo-I)
	* [EA Portal User Management](https://www.youtube.com/watch?v=621jVkvmwm8)
	* [EA Portal Usage Summary Video](https://www.youtube.com/watch?v=Cv2IZ9QCn9E)
## Premiere Workshops
* [Activate Azure with Azure Monitor](https://datasheet.azureedge.net/offerings-datasheets/9080/EN.pdf)
* [WorkshopPLUS - Azure: Modern Monitoring and Management](https://datasheet.azureedge.net/offerings-datasheets/8786/EN.pdf)  
* [WorkshopPLUS - Microsoft Azure: Application, Monitoring and Diagnostics for IT Professionals](https://datasheet.azureedge.net/offerings-datasheets/4270/EN.pdf) 
* [WorkshopPLUS - Microsoft Azure: Azure Monitor Introduction 1 day](https://datasheet.azureedge.net/offerings-datasheets/9484/EN.pdf)
* [WorkshopPLUS - Microsoft Azure: Azure Monitor Visualization 1 day](https://datasheet.azureedge.net/offerings-datasheets/9487/EN.pdf)
