# Azure Tools for Identifying Components in Use within a Subscription

1. **Azure Resource Graph Explorer**:
    - A powerful tool to query and explore resources across subscriptions using a query language similar to KQL (Kusto Query Language).
    - Allows you to list all resources, filter by resource type, region, tags, or other properties.
    - Can provide a holistic view of all components and their relationships in your subscription.

2. **Azure Portal - Resource Groups**:
    - Navigate to the **Resource Groups** blade in the Azure Portal to see all resources organized by their groupings.
    - This provides a basic overview of resources within each resource group but lacks detailed querying or filtering.

3. **Azure Cost Management + Billing**:
    - While focused on cost, it provides insights into which resources and services are being used, their associated costs, and usage patterns.

4. **Azure Monitor - Service Map**:
    - If enabled, **Service Map** automatically discovers application components and their interconnections.
    - It provides a visual map of dependencies between virtual machines, processes, and other Azure components.

5. **Azure Advisor**:
    - A tool that provides recommendations for optimizing your Azure environment.
    - It can surface information about unused or underutilized resources.

6. **Azure Management Groups**:
    - If you have multiple subscriptions, using **Management Groups** allows you to organize and analyze resources across subscriptions.

7. **Third-Party Tools**:
    - Tools like **CloudHealth**, **CloudCheckr**, or **Spot by NetApp** can provide detailed insights into Azure resources and offer additional management features.

8. **Microsoft Assessments**:
    - **Azure Security Center**: Offers security assessments to help you evaluate the security posture of your resources, including recommendations for improving security controls.
    - **Azure Migrate**: Helps assess and plan the migration of on-premises workloads to Azure, offering detailed insights into resource compatibility and readiness.
    - **[Azure Well-Architected Review](https://learn.microsoft.com/en-us/assessments/azure-architecture-review/)**: Provides assessments based on the **Well-Architected Framework** to evaluate your workloads in terms of reliability, security, performance, cost optimization, and operational excellence.
    - **Azure Cost Management + Billing**: Provides cost assessments to help identify underutilized resources, opportunities for cost-saving, and recommendations for more efficient usage.
    - **Azure Policy and Blueprints**: Helps assess compliance with organizational or regulatory standards, allowing you to enforce governance at scale across your subscription.

Each of these tools caters to different levels of detail and use cases, from simple overviews to advanced query-based insights. If you need a comprehensive analysis, **Azure Resource Graph Explorer** is particularly versatile.
