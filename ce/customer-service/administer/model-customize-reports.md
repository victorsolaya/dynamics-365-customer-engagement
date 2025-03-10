---
title: "Model customization of historical and real-time analytics reports in Customer Service | MicrosoftDocs"
description: "Learn how to customize historical and real-time analytics reports in Dynamics 365 Customer Service using Power BI."
ms.date: 11/28/2023
ms.topic: article
author: Soumyasd27
ms.author: sdas
ms.reviewer: shujoshi
ms.custom: 
  - dyn365-customerservice
search.audienceType: 
  - admin
  - customizer
---

# Customize data models of historical and real-time analytics reports

[!INCLUDE[azure-ad-rename](../../includes/cc-azure-ad-rename.md)]

Use the extensibility feature in Microsoft Power BI to extend the out-of-the-box data models for the analytics reports in Customer Service and integrate with other datasets to create new custom metrics. You can customize the out-of-the-box standard reports and add your own KPIs to view the key metrics that are relevant to your organization. You can add custom metrics to the detail reports also.

The key capabilities of model customization include the ability to:

- Edit the out-of-the-box data model and add new metrics.

- Bring in your own custom entities from Dataverse or any other source and extend the Power BI data model.

- Publish the customized report to a specific Power BI workspace.

- Customize the report site map and enable users to access the reports natively from Customer Service workspace.

Enable data model customization for historical and real-time analytics reports in Customer Service admin center, and then do the following tasks:

1. Select a Power BI workspace.
1. Provision the data models and copy of reports.
1. Grant permissions for dataset and reports.
1. Embed customized reports back to Dynamics 365.
    
## Prerequisites

Before you begin, you must complete the following prerequisites:

- Your organization must have the Power BI Professional or Power BI Premium license for all supervisors and administrators.

- Enable insights features in Customer Service:

    - If you're enabling historical data model customization, you must enable at least one of the historical reports, such as Customer Service historical analytics, Omnichannel historical analytics, or knowledge analytics. More information: [Configure analytics and insights dashboards](configure-customer-service-analytics-insights-csh.md)
    - If you're enabling real-time data model customization, you must enable real-time analytics for Omnichannel. More information: [Configure analytics and insights dashboards](configure-customer-service-analytics-insights-csh.md)

- Create a Microsoft Entra ID security group:

    - Your Microsoft Entra ID administrator must create a security group with your preferred name in Microsoft Entra ID and add **Dynamics 365 Analytics** service account as a member of this security group. More information: [Create a basic group and add members using Microsoft Entra ID](/entra/fundamentals/how-to-manage-groups)

        The out-of-the-box **Service Principal Dynamics 365 Analytics** is used to deploy the data model and make changes to the Power BI workspace on behalf of Customer Service.

        Permissions within Power BI can be granted to groups only and not individual service principals, and therefore a group needs to be created.
        
    > [!NOTE]
    > In organizations where Dynamics 365 Analytics service account may not be available, you'll need to use the Dynamics CCA Data Analytics service account.

