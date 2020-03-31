---
title: 合作夥伴中心支援的語言和地區設定
description: 合作夥伴中心所支援的 ISO2 和 ISO3 地區設定清單。
ms.date: 12/03/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: bf12829decaebd8525ef0a51a7856c75aa69785d
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416375"
---
# <a name="partner-center-supported-languages-and-locales"></a>合作夥伴中心支援的語言和地區設定


**適用於**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

某些合作夥伴中心 Api 需要一個值，指出地區設定、國家或地區。 例如，[合作夥伴中心 REST 標頭](headers.md)X-地區設定需要值的格式通常為 "language-country" （"en-us" 表示「英文-美國」）。

在合作夥伴中心受管理的 Api 中， [CountryValidationRules](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.countryvalidationrules.countryvalidationrules)類別和[OfferCategory](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.offers.offercategory.locale)、 [ServiceRequest. CountryCode](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.countrycode)或[CustomerBillingProfile。文化](https://docs.microsoft.com/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile.culture)特性屬性需要字串值，表示語言或國家/地區（以 ISO2 語言代碼或 ISO3 國家/地區代碼的形式）、地區設定或文化特性（與國家/地區代碼結合的語言識別項）。

下表列出合作夥伴中心 Api 支援的文化特性和國際標準組織（ISO）國家/地區代碼。 


| Country/Region                           | ISO Alpha 2 國家/地區代碼 | ISO Alpha 3 國家/地區代碼 | 支援的文化特性                  |
|------------------------------------------|--------------------------|--------------------------|---------------------------------------|
| 阿富汗                              | AF                       | AFG                      | ps-AF/en-us                         |
| 奧蘭島                            | 限於                       | 亨茨維爾                      | sv-SE/en-us                         |
| 阿爾巴尼亞                                  | AL                       | ALB                      | sq-AL/en-us                         |
| 阿爾及利亞                                  | DZ                       | DZA                      | ar-DZ/en-us                         |
| 美屬薩摩亞                           | 一旦                       | ASM                      | en-US                                 |
| 安道爾                                  | 計畫                       | 和                      | ca-ES/en-us                         |
| 安哥拉                                   | AO                       | 曾                      | pt-PT/en-us                         |
| 安圭拉                                 | AI                       | AIA                      | en-US                                 |
| 南極大陸                               | AQ                       | ATA                      | en-US                                 |
| 安地卡及巴布達                      | AG                       | ATG                      | en-US                                 |
| 阿根廷                                | AR                       | ARG                      | es-AR/en-us                         |
| 亞美尼亞                                  | AM                       | ARM                      | hy-AM/en-us                         |
| 阿路巴                                    | AW                       | ABW                      | nl-NL/en-us                         |
| 澳洲                                | AU                       | 澳大利亞                      | en-us/en-us                         |
| 奧地利                                  | AT                       | 自動                      | de/en-us                         |
| 亞塞拜然                               | AZ                       | AZE                      | az-Latn-AZ/en-us                    |
| 巴哈馬                                  | BS                       | BHS                      | en-GB/en-us                         |
| 巴林                                  | BH                       | BHR                      | ar-BH/en-us                         |
| 孟加拉                               | BD                       | BGD                      | bn-BD/en-us                         |
| 巴貝多                                 | BB                       | BRB                      | en-GB/en-us                         |
| 白俄羅斯                                  | BY                       | BLR                      | 由 US/en-us 組成                         |
| 比利時                                  | BE                       | BEL                      | fr/nl-US/en-us                 |
| 貝里斯                                   | 依                       | BLZ                      | en-us-依/en-us                         |
| 貝南                                    | BJ                       | 本                      | fr-FR/en-us                         |
| 百慕達                                  | BM                       | BMU                      | en-GB/en-us                         |
| 不丹                                   | BT                       | BTN                      | en-US                                 |
| 玻利維亞                                  | BO                       | 首                      | es-BO/en-us                         |
| 波奈                                  | BQ                       | BE                      | nl-NL/en-us                         |
| 波士尼亞與赫塞哥維納                   | BA                       | BIH                      | bs-Latn-BA/en-us                    |
| 波札那                                 | BW                       | BWA                      | en-GB/en-us                         |
| 布威島                            | BV                       | BVT                      | nb-否/en-us                         |
| 巴西                                   | BR                       | BRA                      | pt-BR/en-us                         |
| 英屬印度洋領土           | IO                       | IOT                      | en-US                                 |
| 英屬維爾京群島                   | VG                       | VGB                      | en-US                                 |
| 汶萊                                   | BN                       | BRN                      | BN/en-us                         |
| 保加利亞                                 | BG                       | BGR                      | bg-BG/en-us                         |
| 布吉納法索                             | BF                       | BFA                      | fr-FR/en-us                         |
| 蒲隆地                                  | 隔                       | BDI                      | fr-FR/en-us                         |
| 維德角                               | CV                       | CPV                      | pt-CV/en-us                         |
| 柬埔寨                                 | KH                       | KHM                      | 公里-KH/en-us                         |
| 喀麥隆                                 | CM                       | CMR                      | fr-FR/en-us                         |
| 加拿大                                   | CA                       | 可以                      | fr-CA/en-us                         |
| 開曼群島                           | KY                       | CYM                      | en-GB/en-us                         |
| 中非共和國                 | CF                       | CAF                      | fr-FR/en-us                         |
| 查德                                     | TD                       | TCD                      | fr-FR/en-us                         |
| 智利                                    | CL                       | CHL                      | es-CL/en-us                         |
| 中國                                    | CN                       | CHN                      | zh-CN/en-us                         |
| 聖誕島                         | CX                       | .CXR                      | en-US                                 |
| 可可斯群島                  | 副本                       | CCK                      | en-US                                 |
| 哥倫比亞                                 | CO                       | 均值                      | es-共同/en-us                         |
| 葛摩                                  | KM                       | COM                      | fr-FR/en-us                         |
| 剛果共和國                                    | CG                       | 齒輪                      | fr-FR/en-us                         |
| 剛果民主共和國 (DRC)                              | CD                       | COD                      | fr-FR/en-us                         |
| 柯克群島                             | CK                       | COK                      | en-US                                 |
| 哥斯大黎加                               | CR                       | CRI                      | es-CR/en-us                         |
| 科特迪瓦                            | CI                       | CIV                      | fr-FR/en-us                         |
| 克羅埃西亞                                  | HR                       | HRV                      | hr-HR/en-us                         |
| 古拉梳                                  | 順                       | CUW                      | nl-NL/en-us                         |
| 賽普勒斯                                   | CY                       | CYP                      | el-GR/en-us                         |
| Czechia                                  | CZ                       | CZE                      | cs-CZ/en-us                         |
| 丹麥                                  | DK                       | DNK                      | da-深/en-us                         |
| 吉布地                                 | DJ                       | DJI                      | fr-FR/en-us                         |
| 多米尼克                                 | DM                       | DMA                      | en-US                                 |
| 多明尼加共和國                       | DO                       | DOM                      | es-DO/en-us                         |
| 厄瓜多                                  | EC                       | ECU                      | es-EC/en-us                         |
| 埃及                                    | EG                       | EGY                      | ar-例如/en-us                         |
| 薩爾瓦多                              | SV                       | SLV                      | es-SV/en-us                         |
| 赤道幾內亞                        | GQ                       | GNQ                      | es/en-us                         |
| 厄利垂亞                                  | ER                       | ERI                      | ar-SA/en-us                         |
| 愛沙尼亞                                  | EE                       | EST                      | et-EE/en-us                         |
| eSwatini                                 | SZ                       | SWZ                      | en-US                                 |
| 衣索比亞                                 | ET                       | ETH                      | am-ET/en-us                         |
| 福克蘭群島                         | FK                       | FLK                      | en-US                                 |
| 法羅群島                            | FO                       | 從                      | fo/en-us                         |
| 斐濟群島                                     | FJ                       | FJI                      | en-GB/en-us                         |
| 芬蘭                                  | FI                       | FIN                      | wi-fi/sv-FI/en-us                 |
| France                                   | FR                       | FRA                      | fr-FR/en-us                         |
| 法屬圭亞那                            | GF                       | GUF                      | fr-FR/en-us                         |
| 法屬玻里尼西亞                         | PF                       | PYF                      | fr-FR/en-us                         |
| 法屬南半球領土              | TF                       | ATF                      | fr-FR/en-us                         |
| 加彭                                    | GA                       | GAB                      | fr-FR/en-us                         |
| 甘比亞                                   | GM                       | GMB                      | en-US                                 |
| Georgia                                  | GE                       | 異地                      | ka-GE/en-us                         |
| Germany                                  | DE                       | DEU                      | de/en-us                         |
| 迦納                                    | GH                       | GHA                      | en-GB/en-us                         |
| 直布羅陀                                | GI                       | GIB                      | en-US                                 |
| 希臘                                   | GR                       | GRC                      | el-GR/en-us                         |
| 格陵蘭                                | 總帳                       | GRL                      | da-深/en-us                         |
| 格瑞那達                                  | GD                       | GRD                      | en-US                                 |
| 哥德普洛                               | GP                       | GLP                      | fr-FR/en-us                         |
| 關島                                     | GU                       | 黏                      | en-US                                 |
| 瓜地馬拉                                | GT                       | GTM                      | es-GT/en-us                         |
| 根息                                 | GG                       | GGY                      | en-US                                 |
| 幾內亞                                   | GN                       | GIN                      | fr-FR/en-us                         |
| 幾內亞比索                            | GW                       | GNB                      | pt-PT/en-us                         |
| 蓋亞納                                   | GY                       | 傢伙                      | en-US                                 |
| 海地                                    | HT                       | HTI                      | fr-FR/en-us                         |
| 赫德島及麥當勞群島        | HM                       | HMD                      | en-US                                 |
| 宏都拉斯                                 | HN                       | HND                      | es-HN/en-us                         |
| 香港特別行政區                            | HK                       | HKG                      | zh-HK/en-us                         |
| 匈牙利                                  | HU                       | HUN                      | hu-HU/en-us                         |
| 冰島                                  | IS                       | 交換器                      | is/en-us                         |
| 印度                                    | IN                       | IND                      | en-us/hi/en-us                 |
| 印尼                                | ID                       | IDN                      | 識別碼-識別碼/en-us                         |
| 伊拉克                                     | IQ                       | IRQ                      | ar-IQ/en-us                         |
| 愛爾蘭                                  | IE                       | IRL                      | en-IE/en-us                         |
| 曼城島                              | IM                       | IMN                      | en-US                                 |
| 以色列                                   | IL                       | ISR                      | 他-IL/en-us                         |
| 義大利                                    | IT                       | ITA                      | it-en-us                         |
| 牙買加                                  | JM                       | 卡住                      | en-us-JM/en-us                         |
| 尖棉                                | XJ                       | XJA                      | nb-否/en-us                         |
| Japan                                    | JP                       | JPN                      | ja-jp/en-us                         |
| 澤西島                                   | JE                       | JEY                      | en-US                                 |
| 約旦                                   | JO                       | JOR                      | ar-JO/en-us                         |
| 哈薩克                               | KZ                       | KAZ                      | kk-KZ/en-us                         |
| 肯亞                                    | KE                       | KEN                      | sw-KE/en-us                         |
| 吉里巴斯                                 | KI                       | KIR                      | en-US                                 |
| Korea                                    | KR                       | KOR                      | ko-KR/en-us                         |
| 科索沃                                   | XK                       | XKS                      | en-US                                 |
| 科威特                                   | KW                       | KWT                      | ar-KW/en-us                         |
| 吉爾吉斯                               | KG                       | KGZ                      | ky-公斤/en-us                         |
| 寮國                                     | LA                       | 寮文                      | lo-LA/en-us                         |
| 拉脫維亞                                   | LV                       | LVA                      | lv-LV/en-us                         |
| 黎巴嫩                                  | LB                       | LBN                      | ar-LB/en-us                         |
| 賴索托                                  | ！                       | 讓 LSO                      | en-US                                 |
| 賴比瑞亞                                  | LR                       | LBR                      | en-US                                 |
| 利比亞                                    | 去年年初                       | LBY                      | ar-去年年初/en-us                         |
| 列支敦斯登                            | L                       | 遮蔽                      | de-l i/en-us                         |
| 立陶宛                                | LT                       | LTU                      | lt-LT/en-us                         |
| 盧森堡                               | LU                       | LUX                      | de-LU/fr-LU/en-us                 |
| 澳門特別行政區                                | 每月                       | MAC                      | zh-每月/en-us                         |
| 馬其頓 (FYRO)                          | MK                       | MKD                      | mk-MK/en-us                         |
| 馬達加斯加                               | MG                       | MDG                      | fr-FR/en-us                         |
| 馬拉威                                   | MW                       | MWI                      | en-US                                 |
| 馬來西亞                                 | MY                       | MYS                      | en-MY/en-us                         |
| 馬爾地夫                                 | MV                       | MDV                      | dv-MV/en-us                         |
| 馬利                                     | 機器                       | MLI                      | fr-FR/en-us                         |
| 馬爾他                                    | MT                       | MLT                      | mt-MT/en-us                         |
| 馬紹爾群島                         | MH                       | MHL                      | en-US                                 |
| 馬丁尼克                               | MQ                       | MTQ                      | fr-FR/en-us                         |
| 茅利塔尼亞                               | MR                       | MRT.LOG                      | ar-SA/en-us                         |
| 模里西斯                                | MU                       | MUS                      | en-GB/en-us                         |
| 馬約特島                                  | YT                       | MYT                      | fr-FR/en-us                         |
| 墨西哥                                   | MX                       | MEX                      | es-MX/en-us                         |
| 密克羅尼西亞                               | 調頻廣播                       | FSM                      | en-US                                 |
| 摩爾多瓦                                  | MD                       | MDA                      | ro-RO/en-us                         |
| 摩納哥                                   | MC                       | MCO                      | fr-MC/en-us                         |
| 蒙古                                 | MN                       | MNG                      | mn-MN/en-us                         |
| 蒙特內哥羅                               | ME                       | MNE                      | Latn-ME/en-us                    |
| 蒙特色拉特島                               | MS                       | MSR                      | en-US                                 |
| 摩洛哥                                  | MA                       | 2003                      | ar-MA/en-us                         |
| 莫三比克                               | MZ                       | MOZ-APPEARANCE                      | pt-PT/en-us                         |
| 緬甸                                  | MM                       | MMR                      | en-US                                 |
| 納米比亞                                  | NA                       | 越南                      | en-GB/en-us                         |
| 諾魯                                    | NR                       | NRU                      | en-US                                 |
| 尼泊爾                                    | NP                       | NPL                      | ne-NP/en-us                         |
| 荷屬安替列斯                     | ，                       | ANT                      | en-US                                 |
| 荷蘭，                         | NL                       | NLD                      | nl-NL/en-us                         |
| 新喀里多尼亞群島                            | NC                       | NCL                      | fr-FR/en-us                         |
| 紐西蘭                              | NZ                       | NZL                      | en-NZ/en-us                         |
| 尼加拉瓜                                | NI                       | 網卡                      | es-NI/en-us                         |
| 尼日                                    | NE                       | NER                      | fr-FR/en-us                         |
| 奈及利亞                                  | NG                       | NGA                      | ha-Latn-NG/en-us                    |
| 紐威島                                     | NU                       | NIU                      | en-US                                 |
| 諾福克島                           | NF-E                       | NFK                      | en-US                                 |
| 北馬里安納群島                 | MP                       | MNP                      | en-US                                 |
| 挪威                                   | 否                       | NOR                      | nb-否/en-us                         |
| 阿曼                                     | OM                       | OMN                      | ar-OM/en-us                         |
| 巴基斯坦                                 | PK                       | PAK                      | 您的-PK/en-us                         |
| 帛琉                                    | PW                       | PLW                      | en-US                                 |
| 巴勒斯坦民族權力機構                    | PS                       | PSE                      | ar-SA/en-us                         |
| 巴拿馬                                   | PA                       | PAN                      | es-PA/en-us                         |
| 巴布亞紐幾內亞                         | PG                       | PNG                      | en-US                                 |
| 巴拉圭                                 | PY                       | 撬                      | es-.PY/en-us                         |
| 秘魯                                     | PE                       | 依據                      | es-PE/en-us                         |
| 菲律賓                              | PH                       | PHL                      | en-PH/en-us                         |
| 皮特康群島                         | PN                       | PCN                      | en-US                                 |
| 波蘭                                   | PL                       | POL                      | pl-PL/en-us                         |
| 葡萄牙                                 | PT                       | PRT                      | pt-PT/en-us                         |
| 波多黎各                              | PR                       | PRI                      | es-PR/en-us                         |
| 卡達                                    | QA                       | QAT                      | ar-QA/en-us                         |
| 留尼旺                                  | RE                       | REU                      | fr-FR/en-us                         |
| 羅馬尼亞                                  | RO                       | ROU                      | ro-RO/en-us                         |
| 俄羅斯                                   | RU                       | RUS                      | ru-RU/en-us                         |
| 盧安達                                   | CD-RW                       | RWA                      | rw-RW/en-us                         |
| 沙巴                                     | XS                       | XSA                      | nl-NL/en-us                         |
| 聖克里斯多福及尼維斯                    | KN                       | KNA                      | en-GB/en-us                         |
| 聖露西亞                              | 小寫                       | LCA                      | en-US                                 |
| 聖馬丁                             | MF                       | MAF                      | fr-FR/en-us                         |
| 聖匹島                | 下午                       | SPM                      | fr-FR/en-us                         |
| 聖文森及格瑞那丁         | VC                       | VCT                      | en-US                                 |
| 聖巴瑟米                         | BL                       | BLM                      | fr-FR/en-us                         |
| 薩摩亞獨立國                                    | WIN ENT LTSB 2016 Thai 64 Bits                       | WSM                      | en-US                                 |
| 聖馬利諾                               | 這些                       | SMR                      | it-en-us                         |
| 聖多美普林西比                    | ST                       | STP                      | pt-PT/en-us                         |
| 沙烏地阿拉伯                             | SA                       | SAU                      | ar-SA/en-us                         |
| 塞內加爾                                  | SN                       | SEN                      | wo-SN/en-us                         |
| 賽爾維亞                                   | RS                       | SRB                      | Latn-RS/sr-iov-Cyrl-RS/en-us       |
| 塞席爾                               | SC                       | SYC                      | en-US                                 |
| 獅子山                             | SL                       | SLE                      | en-US                                 |
| 新加坡                                | SG                       | SGP                      | en-SG/zh-SG/en-us                 |
| 聖佑達修斯                           | XE                       | XSE                      | nl-NL/en-us                         |
| 荷屬聖馬丁                             | X                       | SXM                      | en-US                                 |
| 斯洛伐克                                 | SK                       | SVK                      | sk-SK/en-us                         |
| 斯洛維尼亞                                 | SI                       | SVN                      | sl-SI/en-us                         |
| 索羅門群島                          | SB                       | SLB                      | en-US                                 |
| 索馬利亞                                  | 因此                       | SOM                      | ar-SA/en-us                         |
| 南非                             | ZA                       | ZAF                      | en-ZA/en-us                         |
| 南喬治亞與南三明治群島 | GS                       | SG                      | en-US                                 |
| 南蘇丹                              | SS                       | SSD                      | en-US                                 |
| 西班牙                                    | ES                       | ESP                      | es/ca-ES/eu-ES/gl-ES/en-us |
| 斯里蘭卡                                | LK                       | LKA                      | si-LK/en-us                         |
| 聖赫勒拿、阿森松、特里斯坦達庫尼亞群島   | SH                       | SHN                      | en-US                                 |
| 蘇利南                                 | SR                       | SUR                      | nl-NL                                 |
| 冷岸                                 | SJ                       | SJM                      | nb-否/en-us                         |
| 瑞典                                   | SE                       | SWE                      | sv-SE/en-us                         |
| 瑞士                              | CH                       | 快取處理                      | de-CH/fr-CH/it-CH/en-us         |
| 台灣                                   | TW                       | TWN                      | zh-幼圓/en-us                         |
| 塔吉克                               | TJ                       | TJK                      | tg-Cyrl-TJ/en-us                    |
| 坦尚尼亞                                 | TZ                       | TZA                      | en-GB/en-us                         |
| 泰國                                 | TH                       | THA                      | th/en-us                         |
| 東帝汶                              | TL                       | TLS                      | pt-PT/en-us                         |
| 多哥                                     | TG                       | TGO                      | fr-FR/en-us                         |
| 托克勞群島                                  | TK                       | TKL                      | en-US                                 |
| 東加                                    | 自                       | 許多                      | en-US                                 |
| 千里達及托巴哥                      | TT                       | 為了                      | en-us/en-us                         |
| 突尼西亞                                  | TN                       | 執行                      | ar-TN/en-us                         |
| 土耳其                                   | TR                       | TUR                      | tr-TR/en-us                         |
| 土庫曼                             | TM                       | TKM                      | tk-TM/en-us                         |
| 土克斯及開科斯群島                 | TC                       | TCA                      | en-US                                 |
| 吐瓦魯                                   | 電視                       | TUV                      | en-US                                 |
| 烏干達                                   | UG                       | UGA                      | en-GB/en-us                         |
| 烏克蘭                                  | UA                       | UKR                      | 英國-UA/en-us                         |
| 阿拉伯聯合大公國                     | AE                       | 確實                      | ar-AE/en-us                         |
| 英國                           | GB                       | GBR                      | en-GB/en-us                         |
| 美國外島                    | UM                       | UMI                      | en-US                                 |
| 美屬維爾京群島                      | VI                       | PR1-ASCS-VIR                      | en-US                                 |
| 美國                            | 美式英文                       | A                      | en-us/es-US                         |
| 烏拉圭                                  | UY                       | URY                      | es-UY/en-us                         |
| 烏茲別克                               | UZ                       | UZB                      | uz-Latn-UZ/en-us                    |
| 萬那杜                                  | VU                       | VUT                      | en-US                                 |
| 梵蒂岡                             | 再次                       | 加值稅                      | it-en-us                         |
| 委內瑞拉                                | VE                       | VEN                      | es-VE/en-us                         |
| 越南                                  | VN                       | VNM                      | vi-VN/en-us                         |
| 瓦利斯及福杜納                        | WF                       | WLF                      | fr-FR/en-us                         |
| 葉門                                    | YE                       | YEM                      | ar-YE/en-us                         |
| 尚比亞                                   | ZM                       | ZMB                      | en-GB/en-us                         |
| 辛巴威                                 | ZW                       | ZWE                      | en-us-ZW/en-us                         |

