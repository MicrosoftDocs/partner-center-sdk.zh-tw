---
title: 合作夥伴中心 webhook
description: Webhook 允許合作夥伴註冊資源變更事件。
ms.date: 04/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ead6d1da325534f2b58667365a509ef07ee295b1
ms.sourcegitcommit: b9d44c881015065e2c375afa4deb05fe6bf3aeb8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2019
ms.locfileid: "74559474"
---
# <a name="partner-center-webhooks"></a>合作夥伴中心 webhook


**適用于**

- 合作夥伴中心   
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心   


合作夥伴中心 Webhook Api 可讓合作夥伴註冊資源變更事件。 這些事件會以 HTTP Post 的形式傳遞給合作夥伴的已註冊 URL。 若要接收來自合作夥伴中心的事件，合作夥伴將裝載可供合作夥伴中心張貼資源變更事件的回呼。 該事件將會經過數位簽署，讓合作夥伴可以驗證它是否已從合作夥伴中心送出。 

合作夥伴可以選擇合作夥伴中心所支援的 Webhook 事件，如下所示。  

- **測試事件（「測試已建立」）**

    此事件可讓您透過要求測試事件並追蹤其進度，自行上線並測試您的註冊。 嘗試傳遞事件時，您將能夠看到 Microsoft 收到的失敗訊息。 這只會套用至「測試建立」事件，而超過7天的資料則會被清除。

- **訂用帳戶更新事件（「訂用帳戶更新」）**

    這個事件會在訂閱變更時引發。 除了在透過合作夥伴中心 API 進行變更時，還會在發生內部變更時產生這些事件。 
    
    >[!NOTE]
    >在訂用帳戶變更和觸發訂閱更新事件的時間之間，最多會有48小時的延遲。 

