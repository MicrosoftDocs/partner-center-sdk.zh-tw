---
title: TransferEntity 資源
description: 當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 550c9cffdc7dd5c6fbf5b2aaf5051618106bd185
ms.sourcegitcommit: 4b1c10f91962861244c9349d5b9a9ba354b35b24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2020
ms.locfileid: "81220744"
---
# <a name="transferentity-resources"></a>TransferEntity 資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。

## <a name="transferentity"></a>TransferEntity

描述 transferEntity。

| 屬性              | 類型             | 描述                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| id                    | string           | 成功建立 transferEntity 時所提供的 transferEntity 識別碼。                               |
| createdTime           | DateTime         | TransferEntity 的建立日期（以日期時間格式）。 已在成功建立 transferEntity 時套用。      |
| lastModifiedTime      | DateTime         | 上次更新 transferEntity 的日期（以日期時間格式）。 已在成功建立 transferEntity 時套用。 |
| lastModifiedUser      | string           | 上次更新 transferEntity 的使用者。 已在成功建立 transferEntity 時套用。                          |
| customerName          | string           | 選擇性。 要轉移其訂閱的客戶名稱。                                              |
| customerTenantId      | string           | 識別客戶的 GUID 格式客戶識別碼。 已在成功建立 transferEntity 時套用。         |
| partnertenantid       | string           | 識別合作夥伴的 GUID 格式合作夥伴識別碼。                                                                   |
| sourcePartnerName     | string           | 選擇性。 起始轉移的夥伴組織名稱。                                           |
| sourcePartnerTenantId | string           | GUID 格式的夥伴識別碼，識別起始傳輸的夥伴。                                           |
| targetPartnerName     | string           | 選擇性。 傳送目標的夥伴組織名稱。                                         |
| targetPartnerTenantId | string           | GUID 格式的夥伴識別碼，可識別傳送目標的夥伴。                                  |
| lineItems             | 物件的陣列 | [TransferLineItem](#transferlineitem)資源的陣列。                                                   |
| status                | string           | TransferEntity 的狀態。 可能的值為「作用中」（可以刪除/提交）和「已完成」（已完成）。 已在成功建立 transferEntity 時套用。|

## <a name="transferlineitem"></a>TransferLineItem

表示 transferEntity 中包含的一個專案。

| 屬性             | 類型                             | 描述                                                                                             |
|----------------------|----------------------------------|---------------------------------------------------------------------------------------------------------|
| id                   | string                           | 傳送明細專案的唯一識別碼。 已在成功建立 transferEntity 時套用。   |
| subscriptionId       | string                           | 訂用帳戶識別碼。                                                                            |
| quantity             | int                              | 授權或實例的數目。                                                                    |
| billingCycle         | 物件                           | 針對目前期間所設定的計費週期類型。                                                   |
| friendlyName         | string                           | 選擇性。 由夥伴定義以協助區分的專案易記名稱。                   |
| partnerIdOnRecord    | string                           | 在購買時 PartnerId 記錄（MPNID），這是在接受轉移時所發生。                 |
| offerId              | string                           | 供應專案識別碼。    |
| addonItems           | **TransferLineItem**物件的清單 | 附加元件的 transferEntity 行專案集合，將與所傳輸的基底訂用帳戶一起傳輸。 已在成功建立 transferEntity 時套用。|
| transferError        | string                           | 在發生錯誤的情況下接受 transferEntity 之後套用。                |
| status               | string           | TransferEntity 中 lineitem 的狀態。|

## <a name="transfersubmitresult"></a>TransferSubmitResult

表示傳輸接受的結果。

| 屬性          | 類型                                                  | 描述                        |
|-------------------|-------------------------------------------------------|------------------------------------|
| 訂單            | [Order](order-resources.md#order)物件的清單。    | 訂單的集合。          |
| transferErrors    | [TransferError](#transfererror)物件的清單。      | 傳輸錯誤的集合。 |

## <a name="transfererror"></a>TransferError

表示接受傳輸時所發生的錯誤。

| 屬性          | 類型   | 描述                                     |
|-------------------|--------|-------------------------------------------------|
| transferGroupId   | string | 具有錯誤之訂單的順序群組識別碼。 |
| code              | int    | 錯誤碼。                                 |
| description       | string | 錯誤的描述。                   |
| lineItems         | **TransferLineItem**物件的清單 | 屬於傳送錯誤之一部分的 transferEntity 行專案集合。|

## <a name="transfererrorcode"></a>TransferErrorCode

具有值的[列舉](https://docs.microsoft.com/dotnet/api/system.enum)，指出順序錯誤的類型。

| 值 | Position | 描述 |
| --- | --- | --- |
| PartnerTokenMissing | 800001 | 要求內容中缺少合作夥伴 Token。 |
| InvalidInput | 800002 | 不正確要求輸入。 |
| ServiceException | 800003 | 未預期的服務錯誤。 |
| InvalidOfferId | 800004 | 供應專案識別碼無效。 |
| CreateOrderError | 800005 | 建立訂單不成功。 |
| MpnIdNotFound | 800015 | 找不到 MPN 識別碼。 |
| NotValidIndirectResellerMpnId | 800016 | MPN 識別碼不是有效的間接轉銷商。 |
| TransferIdNotFound | 900100   | 找不到傳輸要求。   |
| TransferNotAllowedIfStatusIsInProgress | 900101 | 傳送要求已在進行中。|
| TransferNotAllowedIfStatusIsCompleted | 900102 | 傳送要求已完成。|
| TransferCreateOrderError | 900103 | 傳送順序不成功。|
| TransferProcessedByAnotherRequest | 900104 | 傳輸正由另一個要求處理。|