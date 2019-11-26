---
title: 合作夥伴中心 REST 標頭
description: 合作夥伴中心 REST API 支援下列 HTTP 要求和回應標頭。
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: f5adf9a458148c1e68cf17a3014cb1931e8860be
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74487108"
---
# <a name="partner-center-rest-headers"></a>合作夥伴中心 REST 標頭


**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 REST API 支援下列 HTTP 要求和回應標頭。 並非所有的 API 呼叫都會接受所有標頭。

## <a name="span-idrequest_headersspan-idrequest_headersspan-idrequest_headersrequest-headers"></a><span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>要求標頭


合作夥伴中心 REST API 支援下列 HTTP 要求標頭。

| 標頭                       | 描述                                                                                                                                                                                                                                                                            | 值類型 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 驗證               | 必要。 持有人 &lt;權杖&gt;的授權權杖。                                                                                                                                                                                                                    | 字串     |
| 接受                      | 指定要求和回應類型 "application/json"。                                                                                                                                                                                                                           | 字串     |
| MS-RequestId：                | 呼叫的唯一識別碼，用來確保識別碼-含量。 在超時的情況下，重試呼叫應包含相同的值。 收到回應（成功或商務失敗）時，應該針對下一個呼叫重設值。                                            | GUID       |
| MS-CorrelationId：            | 呼叫的唯一識別碼，適用于用於疑難排解錯誤的記錄和網路追蹤。 應針對每個呼叫重設此值。 所有作業都應該包含這個標頭。 如需詳細資訊，請參閱[測試和調試](test-and-debug.md)程式中的相互關聯識別碼資訊。 | GUID       |
| MS-合約-版本：         | 必要。 指定所要求的 API 版本;通常是 api 版本： v1，除非在[案例](scenarios.md)一節中另有指定。                                                                                                                                  | 字串     |
| If-match：                    | 用於並行存取控制。 某些 API 呼叫需要透過 If-match 標頭傳遞 ETag。 ETag 通常是在資源上，因此需要 ting 最新的。 如需詳細資訊，請參閱[測試和調試](test-and-debug.md)程式中的 ETag 資訊。                | 字串     |
| PartnerCenter-應用程式 | 選用。 指定使用合作夥伴中心 REST API 的應用程式名稱。                                                                                                                                                                                             | 字串     |
| X-地區設定：                    | 選用。 指定傳回費率的語言。 預設值為 "en-us"。 如需支援值的清單，請參閱[合作夥伴中心支援的語言和地區](partner-center-supported-languages-and-locales.md)設定。                                                                                                                                                                                                  | 字串     |

 

## <a name="span-idresponse_headersspan-idresponse_headersspan-idresponse_headersresponse-headers"></a><span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>回應標頭


合作夥伴中心 REST API 可能會傳回下列 HTTP 回應標頭。

| 標頭            | 描述                                                                                                                                                                                                                                 | 值類型 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 接受           | 指定要求和回應類型 "application/json"。                                                                                                                                                                                | 字串     |
| MS-RequestId：     | 呼叫的唯一識別碼，用來確保識別碼-含量。 在超時的情況下，重試呼叫應包含相同的值。 收到回應（成功或商務失敗）時，應該針對下一個呼叫重設值。 | GUID       |
| MS-CorrelationId： | 呼叫的唯一識別碼，適用于疑難排解錯誤的記錄和網路追蹤。 應針對每個呼叫重設此值。 所有作業都應該包含這個標頭。                                                       | GUID       |

 

 

 




