---
title: API 節流指導方針
description: 可能發生節流時
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a9fa70f8343ed51b288c1385540a247844e4659a
ms.sourcegitcommit: b3a8b6db5fee1cb8756b94105f358ed4bc94d3a5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/10/2020
ms.locfileid: "89666633"
---
# <a name="api-throttling-guidance"></a>API 節流指導方針 

**適用於**

- 合作夥伴中心

Microsoft 正在實行 API 節流，以在一段時間內為呼叫合作夥伴中心 API 的夥伴，提供更一致的效能。 節流會限制在某個時間範圍內對服務的要求數目，以避免過度使用資源。 雖然合作夥伴中心是設計用來處理大量的要求，但如果少數的夥伴發生大量的要求，則節流有助於維持所有夥伴的最佳效能和可靠性。  

節流限制視情節而異。 例如，如果您正在執行大量的寫入，則節流的可能性要高於僅執行讀取作業的可能性。

## <a name="what-happens-when-throttling-occurs"></a>發生節流時會發生什麼事？ 

當超過節流閾值時，合作夥伴中心會限制該用戶端在一段時間內的任何進一步要求。 節流行為可能取決於要求的類型和數目。   

### <a name="common-throttling-scenarios"></a>常見的節流案例 

造成針對用戶端進行節流的最常見案例包括： 

- **每一合作夥伴租使用者識別碼的 API 有大量要求**：針對某些合作夥伴中心 api，節流是由合作夥伴租使用者識別碼所決定，在相同的合作夥伴租使用者識別碼上，對這些 api 的呼叫過多會導致超過節流閾值。  

- 每個**客戶租使用者識別碼的 api 每個合作夥伴租使用者識別碼的大量要求**：對於其他 api，節流是由合作夥伴租使用者識別碼/客戶租使用者識別碼組合所決定;在這些情況下，對相同客戶租使用者識別碼進行太多呼叫將會導致節流，而對其他客戶的呼叫可能會成功。

## <a name="best-practices-to-avoid-throttling"></a>避免節流的最佳作法 
 
持續輪詢資源以檢查更新和定期掃描資源集合以檢查是否有新的或已刪除資源的程式設計實務，更有可能會導致節流，並會降低整體效能。 並行 API 呼叫可能會導致每個單位時間有大量的要求，這也會導致要求進行節流。 您應改為利用變更追蹤和變更通知。 此外，您應該能夠利用活動記錄來偵測變更，請參閱 [合作夥伴中心活動記錄](get-a-record-of-partner-center-activity-by-user.md) 檔以取得詳細資訊。  強烈建議合作夥伴考慮使用活動記錄 API 來提高效率，並避免節流。 另請參閱下方的使用活動記錄範例。

## <a name="best-practices-to-handle-throttling"></a>處理節流的最佳做法

以下是處理節流的最佳作法： 

- 降低平行處理原則的程度。 
- 減少呼叫的頻率。 
- 避免立即重試，因為所有要求都是根據您的使用量限制來累積。 

當您執行錯誤處理時，請使用 HTTP 錯誤碼429來偵測節流。 失敗的回應包含重試後的回應標頭。 使用 [重試] 來關閉要求是從節流復原的最快方式。 

若要使用 [在延遲後重試]，請執行下列動作： 

1. 請等候重試標頭中指定的秒數。 

2. 重試要求。  

3. 如果要求再次失敗，錯誤碼為429，表示您仍在進行節流。 以指數輪詢重試，使用建議的延遲後重試，然後重試要求，直到成功為止。

## <a name="apis-currently-impacted-by-throttling"></a>API 目前受到節流影響

長時間執行時，每個呼叫端點 "api.partnercenter.microsoft.com/" 的單一合作夥伴中心 API 都會進行節流處理。 目前，節流限制只會在下列幾個 API 上強制執行。 合作夥伴中心將會在每個 API 上收集遙測資料，並將動態調整節流限制。 下表列出目前強制執行節流的 API。  


|**運算**| **合作夥伴中心文件**|       
|------------------------|----------------------------|
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions|全客戶-訂用帳戶|    
|https://api.partnercenter.microsoft.com/v1/productUpgrades/eligibility|取得資格-產品升級|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}|依識別碼取得訂用帳戶|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders|取得所有客戶訂單|     
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}|依識別碼取得訂單|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus|取得訂用帳戶布建狀態|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}|管理訂單和管理訂用帳戶|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons|取得訂用帳戶的附加元件清單|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements|取得訂用帳戶的 azure 權利清單|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders|建立訂單|     
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus|取得訂用帳戶註冊狀態|    
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades|轉換訂用帳戶|          
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/transfers|取得所有客戶轉移|   
|https://api.partnercenter.microsoft.com/v1/productUpgrades/{upgrade-id}/status|取得產品升級狀態| 
|https://api.partnercenter.microsoft.com/v1/customers/{customer_id}/orders/{order_id}|依識別碼取得訂單|           
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/orders/{order-id}|購買訂用帳戶的附加元件|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}|建立購物車|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}/checkout|結帳購物車|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/carts/{cart-id}|更新購物車|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations|註冊訂用帳戶|  
|https://api.partnercenter.microsoft.com/v1/productupgrades|建立產品升級實體|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|
取得試用版轉換供應專案的清單|  
|https://api.partnercenter.microsoft.com/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions|
將試用訂用帳戶轉換為付費|   
|https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}|依識別碼取得客戶|

### <a name="error-code-response"></a>錯誤碼回應：

HTTP/1.1 429 的要求太多 

內容-長度：84 

Content-Type: application/json 

重試：57 

日期：週二、21月 2020 04:10:58 GMT 

{"statusCode"：429，"message"： "超過速率限制。 請于57秒後再試一次。」 } 


## <a name="example-of-activity-log"></a>活動記錄範例

為了分析每日變更的最佳做法，我們建議您查詢特定一天的 audit 記錄。 

在回應中，您會得到特定作業類型變更的結果。您可以根據您關心的作業進行篩選。 例如，如果您對新建立的客戶感興趣，您可以查看 operationType = "add_customer"。  

您可以在下列 API 檔中找到 operationtype/資源的清單。  

- [審核資源](https://docs.microsoft.com/partner-center/develop/auditing-resources)  

- [取得使用者的合作夥伴中心活動記錄](https://docs.microsoft.com/partner-center/develop/get-a-record-of-partner-center-activity-by-user)  



### <a name="response-example"></a>回應範例

**要求**：  

Http Get 呼叫： https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

授權：持有人 <token> 

Accept: application/json 

MS-RequestId：127facaa-e389-41f8-8bb7-1d1af99db893 

MS CorrelationId： de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X 地區設定： en-us 

主機： api.partnercenter.microsoft.com 

連接： Keep-alive 

**回應**：    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

  
