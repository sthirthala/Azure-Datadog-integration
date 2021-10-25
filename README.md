
# Azure-Datadog-integration

## Overview

Datadog is a monitoring and analytics platform for large-scale applications. It encompasses infrastructure monitoring, application performance monitoring, log management, and user-experience monitoring. Datadog aggregates data across your entire stack with 400+ integrations for troubleshooting, alerting, and graphing. You can use it as a single source for troubleshooting, optimizing performance, and cross-team collaboration.

Datadog's offering in the Azure Marketplace enables you to manage Datadog in the Azure console as an integrated service. This availability means you can implement Datadog as a monitoring solution for your cloud workloads through a streamlined workflow. The workflow covers everything from procurement to configuration. The onboarding experience simplifies how you start monitoring the health and performance of your applications, whether they're based entirely in Azure or spread across hybrid or multi-cloud environments.

You provision the Datadog resources through a resource provider named `Microsoft.Datadog`. You can create, provision, and manage Datadog organization resources through the [Azure portal](https://portal.azure.com/). Datadog owns and runs the software as a service (SaaS) application including the organization and API keys.

## Capabilities

Integrating Datadog with Azure provides the following capabilities:

- **Integrated onboarding** - Datadog is an integrated service on Azure. You can provision Datadog and manage the integration through the Azure portal.
- **Unified billing** - Datadog costs are reported through Azure monthly bill.
- **Single sign-on to Datadog** - You don't need a separate authentication for the Datadog portal.
- **Log forwarder** - Enables automated forwarding of subscription activity and resource logs to Datadog.
- **Metrics collection** - Automatically send all Azure resource metrics to Datadog.
- **Datadog agent deployment** - Provides a unified management experience of Datadog agents. Install and uninstall Datadog agents as extensions on Virtual Machines and Azure App Services.

# QuickStart: Get started with Datadog by creating new instance

In this quickstart, you'll create a new instance of Datadog. You can either create a new Datadog organization or [link to an existing Datadog organization](link-to-existing-organization.md).


## Find offer

Use the Azure portal to find Datadog.

1. Go to the [Azure portal](https://portal.azure.com/) and sign in.

1. If you've visited the **Marketplace** in a recent session, select the icon from the available options. Otherwise, search for _Marketplace_.

    ![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/marketplace.png)

1. In the Marketplace, search for **Datadog**.

1. In the plan overview screen, select **Set up + subscribe**.

 ![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/datadog-app-2.png)

## Create a Datadog resource in Azure

The portal displays a selection asking whether you would like to create a Datadog organization or link Azure subscription to an existing Datadog organization.

If you are creating a new Datadog organization, select **Create** under the **Create a new Datadog organization**

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/datadog-create-link-selection.png)

The portal displays a form for creating the Datadog resource.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/datadog-create-resource.png)

Provide the following values.

|Property | Description
|:-----------|:-------- |
| Subscription | Select the Azure subscription you want to use for creating the Datadog resource. You must have owner access. |
| Resource group | Specify whether you want to create a new resource group or use an existing one. A [resource group](../../azure-resource-manager/management/overview.md#resource-groups) is a container that holds related resources for an Azure solution. |
| Resource name | Specify a name for the Datadog resource. This name will be the name of the new Datadog organization, when creating a new Datadog organization. |
| Location | Select West US 2. Currently, West US 2 is the only supported region. |
| Pricing plan | When creating a new organization, select from the list of available Datadog plans. |
| Billing Term | Monthly. |

## Configure metrics and logs

Use Azure resource tags to configure which metrics and logs are sent to Datadog. You can include or exclude metrics and logs for specific resources.

Tag rules for sending **metrics** are:

- By default, metrics are collected for all resources, except virtual machines, virtual machine scale sets, and app service plans.
- Virtual machines, virtual machine scale sets, and app service plans with *Include* tags send metrics to Datadog.
- Virtual machines, virtual machine scale sets, and app service plans with *Exclude* tags don't send metrics to Datadog.
- If there's a conflict between inclusion and exclusion rules, exclusion takes priority

Tag rules for sending **logs** are:

- By default, logs are collected for all resources.
- Azure resources with *Include* tags send logs to Datadog.
- Azure resources with  *Exclude* tags don't send logs to Datadog.
- If there's a conflict between inclusion and exclusion rules, exclusion takes priority.

For example, the screenshot below shows a tag rule where only those virtual machines, virtual machine scale sets, and app service plans tagged as *Datadog = True* send metrics to Datadog.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/config-metrics-logs.png)
There are two types of logs that can be emitted from Azure to Datadog.