- Enable Power BI service features from the Power BI admin portal. The Power BI administrator must enable the following, either for the entire organization or for the security group created earlier:

     - [**Create workspace (new workspace experience)**](/power-bi/admin/service-admin-portal-workspace#create-workspaces-new-workspace-experience): Enabling this feature creates two workspaces, a managed workspace and a customer workspace to deploy Dynamics data model and reports.

    - [**Allow service principals to use Power BI APIs**](/power-bi/enterprise/service-premium-service-principal#enable-service-principals): This feature uses the Power BI APIs for creating workspaces, deploying reports and models.

    - **Allow DirectQuery connections to Power BI datasets**: When report authors build new metrics or bring more data sources, they create [composite models](/power-bi/transform-model/desktop-composite-models#managing-composite-models-on-power-bi-datasets), so DirectQuery needs to be enabled. Users who view reports built on top of data model in Dynamics 365 require this permission. Work with your Microsoft Entra ID administrator to identify a security group that has all the required Dynamics users.
  
    - **Allow XMLA endpoints and Analyze in Excel with on-premise datasets**: When report authors build new metrics or bring more data sources, they create [composite models](/power-bi/transform-model/desktop-composite-models#managing-composite-models-on-power-bi-datasets), so this feature needs to be enabled. Users who view reports built on top of data model in Dynamics 365 require this permission.
    
    - **Embed content in apps** (**Optional**): Enabling this feature embeds customized reports in Dynamics 365 ([Step 4: Embed customized reports back to Dynamics 365](#step-4-embed-customized-reports-back-to-dynamics-365)). Users who view the custom reports from Dynamics 365 Customer Service require this permission. Work with your Microsoft Entra ID administrator to identify a security group that has all the required Dynamics users.
        
- If you plan to use an existing Power BI workspace to host the copy of the out-of-the-box reports (customer workspace), make sure that the Dynamics Administrator (user login) enabling the model customization is a workspace administrator of that Power BI workspace.

## Enable Power BI data model customization

 1. In the Customer Service admin center site map, select **Insights** in **Operations**.
 1. On the **Insights** page in the **Report settings** section:
     1. For historical, select **Embedded Power BI extensibility - Historical data model customization** and then select **Manage**.
     1. For real time, select **Embedded Power BI extensibility - Real-time data model customization** and then select **Manage**.
 1. On the selected page, switch the **Enable embedded Power BI data model customization** toggle to **On**.

## Step 1: Select a Power BI workspace

Specify the Power BI workspace where the Dynamics data model and reports are provisioned.

1. From the Insights page, go to the data model for which you want to select a Power BI workspace.

1. Select **Create new workspace** or to use an existing workspace, select a workspace from the dropdown list.

1. Select **Save**. This action initiates the provisioning of the reports.

> [!NOTE]
> The specified workspace applies only to the customer's workspace. A new managed workspace is created by Microsoft for historical and real-time reports each, when configured. For more information, go to: [How data model customization works](../use/datamodel-overview.md#how-data-model-customization-works). You can also specify the same workspace for both historical and real-time analytics reports.

## Step 2: Provision the data models

It could take up to 24 hours for the provisioning to complete. You can leave the **Settings** page and check back after a few hours. Select **Refresh** to check the provisioning status.

## Step 3: Grant permissions for dataset and reports

After the report is provisioned, you must provide **Write** permissions for users who author reports in Power BI and **Read** permissions for supervisors and other consumers of the reports.

You must be a **Workspace Administrator** on both managed and customer workspaces (configured on Step 1) in Power BI to complete this step. By default, the user who starts the provisioning (Step 2) has the necessary permissions added.

:::image type="content" source="../media/step3-grant-permissions.png" alt-text="Image for step 3 grant read and write permissions":::

### Grant access to the Power BI data model

Report authors connect to the specified data model to build custom reports. When you select the **Power BI Data model** link, the managed workspace opens up and the details of the data model are displayed. Use the **Share** dialog to provide access to users by entering their email address. More information: [Share access to a dataset](/power-bi/connect-data/service-datasets-share).

You need to:

- Provide report authors with **Allow recipients to build content with the data associated with this dataset** access.

- For report viewers like supervisors, you may choose to share the dataset without providing any extra permissions.

### Grant permissions to the customized Power BI report (optional)

When you select the **Customized Power BI Report** link, the Power BI workspace where the sample reports are provided appears in a lineage view. These reports are the copy of your out-of-the-box reports and can be edited and modified. You must provide access to the workspace only if your organization plans on using these copies to develop reports.

From the lineage view, select **Access**, and provide **Contributor** access to your report authors and **Viewer** access to users who view these or any other reports built in this workspace. For more information on data permissions, go to: [Manage dataset access permissions (preview)](/power-bi/connect-data/service-datasets-manage-access-permissions). You must provide these permissions only if you plan to use these reports.  

## Step 4: Embed customized reports back to Dynamics 365

After your report authors create and publish the customized reports, you can allow Dynamics users to access these reports from the Customer service workspace.

1. Select the data model reports.

### [Historical data model customization](#tab/historicaldatamodelcustomization)

  - From the **Embedded Power BI extensibility - Historical data model customization** page, go to Step 4.
    :::image type="content" source="../media/embed-historical.png" alt-text="Select the historical reports you want to view on the site map.":::

### [Real-time data model customization](#tab/realtimedatamodelcustomization)

  - From the **Embedded Power BI extensibility - Real-time data model customization** page, go to Step 4.
    :::image type="content" source="../media/embed-realtime.png" alt-text="Select the real-time reports you want to view on the site map.":::

---

2. Select **Add report**. The **Add report** dialog appears.
3. Enter a preferred name in the **Report name** text box.
4. From the **Select Power BI report** dropdown list, select the Power BI report in the workspace.
5. Select **Add** and **Save**.

The dropdown list is populated with the reports in the workspace configured on Step 1. The preferred report name appears for your Dynamics users when they access the reports. You can add a maximum of 40 reports.

The customized reports site map in the Customer service workspace is shared between historical and real-time data model customization features. You can reorder the reports on both historical and real time admin pages. For both historical and real time, you can modify or delete reports added from the respective historical and real-time data model customization pages only.

> [!NOTE]
> Supervisor actions like assign, transfer, monitor, and force close aren't available for model customized reports.

## View customized reports

If you customized the Customer Service workspace app, you must complete the following steps to be able to view the reports.

1. On the Customer Service workspace app tile, select the ellipsis for **More Options**, and then select **Open in App Designer**.
1. Select **New**.
1. On the **New page** dialog, select **URL**, and then select **Next**.
1. Enter the following information, and then select **Add**
      - **URL**: [Organization Url]/main.aspx?pagetype=control&controlName=MscrmControls.Analytics.ModernReportingControl&data={"featureIds":"f2266eb4-226f-4cf1-b422-89c5f48b40cb,09c168be-efe2-4f08-a986-3aab7095c863"}
      - **Title** Customized Reports
1. From **Navigation**, select **Customized Reports**.
1. Enter the following information for **Display options**.
    - **Title**: Customized Reports
    - **Icon**: Select **Use web resource**.
    - **Select icon**: msdyn_/Analytics/imgs/CustomizedReportsIcon.svg
    - **ID**: CustomizedReportsSubArea
1. Select **Advanced Settings**, and then select the following checkboxes:
   - **SKU**: **All**, **On premise**, **Live**, and **SPLA**.
   - **Client**: **Web**.
   - **Outlook shortcut**: **Pass parameters** and **Offline availability**.
1. Select **Save**, and then select **Publish**.

### See also

[Customize the display of analytics reports](../use/customize-reports.md#customize-the-display-of-analytics-reports)  
[Introduction to Customer Service Insights](../implement/introduction-customer-service-analytics.md)  
[Configure Customer Service analytics and insights](configure-customer-service-analytics-insights-csh.md)  
[Configure Customer Service Analytics dashboards in Power BI](../implement/configure-customer-service-analytics-dashboard.md)  
[Configure Omnichannel historical analytics](oc-historical-analytics-reports.md)  
