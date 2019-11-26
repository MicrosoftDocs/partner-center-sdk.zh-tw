---
title: 計量使用量記錄資源
description: 您可以使用 MeterUsageRecord 資源來描述目前計費週期中，訂用帳戶計量層級使用量的預估貨幣成本。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 003db39c92e96b12863edebb46b3e3341ffae10e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488308"
---
# <a name="meter-usage-record-resource"></a>計量使用量記錄資源

適用於：

- 合作夥伴中心

您可以使用**MeterUsageRecord**資源來描述目前計費週期中，訂用帳戶計量層級使用量的預估貨幣成本。

## <a name="meterusagerecord"></a>MeterUsageRecord

| 屬性         | 類型               | 說明                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | 對應至合作夥伴中心訂用帳戶[資源](subscription-resources.md#subscription)識別碼的 GUID，代表 MICROSOFT AZURE （Ms-azr-0017p-流程 ms-azr-0145p）訂用帳戶或 Azure 方案。 對於 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶，此值是 commerce 訂閱識別碼。 若為 Azure 方案訂用帳戶資源，此值為 Azure 方案識別碼。                  |
| MeterId  | string             | 取得或設定計量識別碼。                                                        |
| MeterName          | string             | 取得或設定計量名稱。                                       |
| 分類               | string             | 取得或設定 Azure 資源類別。                                                 |
| 子類別             | string             |  取得或設定 Azure 資源子類別。                                                     |
| QuantityUsed        | 十進位             | 取得或設定所使用的 Azure 資源數量。   |
| 單位   | string             | 取得或設定 Azure 資源的測量單位。 |
| TotalCost   | 十進位             | 取得或設定使用量的預估總成本。 |
| CurrencyLocale   | string             | 使用訂閱的地區設定。 這個屬性會決定發票上所使用的貨幣。 此屬性適用于 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱。 |
| CurrencyCode   | string             | 取得或設定貨幣代碼。 此屬性適用于 Azure 方案。                                         |
| USDTotalCost   | 十進位             | 取得或設定估計的總成本（美元）。 此屬性適用于 Azure 方案。                                         |
| lastModifiedDate | string             | 此記錄上次修改的日期（日期時間格式）。                             |
| 屬性       | ResourceAttributes | 對應至資源的中繼資料屬性。                                        |                                           |
