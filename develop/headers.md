---
title: 合作夥伴中心 REST 標頭
description: 合作夥伴中心 REST API 支援下列 HTTP 要求和回應標頭。
ms.assetid: 38A43A4C-EC31-4554-A747-0DC04B77CB99
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 5ec3532ed30b3a9ff933bbda4e4923862091c895
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82157140"
---
# <a name="partner-center-rest-headers"></a>合作夥伴中心 REST 標頭

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 REST API 支援下列 HTTP 要求和回應標頭。 並非所有的 API 呼叫都會接受所有標頭。

## <a name="rest-request-headers"></a>REST 要求標頭

合作夥伴中心 REST API 支援下列 HTTP 要求標頭。

| 頁首                       | 描述                                                                                                                                                                                                                                                                            | 數值類型 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 授權：               | 必要。 採用持有人&lt;權杖&gt;格式的授權權杖。                                                                                                                                                                                                                    | 字串     |
| 接受                      | 指定要求和回應類型 "application/json"。                                                                                                                                                                                                                           | 字串     |
| MS-RequestId：                | 呼叫的唯一識別碼，用來確保 id-potency。 如果有超時，則重試呼叫應包含相同的值。 收到回應 (成功或業務失敗) 時，應針對下一個呼叫重設此值。                                            | GUID       |
| MS-CorrelationId：            | 呼叫的唯一識別碼，適用於要用來針對錯誤進行疑難排解的記錄和網路追蹤。 應針對每個呼叫重設此值。 所有作業都應該包含這個標頭。 如需詳細資訊，請參閱[測試和調試](test-and-debug.md)程式中的相互關聯識別碼資訊。 | GUID       |
| MS-合約-版本：         | 必要。 指定所要求的 API 版本;通常是 api 版本： v1，除非在[案例](scenarios.md)一節中另有指定。                                                                                                                                  | 字串     |
| If-Match：                    | 用於並行存取控制。 某些 API 呼叫需要透過 If-Match 標頭來傳遞 ETag。 ETag 通常位於資源上，因此需要最新的 GET-ting。 如需詳細資訊，請參閱[測試和調試](test-and-debug.md)程式中的 ETag 資訊。                | 字串     |
| PartnerCenter-應用程式 | 選擇性。 指定使用合作夥伴中心 REST API 的應用程式名稱。                                                                                                                                                                                             | 字串     |
| X-地區設定：                    | 選擇性。 指定傳回費率的語言。 預設值為 "en-us"。 如需支援值的清單，請參閱[合作夥伴中心支援的語言和地區](partner-center-supported-languages-and-locales.md)設定。                                                                                                                                                                                                  | 字串     |

## <a name="rest-response-headers"></a>REST 回應標頭

合作夥伴中心 REST API 可能會傳回下列 HTTP 回應標頭。

| 頁首            | 描述                                                                                                                                                                                                                                 | 數值類型 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| 接受           | 指定要求和回應類型 "application/json"。                                                                                                                                                                                | 字串     |
| MS-RequestId：     | 呼叫的唯一識別碼，用來確保 id-potency。 如果有超時，則重試呼叫應包含相同的值。 收到回應 (成功或業務失敗) 時，應針對下一個呼叫重設此值。 | GUID       |
| MS-CorrelationId： | 呼叫的唯一識別碼。 此值適用于疑難排解記錄和網路追蹤，以找出錯誤。 應針對每個呼叫重設此值。 所有作業都應該包含這個標頭。                                                       | GUID       |
