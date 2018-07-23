# Create a static HTML web app in Azure

[部屬HTML+CSS web site -> Azure Web Apps](https://docs.microsoft.com/en-us/azure/app-service/app-service-web-get-started-html)


---

## 1. Prerequisites

安裝Git

---

## 2. 下載範例

```
$ git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

---

## 3. 使用Azure Cloud Shell && 開始部屬

    
    
    要把靜態網頁部屬到Azure提供的「web app」服務, 在此之前需要建立一些東西~~

    1. 有部屬權限的使用者

    2. Resource Group

    3. App Service Plan

    4. Web App

    5. 將本地檔案部屬到Azure Git

---


### 1. Create Deployment user

| 建立帳號密碼 |
| --- |
| ```az webapp deployment user set --user-name <userName> --password <passWord>``` |

```
staticHTML
userName: tony0920
passWord: (123ssd)

python
userName: cool21540125
passWord: you won't know..^^
```

```
取得回傳資訊
{
"id": null,
"kind": null,
"location": null,
"name": "web",
"publishingPassword": null,
"publishingPasswordHash": null,
"publishingPasswordHashSalt": null,
"publishingUserName": "tony0920",
"tags": null,
"type": "Microsoft.Web/publishingUsers/web",
"userName": null
}
```

### 2. Create Resource Group

| 可以查看所有可用的 ResourceGroup | 建立 ResourceGroup |
| --- | --- | 
| ```az appservice list-locations``` | ```az group create --name <resourceGroup> --location <location>``` |

```
resourceGroup: myResourceGroup0920
location: "East Asia"
```

```
取得回傳資訊
{
"id": "/subscriptions/69c17f22-64ec-4e03-9c84-1225119062f5/resourceGroups/myResourceGroup0920",
"location": "eastasia",
"managedBy": null,
"name": "myResourceGroup0920",
"properties": {
    "provisioningState": "Succeeded"
},
"tags": null
}
```

### 3. Create Azure App Service plan

```
platform-as-a-service(PaaS)平台服務
讓我們專注業務邏輯
Cloud端負責運行和擴展應用程序的基礎架構

A web app is the compute resources that Azure provides for hosting a website or web application.

App Service plans defination:
- Region (for example: North Europe, East US, or Southeast Asia)
- Instance size (small, medium, or large)
- Scale count (1 to 20 instances)
- SKU (Free, Shared, Basic, Standard, or Premium)
```

| 建立App Service plan |
| --- |
| ```az appservice plan create --name <appServicePlan> --resource-group <resourceGroup> --sku FREE``` |

```
appServicePlan: myAppServicePlan0920
resourceGroup: myResourceGroup0920
```

```
取得回傳資訊
{
"adminSiteName": null,
"appServicePlanName": "myAppServicePlan0920",
"geoRegion": "East Asia",
"hostingEnvironmentProfile": null,
"id": "/subscriptions/69c17f22-64ec-4e03-9c84-1225119062f5/resourceGroups/myResourceGroup0920/providers/Microsoft.Web/serverfarms/myAppServicePlan0920",
"kind": "app",
"location": "East Asia",
"maximumNumberOfWorkers": 1,
"name": "myAppServicePlan0920",
"numberOfSites": 0,
"perSiteScaling": false,
"provisioningState": "Succeeded",
"reserved": false,
"resourceGroup": "myResourceGroup0920",
"sku": {
    "capabilities": null,
    "capacity": 0,
    "family": "F",
    "locations": null,
    "name": "F1",
    "size": "F1",
    "skuCapacity": null,
    "tier": "Free"
},
"status": "Ready",
"subscription": "69c17f22-64ec-4e03-9c84-1225119062f5",
"tags": null,
"targetWorkerCount": 0,
"targetWorkerSizeId": 0,
"type": "Microsoft.Web/serverfarms",
"workerTierName": null
}
```

### 4. Create web app

```
web app defination:
- web app為程式碼提供一個託管空間. 另外, web app提供了一個URL來讓你查看部屬好的app(deployed app).
```

| 建立app |
| --- |
| ```az webapp create --name <app_name> --resource-group <resourceGroup> --plan <appServicePlan> --deployment-local-git``` |

```
app_name: appname0920
resourceGroup: myResourceGroup0920
appServicePlan: myAppServicePlan0920
```

```
{
取得回傳資訊
"availabilityState": "Normal",
"clientAffinityEnabled": true,
"clientCertEnabled": false,
"cloningInfo": null,
"containerSize": 0,
"dailyMemoryTimeQuota": 0,
"defaultHostName": "appname0920.azurewebsites.net",
"deploymentLocalGitUrl": "https://tony0920@appname0920.scm.azurewebsites.net/appname0920.git",
"enabled": true,
"enabledHostNames": [
    "appname0920.azurewebsites.net",
    "appname0920.scm.azurewebsites.net"
],
"ftpPublishingUrl": "ftp://waws-prod-hk1-011.ftp.azurewebsites.windows.net/site/wwwroot",
"gatewaySiteName": null,
"hostNameSslStates": [
    {
    "hostType": "Standard",
    "name": "appname0920.azurewebsites.net",
    "sslState": "Disabled",
    "thumbprint": null,
    "toUpdate": null,
    "virtualIp": null
    },
    {
    "hostType": "Repository",
    "name": "appname0920.scm.azurewebsites.net",
    "sslState": "Disabled",
    "thumbprint": null,
    "toUpdate": null,
    "virtualIp": null
    }
],
"hostNames": [
    "appname0920.azurewebsites.net"
],
"hostNamesDisabled": false,
"hostingEnvironmentProfile": null,
"id": "/subscriptions/69c17f22-64ec-4e03-9c84-1225119062f5/resourceGroups/myResourceGroup0920/providers/Microsoft.Web/sites/appname0920",
"isDefaultContainer": null,
"kind": "app",
"lastModifiedTimeUtc": "2017-09-21T08:58:58.087000",
"location": "East Asia",
"maxNumberOfWorkers": null,
"microService": null,
"name": "appname0920",
"outboundIpAddresses": "13.75.42.131,13.75.45.50,13.75.46.209,13.75.43.228",
"premiumAppDeployed": null,
"repositorySiteName": "appname0920",
"reserved": false,
"resourceGroup": "myResourceGroup0920",
"scmSiteAlsoStopped": false,
"serverFarmId": "/subscriptions/69c17f22-64ec-4e03-9c84-1225119062f5/resourceGroups/myResourceGroup0920/providers/Microsoft.Web/serverfarms/myAppServicePlan0920",
"siteConfig": null,
"slotSwapStatus": null,
"state": "Running",
"suspendedTill": null,
"tags": null,
"targetSwapSlot": null,
"trafficManagerHostNames": null,
"type": "Microsoft.Web/sites",
"usageState": "Normal"
}
```

### 4.5 (for python, 多一道工)
| Configure web app to python version |
| --- |
| ```az webapp config set --python-version 3.4 --name <app_name> --resource-group <resourceGroup>``` |

```
app_name: appname0920py
resourceGroup: myResourceGroup0920py
```

```
取得回傳資訊
{
  "alwaysOn": false,
  "apiDefinition": null,
  "appCommandLine": "",
  "appSettings": null,
  "autoHealEnabled": false,
  "autoHealRules": {
    "actions": null,
    "triggers": null
  },
  "autoSwapSlotName": null,
  "connectionStrings": null,
  "cors": null,
  "defaultDocuments": [
    "Default.htm",
    "Default.html",
    "Default.asp",
    "index.htm",
    "index.html",
    "iisstart.htm",
    "default.aspx",
    "index.php",
    "hostingstart.html"
  ],
  "detailedErrorLoggingEnabled": false,
  "documentRoot": null,
  "experiments": {
    "rampUpRules": []
  },
  "handlerMappings": null,
  "httpLoggingEnabled": false,
  "id": "/subscriptions/69c17f22-64ec-4e03-9c84-1225119062f5/resourceGroups/myResourceGroup0920py/providers/Microsoft.Web/sites/appname0920py",
  "ipSecurityRestrictions": null,
  "javaContainer": null,
  "javaContainerVersion": null,
  "javaVersion": null,
  "kind": null,
  "limits": null,
  "linuxFxVersion": "",
  "loadBalancing": "LeastRequests",
  "localMySqlEnabled": false,
  "location": "East Asia",
  "logsDirectorySizeLimit": 35,
  "machineKey": null,
  "managedPipelineMode": "Integrated",
  "name": "appname0920py",
  "netFrameworkVersion": "v4.0",
  "nodeVersion": "",
  "numberOfWorkers": 1,
  "phpVersion": "5.6",
  "publishingUsername": "$appname0920py",
  "push": null,
  "pythonVersion": "3.4",
  "remoteDebuggingEnabled": false,
  "remoteDebuggingVersion": "VS2012",
  "requestTracingEnabled": false,
  "requestTracingExpirationTime": null,
  "resourceGroup": "myResourceGroup0920py",
  "scmType": "LocalGit",
  "tags": null,
  "tracingOptions": null,
  "type": "Microsoft.Web/sites",
  "use32BitWorkerProcess": true,
  "virtualApplications": [
    {
      "physicalPath": "site\\wwwroot",
      "preloadEnabled": false,
      "virtualDirectories": null,
      "virtualPath": "/"
    }
  ],
  "vnetName": "",
  "webSocketsEnabled": false
}
```


### 5. Configure local Git deployment (將本地檔案部屬到Azure Git)

| 部屬指令 |
| --- |
| ```az webapp deployment source config-local-git --name <app_name> --resource-group <resourceGroup> --query url --output tsv``` |

```
app_name: appname0920
resourceGroup: myResourceGroup0920
```

```
指令沒問題的話, 會取得git空間
https://tony0920@appname0920.scm.azurewebsites.net/appname0920.git
https://tony0920py@appname0920py.scm.azurewebsites.net/appname0920py.git
接著, 把資料push到這個連結就可以囉
```





bash

```
$ git remote -v
    origin  https://github.com/Azure-Samples/html-docs-hello-world.git (fetch)
    origin  https://github.com/Azure-Samples/html-docs-hello-world.git (push)

$ git remote add azure https://tony0920@appname0920.scm.azurewebsites.net/appname0920.git

$ git remote -v
    azure   https://tony0920@appname0920.scm.azurewebsites.net/appname0920.git (fetch)
    azure   https://tony0920@appname0920.scm.azurewebsites.net/appname0920.git (push)
    origin  https://github.com/Azure-Samples/html-docs-hello-world.git (fetch)
    origin  https://github.com/Azure-Samples/html-docs-hello-world.git (push)

$ git push azure master
```


如此, 便將HTML app 部屬到 App Service

https://appname0920.azurewebsites.net/

去改變index.html, 存檔後

```
$ git commit -am '<commit string>'

$ git push azure master
```

https://appname0920.azurewebsites.net/

| 刪除app指令 |
| --- |
| ```az group delete --name myResourceGroup0920``` |
