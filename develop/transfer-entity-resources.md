---
title: TransferEntity 資源
description: 當客戶想要將其訂用帳戶轉移給另一位合作夥伴時，夥伴會建立轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96c43d255fcd31e6dc4de50baa0e19f5d8855685
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90925780"
---
# <a name="transferentity-resources"></a>TransferEntity 資源

**適用於：**

- 合作夥伴中心

當客戶想要將其訂用帳戶轉移給另一位合作夥伴時，夥伴會建立轉移。

## <a name="transferentity"></a>TransferEntity

描述 transferEntity。

| 屬性              | 類型             | 描述                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | 字串           | 成功建立 transferEntity 時所提供的 transferEntity 識別碼。                               |
| createdTime           | Datetime         | TransferEntity 的建立日期（以日期時間格式）。 在成功建立 transferEntity 時套用。      |
| lastModifiedTime      | Datetime         | 上次更新 transferEntity 的日期（以日期時間格式）。 在成功建立 transferEntity 時套用。 |
| lastModifiedUser      | 字串           | 上次更新 transferEntity 的使用者。 在成功建立 transferEntity 時套用。                          |
| customerName          | 字串           | 選擇性。 要轉移其訂用帳戶的客戶名稱。                                              |
| customerTenantId      | 字串           | 可識別客戶的 GUID 格式化客戶識別碼。 在成功建立 transferEntity 時套用。         |
| partnertenantid       | 字串           | 識別夥伴的 GUID 格式化夥伴識別碼。                                                                   |
| sourcePartnerName     | 字串           | 選擇性。 正在起始傳輸的夥伴組織名稱。                                           |
| sourcePartnerTenantId | 字串           | GUID 格式的夥伴識別碼，可識別起始傳送的夥伴。                                           |
| targetPartnerName     | 字串           | 選擇性。 傳送目標夥伴組織的名稱。                                         |
| targetPartnerTenantId | 字串           | GUID 格式的夥伴識別碼，可識別傳送目標的夥伴。                                  |
| lineItems             | 物件的陣列 | [TransferLineItem](#transferlineitem)資源的陣列。                                                   |
| status                | 字串           | TransferEntity 的狀態。 可能的值為「作用中」 (可以刪除/提交) 和「已完成」 (已經) 完成。 在成功建立 transferEntity 時套用。|

## <a name="transferlineitem"></a>TransferLineItem

表示 transferEntity 中包含的一個專案。

| 屬性             | 類型                             | 描述                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | 字串                           | 傳送明細專案的唯一識別碼。 在成功建立 transferEntity 時套用。   |
| subscriptionId       | 字串                           | 訂用帳戶識別碼。                                                                            |
| quantity             | int                              | 授權或實例的數目。                                                                    |
| billingCycle         | 物件                           | 針對目前期間設定的計費週期類型。                                                   |
| friendlyName         | 字串                           | 選擇性。 由夥伴定義之專案的易記名稱，以協助區分。                   |
| partnerIdOnRecord    | 字串                           | PartnerId 記錄 (MPNID 在接受轉移時所發生的購買上) 。                 |
| offerId              | 字串                           | 供應項目識別碼。    |
| addonItems           | **TransferLineItem**物件的清單 | 附加元件的 transferEntity 行專案集合，會連同正在傳送的基底訂用帳戶一起傳送。 在成功建立 transferEntity 時套用。|
| transferError        | 字串                           | 如果發生錯誤，則會接受 transferEntity 之後套用。                |
| status               | 字串           | TransferEntity 中 lineitem 的狀態。|

## <a name="transfersubmitresult"></a>TransferSubmitResult

代表傳輸接受的結果。

| 屬性          | 類型                                                  | 描述                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| 訂單            | [Order](order-resources.md#order)物件的清單。    | 訂單的集合。          |
| transferErrors    | [TransferError](#transfererror)物件的清單。      | 傳送錯誤的集合。 |

## <a name="transfererror"></a>TransferError

表示接受傳送時所發生的錯誤。

| 屬性          | 類型   | 描述                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | 字串 | 具有錯誤之訂單的訂單群組識別碼。 |
| code              | int    | 錯誤碼。                                 |
| description       | 字串 | 錯誤的描述。                   |
| lineItems         | **TransferLineItem**物件的清單 | TransferEntity 行專案的集合，這些專案是傳送錯誤的一部分。|

## <a name="transfererrorcode"></a>TransferErrorCode

[Enum/dotnet/api/system.string) 具有指出順序錯誤類型的值。

| 值 | 位置 | 描述 |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | 要求內容中缺少夥伴權杖。 |
| InvalidInput | 800002 | 要求輸入無效。 |
| >serviceexception | 800003 | 未預期的服務錯誤。 |
| InvalidOfferId | 800004 | 不正確供應專案識別碼。 |
| CreateOrderError | 800005 | Create order 不成功。 |
| MpnIdNotFound | 800015 | 找不到 MPN 識別碼。 |
| NotValidIndirectResellerMpnId | 800016 | MPN 識別碼不是有效的間接轉銷商。 |
| TransferIdNotFound | 900100   | 找不到傳輸要求。   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | 傳送要求已在進行中。|
| TransferNotAllowedIfStatusIsCompleted | 900102 | 傳送要求已完成。|
| TransferCreateOrderError | 900103 | 傳送順序不成功。|
| TransferProcessedByAnotherRequest | 900104 | 傳送正在由另一個要求處理。|