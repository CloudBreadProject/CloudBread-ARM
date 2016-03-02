### CloudBread-ARM
This porject is automatic provision script for CloudBread service instances on Cloud.

CloudBread-ARM project is using Microsoft Azure Resource Manager for automatic service deployment.

[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/)

### Input Parameters info
Input parameter|Detail
---|---|
Redis Name|For the leader board (ranking system), handling massive game log data saving queue, real time socket Authentication.
Resource Group|Created new, or used the established resource group.
Resource Group Name|If you create the resource group, you will input a group name.
Noti Namespace|Namespace of notification hubs.
Notification Hubs Name|Notitfication hubs name for the push alarm.
Server Name|Sql server name for application.
Database Name|Azure Relational database.
Storage Accounts Name|Cheap database for saving game log.
Site Name_mobile|mobile app name.
Site Name_adminweb|admin web page name.
Site Name_web|web page name.

### Direction
1.Fork the Cloudbread project in personal repository.

![](./cb-arm-direction/deployment/cb-arm-fork.png)

2.Click the [Deploy to Azure] button.

3.Fill in the blanks about parameter. and Click the [Next>] button

![](./cb-arm-direction/deployment/cb-arm-deploy01.png)

4.Wait for checking the parameters about error, and Click the [Deploy>] button.

![](./cb-arm-direction/deployment/cb-arm-deploy02.png)

5.Wait a minute, and then deployment was completed!
 
![](./cb-arm-direction/deployment/cb-arm-deploy03.png)


#### And then, follow the Continuous Deployment with automation
1.Enter the Azure cloud portal site.

2.In the resource group, find the MobileApp and click it.

![](./cb-arm-direction/automationCD/arm-auto01.png)

3.In the MobileApp, click setting and find Continuous deployment.

![](./cb-arm-direction/automationCD/arm-auto02.png)

4.Choose source what you want.

![](./cb-arm-direction/automationCD/arm-auto03.png)

5.If you select GitHub, you will have to exist the repository.
  select the all of things, and click the [OK] button.

![](./cb-arm-direction/automationCD/arm-auto04.png)

6.Now, Continuous deployment success!

![](./cb-arm-direction/automationCD/arm-auto05.png)
