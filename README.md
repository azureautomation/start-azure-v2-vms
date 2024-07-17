# ﻿Start Azure V2 VMs 

  

             

  

DESCRIPTION 

This runbook connects to Azure using system assigned identity and starts all V2 VMs in an Azure subscription or resource group or a single named V2 VM. 

  

You can attach a recurring schedule to this runbook to run it at a specific time. 

  

REQUIRED 

1. An Automation Account system assigned identity with at least Virtual Machine Contributor permission on the VM’s, resource group, or the subscription. To use a user assigned identity you can pass the Account ID as a parameter. 

  

2. The subscription ID of the VM’s. 

  

OPTIONAL 

  

3. A ResourceGroupName input parameter value that allows scoping the V2 VMs to a particular resource group. 

  

4. A VMName input parameter that allows specification of a single V2 VM. 

    

NOTES 

- Link Conditions to determine how to get the VMs -Following the 'Connect to Azure' activity there are three sequence links that have conditions set. These conditions are mutually exclusive and will direct the workflow to only one of the connected activities to get VMs. 

  

- Merge VMs activity -The 'Merge VMs' activity is used to merge the output of the immediately preceding activities.  By merging the output into a single activity, which then re-outputs the objects, the downstream activities, like 'Start VM' are able to refer to a single activity for input data.  At design time, we don't know which of the immediately preceding activities will run, so 'Start VM' doesn't know which activity to refer to for input data.  By creating 'Merge VMs', 'Start VM' has a single activity to refer to for input. 

  

AUTHOR 

Azure Automation Team 

  

LAST EDIT 

2023-5-3 

  

RELEASE NOTES 

  

2016-5-9 First release 

  

2016-10-22 Handle changes to the output object properties from Start-AzureRmVm 

  

2023-5-3 The runbook converted to support Az modules and authenticating using a managed identity 

#> 

  

  

![Image](https://github.com/azureautomation/start-azure-v2-vms/raw/master/startazurev2vm.png) 

  

 

     

TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories. 

  

# Setup Tutorial 

  

To download and configure this runbook, do the following:  

  

1. Navigate to https://portal.azure.com then search for and select **Automation Accounts**.  

2. Click **Create**.  

3. Select the Subscription, Resource group, and region. Enter a name for the Automation account.  


  

4. Click **Review + Create**.  

5. Click **Create**.  

6. When the deployment is complete, go to the resource.  

7. Go to the **Identity** blade and verify that System assigned status is set to **On**.  

  

 

  

8. Under **permissions**, select **Azure role assignments**.  

9. Select **Add role assignment (Preview)**.  

10. Select the appropriate scope. Under **Role**, select **Virtual Machine Contributer**. Click **Save**.  

  

NOTE: It is recommended to select the least privileged scope possible.  

  

11. Navigate back to the Automation Account and under **Process Automation**, select **Runbooks**.   

12. Click **Create**.  

13. Select **Browse from gallery** then click **Click here to browse from gallery**.  

14. Search for and select **Start Azure V2 VMs**.  

15. Click **Select**.  

16. Enter a name for the runbook and click **Review + Create**.  

17. Click **Create**.  

18. It should redirect you to the Edit Graphical Runbook interface. Select **Publish** and click **Yes**.  

 

 

  

# Test the configuration  

  

1. Navigate to the runbook and in the **Overview** blade, click **Start**.  

2. Enter the subscription ID and optionally a ResourceGroupName and VMName.  

  

NOTE: By entering a subscription ID, you will start all VM’s in the subscription. If you enter a ResourceGroupName, you will start all VM’s in the resource group. To start a specific VM, you must enter both the VMName and the ResourceGroupName where it resides.  

  

3. Click **Start**.  

4. Verify that the VM(s) start as expected.  

  

# Configure the VM(s) to start on a schedule  

  

To configure a schedule for a runbook, follow the guidance in MIcrosoft’s [official documentation](https://learn.microsoft.com/azure/automation/manage-runbooks#schedule-a-runbook-in-the-azure-portal). 

 
