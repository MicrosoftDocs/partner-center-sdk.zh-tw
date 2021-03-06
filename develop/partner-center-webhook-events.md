---
title: 合作夥伴中心 webhook 事件
description: 合作夥伴中心所支援之所有 Webhook 事件的檔。
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 5358aab8efdd68ad52c583936304f99ffae12708
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90926851"
---
# <a name="partner-center-webhook-events"></a>合作夥伴中心 webhook 事件

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 webhook 事件是以 HTTP Post 形式傳遞至已註冊 URL 的資源變更事件。 若要接收來自合作夥伴中心的事件，您可以裝載合作夥伴中心可以張貼事件的回呼。 事件經過數位簽署，因此您可以驗證它是否已從合作夥伴中心傳送。

如需如何接收事件、驗證回呼，以及使用合作夥伴中心 webhook Api 來建立、查看及更新事件註冊的詳細資訊，請參閱 [合作夥伴中心 webhook](partner-center-webhooks.md)。

## <a name="supported-events"></a>支援的事件

合作夥伴中心支援下列 webhook 事件。

### <a name="test-event"></a>測試事件

此事件可讓您藉由要求測試事件並追蹤其進度，來自我上架並測試您的註冊。 當您嘗試傳遞事件時，您將能夠看到 Microsoft 收到的失敗訊息。 這只會套用至「測試建立」事件，超過7天的資料將會被清除。

>[!NOTE]
>張貼測試建立事件時，每分鐘會有2個要求的節流限制。

#### <a name="properties"></a>屬性

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 格式為 {resource}-{action}。 對於此事件，此值為「測試建立」。                                          |
| ResourceUri               | URI                                | 取得資源的 URI。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | 字串                             | 將觸發事件之資源的名稱。 對於此事件，此值為 "test"。                                  |
| AuditUri                  | URI                                |  (選擇性) URI 取得審核記錄（如果有的話）。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |

#### <a name="example"></a>範例

```json
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="subscription-updated-event"></a>訂用帳戶更新事件

當指定的訂閱變更時，就會引發此事件。 除了透過合作夥伴中心 API 進行變更以外，還有內部變更時，也會產生訂用帳戶更新事件。  此事件只會在有商務層級變更時產生，例如，當您修改授權數目時，以及當訂用帳戶的狀態變更時。 在訂用帳戶內建立資源時，不會產生此檔案。

>[!NOTE]
>訂用帳戶變更和觸發訂閱更新事件的時間之間，延遲最多為48小時。

#### <a name="properties"></a>屬性

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 格式為 {resource}-{action}。 對於此事件，此值為「訂閱更新」。                                  |
| ResourceUri               | URI                                | 取得資源的 URI。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | 字串                             | 將觸發事件之資源的名稱。 對於此事件，此值為 "訂用帳戶"。                          |
| AuditUri                  | URI                                |  (選擇性) URI 取得審核記錄（如果有的話）。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |

#### <a name="example"></a>範例

```json
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}",
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```

### <a name="threshold-exceeded-event"></a>超過閾值事件

當任何客戶 Microsoft Azure 使用量超過其使用量支出預算 (其) 的閾值時，就會引發此事件。 如需詳細資訊，請參閱 [為您的客戶/合作夥伴中心/集合---azure-消費-預算-客戶) 設定 Azure 費用預算。

#### <a name="properties"></a>屬性

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 格式為 {resource}-{action}。 對於此事件，此值為 ">usagerecords-thresholdExceeded"。                                  |
| ResourceUri               | URI                                | 取得資源的 URI。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | 字串                             | 將觸發事件之資源的名稱。 此事件的值為 ">usagerecords"。                          |
| AuditUri                  | URI                                |  (選擇性) URI 取得審核記錄（如果有的話）。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |

#### <a name="example"></a>範例

```json
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>參考建立的事件

建立參考時，就會引發此事件。

#### <a name="properties"></a>屬性

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 格式為 {resource}-{action}。 對於此事件，此值為「參考建立」。                                  |
| ResourceUri               | URI                                | 取得資源的 URI。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | 字串                             | 將觸發事件之資源的名稱。 對於此事件，此值為「參考」。                          |
| AuditUri                  | URI                                |  (選擇性) URI 取得審核記錄（如果有的話）。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |

#### <a name="example"></a>範例

```json
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>參考更新事件

當參考更新時，就會引發此事件。

#### <a name="properties"></a>屬性

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 格式為 {resource}-{action}。 對於此事件，此值為「參考更新」。                                  |
| ResourceUri               | URI                                | 取得資源的 URI。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | 字串                             | 將觸發事件之資源的名稱。 對於此事件，此值為「參考」。                          |
| AuditUri                  | URI                                |  (選擇性) URI 取得審核記錄（如果有的話）。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |

#### <a name="example"></a>範例

```json
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>發票就緒活動

當新的發票就緒時，就會引發此事件。

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | 字串 | 事件的名稱。 格式為 {resource}-{action}。 對於此事件，此值為「發票就緒」。 |
| ResourceUri | URI | 取得資源的 URI。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | 字串 | 將觸發事件之資源的名稱。 對於此事件，此值為 "invoice"。 |
| AuditUri |  URI |  (選擇性) URI 取得審核記錄（如果有的話）。 使用語法： "[*{baseURL}*](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" )  |
| ResourceChangeUtcDate | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。 |

#### <a name="example"></a>範例

```json
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```
