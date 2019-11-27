---
title: 驗證位址
description: 如何使用位址驗證 API 驗證位址。
ms.assetid: 38A136CD-5E42-46D2-85A4-ED08E30444B8
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: aaa7e7ecb10b73a27ce6e406df95f1fe073d8f28
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487748"
---
# <a name="validate-an-address"></a>驗證位址

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

如何使用位址驗證 API 驗證位址。

位址驗證 API 只應用於客戶設定檔更新的預先驗證。 請使用它來瞭解，如果國家/地區為美國、加拿大、中國或墨西哥，則 [狀態] 欄位會針對個別國家/地區的有效狀態清單進行驗證。 在所有其他國家/地區，則不會進行這項測試，而且 API 只會檢查狀態是否為有效的字串。

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件

如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。

## <a name="span-idexamplesspan-idexamplesspan-idexamplesexamples"></a><span id="Examples"/><span id="examples"><span id="EXAMPLES"/>範例

### <a name="c"></a>C#

若要驗證位址，請先具現化新的**位址**物件，並在其中填入要驗證的位址。 然後，抓取介面來**驗證** **iaggregatepartner.customers.byid**屬性的作業，並使用 address 物件呼叫**IsAddressValid**方法。

```csharp
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address()
{
    AddressLine1 = "One Microsoft Way",
    City = "Redmond",
    State = "WA",
    PostalCode = "98052",    
    Country = "US"
};

// Validate the address.
bool result = partnerOperations.Validations.IsAddressValid(address);

// If the address is valid, the result should equal true.
Console.WriteLine("Result: " + result.ToString());

// The following is an example that causes address validation to fail.
try
{
    // Change to an invalid postal code for this address.
    address.PostalCode = "98007";
             
    // Validate the address.
    result = partnerOperations.Validations.IsAddressValid(address);
    
    Console.WriteLine("ERROR: The code should have thrown an exception - BadRequest(400).");
}
catch (PartnerException exception)
{
    if (exception.ErrorCategory == PartnerErrorCategory.BadInput)
    {
        Console.WriteLine(exception.ErrorCategory.ToString());
        Console.WriteLine("Exception:");
        Console.WriteLine("Message: {0}", exception.Message);
    }
    else
    {
        throw;
    }
}
```

### <a name="java"></a>Java

若要驗證位址，請先具現化新的**位址**物件，並在其中填入要驗證的位址。 然後，抓取介面以**驗證**來自**iaggregatepartner.customers.byid. getValidations**函式的作業，並使用 address 物件呼叫**isAddressValid**方法。

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

```java
// IAggregatePartner partnerOperations;

// Create an address to validate.
Address address = new Address();

address.setAddressLine1("One Microsoft Way");
address.setCity("Redmond");
address.setState("WA");
address.setCountry("US");
address.setPostalCode("98052");

try
{
    // Validate the address
    Boolean validationResult = partnerOperations.getValidations().isAddressValid(address);

    System.out.println(validationResult ? "The address is valid." : "Invalid address");
}
catch (Exception exception)
{
    System.out.println("Address is invalid");
    
    if (! StringHelper.isNullOrWhiteSpace(exception.getMessage()))
    {
        System.out.println(exception.getMessage());
    }
}
```

### <a name="powershell"></a>PowerShell

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

若要驗證位址，請使用已填入的位址參數執行[**測試 PartnerAddress**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Test-PartnerAddress.md) 。

```powershell
Test-PartnerAddress -AddressLine1 '700 Bellevue Way NE' -City 'Bellevue' -Country 'US' -PostalCode '98004' -State 'WA'
```

## <a name="span-id_requestspan-id_requestspan-id_request-rest-request"></a><span id="_Request"/><span id="_request"/><span id="_REQUEST"/> REST 要求

**要求語法**

| 方法   | 要求 URI                                                                 |
|----------|-----------------------------------------------------------------------------|
| **發佈** | [ *{baseURL}* ](partner-center-rest-urls.md)/v1/validations/address HTTP/1。1 |

**要求標頭**

- 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

**要求本文**

下表描述要求主體中的必要屬性。

| 名稱         | 類型   | 必要 | 描述                                                |
|--------------|--------|----------|------------------------------------------------------------|
| addressline1 | 字串 | Y        | 位址的第一行。                             |
| addressline2 | 字串 | N        | 位址的第二行。 這個屬性為選擇性。 |
| 鹽湖城         | 字串 | Y        | 城市。                                                  |
| state        | 字串 | Y        | 狀態。                                                 |
| postalcode   | 字串 | Y        | 郵遞區號。                                           |
| 國家/地區      | 字串 | Y        | 兩個字元的 ISO Alpha 2 國家/地區代碼。                |

**要求範例**

```http
POST https://api.partnercenter.microsoft.com/v1/validations/address HTTP/1.1
Content-Type: application/json
Authorization: Bearer <token> 
Accept: application/json
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 129

{
    AddressLine1: "One Microsoft Way",
    City: "Redmond",
    State: "WA",
    PostalCode: "98052",
    Country: "US"
}
```

## <a name="span-idresponsespan-idresponsespan-idresponseresponse"></a><span id="Response"/><span id="response"/><span id="RESPONSE"/>回應

如果成功，方法會傳回狀態碼200，如下列回應驗證成功範例所示。

如果要求失敗，此方法會傳回狀態碼400，如以下顯示的回應驗證失敗範例所示。 回應主體包含 JSON 承載，以及有關錯誤的其他資訊。

**回應成功和錯誤碼**

每個回應都隨附 HTTP 狀態碼，指出成功或失敗，以及其他的偵錯工具資訊。 使用網路追蹤工具來讀取此程式碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

**回應驗證成功範例**

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: IqhjoWVyq0Kl81dO.0
MS-ServerId: 030011719
Date: Mon, 13 Mar 2017 23:56:12 GMT
```

**回應-驗證失敗範例**

```http
HTTP/1.1 400 Bad Request
Content-Length: 418
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8a853a1a-b0e6-4cb0-ae87-d6dd32ac3a0c
MS-RequestId: 0b30452a-8be2-4b8b-b25b-2d4850f4345f
MS-CV: pdlItMyvtkmGHDWt.0
MS-ServerId: 101112012
Date: Tue, 14 Mar 2017 01:57:55 GMT

{
    "code": 2007,
    "description": "{\"code\":\"60071\",\"reason\":\"ZipCityInvalid - Details: Field - &#39;City&#39; is corrected from OldValue: &#39;Redmond&#39; to NewValue: &#39;BELLEVUE&#39;.\",\"corrected_address\":{\"country\":\"US\",\"region\":\"WA\",\"city\":\"BELLEVUE\",\"address_line1\":\"One Microsoft Way\",\"postal_code\":\"98007\"},\"object_type\":\"AddressValidation\",\"resource_status\":\"Active\"}",
    "data": [],
    "source": "PartnerFD"
}
```