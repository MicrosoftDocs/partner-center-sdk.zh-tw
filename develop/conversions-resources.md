---
title: 轉換資源
description: 轉換資源支援將試用訂閱轉換成付費訂用帳戶。
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
# <a name="conversions-resources"></a>轉換資源

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

轉換資源支援將試用訂閱轉換成付費訂用帳戶。

## <a name="conversion"></a>轉換

包含用來將試用訂閱轉換成付費訂用帳戶的資訊。

| 屬性 | 類型 | 描述 |
| -------- | ---- | ----------- |
| offerId | 字串 | 原始試用版供應專案的供應專案識別碼。 |
| targetOfferId | 字串 | 目標供應專案的供應專案識別碼。 |
| orderId | 字串 | 訂單識別碼。 |
| quantity | 整數 | 授權的數目。 預設值為試用訂用帳戶中的授權數目。 |
| billingCycle | 字串 | 表示訂用帳戶的交易夥伴收費頻率。 可能的值： [**每月**] （夥伴依月計費）、[**年度**] （合作夥伴會以每年計費）或 [**無**] （不計費合作夥伴）。 用於試用訂閱）。 |

## <a name="conversionerror"></a>ConversionError

表示在轉換期間發生的錯誤。

| 屬性 | 類型 | 描述 |
| -------- | ---- | ----------- |
| code | 字串 | 與問題相關聯的錯誤碼。 可能的值： [**其他**（一般錯誤）]、[ **ConversionsNotFound** ] （若要轉換為試用訂用帳戶，則找不到任何轉換）。
| description | 字串 | 描述問題的易記文字。 |

## <a name="conversionresult"></a>ConversionResult

表示執行訂閱轉換的結果。

| 屬性       | 類型                                | 描述                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| 訂閱 | 字串                              | 訂用帳戶識別碼。                                           |
| offerId        | 字串                              | 原始供應專案識別碼。                                         |
| targetOfferId  | 字串                              | 目標供應專案的供應專案識別碼。                             |
| 錯誤 (error)          | [ConversionError](#conversionerror) | 嘗試轉換時所發生的錯誤（如果適用的話）。 |