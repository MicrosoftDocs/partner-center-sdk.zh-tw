---
title: Analytics resources
description: Partner Center resources for data used to report on usage, deployment, and consumption.
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 8098de53c3fc4632d17ef6cdba7fe983d9fffbbe
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489198"
---
# <a name="analytics-resources"></a>Analytics resources

適用於：

- 合作夥伴中心

The resources defined here contain data used to report on usage, deployment, and consumption.

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

The **PartnerLicensesDeploymentInsights** resource contains partner-level insights about license deployment.

| 屬性                  | 在工作列搜尋方塊中輸入                                                           | 說明                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | 數目                                                         | The percentage of licenses deployed.                                                |
| licensesSold              | 數目                                                         | The number of licenses sold.                                                        |
| processedDateTime         | string in UTC date-time format                                 | The date and time when the data was aggregated.                                     |
| serviceName               | 字串                                                         | The service name (e.g. o365, crm).                                                  |
| channel                   | 字串                                                         | The channel name of the service (e.g. reseller).                                    |
| 屬性                | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

The **PartnerLicensesUsageInsights** resource contains partner-level insights about license usage.

| 屬性                     | 在工作列搜尋方塊中輸入                                                           | 說明                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | 數目                                                         | The percentage of licenses deployed.                                           |
| workloadName                 | 字串                                                         | The workload name (e.g. exchange).                                             |
| processedDateTime            | string in UTC date-time format                                 | The date and time when the data was aggregated.                                |
| serviceName                  | 字串                                                         | The service name (e.g. o365, crm).                                             |
| channel                      | 字串                                                         | The channel name of the service (e.g. reseller).                               |
| 屬性                   | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

The **CustomerLicensesDeploymentInsights** resource contains customer-level insights about license deployment.

| 屬性          | 在工作列搜尋方塊中輸入                                                           | 說明                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | 數目                                                         | The number of licenses deployed.                                                     |
| licensesSold      | 數目                                                         | The number of licenses sold.                                                         |
| deploymentPercent | 數目                                                         | The adjusted percentage of licenses deployed.                                        |
| customerId        | 字串                                                         | The customer identifier.                                                             |
| customerName      | 字串                                                         | The customer name.                                                                   |
| productName       | 字串                                                         | The product name.                                                                    |
| serviceCode       | 字串                                                         | The service code of the license.                                                     |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                      |
| serviceName       | 字串                                                         | The service name (e.g. o365, crm).                                                   |
| channel           | 字串                                                         | The channel name of the service (e.g. reseller).                                     |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

The **CustomerLicensesUsageInsights** resource contains customer-level insights about license usage.

| 屬性          | 在工作列搜尋方塊中輸入                                                           | 說明                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | 字串                                                         | The workload code.                                                              |
| workloadName      | 數目                                                         | The workload name (e.g. Exchange).                                              |
| usagePercent      | 數目                                                         | The adjusted percentage of licenses used.                                       |
| licensesActive    | 數目                                                         | The number of active licenses.                                                  |
| licensesQualified | 數目                                                         | The number of qualified licenses.                                               |
| customerId        | 字串                                                         | The customer identifier.                                                        |
| customerName      | 字串                                                         | The customer name.                                                              |
| productName       | 字串                                                         | The product name.                                                               |
| serviceCode       | 字串                                                         | The service code of the license.                                                |
| processedDateTime | string in UTC date-time format                                 | The date and time when the data was aggregated.                                 |
| serviceName       | 字串                                                         | The service name (e.g. o365, crm).                                              |
| channel           | 字串                                                         | The channel name of the service (e.g. reseller).                                |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes. Includes "objectType": "CustomerLicensesUsageInsights" |