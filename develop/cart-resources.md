---
title: 購物車資源
description: 當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 22b9ec1799a9d8c5423fb9dea3db61d028ec6dba
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413024"
---
# <a name="cart-resources"></a>購物車資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要從供應專案清單購買訂用帳戶時，合作夥伴會進行訂單。

## <a name="cart"></a>購物車

描述購物車。

| 屬性              | 類型             | 描述                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | 成功建立購物車時所提供的購物車識別碼。                               |
| creationTimeStamp     | DateTime         | 購物車的建立日期（以日期時間格式）。 已在成功建立購物車時套用。      |
| lastModifiedTimeStamp | DateTime         | 購物車上次更新的日期（以日期時間格式）。 已在成功建立購物車時套用。 |
| expirationTimeStamp   | DateTime         | 購物車將到期的日期，以日期時間格式為限。 已在成功建立購物車時申請。          |
| lastModifiedUser      | string           | 上次更新購物車的使用者。 已在成功建立購物車時申請。                          |
| lineItems             | 物件的陣列 | [CartLineItem](#cartlineitem)資源的陣列。                                                   |
| status                | string           | 購物車的狀態。 可能的值為「作用中」（可更新/提交）和「已訂購」（已提交）。 |

## <a name="cartlineitem"></a>CartLineItem

表示購物車中包含的一個專案。

| 屬性             | 類型                             | 描述                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| id                   | string                           | 購物車明細專案的唯一識別碼。 已在成功建立購物車時申請。                                                                   |
| catalogItemId        | string                           | 目錄專案識別碼。                                                                                                                          |
| friendlyName         | string                           | 選擇性。 由夥伴定義以協助區分的專案易記名稱。                                                                 |
| quantity             | int                              | 授權或實例的數目。                                                                                                                  |
| currencyCode         | string                           | 貨幣代碼。                                                                                                                                    |
| BillingCycle         | 物件                           | 針對目前期間所設定的計費週期類型。                                                                                                 |
| termDuration         | string                           | 詞彙持續時間的 ISO 8601 標記法。 目前支援的值為 P1M （1個月）、P1Y （1年）和 P3Y （3年）。                                |
| participants         | 物件字串配對的清單      | 在購買時，記錄（MPNID）上的 PartnerId 集合。                                                                                          |
| provisioningCoNtext  | 字典 < 字串，字串 >       | 布建購買的專案時所使用的其他內容。 若要判斷特定專案需要哪些值，請參閱 SKU 的 provisioningVariables 屬性。 |
| orderGroup           | string                           | 一個群組，用來指出可以用相同順序將哪些專案提交在一起。                                                                          |
| addonItems           | **CartLineItem**物件的清單 | 附加元件的購物車明細專案集合，會向基礎購物車明細專案購買所產生的基本訂用帳戶購買。 |
| 錯誤                | 物件                           | 在購物車建立後，發生錯誤時套用。                                                                                                    |
| renewsTo             | 物件的陣列                 | [RenewsTo](#renewsto)資源的陣列。                                                                            |

## <a name="renewsto"></a>renewsTo

表示購物車明細專案中包含的一個專案。

| 屬性              | 類型             | 必要項        | 描述 |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | string           | 否              | 續訂詞彙之持續時間的 ISO 8601 標記法。 目前支援的值為**P1M** （1個月）和**P1Y** （1年）。 |

## <a name="carterror"></a>CartError

表示在建立購物車之後發生的錯誤。

| 屬性         | 類型                                   | 描述                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CartErrorCode](#carterrorcode) | 購物車錯誤的類型。                                                                       |
| errorDescription | string                                 | 錯誤描述，包括有關支援的值、預設值或限制的任何附注。 |

## <a name="carterrorcode"></a>CartErrorCode

具有表示購物車錯誤類型之值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)。

| 值                                | Position | 描述                                             |
|--------------------------------------|----------|---------------------------------------------------------|
| 未知                              | 0        | 預設值。                                          |
| CurrencyIsNotSupported               | 10000    | 指定的市場不支援貨幣。 |
| CatalogItemIdIsNotValid              | 10001    | 目錄專案識別碼無效。                       |
| QuotaNotAvailable                    | 10002    | 可用的配額不足。                    |
| InventoryNotAvailable                | 10003    | 選取的供應專案無法使用清查。  |
| ParticipantsIsNotSupportedForPartner | 10004    | 此合作夥伴不支援設定參與者。 |
| UnableToProcessCartLineItem          | 10006    | 無法處理購物車明細專案。                   |
| SubscriptionIsNotValid               | 10007    | 訂用帳戶無效。                          |
| SubscriptionIsNotEnabledForRI        | 10008    | 訂用帳戶未啟用 Azure 保留。 |
| SandboxLimitExceeded                 | 10009    | 已超過沙箱限制。                    |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

表示購物車結帳的結果。

| 屬性    | 類型                                              | 描述                     |
|-------------|---------------------------------------------------|---------------------------------|
| 訂單      | [Order](order-resources.md#order)物件的清單。         | 訂單的集合。       |
| orderErrors | [OrderError](#ordererror)物件的清單。 | 順序錯誤的集合。 |

## <a name="ordererror"></a>OrderError

代表當訂單建立時，在購物車簽出期間發生的錯誤。

| 屬性     | 類型   | 描述                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | string | 具有錯誤之訂單的順序群組識別碼。 |
| code         | int    | 錯誤碼。                                 |
| 描述  | string | 錯誤的描述。                   |

## <a name="ordererrorcode"></a>OrderErrorCode

具有值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)，指出順序錯誤的類型。

| 值 | Position | 描述 |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | 要求內容中缺少合作夥伴 Token。 |
| InvalidInput | 800002 | 不正確要求輸入。 |
| ServiceException | 800003 | 未預期的服務錯誤。 |
| InvalidOfferId | 800004 | 供應專案識別碼無效。 |
| CreateOrderError | 800005 | 建立訂單不成功。 |
| ProvisioningStatusNotFound | 800007 | 無法取出布建資訊。 |
| CartIdNotFound | 800008 | 無法取出購物車識別碼。 |
| CartItemErrorInCreateOrder | 800009 | 購物車專案發生錯誤。 |
| InventoryNotAvailable | 800010 | 此類別目錄專案無法使用清查。 |
| AzureSubscriptionNotValid | 800011 | 此訂用帳戶不是有效的 Azure 訂用帳戶。 |
| SubscriptionIsNotActive | 800012 | 此訂用帳戶不是有效的訂用帳戶。 |
| SubscriptionIsNotEnabledForRI | 800013 | 此訂用帳戶未啟用 RI 購買。 |
| PendingAdjustment | 800014 | 此訂單需要暫止的調整。 |
| MpnIdNotFound | 800015 | 找不到 MPN 識別碼。 |
| NotValidIndirectResellerMpnId | 800016 | MPN 識別碼不是有效的間接轉銷商。 |
| InvalidQuantity | 800017 | 此類別目錄專案無法使用此數量。 |
| SandboxLimitExceeded | 800018 | 已符合沙箱限制。 |
| SandboxTenantOnly | 800019 | 此作業只會針對沙箱租使用者啟用。 |
| CatalogItemNotEligibleForPurchase | 800020 | 類別目錄專案不符合購買資格。 |
| SubscriptionIsNotValid | 800021 | 此訂用帳戶不是有效的訂用帳戶。 |
| ManualReviewRequired | 800022 | 您可能符合此交易的資格。 請洽詢支援人員以取得協助。|
| InsufficientFunds | 800023 | 您不符合此交易的資格，因為您的點數線路未達到此購買的最低閾值。請更新您的訂單（或）連絡人支援以取得協助。 |
| ReviewCancelled | 800024 | 您不符合此交易的資格。 |
| LineOfCreditNotDefined | 800025 | 您不符合此交易的資格，因為您的點數線路未達到此購買的最低閾值。 請更新您的訂單（或）連絡人支援以取得協助。 |
| RiskError | 800026 | 您不符合此交易的資格。 |
| SubscriptionNotRegistered | 800030 | 此訂用帳戶未註冊。 |
| PurchaseSystemNotSupported | 800031 | 不支援購買系統。 |
| ConditionFailed | 800036 | 前置條件失敗。 |
| AssetIdNotFound | 800037 | 找不到資產識別碼。 |
| AssetFutureBillingInfoNotFound | 800038 | 找不到資產 FutureBillingInfo。 |
| ResellerProgramStatusNotActive | 800039 | 轉售商計畫狀態並非使用中。 |
| AssetStatusChangeNotValid | 800040 | 資產狀態無法從 **{1}** 變更為 **{0}** 。 |
| ItemAlreadyActivated | 800041 | 這個專案已經啟用。 |
| NotSupported | 800042 | 不支援。 |
| PricingAccessForbidden | 800043 | 未授與定價資訊的存取權。 |
| OrderInProgress | 800060 | 您的訂單正在進行中。 請在幾分鐘內檢查訂單歷程記錄中最近的訂單。 |
| OrderCannotBeCancelled | 800061 | 無法取消訂單。 |
| ReviewRejected | 800062 | 您不符合此交易的資格。 |
| CancelLegacyOrder | 800063 | 無法取消此順序 **{0}** 。 使用 `PATCH /customers/{1}/subscriptions/<subscriptionId>` 來暫止訂閱。 |
| CartProcessedByAnotherRequest | 800064 | 購物車 **{0}** 正由另一個要求處理。 |
| CartCheckOutNotAllowedWhenStatusIsOrdered | 800065 | 無法簽出已提交的購物車 **{0}** 。 |
