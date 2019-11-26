---
title: Partner Center supported languages and locales
description: List of ISO2 and ISO3 supported locales for Partner Center.
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6b066c4afb87656717327e57cef94ab84eb93309
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488288"
---
# <a name="partner-center-supported-languages-and-locales"></a>Partner Center supported languages and locales


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Some Partner Center APIs require a value indicating a locale, country or region. For example, the [Partner Center REST header](headers.md) X-Locale requires a value often in the format "language-country" ("en-US" indicates "English - United States").

In the Partner Center managed APIs, the [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules) class and the [OfferCategory.Locale](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale), [ServiceRequest.CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode), or [CustomerBillingProfile.Culture](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture) properties require string values that indicate a language or country/region (in the form of an ISO2 language code or ISO3 country/region code), a locale, or a culture (a language ID combined with a country/region code).

The following table lists the cultures and International Standards Organization (ISO) country codes that are supported in the Partner Center APIs. 


| 國家/地區                           | ISO Alpha 2 Country Code | ISO Alpha 3 Country Code | Supported Culture(s)                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| 阿富汗                              | AF                       | AFG                      | ps-AF / en-US                         |
| 奧蘭島                            | AX                       | ALA                      | sv-SE / en-US                         |
| 阿爾巴尼亞                                  | AL                       | ALB                      | sq-AL / en-US                         |
| 阿爾及利亞                                  | DZ                       | DZA                      | ar-DZ / en-US                         |
| 美屬薩摩亞                           | AS                       | ASM                      | en-US                                 |
| 安道爾                                  | AD                       | 和                      | ca-ES / en-US                         |
| 安哥拉                                   | AO                       | AGO                      | pt-PT / en-US                         |
| 安圭拉                                 | AI                       | AIA                      | en-US                                 |
| 南極大陸                               | AQ                       | ATA                      | en-US                                 |
| 安地卡及巴布達                      | AG                       | ATG                      | en-US                                 |
| 阿根廷                                | AR                       | ARG                      | es-AR / en-US                         |
| 亞美尼亞                                  | AM                       | ARM                      | hy-AM / en-US                         |
| 阿路巴                                    | AW                       | ABW                      | nl-NL / en-US                         |
| 澳大利亞                                | AU                       | AUS                      | en-AU / en-US                         |
| 奧地利                                  | AT                       | AUT                      | de-AT / en-US                         |
| 亞塞拜然                               | AZ                       | AZE                      | az-Latn-AZ / en-US                    |
| 巴哈馬                                  | BS                       | BHS                      | en-GB / en-US                         |
| 巴林                                  | BH                       | BHR                      | ar-BH / en-US                         |
| 孟加拉                               | BD                       | BGD                      | bn-BD / en-US                         |
| 巴貝多                                 | BB                       | BRB                      | en-GB / en-US                         |
| 白俄羅斯                                  | BY                       | BLR                      | be-BY / en-US                         |
| 比利時                                  | BE                       | BEL                      | fr-BE / nl-BE / en-US                 |
| 貝里斯                                   | BZ                       | BLZ                      | en-BZ / en-US                         |
| 貝南                                    | BJ                       | BEN                      | fr-FR / en-US                         |
| 百慕達                                  | BM                       | BMU                      | en-GB / en-US                         |
| 不丹                                   | BT                       | BTN                      | en-US                                 |
| 玻利維亞                                  | BO                       | BOL                      | es-BO / en-US                         |
| 波奈                                  | BQ                       | BES                      | nl-NL / en-US                         |
| 波士尼亞與赫塞哥維納                   | BA                       | BIH                      | bs-Latn-BA / en-US                    |
| 波札那                                 | BW                       | BWA                      | en-GB / en-US                         |
| 布威島                            | BV                       | BVT                      | nb-NO / en-US                         |
| 巴西                                   | BR                       | BRA                      | pt-BR / en-US                         |
| 英屬印度洋領土           | IO                       | IOT                      | en-US                                 |
| 英屬維爾京群島                   | VG                       | VGB                      | en-US                                 |
| 汶萊                                   | BN                       | BRN                      | ms-BN / en-US                         |
| 保加利亞                                 | BG                       | BGR                      | bg-BG / en-US                         |
| 布吉納法索                             | BF                       | BFA                      | fr-FR / en-US                         |
| 蒲隆地                                  | BI                       | BDI                      | fr-FR / en-US                         |
| 維德角                               | CV                       | CPV                      | pt-CV / en-US                         |
| 柬埔寨                                 | KH                       | KHM                      | km-KH / en-US                         |
| 喀麥隆                                 | CM                       | CMR                      | fr-FR / en-US                         |
| 加拿大                                   | CA                       | CAN                      | fr-CA / en-US                         |
| 開曼群島                           | KY                       | CYM                      | en-GB / en-US                         |
| 中非共和國                 | CF                       | CAF                      | fr-FR / en-US                         |
| 查德                                     | TD                       | TCD                      | fr-FR / en-US                         |
| 智利                                    | CL                       | CHL                      | es-CL / en-US                         |
| 中國                                    | CN                       | CHN                      | zh-CN / en-US                         |
| 聖誕島                         | CX                       | CXR                      | en-US                                 |
| 可可斯群島                  | CC                       | CCK                      | en-US                                 |
| 哥倫比亞                                 | CO                       | COL                      | es-CO / en-US                         |
| 葛摩                                  | KM                       | COM                      | fr-FR / en-US                         |
| 剛果共和國                                    | CG                       | COG                      | fr-FR / en-US                         |
| 剛果民主共和國 (DRC)                              | CD                       | COD                      | fr-FR / en-US                         |
| 柯克群島                             | CK                       | COK                      | en-US                                 |
| 哥斯大黎加                               | CR                       | CRI                      | es-CR / en-US                         |
| 科特迪瓦                            | CI                       | CIV                      | fr-FR / en-US                         |
| 克羅埃西亞                                  | HR                       | HRV                      | hr-HR / en-US                         |
| 古拉梳                                  | CW                       | CUW                      | nl-NL / en-US                         |
| 賽普勒斯                                   | CY                       | CYP                      | el-GR / en-US                         |
| Czechia                                  | CZ                       | CZE                      | cs-CZ / en-US                         |
| 丹麥                                  | DK                       | DNK                      | da-DK / en-US                         |
| 吉布地                                 | DJ                       | DJI                      | fr-FR / en-US                         |
| 多米尼克                                 | DM                       | DMA                      | en-US                                 |
| 多明尼加共和國                       | DO                       | DOM                      | es-DO / en-US                         |
| 厄瓜多                                  | EC                       | ECU                      | es-EC / en-US                         |
| 埃及                                    | EG                       | EGY                      | ar-EG / en-US                         |
| 薩爾瓦多                              | SV                       | SLV                      | es-SV / en-US                         |
| 赤道幾內亞                        | GQ                       | GNQ                      | es-ES / en-US                         |
| 厄利垂亞                                  | ER                       | ERI                      | ar-SA / en-US                         |
| 愛沙尼亞                                  | EE                       | EST                      | et-EE / en-US                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| 衣索比亞                                 | ET                       | ETH                      | am-ET / en-US                         |
| 福克蘭群島                         | FK                       | FLK                      | en-US                                 |
| 法羅群島 (丹麥)                            | FO                       | FRO                      | fo-FO / en-US                         |
| 斐濟群島                                     | FJ                       | FJI                      | en-GB / en-US                         |
| 芬蘭                                  | FI                       | FIN                      | fi-FI / sv-FI / en-US                 |
| 法國                                   | FR                       | FRA                      | fr-FR / en-US                         |
| 法屬圭亞那                            | GF                       | GUF                      | fr-FR / en-US                         |
| 法屬玻里尼西亞                         | PF                       | PYF                      | fr-FR / en-US                         |
| 法屬南半球領土              | TF                       | ATF                      | fr-FR / en-US                         |
| 加彭                                    | GA                       | GAB                      | fr-FR / en-US                         |
| 甘比亞                                   | GM                       | GMB                      | en-US                                 |
| 喬治亞                                  | GE                       | GEO                      | ka-GE / en-US                         |
| 德國                                  | DE                       | DEU                      | de-DE / en-US                         |
| 迦納                                    | GH                       | GHA                      | en-GB / en-US                         |
| 直布羅陀                                | GI                       | GIB                      | en-US                                 |
| 希臘                                   | GR                       | GRC                      | el-GR / en-US                         |
| 格陵蘭 (丹麥)                                | GL                       | GRL                      | da-DK / en-US                         |
| 格瑞那達                                  | GD                       | GRD                      | en-US                                 |
| 瓜地洛普                               | GP                       | GLP                      | fr-FR / en-US                         |
| 關島                                     | GU                       | GUM                      | en-US                                 |
| 瓜地馬拉                                | GT                       | GTM                      | es-GT / en-US                         |
| 根息                                 | GG                       | GGY                      | en-US                                 |
| 幾內亞                                   | GN                       | GIN                      | fr-FR / en-US                         |
| 幾內亞比索                            | GW                       | GNB                      | pt-PT / en-US                         |
| 蓋亞納                                   | GY                       | GUY                      | en-US                                 |
| 海地                                    | HT                       | HTI                      | fr-FR / en-US                         |
| 赫德島及麥當勞群島        | HM                       | HMD                      | en-US                                 |
| 宏都拉斯                                 | HN                       | HND                      | es-HN / en-US                         |
| 香港特別行政區                            | HK                       | HKG                      | zh-HK / en-US                         |
| 匈牙利                                  | HU                       | HUN                      | hu-HU / en-US                         |
| 冰島                                  | IS                       | ISL                      | is-IS / en-US                         |
| 印度                                    | IN                       | IND                      | en-IN / hi-IN / en-US                 |
| 印尼                                | 識別碼                       | IDN                      | id-ID / en-US                         |
| 伊拉克                                     | IQ                       | IRQ                      | ar-IQ / en-US                         |
| 愛爾蘭                                  | IE                       | IRL                      | en-IE / en-US                         |
| 曼城島                              | IM                       | IMN                      | en-US                                 |
| 以色列                                   | IL                       | ISR                      | he-IL / en-US                         |
| 義大利                                    | IT                       | ITA                      | it-IT / en-US                         |
| 牙買加                                  | JM                       | JAM                      | en-JM / en-US                         |
| Jan Mayen                                | XJ                       | XJA                      | nb-NO / en-US                         |
| 日本                                    | JP                       | JPN                      | ja-JP / en-US                         |
| 澤西島                                   | JE                       | JEY                      | en-US                                 |
| 約旦                                   | JO                       | JOR                      | ar-JO / en-US                         |
| 哈薩克                               | KZ                       | KAZ                      | kk-KZ / en-US                         |
| 肯亞                                    | KE                       | KEN                      | sw-KE / en-US                         |
| 吉里巴斯                                 | KI                       | KIR                      | en-US                                 |
| 韓國                                    | KR                       | KOR                      | ko-KR / en-US                         |
| Kosovo                                   | XK                       | XKS                      | en-US                                 |
| 科威特                                   | KW                       | KWT                      | ar-KW / en-US                         |
| 吉爾吉斯                               | KG                       | KGZ                      | ky-KG / en-US                         |
| 寮國                                     | LA                       | LAO                      | lo-LA / en-US                         |
| 拉脫維亞                                   | LV                       | LVA                      | lv-LV / en-US                         |
| 黎巴嫩                                  | LB                       | LBN                      | ar-LB / en-US                         |
| 賴索托                                  | LS                       | LSO                      | en-US                                 |
| 賴比瑞亞                                  | LR                       | LBR                      | en-US                                 |
| 利比亞                                    | LY                       | LBY                      | ar-LY / en-US                         |
| 列支敦斯登                            | LI                       | LIE                      | de-LI / en-US                         |
| 立陶宛                                | LT                       | LTU                      | lt-LT / en-US                         |
| 盧森堡                               | LU                       | LUX                      | de-LU / fr-LU / en-US                 |
| 澳門特別行政區                                | MO                       | MAC                      | zh-MO / en-US                         |
| 馬其頓 (FYRO)                          | MK                       | MKD                      | mk-MK / en-US                         |
| 馬達加斯加                               | MG                       | MDG                      | fr-FR / en-US                         |
| 馬拉威                                   | MW                       | MWI                      | en-US                                 |
| 馬來西亞                                 | MY                       | MYS                      | en-MY / en-US                         |
| 馬爾地夫                                 | MV                       | MDV                      | dv-MV / en-US                         |
| 馬利                                     | ML                       | MLI                      | fr-FR / en-US                         |
| 馬爾他                                    | MT                       | MLT                      | mt-MT / en-US                         |
| 馬紹爾群島                         | MH                       | MHL                      | en-US                                 |
| 馬丁尼克島                               | MQ                       | MTQ                      | fr-FR / en-US                         |
| 茅利塔尼亞                               | [MR]                       | MRT                      | ar-SA / en-US                         |
| 模里西斯                                | MU                       | MUS                      | en-GB / en-US                         |
| 馬約特島                                  | YT                       | MYT                      | fr-FR / en-US                         |
| 墨西哥                                   | MX                       | MEX                      | es-MX / en-US                         |
| 密克羅尼西亞                               | FM                       | FSM                      | en-US                                 |
| 摩爾多瓦                                  | MD                       | MDA                      | ro-RO / en-US                         |
| 摩納哥                                   | [MC]                       | MCO                      | fr-MC / en-US                         |
| 蒙古                                 | MN                       | MNG                      | mn-MN / en-US                         |
| 蒙特內哥羅                               | ME                       | MNE                      | sr-Latn-ME / en-US                    |
| 蒙特色拉特島                               | MS                       | MSR                      | en-US                                 |
| 摩洛哥                                  | MA                       | MAR                      | ar-MA / en-US                         |
| 莫三比克                               | MZ                       | MOZ                      | pt-PT / en-US                         |
| 緬甸文                                  | MM                       | MMR                      | en-US                                 |
| 納米比亞                                  | NA                       | NAM                      | en-GB / en-US                         |
| 諾魯                                    | NR                       | NRU                      | en-US                                 |
| 尼泊爾聯邦民主共和國                                    | NP                       | NPL                      | ne-NP / en-US                         |
| 荷屬安替列斯                     | AN                       | ANT                      | en-US                                 |
| Netherlands, The                         | NL                       | NLD                      | nl-NL / en-US                         |
| 新喀里多尼亞群島領土                            | NC                       | NCL                      | fr-FR / en-US                         |
| 紐西蘭                              | NZ                       | NZL                      | en-NZ / en-US                         |
| 尼加拉瓜                                | NI                       | NIC                      | es-NI / en-US                         |
| 尼日                                    | NE                       | NER                      | fr-FR / en-US                         |
| 奈及利亞                                  | NG                       | NGA                      | ha-Latn-NG / en-US                    |
| 紐威島                                     | NU                       | NIU                      | en-US                                 |
| 諾福克島                           | NF                       | NFK                      | en-US                                 |
| 北馬里安納群島                 | MP                       | MNP                      | en-US                                 |
| 挪威                                   | 否                       | NOR                      | nb-NO / en-US                         |
| 阿曼                                     | OM                       | OMN                      | ar-OM / en-US                         |
| 巴基斯坦                                 | PK                       | PAK                      | ur-PK / en-US                         |
| 帛琉                                    | PW                       | PLW                      | en-US                                 |
| 黎凡特                    | PS                       | PSE                      | ar-SA / en-US                         |
| 巴拿馬                                   | PA                       | PAN                      | es-PA / en-US                         |
| 巴布亞紐幾內亞                         | PG                       | PNG                      | en-US                                 |
| 巴拉圭                                 | PY                       | PRY                      | es-PY / en-US                         |
| 秘魯                                     | PE                       | PER                      | es-PE / en-US                         |
| 菲律賓                              | PH                       | PHL                      | en-PH / en-US                         |
| 皮特康群島                         | PN                       | PCN                      | en-US                                 |
| 波蘭                                   | PL                       | POL                      | pl-PL / en-US                         |
| 葡萄牙                                 | PT                       | PRT                      | pt-PT / en-US                         |
| 波多黎各                              | PR                       | PRI                      | es-PR / en-US                         |
| 卡達                                    | QA                       | QAT                      | ar-QA / en-US                         |
| 留尼旺                                  | RE                       | REU                      | fr-FR / en-US                         |
| 羅馬尼亞                                  | RO                       | ROU                      | ro-RO / en-US                         |
| 俄羅斯                                   | RU                       | RUS                      | ru-RU / en-US                         |
| 盧安達                                   | RW                       | RWA                      | rw-RW / en-US                         |
| Saba                                     | XS                       | XSA                      | nl-NL / en-US                         |
| 聖克里斯多福及尼維斯                    | KN                       | KNA                      | en-GB / en-US                         |
| 聖露西亞                              | LC                       | LCA                      | en-US                                 |
| 聖馬丁                             | MF                       | MAF                      | fr-FR / en-US                         |
| 聖匹島                | PM                       | SPM                      | fr-FR / en-US                         |
| 聖文森及格瑞那丁         | VC                       | VCT                      | en-US                                 |
| Saint-Barthélemy                         | BL                       | BLM                      | fr-FR / en-US                         |
| 薩摩亞獨立國                                    | WIN ENT LTSB 2016 Thai 64 Bits                       | WSM                      | en-US                                 |
| 聖馬利諾                               | SM                       | SMR                      | it-IT / en-US                         |
| 聖多美普林西比                    | ST                       | STP                      | pt-PT / en-US                         |
| 沙烏地阿拉伯                             | SA                       | SAU                      | ar-SA / en-US                         |
| 塞內加爾                                  | SN                       | SEN                      | wo-SN / en-US                         |
| 賽爾維亞                                   | RS                       | SRB                      | sr-Latn-RS / sr-Cyrl-RS / en-US       |
| 塞席爾                               | SC                       | SYC                      | en-US                                 |
| 獅子山                             | SL                       | SLE                      | en-US                                 |
| 新加坡                                | SG                       | SGP                      | en-SG / zh-SG / en-US                 |
| Sint Eustatius                           | XE                       | XSE                      | nl-NL / en-US                         |
| 荷屬聖馬丁                             | SX                       | SXM                      | en-US                                 |
| 斯洛伐克                                 | SK                       | SVK                      | sk-SK / en-US                         |
| 斯洛維尼亞                                 | SI                       | SVN                      | sl-SI / en-US                         |
| 索羅門群島                          | SB                       | SLB                      | en-US                                 |
| 索馬利亞                                  | SO                       | SOM                      | ar-SA / en-US                         |
| 南非                             | ZA                       | ZAF                      | en-ZA / en-US                         |
| South Georgia and South Sandwich Islands | GS                       | SGS                      | en-US                                 |
| 南蘇丹                              | SS                       | SSD                      | en-US                                 |
| 西班牙                                    | ES                       | ESP                      | es-ES / ca-ES / eu-ES / gl-ES / en-US |
| 斯里蘭卡                                | LK                       | LKA                      | si-LK / en-US                         |
| St Helena, Ascension, Tristan da Cunha   | SH                       | SHN                      | en-US                                 |
| 蘇利南                                 | SR                       | SUR                      | nl-NL                                 |
| Svalbard                                 | SJ                       | SJM                      | nb-NO / en-US                         |
| 瑞典                                   | SE                       | SWE                      | sv-SE / en-US                         |
| 瑞士                              | CH                       | CHE                      | de-CH / fr-CH / it-CH / en-US         |
| 台灣                                   | TW                       | TWN                      | zh-TW / en-US                         |
| 塔吉克                               | TJ                       | TJK                      | tg-Cyrl-TJ / en-US                    |
| 坦尚尼亞                                 | TZ                       | TZA                      | en-GB / en-US                         |
| 泰國                                 | TH                       | THA                      | th-TH / en-US                         |
| 東帝汶                              | TL                       | TLS                      | pt-PT / en-US                         |
| 多哥                                     | TG                       | TGO                      | fr-FR / en-US                         |
| 托克勞群島                                  | TK                       | TKL                      | en-US                                 |
| 東加                                    | TO                       | TON                      | en-US                                 |
| 千里達及托巴哥                      | TT                       | TTO                      | en-TT / en-US                         |
| 突尼西亞                                  | TN                       | TUN                      | ar-TN / en-US                         |
| 土耳其                                   | TR                       | TUR                      | tr-TR / en-US                         |
| 土庫曼                             | TM                       | TKM                      | tk-TM / en-US                         |
| 土克斯及開科斯群島                 | TC                       | TCA                      | en-US                                 |
| 吐瓦魯                                   | TV                       | TUV                      | en-US                                 |
| 烏干達                                   | UG                       | UGA                      | en-GB / en-US                         |
| 烏克蘭                                  | UA                       | UKR                      | uk-UA / en-US                         |
| 阿拉伯聯合大公國                     | AE                       | ARE                      | ar-AE / en-US                         |
| 英國                           | GB                       | GBR                      | en-GB / en-US                         |
| 美國外島                    | UM                       | UMI                      | en-US                                 |
| 美屬維爾京群島                      | VI                       | VIR                      | en-US                                 |
| 美國                            | 美國                       | USA                      | en-US / es-US                         |
| 烏拉圭                                  | UY                       | URY                      | es-UY / en-US                         |
| 烏茲別克                               | UZ                       | UZB                      | uz-Latn-UZ / en-US                    |
| 萬那杜                                  | VU                       | VUT                      | en-US                                 |
| 梵蒂岡                             | VA                       | VAT                      | it-IT / en-US                         |
| 委內瑞拉                                | VE                       | VEN                      | es-VE / en-US                         |
| 越南                                  | VN                       | VNM                      | vi-VN / en-US                         |
| 瓦利斯及福杜納                        | WF                       | WLF                      | fr-FR / en-US                         |
| 葉門                                    | YE                       | YEM                      | ar-YE / en-US                         |
| 尚比亞                                   | ZM                       | ZMB                      | en-GB / en-US                         |
| 辛巴威                                 | ZW                       | ZWE                      | en-ZW / en-US                         |

