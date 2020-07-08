---
title: 分析資源
description: 用於報告使用量、部署和耗用量之資料的合作夥伴中心資源。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: v-sumukh
ms.author: v-sumukh
ms.openlocfilehash: 613f97cf36a3ecb978b7764fbf9fc5065bd74c30
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095412"
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