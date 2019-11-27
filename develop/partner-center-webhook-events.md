---
title: 合作夥伴中心 webhook 事件
description: 合作夥伴中心所支援之所有 Webhook 事件的檔。
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: c06f109132ba147baa2c243414ed1512998682ed
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486968"
---
# <a name="partner-center-webhook-events"></a>合作夥伴中心 webhook 事件

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 webhook 事件是以 HTTP Post 形式傳遞至已註冊 URL 的資源變更事件。 若要接收來自合作夥伴中心的事件，您可以裝載可供合作夥伴中心張貼事件的回呼。 事件經過數位簽署，因此您可以驗證它是否已從合作夥伴中心傳送。 

如需有關如何接收事件、驗證回呼，以及使用合作夥伴中心 webhook Api 來建立、查看和更新事件註冊的詳細資訊，請參閱[合作夥伴中心 webhook](partner-center-webhooks.md)。


## <a name="supported-events"></a>支援的事件

合作夥伴中心支援下列 webhook 事件。

### <a name="test-event"></a>測試事件

此事件可讓您透過要求測試事件並追蹤其進度，自行上線並測試您的註冊。 嘗試傳遞事件時，您將能夠看到 Microsoft 收到的失敗訊息。 這只會套用至「測試建立」事件，而超過7天的資料則會被清除。

>[!NOTE]
>發佈測試建立的事件時，每分鐘有2個要求的節流限制。

**屬性**

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 以 {resource}-{action} 形式呈現。 對於此事件，此值為「測試已建立」。                                          |
| resourceUri               | URI                                | 用來取得資源的 URI。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | 字串                             | 將觸發事件的資源名稱。 對於此事件，此值為 "test"。                                  |
| AuditUri                  | URI                                | 選擇性取得 audit 記錄的 URI （如果有的話）。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |



**範例**

```
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{{CorrelationId}}",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


### <a name="subscription-updated-event"></a>訂閱更新事件

當指定的訂用帳戶變更時，就會引發這個事件。 當透過合作夥伴中心 API 進行變更時，除了進行內部變更之外，也會產生訂用帳戶更新事件。 

>[!NOTE]
>在訂用帳戶變更和觸發訂閱更新事件的時間之間，最多會有48小時的延遲。  

**屬性**

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 以 {resource}-{action} 形式呈現。 對於此事件，此值為「訂用帳戶更新」。                                  |
| resourceUri               | URI                                | 用來取得資源的 URI。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | 字串                             | 將觸發事件的資源名稱。 對於此事件，值為「訂用帳戶」。                          |
| AuditUri                  | URI                                | 選擇性取得 audit 記錄的 URI （如果有的話）。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |



**範例**

```
{
    "EventName": "subscription-updated",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}",
    "ResourceName": "subscription",
    "AuditUri": "https://api.partnercenter.microsoft.com/v1/auditrecords/{{AuditId}}", 
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


### <a name="threshold-exceeded-event"></a>閾值已超過事件

這個事件會在任何客戶的 Microsoft Azure 使用量超過其使用量消費預算 (閾值) 時引發。 如需詳細資訊，請參閱[為您的客戶設定 Azure 消費預算](https://docs.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers)。

**屬性**

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 以 {resource}-{action} 形式呈現。 對於此事件，此值為 "usagerecords 和 resources-thresholdExceeded"。                                  |
| resourceUri               | URI                                | 用來取得資源的 URI。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | 字串                             | 將觸發事件的資源名稱。 對於此事件，此值為 "usagerecords 和 resources"。                          |
| AuditUri                  | URI                                | 選擇性取得 audit 記錄的 URI （如果有的話）。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |



**範例**

```
{
    "EventName": "usagerecords-thresholdExceeded",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/customers/usagerecords",
    "ResourceName": "usagerecords",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-created-event"></a>參考已建立事件

建立參考時，會引發此事件。 

**屬性**

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 以 {resource}-{action} 形式呈現。 對於此事件，此值為「已建立參考」。                                  |
| resourceUri               | URI                                | 用來取得資源的 URI。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | 字串                             | 將觸發事件的資源名稱。 對於此事件，此值為「參考」。                          |
| AuditUri                  | URI                                | 選擇性取得 audit 記錄的 URI （如果有的話）。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |



**範例**

```
{
    "EventName": "referral-created",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="referral-updated-event"></a>參考已更新事件

當參考更新時，就會引發此事件。 

**屬性**

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | 事件的名稱。 以 {resource}-{action} 形式呈現。 對於此事件，此值為「已更新參照」。                                  |
| resourceUri               | URI                                | 用來取得資源的 URI。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | 字串                             | 將觸發事件的資源名稱。 對於此事件，此值為「參考」。                          |
| AuditUri                  | URI                                | 選擇性取得 audit 記錄的 URI （如果有的話）。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。                                                         |



**範例**

```
{
    "EventName": "referral-updated",
    "ResourceUri": "https://api.partnercenter.microsoft.com/engagements/v1/referrals/{{ReferralID}}",
    "ResourceName": "referral",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}
```

### <a name="invoice-ready-event"></a>發票就緒事件

當新發票準備就緒時，就會引發此事件。

| 屬性                  | 類型                               | 描述                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | 字串 | 事件的名稱。 以 {resource}-{action} 形式呈現。 對於此事件，此值為「發票就緒」。 |
| resourceUri | URI | 用來取得資源的 URI。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | 字串 | 將觸發事件的資源名稱。 對於此事件，此值為 "invoice"。 |
| AuditUri |  URI | 選擇性取得 audit 記錄的 URI （如果有的話）。 使用語法： "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}"） |
| ResourceChangeUtcDate | UTC 日期時間格式的字串 | 發生資源變更的日期和時間。 |

**範例**

```
{
    "EventName": "invoice-ready",
    "ResourceUri": "https://api.partnercenter.microsoft.com/v1/invoices/{{InvoiceId}}",
    "ResourceName": "invoice",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2018-02-17T00:05:39.5485487+00:00"
}

```