---
title: 取得 Microsoft 客戶合約範本的下載連結
description: 取得 Microsoft 客戶合約範本的下載連結。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: dcc81acbab84e7f6ac9a495c00b2798c87075d89
ms.sourcegitcommit: 89cdf326f5684fb447d91d817f32dfcbf08ada3a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/25/2020
ms.locfileid: "82155578"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>取得 Microsoft 客戶合約範本的下載連結

**適用於：**

- 合作夥伴中心

合作夥伴中心目前僅支援在*Microsoft 公用雲端*中使用**AgreementDocument**資源。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本文說明如何根據客戶的國家/地區和語言，取得下載 Microsoft 客戶合約範本的連結。

## <a name="prerequisites"></a>必要條件

- 如果您使用合作夥伴中心 .NET SDK，則需要 1.14 版或更新版本。

- 認證，如[合作夥伴中心驗證](./partner-center-authentication.md)所述。 此案例僅支援「應用程式 + 使用者」驗證。 

- Microsoft 客戶合約範本適用的客戶國家/地區。

- 應在其中當地語系化 Microsoft 客戶合約範本的語言。

> [!IMPORTANT]
>
> - Microsoft 客戶合約是國家/地區特定的。 當要求下載 Microsoft 客戶合約範本的連結時，請務必根據客戶的位置指定正確的國家/地區。 或支援的國家/地區清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。
>
> - 針對某些國家/地區，Microsoft 客戶合約提供多種語言。 為獲得最佳的客戶體驗，請挑選最符合客戶需求的語言。 如需支援的語言清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。
> - 只有 Microsoft 客戶合約支援此方法。

## <a name="net"></a>.NET

若要取出連結以下載 Microsoft 客戶合約範本：

1. 擷取 Microsoft 客戶合約的合約中繼資料。 您必須取得 Microsoft 客戶合約的 **templateId**。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](get-customer-agreement-metadata.md)。

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. 使用 Iaggregatepartner.customers.byid. AgreementTemplates 集合。

3. 呼叫**ById**方法，並指定 Microsoft 客戶合約的**templateId** 。

4. 提取**Document**屬性。

5. 呼叫**ByCountry**方法，並指定要套用合約範本的客戶國家/地區。 如果未指定方法，則查詢會預設為*US* 。 如需支援的國家/地區代碼清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。 這個方法會區分**大小寫**。

6. 呼叫**ByLanguage**方法，並指定應該在其中當地語系化協定範本的語言。 如果未指定方法，或指定國家/地區代碼不支援指定的國家/地區碼，則查詢會預設為*en-us* 。 如需支援的語言代碼清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。

7. 呼叫**Get**或**GetAsync**方法。

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

您可以從[主控台測試應用程式](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples)專案的[GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs)類別中找到完整的範例。

## <a name="rest-request"></a>REST 要求

若要取出連結以下載 Microsoft 客戶合約範本：

1. 擷取 Microsoft 客戶合約的合約中繼資料。 您必須取得 Microsoft 客戶合約的 **templateId**。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](get-customer-agreement-metadata.md)。

2. 建立 REST 要求以提取[ **AgreementDocument**資源](./agreement-document-resources.md)。 如需範例，請參閱[要求語法](#request-syntax)範例。 您必須指定下列資訊：

    - Microsoft 客戶合約的**templateId** 。
    - Microsoft 客戶合約範本適用的國家/地區。
    - 應在其中當地語系化 Microsoft 客戶合約範本的語言。

### <a name="request-syntax"></a>要求的語法

針對此資源使用下列要求語法：

| 方法 | 要求 URI |
|--------|---------------------------------------------------------------------|
| GET | baseURL/v1/agreementtemplates/{agreement-template-id}/document？ language = {language} &country = {country} HTTP/1.1 [* \{ \} *](partner-center-rest-urls.md) |

### <a name="uri-parameters"></a>URI 參數

您可以搭配您的要求使用下列 URI 參數：

| 名稱                   | 類型   | 必要 | 描述                                 |
|------------------------|--------|----------|---------------------------------------------|
| 合約-範本識別碼  | 字串 | 是      | 合約類型的唯一識別碼。 您可以藉由擷取 Microsoft 客戶合約的合約中繼資料，取得 Microsoft 客戶合約的 templateId。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](./get-customer-agreement-metadata.md)。 這個參數會區分**大小寫**。|
| country                | 字串 | 否       | 指出套用合約範本的國家/地區。 如果未指定參數，查詢會預設為*US* 。 如需支援的國家/地區代碼清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。|
| 語言               | 字串 | 否       | 指出應在其中當地語系化協定範本的語言。 如果未指定參數，或指定的國家（地區）代碼 in't 支援指定的國家/地區碼，則查詢會預設為*en-us* 。 如需支援的國家/地區代碼清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。|

