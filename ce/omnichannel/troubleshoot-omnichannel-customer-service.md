---
title: "Troubleshoot Omnichannel for Customer Service | MicrosoftDocs"
description: "Learn how to troubleshoot the issues you may face while working on Omnichannel for Customer Service."
keywords: ""
author: kabala123
ms.author: kabala
manager: shujoshi
applies_to: 
ms.date: 09/11/2019
ms.service: dynamics-365-customerservice
ms.topic: article
ms.assetid: 2507DF5E-99CF-4AF9-BAEF-5B9C7B43ECF7
ms.custom: 
---

# Troubleshoot Omnichannel for Customer Service

[!INCLUDE[cc-use-with-omnichannel](../includes/cc-use-with-omnichannel.md)]

Use the following list of troubleshooting topics to quickly find information to solve your issue.

## Omnichannel provisioning fails due to expired Teams Service Principal

### Issue:

If your tenant has an expired Office 365 license, then the Omnichannel for Customer Service provisioning fails in your organization.

### Resolution:

To avoid the provisioning failure, you must remove the **Teams Service Principal** in **Azure Active Directory**. Follow the steps to remove **Teams Service Principal**.

[Step 1: Identify Teams Service Principal in Azure Active Directory](#step-1-identify-teams-service-principal-in-azure-active-directory)

[Step 2: Use PowerShell to remove Microsoft Teams Service Principal](#step-2-use-powershell-to-remove-microsoft-teams-service-principal)

#### Step 1: Identify Teams Service Principal in Azure Active Directory

1.	Sign in to the [Azure portal](https://portal.azure.com/).
2.	Select **Active Directory** in the left pane.
3.	Select **Enterprise Applications**.
4.	Type **Microsoft Teams** in the search box.
5.	Copy the **Object ID** and **Application ID** against **Microsoft Teams** and save it for future use. Ensure that the Application Id is  `cc15fd57-2c6c-4117-a88c-83b1d56b4bbe` as this Id is same for every tenant.

   > [!div class=mx-imgBorder]
   > ![Microsoft Teams object and app Id](media/teams-object-appid.png "Microsoft Teams object and app Id")

#### Step 2: Use PowerShell to remove Microsoft Teams Service Principal
1.	Select **Start**, type **PowerShell**, and right-click **Windows PowerShell** and select **Run as administrator**.  <br>
![Run PowerShell as an administrator](media/powershell.png "Run PowerShell as an administrator")

2.	Select **Yes** on the **User Control** dialog to allow the application to make changes.
3.	Type the `Install-Module AzureAD` command in the Powershell window, and press **Enter**. This command installs the PowerShell commands for interacting with Azure Active Directory. <br>
![Execute command](media/powershell2.png "Execute command")

4.	PowerShell prompts whether to trust the repository. Type **Y** for yes and press **Enter**.  <br>
![Execute command](media/powershell3.png "Execute command")

5.	Type the `Connect-AzureAD` command in the PowerShell window, and press **Enter**.
This establishes a connection with the tenant's Azure Active Directory, so you can manage it using Powershell.
6.	Sign in to your organization as a tenant admin.
7.	Type the `Remove-AzureADServicePrincipal -ObjectID <ObjectID>` command in the PowerShell window. Replace **<ObjectID>** with the object ID you had stored earlier. This command deletes the expired Teams service principal from Azure Active Directory.

   > [!Note]
   > Right click in the PowerShell window to paste the Object ID.

The Microsoft Teams Service Principal has been removed from your organization. You can try to provision Omnichannel for Customer Service again.


## Chat widget icon does not load on the portal

### Issue: 

Chat icon doesn't load on the portal. The chat icon URL which was configured as default doesn't load.

### Resolution:

Open Chat Settings, navigate to Design tab and change **Logo** field and use an icon URL of your choice.

1. Sign in to Omnichannel for Customer Engagement.
2. Select the **Omnichannel Administration** app.
3. Go to **Administration** > **Chat**.
4. Select a chat widget from the list.
5. Select the **Design** tab.
6. Specify the URL of the icon you want to use in the **Logo** field.
7. Select **Save** to save the record.

## Chat not getting initiated on starting a new chat from portal 

### Issue

A message stating **Sorry, we're not able to serve you at the moment** is shown to the customers when they start a chart on the portal. The possible issues might be: 
- Agents not configured in the Queue.
- Allowed Presence is not updated in the work stream: The default work streams that are shipped out-of-the-box, does not have **Allowed Presence** values in the work stream.

   > [!div class=mx-imgBorder]
   > ![Sorry, we are not able to serve you at this moment message on portal chat widget](media/oceh/chat-widget-not-able-serve.png "Sorry, we are not able to serve you at this moment")

### Resolution:

 To configure agents in the queue, follow these steps:

 1. Sign in to Omnichannel for Customer Engagement.
 2. Select the **Omnichannel Administration** app.
 3. Go to **Queues & Users** > **Queues**
 4. Select the queue from the list.
 5. In the **Users (Agents)** section, select **Add Existing User** to add existing agents to the queue.
 6. On the **Lookup Records** pane, select the agents to add, and then select **Add**.
 7. Select **Save** to save the record.


To Update default **Allowed Presence** in the Live Work Stream, follow these steps:

1. Sign in to Omnichannel for Customer Engagement.
2. Select the **Omnichannel Administration** app.
3. Go to **Work Distribution Management** > **Work Streams**.
4. Select a record from the list.
5. In the Work Distribution tab, under the Work Distribution section, type **Available**. Select the check box to add it. Similarly, type **Busy** and then select the check box to add it.
6. Select **Save** to save the record.

## Chat widget does not load on the portal

### Issue: 

Chat widget does not load on the portal. The Location option for the chat widget might be configured incorrectly.

### Resolution:

Delete the **Widget location** location of the chat widget and again create it.

To delete and add **Widget location** for the chat widget, follow these steps:

1. Sign in to Omnichannel for Customer Engagement.
2. Select the **Omnichannel Administration** app.
3. Go to **Administration** > **Chat**.
4. Select a chat widget from the list.
5. Select the **Location** tab.
6. Select a record in the **Widget Location** section, and select **Delete**.
7. Select **Save**.
8. Select **+ Add** in the **Widget Location** section to add a record. Quick create pane of the chat widget location appears.
9. Specify the following.

   | Field | Value |
   |---------------------------|-----------------------------------------|
   | Title | Type the title of record. |
   | Value | The website domain where the chat widget must be displayed. The domain format should not include the protocol (http or https). For example, the website is  `https://contoso.microsoftcrmportals.com`. Now, the value is  `contoso.microsoftcrmportals.com`. | 
10. Select **Save** to save the record.
11. Go to the website and check if the chat widget loads.

## Dashboards do not appear in Omnichannel for Customer Service active dashboards view

### Issue:

When you use the Omnichannel for Customer Service app on Unified Service Desk or on web, the **Active Omnichannel Agent Dashboard** view doesn't show certain dashboards like Tier 1 Dashboard, Tier 2 Dashboard, Knowledge Manager, and My Knowledge Dashboard.

### Resolution:

As a system customizer or administrator, you must manually add these dashboards using app designer.

To add the dashboards using app designer, follow these steps:

1. Go to `https://<orgURL>.dynamics.com/apps`.
2. Select the ellipsis (**...**) button in the **Omnichannel for Customer Service** app tile. <br>
    ![Sign in to Omnichannel for Customer Service](media/oceh-sign-in.png "Sign in to Omnichannel for Customer Service")
3. Select **OPEN IN APP DESIGNER**. The App Designer opens in a new tab.
4. Select **Dashboards** in the canvas area. The **Components** pane in the right side shows the list of **Classic Dashboards** and **Interactive Dashboards**.
5. Select the following dashboards under **Interactive Dashboards**.<br>
    - Knowledge Manager
    - My Knowledge Dashboard
    - Tier 1 Dashboard
    - Tier 2 Dashboard <br>
    ![Add dashboards in the app designer canvas area](media/oceh-app-designer-add-dashboard.png "Add dashboards")
6. Select **Save** and then select **Publish**.

## Pre-imported Unified Service Desk configurations in Customer Engagement organization

### Issue:

Dynamics 365 for Customer Engagement organization that you create from **demos.microsoft.com** have pre-imported sample Unified Service Desk configuration.

If you import the Unified Service Desk - Omnichannel for Customer Service package without deleting the existing configuration in the new demo org, you see an error after signing in to Unified Service Desk client application. The reason for the issue is multiple sample Unified Service Desk configurations cannot exist in an Customer Engagement instance.

   > [!div class=mx-imgBorder]
   > ![The hosted application couldn't be created](media/oceh/usd-client-error.png "The hosted application couldn't be created")


### Resolution:

You must delete the existing sample solutions before importing the Omnichannel for Customer Service - Unified Service Desk package. The pre-imported sample solutions are as follows:

- USDISHCustomization or USDWebClientCustomization (one of these solutions would be present depending on the org template)
- USDUnifiedInterfaceCustomization
- DynamicsUnifiedServiceDesk
- UiiForMicrosoftDynamicsCRM

After you delete the solutions, import the Unified Service Desk - Omnichannel for Customer Service package.

To delete the solutions, follow these steps:

1. Sign in to [!INCLUDE[pn_microsoftcrm](../includes/pn-microsoftcrm.md)] apps.
2. Choose **Settings** > **Solutions** on the nav bar.
4. Select one of the solutions on the **Solutions** page by selecting the check box, and then choose **Delete**. You are prompted to confirm uninstalling a managed solution. Choose **OK** to proceed. <br>
   - USDISHCustomization or USDWebClientCustomization (one of these solutions would be present depending on the org template)
   - USDUnifiedInterfaceCustomization
   - DynamicsUnifiedServiceDesk
   - UiiForMicrosoftDynamicsCRM
      > [!NOTE]
      > You must the delete the solutions in the following order:
      > 1. USDISHCustomization or USDWebClientCustomization
      > 2. USDUnifiedInterfaceCustomization
      > 3. DynamicsUnifiedServiceDesk
      > 4. UiiForMicrosoftDynamicsCRM2011
      > 
      >  You must follow the order to remove the solutions because some of the components in the solution depend on the components in the other solution.
5. After the solution is removed, repeat the steps to delete the other solutions.

## Unable to launch Unified Service Desk client application

### Issue:

When you sign in to Unified Service Desk, you see the following error. 

**APPLICATION_HOST_ERR_NO_CONFIGURED_APPS: applications are configured for your use.**

   > [!div class=mx-imgBorder]
   > ![Unified Service Desk application error](media/oceh/usd-application-host-error.png "Unified Service Desk application error")

The issue is due to the package deployment failure.

### Resolution:

You must the deploy the Unified Service Desk - Omnichannel for Customer Service package again. To learn more, see [Deploy Unified Service Desk – Omnichannel for Customer Service package](administrator/omnichannel-customer-service-package.md#deploy-unified-service-desk---omnichannel-for-customer-service-package).

## An error occurred in the communication panel

### Issue: 

After you sign in to the Unified Service Desk client application, you see the following error message.

**An error occurred in the Communication panel. Restart Unified Service Desk and try again. (Error Code - AAD_ID_MISMATCH - Azure ADID mismatched with logged-in user id)**

   > [!div class=mx-imgBorder]
   > ![Unified Service Desk application error](media/oceh/usd-communication-panel-error.png "Unified Service Desk application error")

While signing in to Unified Service Desk you must enter the Customer Engagement apps credentials and sign in, and again, you are shown a dialog to enter credentials to connect to Customer Engagement server. 
When you enter different credentials, this issue occurs. 

### Resolution:

If you use **IE process** to host applications, open Internet Explorer browser, and go to http://login.microsoftonline.com/logout.srf. The URL signs you from office.com. Now, sign in to Unified Service Des client application and try again. 

If you use **Chrome process** to host applications, go to `C:\Users\<USER_NAME>\AppData\Roaming\Microsoft\USD` and delete the **CEF** folder. Now, sign in to Unified Service Des client application and try again. 

## Communication panel doesn't load in Omnichannel for Customer Service app

### Issue:

Communication panel doesn't load in Omnichannel for Customer Service app:

- When a record doesn't exist in the Channel Integration Framework app.
- When configurations don't sync.

### Resolution:

- Create a Channel Integration Framework record with the following values. 

   | Field | value |
   |-------------------------------------------|--------------------------------------------------|
   | Name | Omnichannel |
   | Label | Omnichannel |
   | Channel URL | \<Chat control cdn url>?uci=true&env=<env>&ocBaseUrl=\<oc endpoint\>&ucilib=\<crm org url\>/webresources/Widget/msdyn_ciLibrary.js |
   | Enable Outbound Communication | No |
   | Channel Order | 0 |
   | API Version | 1.0 |
   | Select Unified Interface Apps for the Channel | Omnichannel for Customer Service |
   | Select the Roles for the Channel | <li>Omnichannel administrator</li>  <li>Omnichannel agent</li> <li>Omnichannel supervisor</li> |

   To learn how to create a record, see [Configure a channel provider for your Dynamics 365 organization](/dynamics365/customer-engagement/developer/channel-integration-framework/configure-channel-provider-channel-integration-framework).

- To sync the configurations, remove the channel and roles, add it again and save the record.

   1. Sign in to Dynamics 365 for Customer Engagement apps.
   2. Select the drop-down button on Dynamics 365 and select **Channel Integration Framework**.
   3. Select the **Omnichannel** record from the list.
   4. Remove **Omnichannel for Customer Service** from the **Select Unified Interface Apps for the Channel** section.
   5. Add **Omnichannel for Customer Service** again in the **Select Unified Interface Apps for the Channel** section.
   6. Remove **Omnichannel agent**, **Omnichannel supervisor**, and **Omnichannel administrator** from the **Select the Roles for the Channel** section.
   7. Add **Omnichannel agent**, **Omnichannel supervisor**, and **Omnichannel administrator** again in the **Select the Roles for the Channel** section.
   8. Select **Save** to save the record.
   9. Sign in to Omnichannel for Customer Service app and check if the communication panel loads.


## Agents not receiving chat in Omnichannel for Customer Service

### Issue:

As an agent, you aren't receiving chat in the Omnichannel for Customer Service app. The issue is caused when you receive the chats in Customer Service Hub app.

### Resolution:

You must remove the Customer Service Hub app from the channel provider configuration in the Channel Integration Framework app.

1. Sign in to Dynamics 365 for Customer Engagement apps.
2. Select the drop-down button on Dynamics 365 and select **Channel Integration Framework**.
3. Select the record that is related to omnichannel.
4. Remove **Customer Service Hub** from the **Select Unified Interface Apps for the Channel** section.
5. Select **Save** to save the record.

## User presence isn’t loading or it’s showing Unknown

### Issue:

The issue might happen due to the following reasons:

- Azure Active Directory consent is not available for Omnichannel for Customer Service app.
- Agent doesn't the Omnichannel agent role privileges.
- Capacity and Default presence is not.

### Resolution:

Perform the following:

- Contact your administrator to verify Azure Active Directory consent is given to the Omnichannel for Customer Service application on your tenant. Go to [Authorize access](https://go.microsoft.com/fwlink/?linkid=2070932) to get access. For more information, see [Provision for Omnichannel for Customer Service](administrator/omnichannel-provision-license.md). 
- Ensure the agent account has **Omnichannel Agent**. For more information, see [Assign roles and enable users for Omnichannel Engagement Hub](administrator/add-users-assign-roles.md).
- Ensure the agent account has values set for **Capacity** and **Default presence** within the Omnichannel Administration app. To learn more, see [Create and manage users and user profiles](administrator/users-user-profiles.md).

## Agent dashboard isn’t loading or is giving an authorization error

## Issue:

The issue might happen due to the following reasons:

- Azure Active Directory consent is not available for Omnichannel for Customer Service app.
- Agent doesn't the Omnichannel agent role privileges.
- Agent is not assigned to any queue.

### Resolution:

Perform the following:

- Contact your administrator to verify Azure Active Directory consent is given to the Omnichannel for Customer Service application on your tenant. Go to [Authorize access](https://go.microsoft.com/fwlink/?linkid=2070932) to get access. To learn more, see [Provide data access consent](administrator/omnichannel-provision-license.md#provide-data-access-consent).
- Ensure the agent account has the role **Omnichannel Agent**. For more information about the relevant roles, see [Understand roles and their privileges](administrator/add-users-assign-roles.md#understand-roles-and-their-privileges). 
- Ensure the agent account is assigned to at least one queue in the Omnichannel Administration app. To learn more, see [Manage users in Omnichannel for Customer Service](administrator/users-user-profiles.md).
