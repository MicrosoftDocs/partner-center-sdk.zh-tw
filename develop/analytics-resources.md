---
title: 分析資源
description: 用於報告使用量、部署和耗用量之資料的合作夥伴中心資源。
ms.assetid: 1FEB08D6-AD0C-4B01-B7A8-AE05C914912B
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 50c04b1df512ab2475cd555e06bc2b6b92b6c8a7
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022686"
---
# <a name="analytics-resources"></a>分析資源

**適用於：**

- 合作夥伴中心

此處定義的資源包含用來報告使用量、部署和耗用量的資料。

## <a name="partnerlicensesdeploymentinsights"></a>PartnerLicensesDeploymentInsights

**PartnerLicensesDeploymentInsights**資源包含有關授權部署的夥伴層級深入解析。

| 屬性                  | 類型                                                           | Description                                                                         |
|---------------------------|----------------------------------------------------------------|-------------------------------------------------------------------------------------|
| proratedDeploymentPercent | number                                                         | 已部署的授權百分比。                                                |
| licensesSold              | number                                                         | 售出的授權數目。                                                        |
| processedDateTime         | UTC 日期時間格式的字串                                 | 匯總資料的日期和時間。                                     |
| serviceName               | 字串                                                         | 服務名稱（例如： o365、crm）。                                                  |
| 通道                   | 字串                                                         | 服務的通道名稱（例如：轉銷商）。                                    |
| 屬性                | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 包含 "objectType"： "PartnerLicensesDeploymentInsights" |

## <a name="partnerlicensesusageinsights"></a>PartnerLicensesUsageInsights

**PartnerLicensesUsageInsights**資源包含有關授權使用方式的合作夥伴層級深入解析。

| 屬性                     | 類型                                                           | Description                                                                    |
|------------------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------|
| proratedLicensesUsagePercent | number                                                         | 已部署的授權百分比。                                           |
| workloadName                 | 字串                                                         | 工作負載名稱（例如： exchange）。                                             |
| processedDateTime            | UTC 日期時間格式的字串                                 | 匯總資料的日期和時間。                                |
| serviceName                  | 字串                                                         | 服務名稱（例如： o365、crm）。                                             |
| 通道                      | 字串                                                         | 服務的通道名稱（例如：轉銷商）。                               |
| 屬性                   | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 包含 "objectType"： "PartnerLicensesUsageInsights" |

## <a name="customerlicensesdeploymentinsights"></a>CustomerLicensesDeploymentInsights

**CustomerLicensesDeploymentInsights**資源包含有關授權部署的客戶層級深入解析。

| 屬性          | 類型                                                           | Description                                                                          |
|-------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| licensesDeployed  | number                                                         | 已部署的授權數量。                                                     |
| licensesSold      | number                                                         | 售出的授權數目。                                                         |
| deploymentPercent | number                                                         | 已部署的已調整授權百分比。                                        |
| customerId        | 字串                                                         | 客戶識別碼。                                                             |
| customerName      | 字串                                                         | 客戶名稱。                                                                   |
| productName       | 字串                                                         | 產品名稱。                                                                    |
| serviceCode       | 字串                                                         | 授權的服務代碼。                                                     |
| processedDateTime | UTC 日期時間格式的字串                                 | 匯總資料的日期和時間。                                      |
| serviceName       | 字串                                                         | 服務名稱（例如： o365、crm）。                                                   |
| 通道           | 字串                                                         | 服務的通道名稱（例如：轉銷商）。                                     |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 包含 "objectType"： "CustomerLicensesDeploymentInsights" |

## <a name="customerlicensesusageinsights"></a>CustomerLicensesUsageInsights

**CustomerLicensesUsageInsights**資源包含有關授權使用方式的客戶層級深入解析。

| 屬性          | 類型                                                           | Description                                                                     |
|-------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| workloadCode      | 字串                                                         | 工作負載程式碼。                                                              |
| workloadName      | number                                                         | 工作負載名稱（例如： Exchange）。                                              |
| usagePercent      | number                                                         | 所用授權的已調整百分比。                                       |
| licensesActive    | number                                                         | 使用中授權的數目。                                                  |
| licensesQualified | number                                                         | 合格授權的數目。                                               |
| customerId        | 字串                                                         | 客戶識別碼。                                                        |
| customerName      | 字串                                                         | 客戶名稱。                                                              |
| productName       | 字串                                                         | 產品名稱。                                                               |
| serviceCode       | 字串                                                         | 授權的服務代碼。                                                |
| processedDateTime | UTC 日期時間格式的字串                                 | 匯總資料的日期和時間。                                 |
| serviceName       | 字串                                                         | 服務名稱（例如： o365、crm）。                                              |
| 通道           | 字串                                                         | 服務的通道名稱（例如：轉銷商）。                                |
| 屬性        | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 包含 "objectType"： "CustomerLicensesUsageInsights" |