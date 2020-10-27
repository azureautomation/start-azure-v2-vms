Start Azure V2 VMs
==================

            

DESCRIPTION
This Azure Automation Graphical PowerShell runbook connects to Azure using an Automation Run As account and starts all V2 VMs in an Azure subscription or in a resource group or a single named V2 VM.  You can attach a recurring schedule to this runbook
 to run it at a specific time.  The associated runbook StopAzureV2Vm is also available for download.


REQUIRED
1. An Automation connection asset called AzureRunAsConnection that contains the information for connecting with Azure using a service principal.  To use an asset with a different name you can pass the asset name as a input parameter to this runbook or
 change the default value for the AzureConnectionAssetName input parameter.


OPTIONAL
2. A ResourceGroupName input parameter value that allows scoping the V2 VMs to a particular resource group.3. A VMName input parameter that allows specification of a single V2 VM.


NOTES
- Link Conditions to determine how to get the VMs -Following the 'Connect to Azure' activity there are three sequence links that have conditions set.  These conditions are mutually exclusive and will direct the workflow to only one of the connected activities
 to get VMs.

- Merge VMs activity -The 'Merge VMs' activity is used to merge the output of the immediately preceding activities.  By merging the output into a single activity, which then re-outputs the objects, the downstream activities, like 'Start VM'  are able
 to refer to a single activity for input data.  At design time, we don't know which of the immediately preceding activities will run, so 'Start VM' doesn't know which activity to refer to for input data.  By creating 'Merge VMs', 'Start VM' has a
 single activity to refer to for input.


AUTHOR
System Center Automation Team 


LAST EDIT
2016-10-22


RELEASE NOTES


2016-5-9 First release


2016-10-22 Handle changes to the output object properties from Start-AzureRmVm
#>


 


![Image](https://github.com/azureautomation/start-azure-v2-vms/raw/master/startazurev2vm.png)


 

 

        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
