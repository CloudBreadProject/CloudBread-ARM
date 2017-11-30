# CloudBread-ARM
This project is automatic provision script for CloudBread service instances on Cloud.

This document introduces the recipe for the deploy CloudBread to Azure. First, we deploy Azure resources used in CloudBread with ARM (Azure Resource Manager). Next, we install CloudBread on the resources we deployed in the previous step. Finally, we need to create database.
Now, you can deploy your game server very easy with this document.

## 1. Deploy resources used in CloudBread to Azure
We will use ARM(Microsoft Azure Resource Manager). It is very powerful tools for automatic deployment on Azure.

**1) Fork the Cloudbread-ARM to personal repository.**

**2) Click the [Deploy to Azure] button.**

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fyshong93%2FCloudBread-ARM%2Fmaster%2Fdeploy%2Frelesase%202.0.1%2Fdeploy_without_notihub.json" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"/></a>  
___Please click the button above.___

**3) Make a new resource group, or use the existed resource group.**
![](./cb-arm-direction/deployment/cb-arm-deploy02.png)

**4) Fill in the blanks about parameter. and Click the [OK] button.**

you can see the detailed explanation for the parameters.
![](./cb-arm-direction/deployment/cb-arm-deploy01.png)

#### Parameter info
When you click upper buttons, maybe you can see Microsoft Azure Template Deploy Pages, and then you have to write this parameters. Red star mark is the required parameters.

|Required|Parameter Name|Remarks|
|---|---|---|
|*|Administrator Login|This is for SQL Server. It will be used for SQL User ID.|
|*|Administrator Login Password|This is for SQL Server, too. It will be used for SQL User Password.|
|*|Database Name|This parameter is for Database name|
|*|Storage Name|This is Storage Account. So you can't use duplicated string account like ID.|

___you must remember the parameters marked with required in the table above. They're admin account for CloudBread's DB and storage.___

**5) Wait for 15~20 minutes, and then deployment was completed!**

#### Generated Resources

|Name|Resource|Detail|
|---|---|---|
|Group Name|Resource Group||
|cb-core-```<GroupID>```|Mobile App|This is a very important part. This is a **core server** that communicates with users' smartphones.|
|cb-redis-```<GroupID>```|Redis|It is a redis cache server for quickly processing user data in database. (_i.g.the leader board, handling massive game log data saving queue, real time socket Authentication and so on._)|
|cb-sqlserver-```<GroupID>```|SQL Server||
|```<Database Name>```|SQL Database| |
|```<Storage Name>```|Storage Account||
|HostingPlan-```<GroupID>```|App Service Plan||
|cb-adminweb-```<GroupID>```|API App||
|cb-socket-```<GroupID>```|API App||

	* ```<GroupID>``` is generated automatically with Resource Group.


## 2. Install CloudBread on the resources
We use the Continuous Deployment. This is very convenient to use with GitHub's repositories.

**1) Now you have to go to CloudBread repository and clone it.**

**2) Install CloudBread using Azure Continuous Deployment tools.**

And then, follow the Continuous Deployment with automation
1.Fork the Cloudbread project to personal repository.

2.Enter the Azure cloud portal site.

3.In the resource group, find the MobileApp and click it.

![](./cb-arm-direction/automationCD/arm-auto01.png)

4.In the MobileApp, click setting and find Continuous deployment.

![](./cb-arm-direction/automationCD/arm-auto02.png)

5.Choose source what you want.

![](./cb-arm-direction/automationCD/arm-auto03.png)

6.GitHub -> you must have the Cloudbread repository that you forked previously.
  select the all of things as below screen, and click the [OK] button.

![](./cb-arm-direction/automationCD/arm-auto04.png)

7.Now, Continuous deployment success!

![](./cb-arm-direction/automationCD/arm-auto05.png)

## 3. Create database for CloudBread
Now you can see this documents.


## Limiation of BizSaprk datacenter region issue
Regarding to BizSpark enroll duration, deployment on some region limited - reported from facebook group Jung Hoon Baek.
- Could not select Japan area but Southeast Asia.

It's limitation of BizSaprk program.

By default, CloudBread is using Japan, East Asia. You might need to change ARM script region and execute it on your machine.  
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview  

Refer issue #22 - https://github.com/CloudBreadProject/CloudBread-ARM/issues/22  
```
"code": "40856",  
  "message": "Location 'Japan West' is not accepting creation of new Azure SQL Database Servers of version '12.0' at this time.  This location only supports the following server versions: ''.  Please retry using a supported server version.",  
  "target": null,  
  "details": [  
    {  
      "code": "40856",  
      "message": "Location 'Japan West' is not accepting creation of new Azure SQL Database Servers of version '12.0' at this time.  This location only supports the following server versions: ''.  Please retry using a supported server version.",
      "target": null,
      "severity": "16"  
    }  
  ],  
  "innererror": []  
}  
```
