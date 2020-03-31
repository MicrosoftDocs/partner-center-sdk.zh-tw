---
title: 訂用帳戶資源
description: 訂用帳戶資源可以在整個生命週期中提供有關訂閱的進一步資訊，例如支援、退款、Azure 權利。
ms.assetid: E99B5EC3-2247-4CAD-B651-3000E36AF6B6
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e817762b2e058614a1fe594a9e2ee74f001cbfb9
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80415121"
---
# <a name="subscription-resources"></a>訂用帳戶資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

「訂用帳戶」可讓客戶在一段特定時間內使用服務。 並非所有的欄位都適用于所有訂閱。 許多欄位僅適用于生命週期中的特定點，例如，如果訂閱已暫停或取消。

## <a name="subscription"></a>訂閱

>[!NOTE]
>**訂**用帳戶資源的速率限制為每個租使用者識別碼每分鐘500個要求。

**訂**用帳戶資源代表訂用帳戶的生命週期，並包含定義整個訂用帳戶生命週期中狀態的屬性。

| 屬性             | 類型                                                          | 描述                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                                                        | 訂用帳戶識別碼。                                                                                                                                                  |
| offerId              | string                                                        | 供應專案識別碼。                                                                                                                                                         |
| entitlementId        | string                                                        | 權利識別碼（Azure 訂用帳戶 ID）。                                                                                                                        |
| offerName            | string                                                        | 供應專案名稱。                                                                                                                                                               |
| friendlyName         | string                                                        | 合作夥伴所定義之訂用帳戶的易記名稱，以協助區分。                                                                                           |
| quantity             | 數字                                                        | 數量。 例如，如果是以授權為基礎的計費，此屬性會設定為授權計數。                                                            |
| Unittype.pixel 表示             | string                                                        | 為訂用帳戶定義數量的單位。                                                                                                                             |
| parentSubscriptionId | string                                                        | 取得或設定父訂用帳戶識別碼。                                                                                                                              |
| creationDate         | string                                                        | 取得或設定日期時間格式的建立日期。                                                                                                                          |
| RateplaNcharge.effectivestartdate   | UTC 日期時間格式的字串                                | 取得或設定此訂用帳戶的有效開始日期（以日期時間格式表示）。 它可用來備份已遷移的訂閱，或將它與另一個訂用帳戶對齊。                |
| commitmentEndDate    | UTC 日期時間格式的字串                                | 此訂用帳戶的承諾結束日期（以日期時間格式表示）。 對於不是自動可續訂的訂用帳戶，這代表未來最遠的日期。       |
| status               | string                                                        | 訂用帳戶狀態： [無]、[作用中]、[擱置中]、[已暫停] 或 [已刪除]。                                                                                                         |
| autoRenewEnabled     | 布林值                                                       | 取得值，指出是否自動更新訂閱。                                                                                                    |
| billingType          | string                                                        | 指定訂用帳戶的計費方式： [無]、[使用量] 或 [授權]。                                                                                                      |
| BillingCycle         | string                                                        | 指出此訂單的夥伴計費頻率。 支援的值為在[**為 billingcycletype**](product-resources.md#billingcycletype)中找到的成員名稱。 |
| hasPurchasableAddons | 布林值                                                       | 取得或設定值，指出訂閱是否有可購買附加元件。                                                                                             |
| isTrial              | 布林值                                                       | 值，指出這是否為試用訂閱。                                                                                                                      |
| isMicrosoftProduct   | 布林值                                                       | 值，指出這是否為 Microsoft 產品。                                                                                                                       |
| publisherName        | string                                                        | 發行者名稱。                                                                                                                                                           |
| actions              | 字串的陣列                                              | 取得或設定允許的動作。 可能的值： [編輯]、[取消]                                                                                                  |
| partnerId            | string                                                        | 記錄轉銷商的 MPN 識別碼，用於間接夥伴模型。                                                                                                     |
| suspensionReasons    | 字串的陣列                                              | 唯讀。 如果訂用帳戶已暫止，則會指出原因。                                                                                                                  |
| contractType         | string                                                        | 唯讀。 合約的類型： "訂用帳戶"、"productKey" 或 "redemptionCode"。                                                                                           |
| refundOptions        | [RefundOption](#refundoption)資源的陣列   | 唯讀。 適用于此訂用帳戶的退款選項組。                                                                                              |
| 連結                | [SubscriptionLinks](#subscriptionlinks)                       | 取得或設定訂用帳戶連結。                                                                                                                                          |
| orderId              | string                                                        | 已放置以開始訂閱的訂單識別碼。                                                                                                                |
| termDuration         | string                                                        | 詞彙持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）、 **P1Y** （1年）和**P3Y** （3年）。                                                        |
| 屬性           | [ResourceAttributes](utility-resources.md#resourceattributes) | 對應至訂閱的中繼資料屬性。                                                                                                                    |
| renewalTermDuration  | string                                                        | 詞彙持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）和**P1Y** （1年）。                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**SubscriptionLinks**資源描述附加到訂用帳戶資源的連結集合。

| 屬性           | 類型                               | 描述                           |
|--------------------|------------------------------------|---------------------------------------|
| 產品              | [連結](utility-resources.md#link) | 取得或設定供應專案。               |
| parentSubscription | [連結](utility-resources.md#link) | 取得或設定父訂用帳戶。 |
| 產品            | [連結](utility-resources.md#link) | 取得與訂用帳戶相關聯的產品。 |
| sku                | [連結](utility-resources.md#link) | 取得與訂用帳戶相關聯的產品 sku。 |
| 可用性       | [連結](utility-resources.md#link) | 取得與訂用帳戶相關聯的產品 sku 可用性。 |
| activationLinks    | [連結](utility-resources.md#link) | 取得與訂用帳戶相關聯的啟用連結清單。 |
| self               | [連結](utility-resources.md#link) | 自我 URI。                         |
| next               | [連結](utility-resources.md#link) | 下一個頁面的專案。               |
| previous           | [連結](utility-resources.md#link) | 前一頁的專案。           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

**SubscriptionProvisioningStatus**資源會提供訂用帳戶布建狀態的相關資訊。

| 屬性   | 類型                                                           | 描述                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | 識別產品 SKU 的 GUID 格式字串。             |
| status     | string                                                         | 指出布建狀態：「成功」、「擱置」或「失敗」。 |
| quantity   | 數字                                                         | 提供布建後的訂用帳戶數量。               |
| endDate    | UTC 日期時間格式的字串                                 | 訂用帳戶的結束日期。                                    |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

**SubscriptionRegistrationStatus**資源描述附加到訂用帳戶資源的連結集合。

| 屬性           | 類型                               | 描述                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | string                             | 訂用帳戶識別碼。                                                          |
| status             | string                             | 指出註冊狀態：「已註冊」、「正在註冊」或「notregistered」。    |

## <a name="supportcontact"></a>SupportContact

**SupportContact**資源代表客戶訂用帳戶的支援連絡人。

| 屬性        | 類型                                                           | 描述                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | string                                                         | GUID 格式的字串，表示支援連絡人的租使用者識別碼。 |
| supportMpnId    | string                                                         | 連絡人的 Microsoft 合作夥伴網路（MPN）識別碼。                       |
| 名稱            | string                                                         | 支援連絡人的名稱。                                                |
| 連結           | [ResourceLinks](utility-resources.md#resourcelinks)            | 支援連絡人的相關連結。                                              |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。 包含 "objectType"： "SupportContact"。              |

## <a name="registersubscription"></a>RegisterSubscription

**RegisterSubscription**資源會傳回可用來查詢訂用帳戶註冊狀態的連結。 註冊狀態會在成功接受要求的回應本文中傳回，以註冊 Azure 訂用帳戶。

| 屬性                | 類型                               | 描述                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| HTTPResponseMessage     | object                             | 傳回 HTTP 狀態碼202「已接受」，其位置標頭包含查詢註冊狀態的連結。 例如，`"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

**RefundOption**資源代表訂用帳戶的可能退款選項。

| 屬性          | 類型 | 描述                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| 類型 | string | 退款的類型。 支援的值為「部分」和「完整」 |
| expiresAfter      | UTC 日期時間格式的字串 | 此選項到期時的時間戳記。 如果是 null，這表示它沒有到期日。 |

## <a name="azureentitlement"></a>AzureEntitlement

**AzureEntitlement**資源代表訂用帳戶的 Azure 權利。

| 屬性          | 類型 | 描述                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| id | string | 權利識別碼 |
| friendlyName      | string | 權利的易記名稱。 |
| status | string | 權利的狀態。 |
| subscriptionId | string | 權利所屬的訂用帳戶識別碼。 |
