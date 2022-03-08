# **Enable Availability Zone for Existing Region**

## **Introduction**
Customers who have existing Cosmos DB accounts deployed who want to leverage Availability Zones (AZ) may find that they are unable to configure them. If you view an existing region in the "Replicate data globally" blade, you will notice you can not change the state of the checkbox. Availability Zones (AZ) can only be configured at time of  deplyment: either when deploying a new account or a new region.

To deploy AZ to a new Cosmos DB account, "enable" AZ in the "Global Distribution" section of the new service wizard. 

![](https://github.com/Azure/mwr-mda-guild/blob/main/Guides/Cosmos%20DB/Cosmos%20DB%20Enable%20Availability%20Zone%20for%20existing%20region/images/cosmosdb-az-newAccount.png)

Or, when you are configuring a new region in your Cosmos DB account, you may notice that a checkbox is available to enable AZ:

![](https://github.com/Azure/mwr-mda-guild/blob/main/Guides/Cosmos%20DB/Cosmos%20DB%20Enable%20Availability%20Zone%20for%20existing%20region/images/cosmosdb-az-newRegion.png)

This guide shows you how to enable AZ for an existing Cosmos DB region. It requires manually migrating to a secondary region, deleting, and re-adding the primary region. This process is seemeless to the clients and there is no data-loss as Cosmos DB fails gracefully when performing a manual failover.

&nbsp;

### _**Note**: If AZ is not available when creating a new Cosmos DB account in your region of choice, or unavailable when creating a new region in your account, you may need to open a support ticket to request Azure Capacity for new AZ in your region._

&nbsp;

## **Steps**
First, if you do not have a secondary region configured in your Cosmos DB account, create a new one close to your primary region.

[Add global database regions using the Azure portal](https://docs.microsoft.com/en-us/azure/cosmos-db/sql/tutorial-global-distribution-sql-api?tabs=dotnetv2%2Capi-async#addregion)

Perform a manual failover by clicking on the "Manual Failover" button in the "Replicate data globally" blade. If it is grayed out, you have automatic failover configured. You wil need to disable automatic failover by clicking the "Automatic Failover" button and turning it to "OFF".

Now that your workload is transferred to a new region, you can delete and re-add your primary region. When you re-add, check the box for AZ. 

_See the note above if the checkbox is not available!_

Finally, manually failover from your secondary region to the primary region. 