- **閾值已超過事件（"usagerecords 和 resources-thresholdExceeded"）**

    這個事件會在任何客戶的 Microsoft Azure 使用量超過其使用量消費預算 (閾值) 時引發。 如需詳細資訊，請參閱[為您的客戶設定 Azure 消費預算](https://docs.microsoft.com/partner-center/set-an-azure-spending-budget-for-your-customers)。

- **參考建立的事件（「已建立參考」）**

    建立參考時，會引發此事件。 

- **參考已更新事件（「已更新參考」）**

    當參考更新時，就會引發此事件。 

- **發票就緒事件（「發票就緒」）**

    當新發票準備就緒時，就會引發此事件。


未來的 Webhook 事件將會針對在合作夥伴不會控制的系統中變更的資源加入，並會進一步進行更新，以盡可能接近「即時」事件。 來自合作夥伴的意見反應，其中的事件會將價值加入其公司，在判斷要新增的新事件時非常有用。 

如需合作夥伴中心所支援之 Webhook 事件的完整清單，請參閱[合作夥伴中心 Webhook 事件](partner-center-webhook-events.md)。

## <a name="prerequisites"></a>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。   



## <a name="receiving-events-from-partner-center"></a>從合作夥伴中心接收事件

若要從合作夥伴中心接收事件，您必須公開可公開存取的端點;而且因為此端點已公開，所以您必須驗證通訊是否來自合作夥伴中心。 您收到的所有 Webhook 事件都會以連結至 Microsoft 根的憑證進行數位簽署。 也會提供用來簽署事件的憑證連結。 這可讓您更新憑證，而不必重新部署或重新設定您的服務。 合作夥伴中心會進行10次的事件傳遞。 如果嘗試10次後仍未傳遞事件，它會移到離線佇列中，而且不會在傳遞時進行進一步的嘗試。 

下列範例顯示從合作夥伴中心張貼的事件。

```http
POST /webhooks/callback
Content-Type: application/json
Authorization: Signature VOhcjRqA4f7u/4R29ohEzwRZibZdzfgG5/w4fHUnu8FHauBEVch8m2+5OgjLZRL33CIQpmqr2t0FsGF0UdmCR2OdY7rrAh/6QUW+u+jRUCV1s62M76jbVpTTGShmrANxnl8gz4LsbY260LAsDHufd6ab4oejerx1Ey9sFC+xwVTa+J4qGgeyIepeu4YCM0oB2RFS9rRB2F1s1OeAAPEhG7olp8B00Jss3PQrpLGOoAr5+fnQp8GOK8IdKF1/abUIyyvHxEjL76l7DVQN58pIJg4YC+pLs8pi6sTKvOdSVyCnjf+uYQWwmmWujSHfyU37j2Fzz16PJyWH41K8ZXJJkw==
X-MS-Certificate-Url: https://3psostorageacct.blob.core.windows.net/cert/pcnotifications-dispatch.microsoft.com.cer
X-MS-Signature-Algorithm: rsa-sha256
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 195

{
    "EventName": "test-created",
    "ResourceUri": "http://localhost:16722/v1/webhooks/registration/test",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
} 
```

>[!NOTE] 
>Authorization 標頭具有「簽章」的配置。 這是內容的 base64 編碼簽章。

## <a name="how-to-authenticate-the-callback"></a>如何驗證回呼


若要驗證從合作夥伴中心收到的回呼事件，請執行下列動作：

1.  確認所需的標頭存在（Authorization，x-ms-憑證-url，x-ms-signature-演算法）。
2.  下載用來簽署內容的憑證（[x-ms-憑證-url]）。
3.  驗證憑證鏈。
4.  驗證憑證的「組織」。
5.  將具有 UTF8 編碼的內容讀取到緩衝區。
6.  建立 RSA 加密提供者。
7.  確認資料符合指定的雜湊演算法（例如 SHA256）所簽署的內容。
8.  如果驗證成功，則處理訊息。

> [!NOTE]
> 根據預設，簽章權杖會在授權標頭中傳送。 如果您在註冊中將**SignatureTokenToMsSignatureHeader**設定為 true，簽章權杖將會改為以 x-ms-signature 標頭傳送。

## <a name="event-model"></a>事件模型


下表描述合作夥伴中心事件的屬性。

**屬性**

| 名稱                      | 說明                                                                           |
|---------------------------|---------------------------------------------------------------------------------------|
| **EventName**             | 事件的名稱。 以 {resource}-{action} 形式呈現。 例如，「測試已建立」。  |
| **ResourceUri**           | 已變更之資源的 URI。                                                 |
| **ResourceName**          | 已變更之資源的名稱。                                                |
| **AuditUrl**              | 選用。 Audit 記錄的 URI。                                                |
| **ResourceChangeUtcDate** | 發生資源變更時的日期和時間（UTC 格式）。                  |


**抽樣**

下列範例顯示合作夥伴中心事件的結構。

```http
{
    "EventName": "test-created",
    "ResourceUri": "http://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/c0bfd694-3075-4ec5-9a3c-733d3a890a1f",
    "ResourceName": "test",
    "AuditUri": null,
    "ResourceChangeUtcDate": "2017-11-16T16:19:06.3520276+00:00"
}
```


## <a name="webhook-apis"></a>Webhook Api   


[驗證]   

所有對 Webhook Api 的呼叫都會使用 Authorization 標頭中的持有人權杖進行驗證。 您必須取得存取權杖才能存取 https://api.partnercenter.microsoft.com 。 這是用來存取合作夥伴中心 Api 其餘部分的相同權杖。


 
### <a name="get-a-list-of-events"></a>取得事件清單

傳回 Webhook Api 目前支援的事件清單。

**資源 URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/events

**要求範例**   

```http
GET /webhooks/v1/registration/events
content-type: application/json
authorization: Bearer eyJ0e.......
accept: */*
host: api.partnercenter.microsoft.com
```

**回應範例**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 183
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c0bcf3a3-46e9-48fd-8e05-f674b8fd5d66
MS-RequestId: 79419bbb-06ee-48da-8221-e09480537dfc
X-Locale: en-US
 
[ "subscription-updated", "test-created", "usagerecords-thresholdExceeded" ]
```



### <a name="register-to-receive-events"></a>註冊以接收事件      

註冊租使用者以接收指定的事件。

**資源 URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**要求範例**   

```http
POST /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0e.....
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 219
 
{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

**回應範例**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2 

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```



### <a name="view-a-registration"></a>查看註冊        

傳回租使用者的 Webhook 事件註冊。

**資源 URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**要求範例**   

```http
GET /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

**回應範例**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 341
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: c3b88ab0-b7bc-48d6-8c55-4ae6200f490a
MS-RequestId: ca30367d-4b24-4516-af08-74bba6dc6657
X-Locale: en-US

{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```



### <a name="update-an-event-registration"></a>更新事件註冊      

更新現有的事件註冊。 

**資源 URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration


**要求範例**   

```http
PUT /webhooks/v1/registration
Content-Type: application/json
Authorization: Bearer eyJ0eXAiOR...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length: 258
 
{
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": ["subscription-updated", "test-created"]
}
```

**回應範例**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 346
Content-Type: application/json; charset=utf-8
content-encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 718f2336-8b56-4f42-93ac-54896047c59a
MS-RequestId: f04b1b5e-87b4-4d95-b087-d65fffec0bd2 

{
    "SubscriberId": "e82cac64-dc67-4cd3-849b-78b6127dd57d",
    "WebhookUrl": "{{YourCallbackUrl}}",
    "WebhookEvents": [ "subscription-updated", "test-created" ]
}
```


### <a name="send-a-test-event-to-validate-your-registration"></a>傳送測試事件來驗證您的註冊   

產生測試事件以驗證 Webhook 註冊。 此測試的目的是要驗證您是否可以從合作夥伴中心接收事件。 這些事件的資料會在初始事件建立後的7天內刪除。 在傳送驗證事件之前，您必須使用註冊 API 來註冊「測試建立」事件。 

>[!NOTE]
>發佈驗證事件時，每分鐘有2個要求的節流限制。 

**資源 URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents

**要求範例**   

```http
POST /webhooks/v1/registration/validationEvents
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
Content-Length:
```

**回應範例**   

```http
HTTP/1.1 200
Status: 200
Content-Length: 181
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 04af2aea-d413-42db-824e-f328001484d1
MS-RequestId: 2f498d5a-a6ab-468f-98d8-93c96da09051
X-Locale: en-US

{ "correlationId": "04af2aea-d413-42db-824e-f328001484d1" }
```



### <a name="verify-that-the-event-was-delivered"></a>確認已傳遞事件   

傳回驗證事件的目前狀態。 這有助於疑難排解事件傳遞問題。 回應會包含每次嘗試傳遞事件時所得到的結果。

**資源 URL**   
https://api.partnercenter.microsoft.com/webhooks/v1/registration/validationEvents/{correlationId}

**要求範例**   

```http
GET /webhooks/v1/registration/validationEvents/04af2aea-d413-42db-824e-f328001484d1
MS-CorrelationId: 3ef0202b-9d00-4f75-9cff-15420f7612b3
Authorization: Bearer ...
Accept: */*
Host: api.partnercenter.microsoft.com
Accept-Encoding: gzip, deflate
```

**回應範例**     

```http
HTTP/1.1 200
Status: 200
Content-Length: 469
Content-Type: application/json; charset=utf-8
Content-Encoding: gzip
Vary: Accept-Encoding
MS-CorrelationId: 497e0a23-9498-4d6c-bd6a-bc4d6d0054e7
MS-RequestId: 0843bdb2-113a-4926-a51c-284aa01d722e
X-Locale: en-US

{
    "correlationId": "04af2aea-d413-42db-824e-f328001484d1",
    "partnerId": "00234d9d-8c2d-4ff5-8c18-39f8afc6f7f3",
    "status": "completed",
    "callbackUrl": "{{YourCallbackUrl}}",
    "results": [{
        "responseCode": "OK",
        "responseMessage": "",
        "systemError": false,
        "dateTimeUtc": "2017-12-08T21:39:48.2386997"
    }]
}
```


## <a name="example-for-signature-validation"></a>簽章驗證的範例


**範例回呼控制器簽章（ASP.NET）**     

``` csharp
[AuthorizeSignature]
[Route("webhooks/callback")]
public IHttpActionResult Post(PartnerResourceChangeCallBack callback)
```

簽章**驗證**      
下列範例示範如何將授權屬性新增至從 Webhook 事件接收回呼的控制器。

``` csharp
namespace Webhooks.Security
{
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Cryptography;
    using System.Security.Cryptography.X509Certificates;
    using System.Text;
    using System.Threading;
    using System.Threading.Tasks;
    using System.Web.Http;
    using System.Web.Http.Controllers;
    using Microsoft.Partner.Logging;

    /// <summary>
    /// Signature based Authorization
    /// </summary>
    public class AuthorizeSignatureAttribute : AuthorizeAttribute
    {
        private const string MsSignatureHeader = "x-ms-signature";
        private const string CertificateUrlHeader = "x-ms-certificate-url";
        private const string SignatureAlgorithmHeader = "x-ms-signature-algorithm";
        private const string MicrosoftCorporationIssuer = "O=Microsoft Corporation";
        private const string SignatureScheme = "Signature";

        /// <inheritdoc/>
        public override async Task OnAuthorizationAsync(HttpActionContext actionContext, CancellationToken cancellationToken)
        {
            ValidateAuthorizationHeaders(actionContext.Request);

            await VerifySignature(actionContext.Request);
        }

        private static async Task<string> GetContentAsync(HttpRequestMessage request)
        {
            // By default the stream can only be read once and we need to read it here so that we can hash the body to validate the signature from microsoft.
            // Load into a buffer, so that the stream can be accessed here and in the api when it binds the content to the expected model type.
            await request.Content.LoadIntoBufferAsync();

            var s = await request.Content.ReadAsStreamAsync();
            var reader = new StreamReader(s);
            var body = await reader.ReadToEndAsync();

            // set the stream position back to the beginning
            if (s.CanSeek)
            {
                s.Seek(0, SeekOrigin.Begin);
            }

            return body;
        }

        private static void ValidateAuthorizationHeaders(HttpRequestMessage request)
        {
            var authHeader = request.Headers.Authorization;
            if (string.IsNullOrWhiteSpace(authHeader?.Parameter) && string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, MsSignatureHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Authorization header missing."));
            }

            var signatureHeaderValue = GetHeaderValue(request.Headers, MsSignatureHeader);
            if (authHeader != null
                && !string.Equals(authHeader.Scheme, SignatureScheme, StringComparison.OrdinalIgnoreCase)
                && !string.IsNullOrWhiteSpace(signatureHeaderValue)
                && !signatureHeaderValue.StartsWith(SignatureScheme, StringComparison.OrdinalIgnoreCase))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Authorization scheme needs to be '{SignatureScheme}'."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, CertificateUrlHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {CertificateUrlHeader} missing."));
            }

            if (string.IsNullOrWhiteSpace(GetHeaderValue(request.Headers, SignatureAlgorithmHeader)))
            {
                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.BadRequest, $"Request header {SignatureAlgorithmHeader} missing."));
            }
        }

        private static string GetHeaderValue(HttpHeaders headers, string key)
        {
            headers.TryGetValues(key, out var headerValues);

            return headerValues?.FirstOrDefault();
        }

        private static async Task VerifySignature(HttpRequestMessage request)
        {
            // Get signature value from either authorization header or x-ms-signature header.
            var base64Signature = request.Headers.Authorization?.Parameter ?? GetHeaderValue(request.Headers, MsSignatureHeader).Split(' ')[1];
            var signatureAlgorithm = GetHeaderValue(request.Headers, SignatureAlgorithmHeader);
            var certificateUrl = GetHeaderValue(request.Headers, CertificateUrlHeader);
            var certificate = await GetCertificate(certificateUrl);
            var content = await GetContentAsync(request);
            var alg = signatureAlgorithm.Split('-'); // e.g. RSA-SHA1
            var isValid = false;

            var logger = GetLoggerIfAvailable(request);

            // Validate the certificate
            VerifyCertificate(certificate, request, logger);

            if (alg.Length == 2 && alg[0].Equals("RSA", StringComparison.OrdinalIgnoreCase))
            {
                var signature = Convert.FromBase64String(base64Signature);
                var csp = (RSACryptoServiceProvider)certificate.PublicKey.Key;

                var encoding = new UTF8Encoding();
                var data = encoding.GetBytes(content);

                var hashAlgorithm = alg[1].ToUpper();

                isValid = csp.VerifyData(data, CryptoConfig.MapNameToOID(hashAlgorithm), signature);
            }

            if (!isValid)
            {
                // log that we were not able to validate the signature
                logger?.TrackTrace(
                    "Failed to validate signature for webhook callback",
                    new Dictionary<string, string> { { "base64Signature", base64Signature }, { "certificateUrl", certificateUrl }, { "signatureAlgorithm", signatureAlgorithm }, { "content", content } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Signature verification failed"));
            }
        }

        private static ILogger GetLoggerIfAvailable(HttpRequestMessage request)
        {
            return request.GetDependencyScope().GetService(typeof(ILogger)) as ILogger;
        }

        private static async Task<X509Certificate2> GetCertificate(string certificateUrl)
        {
            byte[] certBytes;
            using (var webClient = new WebClient())
            {
                certBytes = await webClient.DownloadDataTaskAsync(certificateUrl);
            }

            return new X509Certificate2(certBytes);
        }

        private static void VerifyCertificate(X509Certificate2 certificate, HttpRequestMessage request, ILogger logger)
        {
            if (!certificate.Verify())
            {
                logger?.TrackTrace("Failed to verify certificate for webhook callback.", new Dictionary<string, string> { { "Subject", certificate.Subject }, { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, "Certificate verification failed."));
            }

            if (!certificate.Issuer.Contains(MicrosoftCorporationIssuer))
            {
                logger?.TrackTrace($"Certificate not issued by {MicrosoftCorporationIssuer}.", new Dictionary<string, string> { { "Issuer", certificate.Issuer } });

                throw new HttpResponseException(request.CreateErrorResponse(HttpStatusCode.Unauthorized, $"Certificate not issued by {MicrosoftCorporationIssuer}."));
            }
        }
    }
}
```
