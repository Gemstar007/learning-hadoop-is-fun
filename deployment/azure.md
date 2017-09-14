## Azure deployment 

Using Azure-cli 2.0 to deploy vms in azure using commandline.

## Prerequisites 

* Linux machine (ubuntu) for running azure cli (should work on windows as well)
* Azure subscription 

## Setup

* Install azcli 
	* apt-get update 
	* apt-get install -y libssl-dev libffi-dev python-dev build-essential
	* curl -L https://aka.ms/InstallAzureCli | bash
		* (select 'Y' for default options)
* Login to azure 
	* az login 
		* follow the steps shown
	* az account set -- subscription <your-subscription-id>
* Create a group (All azure resources must be in a group)
	* az group create -l westcentralus -n <rgroup-name>
	
	
## Azure templates 
Azure can use json templates to specify the work that needs to be done. I have checked in the required files 
* template.json (actual tasks/resources to be done/created)
* parameter.json ( variables to the template for helping reusing the templates)

## create a vm from templates
* az group deployment create -g <rgroup-name> --template-file ./template.json --parameters @parameters.json

## delete a vm and related things 
It us usefult to delete nic and storage account in our case otherwise it will conflict when we recreate the vm. 

* az vm delete -g agveryberry -n agvbnode02
* az network nic delete -g agveryberry -n agvbnode02122
* az storage account delete  -g agveryberry -n agvbnode02storage


## Further investigations
* How to run a shell script in azure vm from azure cli
* how to use amrabri to deploy a blue print
* how to use azure storage sources from within hdfs 
* how to use active directory with hadoop ( azureAD, Apache Ranger)

## Resources

* [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates/tree/master/201-customscript-extension-public-storage-on-ubuntu)
* [customscript-azure-ubuntu](https://github.com/Azure/azure-quickstart-templates/tree/master/201-customscript-extension-azure-storage-on-ubuntu)
* [Azure blob storage from hadoop](https://alexeikh.wordpress.com/2014/01/14/expanding-hdp-hadoop-file-system-to-azure-blob-storage/)


	
	
	




