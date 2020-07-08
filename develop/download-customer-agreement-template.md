---
title: 取得 Microsoft 客戶合約範本的下載連結
description: 取得 Microsoft 客戶合約範本的下載連結。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 8c794d264ad64a42fa6ca823ddfc3841248c01cd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098379"
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
> - Microsoft 客戶合約是國家/地區特定。 當要求下載 Microsoft 客戶合約範本的連結時，請務必根據客戶的位置指定正確的國家/地區。 或支援的國家/地區清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。
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
| GET | [* \{ baseURL \} *](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document？ language = {language} &country = {country} HTTP/1。1 |

### <a name="uri-parameters"></a>URI 參數

您可以搭配您的要求使用下列 URI 參數：

| 名稱                   | 類型   | 必要 | 說明                                 |
|------------------------|--------|----------|---------------------------------------------|
| 合約-範本識別碼  | 字串 | Yes      | 合約類型的唯一識別碼。 您可以藉由擷取 Microsoft 客戶合約的合約中繼資料，取得 Microsoft 客戶合約的 templateId。 如需詳細資訊，請參閱[取得 Microsoft 客戶合約的合約中繼資料](./get-customer-agreement-metadata.md)。 這個參數會區分**大小寫**。|
| country                | 字串 | No       | 指出套用合約範本的國家/地區。 如果未指定參數，查詢會預設為*US* 。 如需支援的國家/地區代碼清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。|
| 語言               | 字串 | No       | 指出應在其中當地語系化協定範本的語言。 如果未指定參數，或指定的國家（地區）代碼 in't 支援指定的國家/地區碼，則查詢會預設為*en-us* 。 如需支援的國家/地區代碼清單，請參閱[支援的國家/地區和語言清單](#list-of-supported-countries-and-languages)。|

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

| 國家/地區                   | 國碼 (地區碼)   | 支援的語言代碼 |
|------------------------|--------|----------|
| 奧蘭島 | 限於 | en-US |
| 阿富汗 | AF | en-US |
| 阿爾巴尼亞 | AL | en-US |
| 阿爾及利亞 | DZ | en-us、fr-fr、en-us |
| 美屬薩摩亞 | AS | en-US |
| 安道爾 | AD | en-US |
| 安哥拉 | AO | en-us、pt |
| 安奎拉 | AI | en-US |
| 南極洲 | AQ | en-US |
| 安地卡及巴布達 | AG | en-US |
| 阿根廷 | AR | en-us、es |
| 亞美尼亞 | AM | en-US |
| 荷屬阿魯巴 | AW | en-US |
| 澳大利亞 | AU | en-US |
| 奧地利 | AT | en-us，de |
| 亞塞拜然 | AZ | en-US |
| 巴哈馬 | BS | en-US |
| 巴林 | BH | en-us，ar-SA |
| 孟加拉 | BD | en-US |
| 巴貝多 | BB | en-US |
| 白俄羅斯 | BY | en-US、ru-RU |
| 比利時 | BE | en-us、nl-NL |
| 貝里斯 | BZ | en-us、es |
| 貝南 | BJ | en-US |
| 百慕達 | BM | en-US |
| 不丹 | BT | en-US |
| 玻利維亞 | BO | en-us、es |
| 波奈 | BQ | en-US |
| 波士尼亞赫塞哥維納 | BA | en-US |
| 波札那 | BW | en-US |
| 布威島 | BV | en-US |
| 巴西 | BR | en-us、pt-BR |
| 英屬印度洋領地 | IO | en-US |
| 英屬維京群島 | VG | en-US |
| 汶萊 | BN | en-US |
| 保加利亞 | BG | en-us、bg-BG |
| 布吉納法索 | BF | en-US |
| 蒲隆地 | BI | en-US |
| 象牙海岸 | CI | en-US、fr-FR |
| 維德角 | CV | en-us、pt |
| 柬埔寨 | KH | en-US |
| 喀麥隆 | CM | en-US、fr-FR |
| Canada | CA | en-US、fr-FR |
| 開曼群島 | KY | en-us、en-us |
| 中非共和國 | CF | en-US |
| 查德 | TD | en-US |
| 智利 | CL | en-us、es |
| 聖誕島 | CX | en-US |
| 科克斯 (基靈) 群島 | CC | en-US |
| 哥倫比亞 | CO | en-us、es |
| 葛摩 | KM | en-US |
| 剛果民主共和國 | CD | en-US |
| 剛果 | CG | en-US |
| 庫克群島 | CK | en-US |
| 哥斯大黎加 | CR | en-us、es |
| 克羅埃西亞 | HR | en-us、hr-HR |
| 古拉果 | CW | en-US |
| 賽浦路斯 | CY | en-US |
| 捷克 | CZ | en-us、cs-CZ |
| 丹麥 | DK | en-us、da-深色 |
| 吉布地 | DJ | en-US |
| 多米尼克 | DM | en-US |
| 多明尼加共和國 | DO | en-us、es |
| 厄瓜多 | EC | en-US |
| 埃及 | EG | en-us，ar-SA |
| 薩爾瓦多 | SV | en-us、es |
| 赤道幾內亞 | GQ | en-US |
| 厄利垂亞 | ER | en-US |
| 愛沙尼亞 | EE | en-us，et-EE |
| eSwatini | SZ | en-US |
| 衣索比亞 | ET | en-US |
| 福克蘭群島 | FK | en-US |
| 法羅群島 | FO | en-US |
| 斐濟 | FJ | en-US |
| 芬蘭 | FI | en-us、fi |
| 法國 | FR | en-US、fr-FR |
| 法屬圭亞那 | GF | en-US、fr-FR  |
| 法屬玻里尼西亞 | PF | en-US |
| 法屬南部屬地 | TF | en-US |
| 加彭 | GA | en-US |
| 甘比亞 | GM | en-US |
| 喬治亞 | GE | en-US |
| 德國 | DE | en-us，de |
| 迦納 | GH | en-US |
| 直布羅陀 | GI | en-US |
| 希臘 | GR | en-us、el-GR |
| 格陵蘭 | GL | en-US |
| 格瑞那達 | GD | en-US |
| 瓜地洛普 | GP | en-US |
| 關島 | GU | en-US |
| 瓜地馬拉 | GT | en-us、es |
| 根息 | GG | en-US |
| 幾內亞 | GN | en-US |
| 幾內亞比索 | GW | en-US |
| 蓋亞那 | GY | en-US |
| 海地 | HT | en-US |
| 赫德島及麥當勞群島 | HM | en-US |
| 宏都拉斯 | HN | en-us、es |
| 香港特別行政區 | HK | en-us、zh-HK |
| 匈牙利 | HU | en-us、hu-HU |
| 冰島 | IS | en-US |
| 印度 | IN | en-us，hi |
| 印尼 | ID | en-us，識別碼識別碼 |
| 伊拉克 | IQ | en-us，ar-SA |
| 愛爾蘭 | IE | en-US |
| 曼島 | IM | en-US |
| 以色列 | IL | en-us、他-IL |
| 義大利 | IT | en-us，it-IT |
| 牙買加 | JM | en-US |
| 尖棉 | XJ | en-US |
| 日本 | JP | en-us、ja-jp |
| 澤西島 | JE | en-US |
| 約旦 | JO | en-us，ar-SA |
| 哈薩克 | KZ | en-us、kk-KZ |
| 肯亞 | KE | en-US |
| 吉里巴斯 | KI | en-US |
| 南韓 | KR | en-us、ko-KR |
| 科索沃 | XK | en-US |
| 科威特 | KW | en-us，ar-SA |
| 吉爾吉斯 | KG | en-US、ru-RU |
| 寮國 | LA | en-US |
| 拉脫維亞 | LV | en-us，lv-LV |
| 黎巴嫩 | LB | en-us，ar-SA |
| 賴索托 | LS | en-US |
| 賴比瑞亞 | LR | en-US |
| 利比亞 | LY | en-us，ar-SA |
| 列支敦斯登 | LI | en-us，de |
| 立陶宛 | LT | en-us、lt-LT |
| 盧森堡 | LU | en-US、fr-FR |
| 澳門特別行政區 | MO | en-us、zh-HK |
| 馬其頓 (FYRO) | MK | en-US |
| 馬達加斯加 | MG | en-US |
| 馬拉威 | MW | en-US |
| 馬來西亞 | MY | en-us、ms-MY |
| 馬爾地夫 | MV | en-US |
| 馬利 | ML | en-US |
| 馬爾他 | MT | en-US |
| 馬紹爾群島 | MH | en-US |
| 馬丁尼克 | MQ | en-US |
| 茅利塔尼亞 | MR | en-US |
| 模里西斯 | MU | en-us，ar-SA |
| 馬約特島 | YT | en-US |
| 墨西哥 | MX | en-us、es |
| 密克羅尼西亞 | FM | en-US |
| 摩爾多瓦 | MD | en-us、ro-RO |
| 摩納哥 | MC | en-US、fr-FR |
| 蒙古 | MN | en-US |
| 蒙特內哥羅 | ME | en-US |
| 蒙哲臘 | MS | en-US |
| 摩洛哥 | MA | en-us、fr-fr、en-us |
| 莫三比克 | MZ | en-US |
| 緬甸 | MM | en-US |
| 納米比亞 | NA | en-US |
| 諾魯 | NR | en-US |
| 尼泊爾 | NP | en-US |
| 荷蘭 | NL | en-us、nl-NL |
| 新喀里多尼亞 | NC | en-US |
| 紐西蘭 | NZ | en-US |
| 尼加拉瓜 | NI | en-us、es |
| 尼日 | NE | en-US |
| 奈及利亞 | NG | en-US |
| 紐埃島 | NU | en-US |
| 諾福克島 | NF | en-US |
| 北馬利安納群島 | MP | en-US |
| 挪威 | 否 | en-us，nb-否 |
| 阿曼 | OM | en-us，ar-SA |
| 巴基斯坦 | PK | en-US |
| 帛琉 | PW | en-US |
| 巴勒斯坦民族權力機構 | PS | en-US |
| 巴拿馬 | PA | en-us、es |
| 巴布亞紐幾內亞 | PG | en-US |
| 巴拉圭 | PY | en-us、es |
| 祕魯 | PE | en-us、es |
| 菲律賓 | PH | en-US |
| 皮特康群島 | PN | en-US |
| 波蘭 | PL | en-us，pl-PL |
| 葡萄牙 | PT | en-us、pt |
| 波多黎各 | PR | en-us、en-us |
| 卡達 | QA | en-us，ar-SA |
| 留尼旺 | RE | en-US |
| 羅馬尼亞 | RO | en-us、ro-RO |
| 俄羅斯 | RU | en-US、ru-RU |
| 盧安達 | RW | en-US、fr-FR |
| 聖多美普林西比 | ST | en-US、fr-FR |
| 沙巴 | XS | en-US |
| 聖巴瑟米 | BL | en-US |
| 聖克里斯多福及尼維斯 | KN | en-US |
| 聖露西亞 | LC | en-us、en-us |
| 法屬聖馬丁 | MF | en-us、en-us |
| 聖匹島 | 下午 | en-US |
| 聖文森及格瑞那丁 | VC | en-US |
| 薩摩亞 | WS | en-US |
| 聖馬利諾 | SM | en-US |
| 沙烏地阿拉伯 | SA | en-US |
| 塞內加爾 | SN | en-US、fr-FR |
| 塞爾維亞 | RS | en-us、sr-iov-Latn-RS、en-us |
| 塞席爾 | SC | en-US |
| 獅子山 | SL | en-US |
| 新加坡 | SG | en-us、zh-SG |
| 聖佑達修斯 | XE | en-US |
| 荷屬聖馬丁 | X | en-us、en-us |
| 斯洛伐克 | SK | en-us，sk |
| 斯洛維尼亞 | SI | en-us、sl-SI |
| 索羅門群島 | SB | en-US |
| 索馬利亞 | SO | en-US |
| 南非 | ZA | en-US |
| 南喬治亞與南三明治群島 | GS | en-US |
| 南蘇丹 | SS | en-US |
| 西班牙 | ES | en-us、es、en-us、en-us （us） |
| 斯里蘭卡 | LK | en-US |
| 聖赫勒拿、阿森松、特里斯坦達庫尼亞群島 | SH | en-US |
| 蘇利南 | SR | en-US |
| 冷岸 | SJ | en-US |
| 瑞典 | SE | en-us、sv-SE |
| 瑞士 | CH | en-us、fr-fr、en-us、en-us （us） |
| 台灣 | TW | en-us、zh-HK |
| 塔吉克 | TJ | en-US |
| 坦尚尼亞 | TZ | en-US |
| 泰國 | 二四 | en-us，第一次 |
| 東帝汶 | TL | en-US |
| 多哥 | TG | en-US |
| 托克勞群島 | TK | en-US |
| 東加 | TO | en-US |
| 千里達及托巴哥 | TT | en-US |
| 突尼西亞 | TN | en-us、fr-fr、en-us |
| 土耳其 | TR | en-us、tr-TR |
| 土庫曼 | TM | en-US |
| 土克斯及開科斯群島 | TC | en-US |
| 吐瓦魯 | TV | en-US |
| 美國外島 | UM | en-US |
| 美式英文維京群島 | VI | en-US |
| 烏干達 | UG | en-US |
| 烏克蘭 | UA | en-us、uk-UA |
| 阿拉伯聯合大公國 | AE | en-us，ar-SA |
| United Kingdom | GB | en-US |
| 美國 | US | en-US |
| 烏拉圭 | UY | en-us、es |
| 烏茲別克 | UZ | en-US、ru-RU |
| 萬那杜 | VU | en-US |
| 梵蒂岡 | VA | en-US |
| 委內瑞拉 | VE | en-us、es |
| 越南 | VN | en-us、vi-VN |
| 瓦利斯及福杜納 | WF | en-US |
| 葉門 | YE | en-us，ar-SA |
| 尚比亞 | ZM | en-US |
| 辛巴威 | ZW | en-US |
