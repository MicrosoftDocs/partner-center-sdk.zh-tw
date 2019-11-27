---
title: Azure 費用
description: CSP 合作夥伴可以使用合作夥伴中心 Api 來查看和管理其 Azure 費用。 他們也可以透過程式設計方式，針對其預算來查看其客戶的 Azure 費用。
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: d4db9a7c8c52b33618652aa5bfaf1fb00d24c49b
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489118"
---
# <a name="azure-spending"></a>Azure 費用

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

雲端解決方案提供者（CSP）合作夥伴可以透過合作夥伴中心 Api 來查看和管理其 Azure 費用。 他們也可以透過程式設計方式，針對 Azure 費用預算來查看其客戶的支出。

如需詳細資訊，請參閱[CSP 合作夥伴可以使用合作夥伴中心 api 來管理客戶和合作夥伴帳戶和訂單的案例](scenarios.md)，特別是[背景區段](scenarios.md#background)。

## <a name="partner-usage-management"></a>合作夥伴使用管理

- 使用**PartnerUsageSummary**資源[取得合作夥伴使用量摘要](get-a-partner-usage-summary.md)
- 使用**CustomerMonthlyUsageRecord**資源[取得所有客戶的使用量記錄](get-a-customer-s-usage-records.md)

## <a name="customer-usage-management"></a>客戶使用方式管理

- 使用**customerrelationshiprequest**資源[取得客戶的使用量摘要](get-a-customer-usage-summary.md)
- 使用**SubscriptionMonthlyUsageRecord**資源[取得客戶的所有訂用帳戶使用方式記錄](get-a-customer-subscription-s-usage-records.md)

## <a name="subscription-usage-management"></a>訂用帳戶使用方式管理

- 使用**SubscriptionUsageSummary**資源[取得訂用帳戶使用量摘要](get-a-customer-subscription-usage-summary.md)
- 使用**AzureResourceMonthlyUsageRecord**資源取得訂用帳戶的[所有每月使用量記錄](get-all-monthly-usage-records-for-a-subscription.md)
- 使用**ResourceUsageRecord**資源以[資源取得訂](get-a-customer-subscription-resource-usage-records.md)用帳戶的使用量資料
- 使用**MeterUsageRecord**資源[依計量取得訂](get-a-customer-subscription-meter-usage-records.md)用帳戶的使用量資料

## <a name="azure-spending-budget-management"></a>Azure 支出預算管理

- 使用**customerrelationshiprequest**資源[取得客戶的使用量預算](get-a-customer-s-usage-spending-budget.md)
- 使用**customerrelationshiprequest**資源[更新客戶的使用量預算](update-a-customer-s-usage-spending-budget.md)
