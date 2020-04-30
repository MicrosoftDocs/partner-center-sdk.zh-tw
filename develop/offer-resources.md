---
title: 供應專案資源
description: 描述在轉銷商目錄中列出的產品，其可提供給客戶。
ms.assetid: 702B18DB-D78A-4E3B-BC8F-EFD4092131DE
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a4bec5d83faa4454857cd093bb109495bce4c17a
ms.sourcegitcommit: bea0d0cf3c1af7a75c9b150d53de53193a673fae
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82118654"
---
# <a name="offer-resources"></a>供應專案資源

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

描述在轉銷商目錄中列出的產品，其可提供給客戶。

## <a name="offer"></a>產品

| 屬性                    | 類型                      | 描述                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                          | 字串                    | 供應項目識別碼。                                                                                           |
| NAME                        | 字串                    | 供應專案名稱。                                                                                                 |
| description                 | 字串                    | 供應專案的描述。                                                                                     |
| minimumQuantity             | int                       | 可用的最小數量。                                                                                 |
| maximumQuantity             | int                       | 可用的最大數量。                                                                                 |
| 排名                        | int                       | 與相同產品線中的其他類別相較之下的供應專案等級或優先順序。 只有當指定的產品線有一個以上的供應專案時，才應該設定此屬性。  |
| uri                         | 字串                    | 供應專案 URI。                                                                                                  |
| 地區設定                      | 字串                    | 套用供應專案的地區設定。                                                                          |
| country                     | 字串                    | 供應專案適用的國家/地區。                                                                    |
| category                    | [OfferCategory](#offercategory)           | 供應專案的類別。                                                                   |
| limitUnitOfMeasure          | 字串                    | 值，指出購買限制的類型。 可能的值包括：<br/> 「無」-根據購買的供應專案，不會限制訂用帳戶數目。<br/> 「並行」-客戶租使用者在指定時間可以存在的訂閱數目，包括作用中或已取消的訂閱。 此值大部分適用于授權計數小於300的小型企業供應專案。 Provisionioned 訂閱不會計入。<br/> 「存留期」-客戶租使用者的存留期可以存在的訂閱數目。 此值最適用于試用。 Provisionioned 訂閱不會計入。      |
| limit                       | int                       | 可以根據 limitUnitOfMeasure 購買此供應專案的訂閱數量。                |
| prerequisiteOffers          | 字串                    | 先決條件供應專案。                                                                                        |
| isAddOn                     | boolean                   | 值，指出這個實例是否為附加元件。                                                           |
| hasAddOns                   | boolean                   | 值，指出此供應專案是否有任何附加元件。                                                           |
| isAvailableForPurchase      | boolean                   | 值，指出此實例是否可供購買。                                             |
| 計費                     | 字串                    | 指定明細專案購買的計費類型： [無]、[使用量] 或 [授權]。                           |
| supportedBillingCycles      | 字串的陣列          | 指出此供應專案支援的計費週期。 支援的值為在[為 billingcycletype](product-resources.md#billingcycletype)中找到的成員名稱   |
| isAutoRenewable             | boolean                   | 值，指出供應專案是否自動續約。                                                      |
| upgradeTargetOffers         | 字串的陣列          | 這項供應專案可升級到的供應專案清單。                                                          |
| conversionTargetOffers      | 字串的陣列          | 可將此供應專案轉換成的供應專案清單。                                                         |
| reselleeQualifications      | 字串的陣列          | 客戶為了讓合作夥伴購買該客戶的供應專案所需的資格。     |
| resellerQualifications      | 字串的陣列          | 合作夥伴所需的資格，以便購買客戶的供應專案。                       |
| salesGroupId                | 字串                    | 用來將供應專案分組成不同訂單的字串。                                                             |
| isTrial                     | boolean                   | 值，指出這是否為試用版供應專案。                                                               |
| product                     | [OfferProduct](#offerproduct)           | 取得供應專案產品。                                                                           |
| Unittype.pixel 表示                    | 字串                    | 單位的類型。                                                                                      |
| 連結                       | [OfferLinks](#offerlinks)               | 供應專案的 [深入瞭解] 連結。                                                                    |
| 屬性                  | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至供應專案的中繼資料屬性。                         |

## <a name="offercategory"></a>OfferCategory

描述供應專案的分類。 這包括此供應專案類別目錄的排名或優先順序（相較于相同產品線中的其他專案）。

| 屬性   | 類型                                                           | 描述                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id         | 字串                                                         | 分類識別碼。                                                                                                                                                   |
| NAME       | 字串                                                         | 類別名稱。                                                                                                                                                         |
| 排名       | int                                                            | 與相同供應專案中的其他類別相較之下的分類次序或優先順序。 只有當指定的供應專案有一個以上的供應專案類別時，才應設定此屬性。 |
| 地區設定     | 字串                                                         | 套用供應專案的地區設定。                                                                                                                        |
| country    | 字串                                                         | 供應專案適用的國家/地區。                                                                                                                   |
| 連結      | [ResourceLinks](utility-resources.md#resourcelinks)           | 對應至 OfferCategory 的資源連結。                                                                                                                     |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至 OfferCategory 的中繼資料屬性。                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

包含連結，以瞭解供應專案的詳細資訊。

| 屬性  | 類型 | 描述                 |
|-----------|------|-----------------------------|
| learnMore | 連結 | [深入瞭解] 連結。      |
| self      | 連結 | 自我 URI                |
| 下一步      | 連結 | 下一個頁面的專案。     |
| previous  | 連結 | 前一頁的專案。 |

## <a name="offerproduct"></a>OfferProduct

可能有多個供應專案相關聯的產品或服務，各有不同的功能集，並以不同的客戶需求為目標。

| 屬性 | 類型   | 描述              |
|----------|--------|--------------------------|
| Id       | 字串 | 分類識別碼。 |
| 名稱     | 字串 | 類別名稱。       |
| 單位     | 字串 | 產品單位。        |