### <a name="request-headers"></a>要求標頭

如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

### <a name="request-body"></a>要求本文

無。

### <a name="request-example"></a>要求範例

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST 回應

如果成功，此方法會在回應主體中傳回[ **AgreementDocument**資源](./agreement-document-resources.md)。

資源具有**downloadUri**屬性，其中包含可用於下載協定範本的 URL 字串。 每次進行查詢時，就會傳回不同的連結。 此連結會在五分鐘後到期。

### <a name="response-success-and-error-codes"></a>回應成功和錯誤碼

每個回應都隨附 HTTP 狀態碼，會指出成功與否以及其他的偵錯資訊。

請使用網路追蹤工具來讀取此錯誤碼、錯誤類型和其他參數。 如需完整清單，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

### <a name="response-example"></a>回應範例

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>支援的國家/地區和語言清單

> [!IMPORTANT]
> [國家/地區代碼] 屬性會區分大小寫。 請務必使用下表中所指定的正確大小寫。

| Country                   | 國碼 (地區碼)   | 支援的語言代碼 |
|------------------------|--------|----------|
| 奧蘭島 | 限於 | zh-TW |
| 阿富汗 | AF | zh-TW |
| 阿爾巴尼亞 | AL | zh-TW |
| 阿爾及利亞 | DZ | en-us、fr-fr、en-us |
| 美屬薩摩亞 | AS | zh-TW |
| 安道爾 | AD | zh-TW |
| 安哥拉 | AO | en-us、pt |
| 安圭拉 | AI | zh-TW |
| 南極大陸 | AQ | zh-TW |
| 安地卡及巴布達 | AG | zh-TW |
| 阿根廷 | AR | en-us、es |
| 亞美尼亞 | AM | zh-TW |
| 阿路巴 | AW | zh-TW |
| 澳大利亞 | AU | zh-TW |
| 奧地利 | AT | en-us，de |
| 亞塞拜然 | AZ | zh-TW |
| 巴哈馬 | BS | zh-TW |
| 巴林 | BH | en-us，ar-SA |
| 孟加拉 | BD | zh-TW |
| 巴貝多 | BB | zh-TW |
| 白俄羅斯 | BY | en-US、ru-RU |
| 比利時 | BE | en-us、nl-NL |
| 貝里斯 | BZ | en-us、es |
| 貝南 | BJ | zh-TW |
| 百慕達 | BM | zh-TW |
| 不丹 | BT | zh-TW |
| 玻利維亞 | BO | en-us、es |
| 波奈 | BQ | zh-TW |
| 波士尼亞赫塞哥維納 | BA | zh-TW |
| 波札那 | BW | zh-TW |
| 布威島 | BV | zh-TW |
| 巴西 | BR | en-us、pt-BR |
| 英屬印度洋領土 | IO | zh-TW |
| 英屬維爾京群島 | VG | zh-TW |
| 汶萊 | BN | zh-TW |
| 保加利亞 | BG | en-us、bg-BG |
| 布吉納法索 | BF | zh-TW |
| 蒲隆地 | BI | zh-TW |
| 象牙海岸 | CI | en-US、fr-FR |
| 維德角 | CV | en-us、pt |
| 柬埔寨 | KH | zh-TW |
| 喀麥隆 | CM | en-US、fr-FR |
| Canada | CA | en-US、fr-FR |
| 開曼群島 | KY | en-us、en-us |
| 中非共和國 | CF | zh-TW |
| 查德 | TD | zh-TW |
| 智利 | CL | en-us、es |
| 聖誕島 | CX | zh-TW |
| 可可斯群島 | CC | zh-TW |
| 哥倫比亞 | CO | en-us、es |
| 葛摩 | KM | zh-TW |
| 剛果民主共和國 (DRC) | CD | zh-TW |
| 剛果共和國 | CG | zh-TW |
| 柯克群島 | CK | zh-TW |
| 哥斯大黎加 | CR | en-us、es |
| 克羅埃西亞 | HR | en-us、hr-HR |
| 古拉果 | 順 | zh-TW |
| 賽浦路斯 | CY | zh-TW |
| 捷克 | CZ | en-us、cs-CZ |
| 丹麥 | DK | en-us、da-深色 |
| 吉布地 | DJ | zh-TW |
| 多米尼克 | DM | zh-TW |
| 多明尼加共和國 | DO | en-us、es |
| 厄瓜多 | EC | zh-TW |
| 埃及 | EG | en-us，ar-SA |
| 薩爾瓦多 | SV | en-us、es |
| 赤道幾內亞 | GQ | zh-TW |
| 厄利垂亞 | ER | zh-TW |
| 愛沙尼亞 | EE | en-us，et-EE |
| eSwatini | SZ | zh-TW |
| 衣索比亞 | ET | zh-TW |
| 福克蘭群島 | FK | zh-TW |
| 法羅群島 | FO | zh-TW |
| 斐濟 | FJ | zh-TW |
| 芬蘭 | FI | en-us、fi |
| 法國 | FR | en-US、fr-FR |
| 法屬圭亞那 | GF | en-US、fr-FR  |
| 法屬玻里尼西亞 | PF | zh-TW |
| 法屬南半球領土 | TF | zh-TW |
| 加彭 | GA | zh-TW |
| 甘比亞 | GM | zh-TW |
| 喬治亞 | GE | zh-TW |
| 德國 | DE | en-us，de |
| 迦納 | GH | zh-TW |
| 直布羅陀 | GI | zh-TW |
| 希臘 | GR | en-us、el-GR |
| 格陵蘭 | GL | zh-TW |
| 格瑞那達 | GD | zh-TW |
| 哥德普洛 | GP | zh-TW |
| 關島 | GU | zh-TW |
| 瓜地馬拉 | GT | en-us、es |
| 根息 | GG | zh-TW |
| 幾內亞 | GN | zh-TW |
| 幾內亞比索 | GW | zh-TW |
| 蓋亞納 | GY | zh-TW |
| 海地 | HT | zh-TW |
| 赫德島及麥當勞群島 | HM | zh-TW |
| 宏都拉斯 | HN | en-us、es |
| 香港特別行政區 | HK | en-us、zh-HK |
| 匈牙利 | HU | en-us、hu-HU |
| 冰島 | IS | zh-TW |
| 印度 | IN | en-us，hi |
| 印尼 | 識別碼 | en-us，識別碼識別碼 |
| 伊拉克 | IQ | en-us，ar-SA |
| 愛爾蘭 | IE | zh-TW |
| 曼城島 | IM | zh-TW |
| 以色列 | IL | en-us、他-IL |
| 義大利 | IT | en-us，it-IT |
| 牙買加 | JM | zh-TW |
| 尖棉 | XJ | zh-TW |
| 日本 | JP | en-us、ja-jp |
| 澤西島 | JE | zh-TW |
| 約旦 | JO | en-us，ar-SA |
| 哈薩克 | KZ | en-us、kk-KZ |
| 肯亞 | KE | zh-TW |
| 吉里巴斯 | KI | zh-TW |
| 南韓 | KR | en-us、ko-KR |
| 科索沃 | XK | zh-TW |
| 科威特 | KW | en-us，ar-SA |
| 吉爾吉斯 | KG | en-US、ru-RU |
| 寮國 | LA | zh-TW |
| 拉脫維亞 | LV | en-us，lv-LV |
| 黎巴嫩 | LB | en-us，ar-SA |
| 賴索托 | LS | zh-TW |
| 賴比瑞亞 | LR | zh-TW |
| 利比亞 | LY | en-us，ar-SA |
| 列支敦斯登 | LI | en-us，de |
| 立陶宛 | LT | en-us、lt-LT |
| 盧森堡 | LU | en-US、fr-FR |
| 澳門特別行政區 | MO | en-us、zh-HK |
| 馬其頓 (FYRO) | MK | zh-TW |
| 馬達加斯加 | MG | zh-TW |
| 馬拉威 | MW | zh-TW |
| 馬來西亞 | MY | en-us、ms-MY |
| 馬爾地夫 | MV | zh-TW |
| 馬利 | ML | zh-TW |
| 馬爾他 | MT | zh-TW |
| 馬紹爾群島 | MH | zh-TW |
| 馬丁尼克 | MQ | zh-TW |
| 茅利塔尼亞 | MR | zh-TW |
| 模里西斯 | MU | en-us，ar-SA |
| 馬約特島 | YT | zh-TW |
| 墨西哥 | MX | en-us、es |
| 密克羅尼西亞 | FM | zh-TW |
| 摩爾多瓦 | MD | en-us、ro-RO |
| 摩納哥 | MC | en-US、fr-FR |
| 蒙古 | MN | zh-TW |
| 蒙特內哥羅 | ME | zh-TW |
| 蒙特色拉特島 | MS | zh-TW |
| 摩洛哥 | MA | en-us、fr-fr、en-us |
| 莫三比克 | MZ | zh-TW |
| 緬甸 | MM | zh-TW |
| 納米比亞 | NA | zh-TW |
| 諾魯 | NR | zh-TW |
| 尼泊爾 | NP | zh-TW |
| 荷蘭 | NL | en-us、nl-NL |
| 新喀里多尼亞群島 | NC | zh-TW |
| 紐西蘭 | NZ | zh-TW |
| 尼加拉瓜 | NI | en-us、es |
| 尼日 | NE | zh-TW |
| 奈及利亞 | NG | zh-TW |
| 紐威島 | NU | zh-TW |
| 諾福克島 | NF | zh-TW |
| 北馬里安納群島 | MP | zh-TW |
| 挪威 | 否 | en-us，nb-否 |
| 阿曼 | OM | en-us，ar-SA |
| 巴基斯坦 | PK | zh-TW |
| 帛琉 | PW | zh-TW |
| 巴勒斯坦民族權力機構 | PS | zh-TW |
| 巴拿馬 | PA | en-us、es |
| 巴布亞紐幾內亞 | PG | zh-TW |
| 巴拉圭 | PY | en-us、es |
| 祕魯 | PE | en-us、es |
| 菲律賓 | PH | zh-TW |
| 皮特康群島 | PN | zh-TW |
| 波蘭 | PL | en-us，pl-PL |
| 葡萄牙 | PT | en-us、pt |
| 波多黎各 | PR | en-us、en-us |
| 卡達 | QA | en-us，ar-SA |
| 留尼旺 | RE | zh-TW |
| 羅馬尼亞 | RO | en-us、ro-RO |
| 俄羅斯 | RU | en-US、ru-RU |
| 盧安達 | RW | en-US、fr-FR |
| 聖多美普林西比 | ST | en-US、fr-FR |
| 沙巴 | XS | zh-TW |
| 聖巴瑟米 | BL | zh-TW |
| 聖克里斯多福及尼維斯 | KN | zh-TW |
| 聖露西亞 | LC | en-us、en-us |
| 聖馬丁 | MF | en-us、en-us |
| 聖匹島 | 下午 | zh-TW |
| 聖文森及格瑞那丁 | VC | zh-TW |
| 薩摩亞獨立國 | WS | zh-TW |
| 聖馬利諾 | SM | zh-TW |
| 沙烏地阿拉伯 | SA | zh-TW |
| 塞內加爾 | SN | en-US、fr-FR |
| 塞爾維亞 | RS | en-us、sr-iov-Latn-RS、en-us |
| 塞席爾 | SC | zh-TW |
| 獅子山 | SL | zh-TW |
| 新加坡 | SG | en-us、zh-SG |
| 聖佑達修斯 | XE | zh-TW |
| 荷屬聖馬丁 | X | en-us、en-us |
| 斯洛伐克 | SK | en-us，sk |
| 斯洛維尼亞 | SI | en-us、sl-SI |
| 索羅門群島 | SB | zh-TW |
| 索馬利亞 | SO | zh-TW |
| 南非 | ZA | zh-TW |
| 南喬治亞與南三明治群島 | GS | zh-TW |
| 南蘇丹 | SS | zh-TW |
| 西班牙 | ES | en-us、es、en-us、en-us （us） |
| 斯里蘭卡 | LK | zh-TW |
| 聖赫勒拿、阿森松、特里斯坦達庫尼亞群島 | SH | zh-TW |
| 蘇利南 | SR | zh-TW |
| 冷岸 | SJ | zh-TW |
| 瑞典 | SE | en-us、sv-SE |
| 瑞士 | CH | en-us、fr-fr、en-us、en-us （us） |
| 台灣 | TW | en-us、zh-HK |
| 塔吉克 | TJ | zh-TW |
| 坦尚尼亞 | TZ | zh-TW |
| 泰國 | 二四 | en-us，第一次 |
| 東帝汶 | TL | zh-TW |
| 多哥 | TG | zh-TW |
| 托克勞群島 | TK | zh-TW |
| 東加 | TO | zh-TW |
| 千里達及托巴哥 | TT | zh-TW |
| 突尼西亞 | TN | en-us、fr-fr、en-us |
| 土耳其 | TR | en-us、tr-TR |
| 土庫曼 | TM | zh-TW |
| 土克斯及開科斯群島 | TC | zh-TW |
| 吐瓦魯 | TV | zh-TW |
| 美國外島 | UM | zh-TW |
| 美屬維爾京群島 | VI | zh-TW |
| 烏干達 | UG | zh-TW |
| 烏克蘭 | UA | en-us、uk-UA |
| 阿拉伯聯合大公國 | AE | en-us，ar-SA |
| United Kingdom | GB | zh-TW |
| 美國 | US | zh-TW |
| 烏拉圭 | UY | en-us、es |
| 烏茲別克 | UZ | en-US、ru-RU |
| 萬那杜 | VU | zh-TW |
| 梵蒂岡 | VA | zh-TW |
| 委內瑞拉 | VE | en-us、es |
| 越南 | VN | en-us、vi-VN |
| 瓦利斯及福杜納 | WF | zh-TW |
| 葉門 | YE | en-us，ar-SA |
| 尚比亞 | ZM | zh-TW |
| 辛巴威 | ZW | zh-TW |
