---
title: Partner Center REST error codes
description: Description of error codes and success responses from the Partner Center APIs.
ms.assetid: 08AC1F2E-5847-4AD8-AE5B-0173C5DB589A
ms.date: 06/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7f9cb33c2518cef84d6948783da7d2c4337ecfaa
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489668"
---
# <a name="partner-center-rest-error-codes"></a>Partner Center REST error codes

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The Partner Center REST APIs return a JSON object that contains a status code. This code that indicates whether your request was successful or why it failed.

## <a name="success-responses"></a>Success responses

A **2xx** status code indicates that the client's request was successfully received, understood, and accepted.

## <a name="error-codes"></a>錯誤碼

The following **4xx** and **5xx** status codes indicate an error:

- 400: Bad request
- 401: Unauthorized
- 403: Forbidden
- 404: Not found
- 405: Method not allowed
- 406: Not acceptable
- 409: Conflict, error code
- 412: Precondition failed
- 429: Too many requests
- 500: Internal server error
- 501: Not implemented
- 502: Bad gateway
- 503: Service unavailable
- 504: Gateway timeout

## <a name="error-responses"></a>錯誤回應

Any response with a **4xx** or **5xx** status code includes an error message with additional details about the error condition(s) encountered.

The following table and code sample describes the schema of an error response:

| 名稱        | 在工作列搜尋方塊中輸入   | 說明                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| code        | 字串 | Always returned. Indicates the kind of error that occurred. Non-null.                                                                                  |
| 描述 | 字串 | Always returned. Describes the error in detail, and provides additional debugging information. Non-null, non-empty. Maximum length is 1024 characters. |
| 資料        | 陣列  | Only returned for some error types. A list of error objects.                                                                                           |
| source      | 字串 | Always returned. The source of the error.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
## }
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```
