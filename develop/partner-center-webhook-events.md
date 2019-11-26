---
title: Partner Center webhook events
description: Documentation for all Webhook events supported by Partner Center.
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
# <a name="partner-center-webhook-events"></a>Partner Center webhook events

**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Partner Center webhook events are resource change events delivered in the form of HTTP POSTs to a registered URL. To receive an event from Partner Center, you host a callback where Partner Center can POST the event. The event is digitally signed so you can validate that it was sent from Partner Center. 

For information on how to receive events, authenticate a callback, and use the Partner Center webhook APIs to create, view, and update an event registration, see [Partner Center Webhooks](partner-center-webhooks.md).


## <a name="supported-events"></a>Supported Events

The following webhook events are supported by Partner Center.

### <a name="test-event"></a>Test Event

This event allows you to self-onboard and test your registration by requesting a test event and then tracking its progress. You will be able to see the failure messages that are being received from Microsoft while trying to deliver the event. This will only apply to "test-created" events and data older than 7 days will be purged.

>[!NOTE]
>There is a throttle limit of 2 requests per minute when posting a test-created event.

**屬性**

| 屬性                  | 在工作列搜尋方塊中輸入                               | 說明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | The name of the event. In the form {resource}-{action}. For this event, the value is "test-created".                                          |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/webhooks/v1/registration/validationEvents/{{CorrelationId}}" |
| ResourceName              | 字串                             | The name of the resource that will trigger the event. For this event, the value is "test".                                  |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



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


### <a name="subscription-updated-event"></a>Subscription Updated Event

This event is raised when the specified subscription changes. A Subscription Updated event is generated when there is an internal change in addition to when changes are made through the Partner Center API. 

>[!NOTE]
>There is a delay of up to 48 hours between the time a subscription changes and when the Subscription Updated event is triggered.  

**屬性**

| 屬性                  | 在工作列搜尋方塊中輸入                               | 說明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | The name of the event. In the form {resource}-{action}. For this event, the value is "subscription-updated".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/webhooks/v1/customers/{{CustomerId}}/subscriptions/{{SubscriptionId}}" |
| ResourceName              | 字串                             | The name of the resource that will trigger the event. For this event, the value is "subscription".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



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


### <a name="threshold-exceeded-event"></a>Threshold Exceeded Event

這個事件會在任何客戶的 Microsoft Azure 使用量超過其使用量消費預算 (閾值) 時引發。 For more information, see  [Set an Azure spending budget for your customers](https://docs.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers).

**屬性**

| 屬性                  | 在工作列搜尋方塊中輸入                               | 說明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | The name of the event. In the form {resource}-{action}. For this event, the value is "usagerecords-thresholdExceeded".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/webhooks/v1/customers/usagerecords" |
| ResourceName              | 字串                             | The name of the resource that will trigger the event. For this event, the value is "usagerecords".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



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

### <a name="referral-created-event"></a>Referral Created Event

This event is raised when the referral is created. 

**屬性**

| 屬性                  | 在工作列搜尋方塊中輸入                               | 說明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | The name of the event. In the form {resource}-{action}. For this event, the value is "referral-created".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | 字串                             | The name of the resource that will trigger the event. For this event, the value is "referral".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



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

### <a name="referral-updated-event"></a>Referral Updated Event

This event is raised when the referral is updated. 

**屬性**

| 屬性                  | 在工作列搜尋方塊中輸入                               | 說明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName                 | 字串                             | The name of the event. In the form {resource}-{action}. For this event, the value is "referral-updated".                                  |
| ResourceUri               | URI                                | The URI to get the resource. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/engagements/v1/referrals/{{ReferralID}}" |
| ResourceName              | 字串                             | The name of the resource that will trigger the event. For this event, the value is "referral".                          |
| AuditUri                  | URI                                | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}" |
| ResourceChangeUtcDate     | string in the UTC date-time format | The date and time when the resource change occurred.                                                         |



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

### <a name="invoice-ready-event"></a>Invoice Ready Event

This event is raised when the new invoice is ready.

| 屬性                  | 在工作列搜尋方塊中輸入                               | 說明                                                                                                  |
|---------------------------|------------------------------------|--------------------------------------------------------------------------------------------------------------|
| EventName | 字串 | The name of the event. In the form {resource}-{action}. For this event, the value is "invoice-ready". |
| ResourceUri | URI | The URI to get the resource. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/v1/invoices/{{InvoiceId}}" |
| ResourceName | 字串 | The name of the resource that will trigger the event. For this event, the value is "invoice". |
| AuditUri |  URI | (Optional) The URI to get the audit record, if it exists. Uses the syntax: "[ *{baseURL}* ](partner-center-rest-urls.md)/auditactivity/v1/auditrecords/{{AuditId}}") |
| ResourceChangeUtcDate | string in the UTC date-time format | The date and time when the resource change occurred. |

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