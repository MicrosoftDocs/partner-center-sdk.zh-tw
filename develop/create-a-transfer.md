---
title: 建立傳輸
description: 如何為客戶建立訂閱的轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e77711f2bda6d4e5af536ed2658df63241462c31
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82154810"
---
# <a name="create-a-transfer"></a>建立傳輸

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

## <a name="prerequisites"></a>Prerequisites

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

- 客戶識別碼（`customer-tenant-id`）。 如果您不知道客戶的識別碼，您可以在 [合作夥伴中心][儀表板](https://partner.microsoft.com/dashboard)中查閱。 從 [合作夥伴中心] 功能表選取 [ **CSP** ]，後面接著 [**客戶**]。 從 [客戶] 清單中選取客戶，然後選取 [**帳戶**]。 在客戶的帳戶頁面上，尋找 [**客戶帳戶資訊**] 區段中的 [ **Microsoft ID** ]。 Microsoft ID 與客戶識別碼（`customer-tenant-id`）相同。

## <a name="rest-request"></a>REST 要求

### <a name="request-syntax"></a>要求的語法

| 方法   | 要求 URI                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **POST** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1。1                    |

### <a name="uri-parameter"></a>URI 參數

使用下列路徑參數來識別客戶。

| 名稱            | 類型     | 必要 | 描述                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **客戶識別碼** | 字串   | 是      | 識別客戶的 GUID 格式客戶識別碼。             |

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

下表描述要求主體中的[TransferEntity](transfer-entity-resources.md)屬性。

| 屬性              | 類型          | 必要  | 描述                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| id                    | 字串        | 否    | 成功建立 transferEntity 時所提供的 transferEntity 識別碼。                               |
| createdTime           | Datetime      | 否    | TransferEntity 的建立日期（以日期時間格式）。 已在成功建立 transferEntity 時套用。      |
| lastModifiedTime      | Datetime      | 否    | 上次更新 transferEntity 的日期（以日期時間格式）。 已在成功建立 transferEntity 時套用。 |
| lastModifiedUser      | 字串        | 否    | 上次更新 transferEntity 的使用者。 已在成功建立 transferEntity 時套用。                          |
| customerName          | 字串        | 否    | 選擇性。 要轉移其訂閱的客戶名稱。                                              |
| customerTenantId      | 字串        | 否    | 識別客戶的 GUID 格式客戶識別碼。 已在成功建立 transferEntity 時套用。         |
| partnertenantid       | 字串        | 否    | 識別合作夥伴的 GUID 格式合作夥伴識別碼。                                                                   |
| sourcePartnerName     | 字串        | 否    | 選擇性。 起始轉移的夥伴組織名稱。                                           |
| sourcePartnerTenantId | 字串        | 是   | GUID 格式的夥伴識別碼，識別起始傳輸的夥伴。                                           |
| targetPartnerName     | 字串        | 否    | 選擇性。 傳送目標的夥伴組織名稱。                                         |
| targetPartnerTenantId | 字串        | 是   | GUID 格式的夥伴識別碼，可識別傳送目標的夥伴。                                  |
| lineItems             | 物件的陣列 | 是| [TransferLineItem](transfer-entity-resources.md#transferlineitem)資源的陣列。                                   |
| status                | 字串        | 否    | TransferEntity 的狀態。 可能的值為「作用中」（可以刪除/提交）和「已完成」（已完成）。 已在成功建立 transferEntity 時套用。|

下表描述要求主體中的[TransferLineItem](transfer-entity-resources.md#transferlineitem)屬性。

|      屬性       |            類型             | 必要 | 描述                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| id                   | 字串                     | 否       | 傳送明細專案的唯一識別碼。 已在成功建立 transferEntity 時套用。|
| subscriptionId       | 字串                     | 是      | 訂用帳戶識別碼。                                                                         |
| quantity             | int                        | 否       | 授權或實例的數目。                                                                 |
| billingCycle         | Object                     | 否       | 針對目前期間所設定的計費週期類型。                                                |
| friendlyName         | 字串                     | 否       | 選擇性。 由夥伴定義以協助區分的專案易記名稱。                |
| partnerIdOnRecord    | 字串                     | 否       | 在購買時 PartnerId 記錄（MPNID），這是在接受轉移時所發生。              |
| offerId              | 字串                     | 否       | 供應項目識別碼。                                                                                |
| addonItems           | **TransferLineItem**物件的清單 | 否 | 附加元件的 transferEntity 行專案集合，將與所傳輸的基底訂用帳戶一起傳輸。 已在成功建立 transferEntity 時套用。|
| transferError        | 字串                     | 否       | 在發生錯誤的情況下接受 transferEntity 之後套用。                                        |
| status               | 字串                     | 否       | TransferEntity 中 lineitem 的狀態。                                                    |

### <a name="request-example"></a>要求範例

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回已填入的[TransferEnity](transfer-entity-resources.md)資源。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。 請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
