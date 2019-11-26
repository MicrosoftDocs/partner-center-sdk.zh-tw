---
title: Conversions resources
description: Conversion resources support the conversion of a trial subscription to a paid subscription.
ms.assetid: 4AE796E3-47D9-428B-8267-A5247B573E0C
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e91e79ce77ac020495c2d09a4bf33dd947231dec
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488898"
---
# <a name="conversions-resources"></a>Conversions resources

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Conversion resources support the conversion of a trial subscription to a paid subscription.

## <a name="conversion"></a>轉換

Contains information used to convert a trial subscription to a paid subscription.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| -------- | ---- | ----------- |
| offerId | 字串 | The offer identifier of the original, trial offer. |
| targetOfferId | 字串 | The offer identifier for the target offer. |
| orderId | 字串 | The order identifier. |
| quantity | 整數 | The number of licenses. The default is the number of licenses in the trial subscription. |
| billingCycle | 字串 | Indicates how often the partner is charged for the subscription. Possible values: **Monthly** (partner is billed monthly), **Annual** (partner is billed annually), or **None** (Partner isn't billed. Used for trial subscriptions). |

## <a name="conversionerror"></a>ConversionError

Represents an error that occurred during conversion.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明 |
| -------- | ---- | ----------- |
| code | 字串 | The error code associated with the issue. Possible values: **Other** (general error), **ConversionsNotFound** (can't find any conversions for the trial subscription to convert to).
| 描述 | 字串 | The friendly text describing the issue. |

## <a name="conversionresult"></a>ConversionResult

Represents the result of performing a subscription conversion.

| 屬性       | 在工作列搜尋方塊中輸入                                | 說明                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | 字串                              | The subscription identifier.                                           |
| offerId        | 字串                              | The original offer identifier.                                         |
| targetOfferId  | 字串                              | The offer identifier for the target offer.                             |
| 錯誤 (error)          | [ConversionError](#conversionerror) | The error encountered while attempting the conversion, if applicable.. |