---
title: Get a download link for the Microsoft Customer Agreement template
description: Get a download link for Microsoft Customer Agreement template.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 76b0b6ceb20504ad0f9903027ac61feca78c3970
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489958"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Get a download link for the Microsoft Customer Agreement template

適用於：

- 合作夥伴中心

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource doesn't apply to:

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

This article describes how to get a link to download the Microsoft Customer Agreement template, based on the customer's country and language.

## <a name="prerequisites"></a>必要條件

- If you are using the Partner Center .NET SDK, version 1.14 or newer is required.
- Credentials as described in [Partner Center authentication](./partner-center-authentication.md). This scenario only supports App+User authentication.
- The customer's country to which the Microsoft Customer Agreement template applies.
- The language in which the Microsoft Customer Agreement template should be localized.

> [!IMPORTANT]
> - The Microsoft Customer Agreement is country-specific. When requesting for a link to download the Microsoft Customer Agreement template, Be sure to specify the correct country based on customer's location. or list of supported countries, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - For some countries, the Microsoft Customer Agreement is available in multiple languages. For best customer experience, pick the language that best match the customer's needs. For list of supported languages, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).
> - This method is only supported with the Microsoft Customer Agreement. You cannot use it to get a download link for Microsoft Cloud Agreement template.

## <a name="net"></a>.NET

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

2. Use the IAggregatePartner.AgreementTemplates collection.
3. Call the **ById** method and specify the **templateId** of the Microsoft Customer Agreement.
4. Fetch the **Document** property.
5. Call the **ByCountry** method and specify the customer's country to which the agreement template applies. The query defaults to *US* if the method isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages). This method is **case-sensitive**.
6. Call the **ByLanguage** method and specify the language which the agreement template should be localized in. The query defaults to *en-US* if the method isn't specified or the country code specified isn't supported for the country specified. For list of supported language codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages)
7. Call the **Get** or **GetAsync** method.

```csharp
// IAggregatePartner partnerOperations;

string customerCountry = "US";

string languageForLocalization = "en-US";

var agreementDocument = partnerOperations.AgreementTemplates.ById(microsoftCustomerAgreementDetails.TemplateId).Document.ByCountry(customerCountry).ByLanguage(languageForLocalization).Get();
```

A complete sample can be found in the [GetAgreementDocument](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDocument.cs) class from the [console test app](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) project.


## <a name="rest-request"></a>REST request

To retrieve a link to download the Microsoft Customer Agreement template:

