---
title: Update a cart
description: How to update an order for a customer in a cart.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 70e20f1261f29468c5b0b7e017f29f6e64b91cf6
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487948"
---
# <a name="update-a-cart"></a>Update a cart


**Applies To**

- 合作夥伴中心


How to update an order for a customer in a cart. 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>Prerequisites


- Credentials as described in [Partner Center authentication](partner-center-authentication.md). This scenario supports authentication with both standalone App and App+User credentials.
- A customer identifier. If you do not have a customer's ID, you can look up the ID in Partner Center by choosing the customer from the customers list, selecting Account, then saving their Microsoft ID.
- A Cart ID for an existing cart.


## <a name="span-idc_span-idc_c"></a><span id="C_"/><span id="c_"/>C#


To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID's using the **ById()** function. Make the necessary changes to the cart. Now call the **Put** method by using customer and cart ID's using the **ById()** method.

Finally, call the **Put()** or **PutAsync()** method to create the order.



``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request


**Request syntax**

| 方法  | 要求 URI                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

 

**URI parameters**

Use the following path parameters to identify the customer, and specify the cart to be updated.

| 名稱            | 在工作列搜尋方塊中輸入     | 必要 | 說明                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | 字串   | [是]      | A GUID formatted customer-id that identifies the customer.             |
| **cart-id**     | 字串   | [是]      | A GUID formatted cart-id that identifies the cart.                     |

 

**Request headers**

- See [Partner Center REST headers](headers.md) for more information.

**Request body**

This table describes the [Cart](cart-resources.md) properties in the request body.

| 屬性              | 在工作列搜尋方塊中輸入             | 必要        | 說明                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| id                    | 字串           | 無              | A cart identifier that is supplied upon successful creation of the cart.                                  |
| creationTimeStamp     | DateTime         | 無              | The date the cart was created, in date-time format. Applied upon successful creation of the cart.        |
| lastModifiedTimeStamp | DateTime         | 無              | The date the cart was last updated, in date-time format. Applied upon successful creation of the cart.    |
| expirationTimeStamp   | DateTime         | 無              | The date the cart will expire, in date-time format.  Applied upon successful creation of cart.            |
| lastModifiedUser      | 字串           | 無              | The user who last updated the cart. Applied upon successful creation of cart.                             |
| lineItems             | Array of objects | [是]             | An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.                                               |


This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.

| 屬性             | 在工作列搜尋方塊中輸入                        | 必要     | 說明                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| id                   | 字串                      | 無           | A Unique identifier for a cart line item. Applied upon successful creation of cart.                |
| catalogId            | 字串                      | [是]          | The catalog item identifier.                                                                       |
| friendlyName         | 字串                      | 無           | 選用。 The friendly name for the item defined by the partner to help disambiguate.              |
| quantity             | 整數                         | [是]          | The number of licenses or instances.     |
| currencyCode         | 字串                      | 無           | The currency code.                                                                                 |
| billingCycle         | 物件                      | [是]          | The type of billing cycle set for the current period.                                              |
| 參與者         | List of Object String pairs | 無           | A collection of participants on the purchase.                                                      |
| provisioningContext  | Dictionary<string, string>  | 無           | A context used for provisioning of offer.                                                          |
| orderGroup           | 字串                      | 無           | A group to indicate which items can be placed together.                                            |
| 錯誤 (error)                | 物件                      | 無           | Applied after cart is created in case of an error.                                                 |


**Request example**

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com 
Content-Length: 496
Expect: 100-continue

{  
    {  
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[  
            {  
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="span-idresponsespan-idresponsespan-idresponserest-response"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>REST Response


If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.

**Response success and error codes**

Each response comes with an HTTP status code that indicates success or failure and additional debugging information. Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Error Codes](error-codes.md).

**Response example**

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }            
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```

 

 