1. **Subscription level logs** - Provide insight into the operations on your resources at the [control plane](../../azure-resource-manager/management/control-plane-and-data-plane.md). Updates on service health events are also included. Use the activity log to determine the what, who, and when for any write operations (PUT, POST, DELETE). There's a single activity log for each Azure subscription.

1. **Azure resource logs** - Provide insight into operations that were taken on an Azure resource at the [data plane](../../azure-resource-manager/management/control-plane-and-data-plane.md). For example, getting a secret from a Key Vault is a data plane operation. Or, making a request to a database is also a data plane operation. The content of resource logs varies by the Azure service and resource type.

To send subscription level logs to Datadog, select **Send subscription activity logs**. If this option is left unchecked, none of the subscription level logs are sent to Datadog.

To send Azure resource logs to Datadog, select **Send Azure resource logs for all defined resources**. The types of Azure resource logs are listed in [Azure Monitor Resource Log categories](../../azure-monitor/essentials/resource-logs-categories.md).  To filter the set of Azure resources sending logs to Datadog, use Azure resource tags.

The logs sent to Datadog will be charged by Azure. For more information, see the [pricing of platform logs](https://azure.microsoft.com/pricing/details/monitor/) sent to Azure Marketplace partners.

Once you have completed configuring metrics and logs, select **Next: Single sign-on**.

## Configure single sign-on

If your organization uses Azure Active Directory as its identity provider, you can establish single sign-on from the Azure portal to Datadog. If your organization uses a different identity provider or you don't want to establish single sign-on at this time, you can skip this section.

To establish single sign-on through Azure Active directory, select the checkbox for **Enable single sign-on through Azure Active Directory**.

The Azure portal retrieves the appropriate Datadog application from Azure Active Directory. The app matches the Enterprise app you provided in an earlier step.

Select the Datadog app name.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/sso.png)

Select **Next: Tags**.

## Add custom tags

You can specify custom tags for the new Datadog resource. Provide name and value pairs for the tags to apply to the Datadog resource.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/tags.png)

When you've finished adding tags, select **Next: Review+Create**.

## Review + Create Datadog resource

Review your selections and the terms of use. After validation completes, select **Create**.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/review-create.png)

Azure deploys the Datadog resource.

When the process completes, select **Go to Resource** to see the Datadog resource.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/create/go-to-resource.png)

# Manage the Datadog resource

This article shows how to manage the settings for your Azure integration with Datadog.

## Resource overview

To see details of your Datadog resource, select **Overview** in the left pane.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/resource-overview.png)

The details include:

- Resource group name
- Location/Region
- Subscription
- Tags
- Single sign-on link to Datadog organization
- Datadog offer/plan
- Billing term

It also provides links to Datadog dashboards, logs, and host maps.

The overview screen provides a summary of the resources sending logs and metrics to Datadog.

- Resource type – Azure resource type.
- Total resources – Count of all resources for the resource type.
- Resources sending logs – Count of resources sending logs to Datadog through the integration.
- Resources sending metrics – Count of resources sending metrics to Datadog through the integration.

## Reconfigure rules for metrics and logs

To change the configuration rules for metrics and logs, select **Metrics and Logs** in the left pane.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/reconfigure-metrics-and-logs.png)

## View monitored resources

To see the list of resources emitting logs to Datadog, select **Monitored Resources** in the left pane.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/view-monitored-resources.png)

You can filter the list of resources by resource type, resource group name, location, and whether the resource is sending logs and metrics.

The column **Logs to Datadog** indicates whether the resource is sending logs to Datadog. If the resource isn't sending logs, this field indicates why logs aren't being sent to Datadog. The reasons could be:

- Resource doesn't support sending logs. Only resources types with monitoring log categories can be configured to send logs to Datadog.
- Limit of five diagnostic settings reached. Each Azure resource can have a maximum of five diagnostic settings. For more information, see [diagnostic settings](../../azure-monitor/essentials/diagnostic-settings.md).
- Error. The resource is configured to send logs to Datadog, but is blocked by an error.
- Logs not configured. Only Azure resources that have the appropriate resource tags are configured to send logs to Datadog.
- Region not supported. The Azure resource is in a region that doesn't currently support sending logs to Datadog.
- Datadog agent not configured. Virtual machines without the Datadog agent installed don't emit logs to Datadog.

## API Keys

To view the list of API keys for your Datadog resource, select the **Keys** in the left pane. You see information about the keys.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/keys.png)

