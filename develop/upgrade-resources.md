---
title: 升級資源
description: 說明用來將使用者從來源訂用帳戶升級至目標訂用帳戶的資源。
ms.assetid: 869007B3-D6D4-4E79-B4F0-445CA5D88D2C
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d75d81dffbe30633038c03cec2cdf85e05536eb9
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80414518"
---
# <a name="upgrade-resources"></a>升級資源


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

說明用來將使用者從來源訂用帳戶升級至目標訂用帳戶的資源。

## <a name="span-idupgradespan-idupgradespan-idupgradeupgrade"></a><span id="Upgrade"/><span id="upgrade"/><span id="UPGRADE"/>升級


描述個別升級資源的行為。

| 屬性      | 類型                   | 描述                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | 產品                  | 目標訂用帳戶的供應專案。                                                        |
| UpgradeType   | string                 | 升級的類型： [無]、[僅限升級\_] 或 [使用\_授權\_傳輸的升級\_]。         |
| isEligible    | 布林值                | 識別是否可以執行升級。                                                  |
| 數量      | integer                | 要購買的新供應專案量化。 預設為來源訂用帳戶數量。 |
| UpgradeErrors | UpgradeErrors 的陣列 | 無法執行升級的原因（如果適用）。                                      |
| 屬性    | ResourceAttributes     | 對應至升級的中繼資料屬性。                                        |

 

## <a name="span-idupgradeerrorspan-idupgradeerrorspan-idupgradeerrorupgradeerror"></a><span id="UpgradeError"/><span id="upgradeerror"/><span id="UPGRADEERROR"/>UpgradeError


描述無法執行升級的原因。

| 屬性          | 類型               | 描述                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 程式碼              | string             | 與問題相關聯的錯誤碼：「其他「，」委派的\_admin\_許可權\_停用」、「訂用帳戶\_狀態\_不\_作用中」、「衝突的\_服務\_類型」、「並行\_的衝突」、「使用者\_內容\_必要」、「訂閱\_新增\_元件\_」、「訂閱\_\_\_\_\_的升級」、「訂用帳戶\_目標\_供應專案\_不\_找到」，或「訂用帳戶\_不\_布建」。\_ |
| 描述       | string             | 描述錯誤的易記文字。                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | 關於錯誤的其他詳細資料。                                                                                                                                                                                                                                                                                                                                                         |
| 屬性        | ResourceAttributes | 對應至錯誤的中繼資料屬性。                                                                                                                                                                                                                                                                                                                                             |

 

## <a name="span-idupgraderesultspan-idupgraderesultspan-idupgraderesultupgraderesult"></a><span id="UpgradeResult"/><span id="upgraderesult"/><span id="UPGRADERESULT"/>UpgradeResult


描述訂閱升級程式的結果。

| 屬性             | 類型                        | 描述                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | 來源訂用帳戶的識別碼。                                           |
| TargetSubscriptionID | string                      | 目標訂用帳戶的識別碼。                                           |
| UpgradeType          | string                      | 升級的類型： [無]、[僅限升級\_] 或 [使用\_授權\_傳輸的升級\_]。 |
| UpgradeErrors        | UpgradeErrors 的陣列      | Attemption 執行升級時遇到的錯誤（如果適用）。           |
| LicenseErrors        | UserLicenseErrrors 的陣列 | 嘗試遷移使用者授權時所發生的錯誤（如果適用）。          |
| 屬性           | ResourceAttributes          | 對應至授權的中繼資料屬性。                                |

 

## <a name="span-iduserlicenseerrorspan-iduserlicenseerrorspan-iduserlicenseerroruserlicenseerror"></a><span id="UserLicenseError"/><span id="userlicenseerror"/><span id="USERLICENSEERROR"/>UserLicenseError


描述因使用者授權傳輸失敗而引發的錯誤。

| 屬性     | 類型                   | 描述                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| Userobjectid 為 | string                 | 使用者物件的唯一識別。                                 |
| 名稱         | string                 | 使用者的名稱。                                                     |
| 電子郵件        | string                 | 使用者的電子郵件。                                                    |
| 錯誤       | ServiceFaults 的陣列 | 嘗試執行使用者授權傳輸時所擲回的例外狀況清單。 |
| 屬性   | ResourceAttributes     | 對應至授權的中繼資料屬性。                     |

 

 

 




