---
title: Partner Center REST headers
description: The following HTTP request and response headers are supported by the Partner Center REST API.
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
# <a name="partner-center-rest-headers"></a>Partner Center REST headers


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The following HTTP request and response headers are supported by the Partner Center REST API. Not all API calls accept all headers.

## <a name="span-idrequest_headersspan-idrequest_headersspan-idrequest_headersrequest-headers"></a><span id="Request_headers"/><span id="request_headers"/><span id="REQUEST_HEADERS"/>Request headers


The following HTTP request headers are supported by the Partner Center REST API.

| 標頭                       | 說明                                                                                                                                                                                                                                                                            | 值類型 |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Authorization:               | 必要。 The authorization token in the form Bearer &lt;token&gt;.                                                                                                                                                                                                                    | 字串     |
| Accept:                      | Specifies the request and response type, "application/json".                                                                                                                                                                                                                           | 字串     |
| MS-RequestId:                | A unique identifier for the call, used to ensure id-potency. In the case of a timeout, the retry call should include the same value. Upon receiving a response (success or business failure), the value should be reset for the next call.                                            | GUID       |
| MS-CorrelationId:            | A unique identifier for the call, useful in logs and network traces for troubleshooting errors. The value should be reset for every call. All operations should include this header. For more information, see the Correlation ID information in [Test and debug](test-and-debug.md). | GUID       |
| MS-Contract-Version:         | 必要。 Specifies the version of the API requested; generally api-version: v1 unless otherwise specified in the [Scenarios](scenarios.md) section.                                                                                                                                  | 字串     |
| If-Match:                    | Used for concurrency control. Some API calls require passing the ETag via the If-Match header. The ETag is usually on the resource and therefore, requires GET-ting the latest. For more information, see the ETag information in [Test and debug](test-and-debug.md).                | 字串     |
| MS-PartnerCenter-Application | 選用。 Specifies the name of the application that is using the Partner Center REST API.                                                                                                                                                                                             | 字串     |
| X-Locale:                    | 選用。 Specifies the language in which the rates are returned. Default is "en-US". For a list of supported values, see [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | 字串     |

 

## <a name="span-idresponse_headersspan-idresponse_headersspan-idresponse_headersresponse-headers"></a><span id="Response_headers"/><span id="response_headers"/><span id="RESPONSE_HEADERS"/>Response headers


The following HTTP response headers may be returned by the Partner Center REST API.

| 標頭            | 說明                                                                                                                                                                                                                                 | 值類型 |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Accept:           | Specifies the request and response type, "application/json".                                                                                                                                                                                | 字串     |
| MS-RequestId:     | A unique identifier for the call, used to ensure id-potency. In the case of a timeout, the retry call should include the same value. Upon receiving a response (success or business failure), the value should be reset for the next call. | GUID       |
| MS-CorrelationId: | A unique identifier for the call, useful the logs and network traces for troubleshooting errors. The value should be reset for every call. All operations should include this header.                                                       | GUID       |

 

 

 