The Azure portal provides a read-only view of the API keys. To manage the keys, select the Datadog portal link. After making changes in the Datadog portal, refresh the Azure portal view.

The Azure Datadog integration provides you the ability to install Datadog agent on a virtual machine or app service. If a default key isn't selected, the Datadog agent installation fails.

## Monitor virtual machines using the Datadog agent

You can install Datadog agents on virtual machines as an extension. Go to **Virtual machine agent** under the Datadog org configurations in the left pane. This screen shows the list of all virtual machines in the subscription.

For each virtual machine, the following data is displayed:

- Resource Name – Virtual machine name
- Resource Status – Whether the virtual machine is stopped or running. The Datadog agent can only be installed on virtual machines that are running. If the virtual machine is stopped, installing the Datadog agent will be disabled.
- Agent version – The Datadog agent version number.
- Agent status – Whether the Datadog agent is running on the virtual machine.
- Integrations enabled – The key metrics that are being collected by the Datadog agent.
- Install Method – The specific tool used to install the Datadog agent. For example, Chef or Script.
- Sending logs – Whether the Datadog agent is sending logs to Datadog.

Select the virtual machine to install the Datadog agent on. Select **Install Agent**.

The portal asks for confirmation that you want to install the agent with the default key. Select **OK** to begin installation. Azure shows the status as **Installing** until the agent is installed and provisioned.

After the Datadog agent is installed, the status changes to Installed.

To see that the Datadog agent has been installed, select the virtual machine and navigate to the Extensions window.

You can uninstall Datadog agents on a virtual machine by going to **Virtual machine agent**. Select the virtual machine and **Uninstall agent**.

## Monitor App Services using the Datadog agent as an extension

You can install Datadog agents on app services as an extension. Go to **App Service extension** in left pane. This screen shows the list of all app services in the subscription.

For each app service, the following data elements are displayed:

- Resource Name – Virtual machine name.
- Resource Status – Whether the app service is stopped or running. The Datadog agent can only be installed on app services that are running. If the app service is stopped, installing the Datadog agent is disabled.
- App service plan – The specific plan configured for the app service.
- Agent version – The Datadog agent version number.

To install the Datadog agent, select the app service and **Install Extension**. The latest Datadog agent is installed on the app service as an extension.

The portal confirms that you want to install the Datadog agent. Also, the application settings for the specific app service are updated with the default key. The app service is restarted after the install of the Datadog agent completes.

Select **OK** to begin the installation process for the Datadog agent. The portal shows the status as **Installing** until the agent is installed. After the Datadog agent is installed, the status changes to Installed.

To uninstall Datadog agents on the app service, go to **App Service Extension**. Select the app service and **Uninstall Extension**

## Reconfigure single sign-on

If you would like to reconfigure single sign-on, select **Single sign-on** in the left pane.

To establish single sign-on through Azure Active directory, select **Enable single sign-on through Azure Active Directory**.

The portal retrieves the appropriate Datadog application from Azure Active Directory. The app comes from the enterprise app name you selected when setting up integration. Select the Datadog app name as shown below:
 
![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/reconfigure-single-sign-on.png)
 
## Change Plan

To change the Datadog billing plan, go to **Overview** and select **Change Plan**.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/datadog-select-change-plan.png)

The portal retrieves all the available Datadog plans for your tenant. Select the appropriate plan and click on **Change Plan**.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/datadog-change-plan.png)
  
## Disable or enable integration

You can stop sending logs and metrics from Azure to Datadog. You'll continue to be billed for other Datadog services that aren't related to monitoring metrics and logs.

To disable the Azure integration with Datadog, go to **Overview**. Select **Disable** and **OK**.
 
![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/disable.png)

To enable the Azure integration with Datadog, go to **Overview**. Select **Enable** and **OK**. Selecting **Enable** retrieves any previous configuration for metrics and logs. The configuration determines which Azure resources emit metrics and logs to Datadog. After completing the step, metrics and logs are sent to Datadog.
 
![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/enable.png)

## Delete Datadog resource

Go to **Overview** in left pane and select **Delete**. Confirm that you want to delete Datadog resource. Select **Delete**.

![](https://github.com/sthirthala/Azure-Datadog-integration/blob/main/media/manage/delete.png)

If only one Datadog resource is mapped to a Datadog organization, logs and metrics are no longer sent to Datadog. All billing stops for Datadog through Azure Marketplace.

If more than one Datadog resource is mapped to the Datadog organization, deleting the Datadog resource only stops sending logs and metrics for that Datadog resource. Because the Datadog organization is linked to other Azure resources, billing continues through the Azure Marketplace.