1. Retrieve the agreement metadata for the Microsoft Customer Agreement. You must obtain the **templateId** of the Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](get-customer-agreement-metadata.md).
2. Create a REST request to fetch an [**AgreementDocument** resource](./agreement-document-resources.md). For an example, see the [request syntax](#request-syntax) example. You must specify the following information:
    - The **templateId** of the Microsoft Customer Agreement.
    - The country to which the Microsoft Customer Agreement template applies.
    - The language in which the Microsoft Customer Agreement template should be localized.

### <a name="request-syntax"></a>要求的語法

Use the following request syntax for this resource:

| 方法 | 要求 URI |
|--------|---------------------------------------------------------------------|
| GET | [ *\{baseURL\}* ](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>URI 參數

You can use the following URI parameters with your request:

| 名稱                   | 在工作列搜尋方塊中輸入   | 必要 | 說明                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | 字串 | [是]      | Unique identifier of the agreement type. You can obtain the templateId for Microsoft Customer Agreement by retrieving the agreement metadata for Microsoft Customer Agreement. For more information, see [Get agreement metadata for Microsoft Customer Agreement](./get-customer-agreement-metadata.md). This parameter is **case-sensitive**.|
| 國家/地區                | 字串 | 無       | Indicates the country to which the agreement template applies. The query defaults to *US* if the parameter isn't specified. For a list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|
| language               | 字串 | 無       | Indicates the language in which the agreement template should be localized. The query defaults to *en-US* if the parameter isn't specified or the country code specified in't supported for the country specified. For list of supported country codes, please refer to [List of supported countries and languages](#list-of-supported-countries-and-languages).|

### <a name="request-headers"></a>要求標頭

For more information, see [Partner Center REST headers](headers.md).

### <a name="request-body"></a>要求主體

無。

### <a name="request-example"></a>要求的範例

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST response

If successful, this method returns an [**AgreementDocument** resource](./agreement-document-resources.md) in the response body.

The resource has a **downloadUri** property, which contains a URL string that can be used to download the agreement template. A different link is returned each time you make a query. This link expires after five minutes.

### <a name="response-success-and-error-codes"></a>Response success and error codes

Each response comes with an HTTP status code that indicates success or failure and additional debugging information.

Use a network trace tool to read this code, error type, and additional parameters. For the full list, see [Partner Center REST error codes](error-codes.md).

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

## <a name="list-of-supported-countries-and-languages"></a>List of supported countries and languages

> [!IMPORTANT]
> The country code property is case-sensitive. Please sure to use the correct casing specified in the table below.

| 國家/地區                   | 國碼 (地區碼)   | Supported language code(s) |
|------------------------|--------|----------|
| 奧蘭島 | AX | en-US |
| 阿富汗 | AF | en-US |
| 阿爾巴尼亞 | AL | en-US |
| 阿爾及利亞 | DZ | en-US, fr-FR, en-US |
| 美屬薩摩亞 | AS | en-US |
| 安道爾 | AD | en-US |
| 安哥拉 | AO | en-US, pt-PT |
| 安圭拉 | AI | en-US |
| 南極大陸 | AQ | en-US |
| 安地卡及巴布達 | AG | en-US |
| 阿根廷 | AR | en-US, es-ES |
| 亞美尼亞 | AM | en-US |
| 阿路巴 | AW | en-US |
| 澳大利亞 | AU | en-US |
| 奧地利 | AT | en-US, de-DE |
| 亞塞拜然 | AZ | en-US |
| 巴哈馬 | BS | en-US |
| 巴林 | BH | en-US, ar-SA |
| 孟加拉 | BD | en-US |
| 巴貝多 | BB | en-US |
| 白俄羅斯 | BY | en-US, ru-RU |
| 比利時 | BE | en-US, nl-NL |
| 貝里斯 | BZ | en-US, es-ES |
| 貝南 | BJ | en-US |
| 百慕達 | BM | en-US |
| 不丹 | BT | en-US |
| 玻利維亞 | BO | en-US, es-ES |
| 波奈 | BQ | en-US |
| 波士尼亞與赫塞哥維納 | BA | en-US |
| 波札那 | BW | en-US |
| 布威島 | BV | en-US |
| 巴西 | BR | en-US, pt-BR |
| 英屬印度洋領土 | IO | en-US |
| 英屬維爾京群島 | VG | en-US |
| 汶萊 | BN | en-US |
| 保加利亞 | BG | en-US, bg-BG |
| 布吉納法索 | BF | en-US |
| 蒲隆地 | BI | en-US |
| 科特迪瓦 | CI | en-US, fr-FR |
| 維德角 | CV | en-US, pt-PT |
| 柬埔寨 | KH | en-US |
| 喀麥隆 | CM | en-US, fr-FR |
| 加拿大 | CA | en-US, fr-FR |
| 開曼群島 | KY | en-US, en-US |
| 中非共和國 | CF | en-US |
| 查德 | TD | en-US |
| 智利 | CL | en-US, es-ES |
| 聖誕島 | CX | en-US |
| 可可斯群島 | CC | en-US |
| 哥倫比亞 | CO | en-US, es-ES |
| 葛摩 | KM | en-US |
| 剛果民主共和國 (DRC) | CD | en-US |
| 剛果共和國 | CG | en-US |
| 柯克群島 | CK | en-US |
| 哥斯大黎加 | CR | en-US, es-ES |
| 克羅埃西亞 | HR | en-US, hr-HR |
| 古拉梳 | CW | en-US |
| 賽普勒斯 | CY | en-US |
| Czechia | CZ | en-US, cs-CZ |
| 丹麥 | DK | en-US, da-DK |
| 吉布地 | DJ | en-US |
| 多米尼克 | DM | en-US |
| 多明尼加共和國 | DO | en-US, es-ES |
| 厄瓜多 | EC | en-US |
| 埃及 | EG | en-US, ar-SA |
| 薩爾瓦多 | SV | en-US, es-ES |
| 赤道幾內亞 | GQ | en-US |
| 厄利垂亞 | ER | en-US |
| 愛沙尼亞 | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| 衣索比亞 | ET | en-US |
| 福克蘭群島 | FK | en-US |
| 法羅群島 (丹麥) | FO | en-US |
| 斐濟群島 | FJ | en-US |
| 芬蘭 | FI | en-US, fi-FI |
| 法國 | FR | en-US, fr-FR |
| 法屬圭亞那 | GF | en-US, fr-FR  |
| 法屬玻里尼西亞 | PF | en-US |
| 法屬南半球領土 | TF | en-US |
| 加彭 | GA | en-US |
| 甘比亞 | GM | en-US |
| 喬治亞 | GE | en-US |
| 德國 | DE | en-US, de-DE |
| 迦納 | GH | en-US |
| 直布羅陀 | GI | en-US |
| 希臘 | GR | en-US, el-GR |
| 格陵蘭 (丹麥) | GL | en-US |
| 格瑞那達 | GD | en-US |
| 瓜地洛普 | GP | en-US |
| 關島 | GU | en-US |
| 瓜地馬拉 | GT | en-US, es-ES |
| 根息 | GG | en-US |
| 幾內亞 | GN | en-US |
| 幾內亞比索 | GW | en-US |
| 蓋亞納 | GY | en-US |
| 海地 | HT | en-US |
| 赫德島及麥當勞群島 | HM | en-US |
| 宏都拉斯 | HN | en-US, es-ES |
| 香港特別行政區 | HK | en-US, zh-HK |
| 匈牙利 | HU | en-US, hu-HU |
| 冰島 | IS | en-US |
| 印度 | IN | en-US, hi-IN |
| 印尼 | 識別碼 | en-US, id-ID |
| 伊拉克 | IQ | en-US, ar-SA |
| 愛爾蘭 | IE | en-US |
| 曼城島 | IM | en-US |
| 以色列 | IL | en-US, he-IL |
| 義大利 | IT | en-US, it-IT |
| 牙買加 | JM | en-US |
| Jan Mayen | XJ | en-US |
| 日本 | JP | en-US, ja-JP |
| 澤西島 | JE | en-US |
| 約旦 | JO | en-US, ar-SA |
| 哈薩克 | KZ | en-US, kk-KZ |
| 肯亞 | KE | en-US |
| 吉里巴斯 | KI | en-US |
| 韓國 | KR | en-US, ko-KR |
| Kosovo | XK | en-US |
| 科威特 | KW | en-US, ar-SA |
| 吉爾吉斯 | KG | en-US, ru-RU |
| 寮國 | LA | en-US |
| 拉脫維亞 | LV | en-US, lv-LV |
| 黎巴嫩 | LB | en-US, ar-SA |
| 賴索托 | LS | en-US |
| 賴比瑞亞 | LR | en-US |
| 利比亞 | LY | en-US, ar-SA |
| 列支敦斯登 | LI | en-US, de-DE |
| 立陶宛 | LT | en-US, lt-LT |
| 盧森堡 | LU | en-US, fr-FR |
| 澳門特別行政區 | MO | en-US, zh-HK |
| 馬其頓 (FYRO) | MK | en-US |
| 馬達加斯加 | MG | en-US |
| 馬拉威 | MW | en-US |
| 馬來西亞 | MY | en-US, ms-MY |
| 馬爾地夫 | MV | en-US |
| 馬利 | ML | en-US |
| 馬爾他 | MT | en-US |
| 馬紹爾群島 | MH | en-US |
| 馬丁尼克島 | MQ | en-US |
| 茅利塔尼亞 | [MR] | en-US |
| 模里西斯 | MU | en-US, ar-SA |
| 馬約特島 | YT | en-US |
| 墨西哥 | MX | en-US, es-ES |
| 密克羅尼西亞 | FM | en-US |
| 摩爾多瓦 | MD | en-US, ro-RO |
| 摩納哥 | [MC] | en-US, fr-FR |
| 蒙古 | MN | en-US |
| 蒙特內哥羅 | ME | en-US |
| 蒙特色拉特島 | MS | en-US |
| 摩洛哥 | MA | en-US, fr-FR, en-US |
| 莫三比克 | MZ | en-US |
| 緬甸文 | MM | en-US |
| 納米比亞 | NA | en-US |
| 諾魯 | NR | en-US |
| 尼泊爾聯邦民主共和國 | NP | en-US |
| 荷蘭 | NL | en-US, nl-NL |
| 新喀里多尼亞群島領土 | NC | en-US |
| 紐西蘭 | NZ | en-US |
| 尼加拉瓜 | NI | en-US, es-ES |
| 尼日 | NE | en-US |
| 奈及利亞 | NG | en-US |
| 紐威島 | NU | en-US |
| 諾福克島 | NF | en-US |
| 北馬里安納群島 | MP | en-US |
| 挪威 | 否 | en-US, nb-NO |
| 阿曼 | OM | en-US, ar-SA |
| 巴基斯坦 | PK | en-US |
| 帛琉 | PW | en-US |
| 黎凡特 | PS | en-US |
| 巴拿馬 | PA | en-US, es-ES |
| 巴布亞紐幾內亞 | PG | en-US |
| 巴拉圭 | PY | en-US, es-ES |
| 秘魯 | PE | en-US, es-ES |
| 菲律賓 | PH | en-US |
| 皮特康群島 | PN | en-US |
| 波蘭 | PL | en-US, pl-PL |
| 葡萄牙 | PT | en-US, pt-PT |
| 波多黎各 | PR | en-US, en-US |
| 卡達 | QA | en-US, ar-SA |
| 留尼旺 | RE | en-US |
| 羅馬尼亞 | RO | en-US, ro-RO |
| 俄羅斯 | RU | en-US, ru-RU |
| 盧安達 | RW | en-US, fr-FR |
| 聖多美普林西比 | ST | en-US, fr-FR |
| Saba | XS | en-US |
| Saint-Barthélemy | BL | en-US |
| 聖克里斯多福及尼維斯 | KN | en-US |
| 聖露西亞 | LC | en-US, en-US |
| 聖馬丁 | MF | en-US, en-US |
| 聖匹島 | PM | en-US |
| 聖文森及格瑞那丁 | VC | en-US |
| 薩摩亞獨立國 | WIN ENT LTSB 2016 Thai 64 Bits | en-US |
| 聖馬利諾 | SM | en-US |
| 沙烏地阿拉伯 | SA | en-US |
| 塞內加爾 | SN | en-US, fr-FR |
| 賽爾維亞 | RS | en-US, sr-Latn-RS, en-US |
| 塞席爾 | SC | en-US |
| 獅子山 | SL | en-US |
| 新加坡 | SG | en-US, zh-SG |
| Sint Eustatius | XE | en-US |
| 荷屬聖馬丁 | SX | en-US, en-US |
| 斯洛伐克 | SK | en-US, sk-SK |
| 斯洛維尼亞 | SI | en-US, sl-SI |
| 索羅門群島 | SB | en-US |
| 索馬利亞 | SO | en-US |
| 南非 | ZA | en-US |
| South Georgia and South Sandwich Islands | GS | en-US |
| 南蘇丹 | SS | en-US |
| 西班牙 | ES | en-US, es-ES, en-US, en-US |
| 斯里蘭卡 | LK | en-US |
| St Helena, Ascension, Tristan da Cunha | SH | en-US |
| 蘇利南 | SR | en-US |
| Svalbard | SJ | en-US |
| 瑞典 | SE | en-US, sv-SE |
| 瑞士 | CH | en-US, fr-FR, en-US, en-US |
| 台灣 | TW | en-US, zh-HK |
| 塔吉克 | TJ | en-US |
| 坦尚尼亞 | TZ | en-US |
| 泰國 | TH | en-US, th-TH |
| 東帝汶 | TL | en-US |
| 多哥 | TG | en-US |
| 托克勞群島 | TK | en-US |
| 東加 | TO | en-US |
| 千里達及托巴哥 | TT | en-US |
| 突尼西亞 | TN | en-US, fr-FR, en-US |
| 土耳其 | TR | en-US, tr-TR |
| 土庫曼 | TM | en-US |
| 土克斯及開科斯群島 | TC | en-US |
| 吐瓦魯 | TV | en-US |
| 美國外島 | UM | en-US |
| 美屬維爾京群島 | VI | en-US |
| 烏干達 | UG | en-US |
| 烏克蘭 | UA | en-US, uk-UA |
| 阿拉伯聯合大公國 | AE | en-US, ar-SA |
| 英國 | GB | en-US |
| 美國 | 美國 | en-US |
| 烏拉圭 | UY | en-US, es-ES |
| 烏茲別克 | UZ | en-US, ru-RU |
| 萬那杜 | VU | en-US |
| 梵蒂岡 | VA | en-US |
| 委內瑞拉 | VE | en-US, es-ES |
| 越南 | VN | en-US, vi-VN |
| 瓦利斯及福杜納 | WF | en-US |
| 葉門 | YE | en-US, ar-SA |
| 尚比亞 | ZM | en-US |
| 辛巴威 | ZW | en-US |


