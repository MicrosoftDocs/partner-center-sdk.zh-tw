---
title: 國家/地區資訊資源
description: 國家/地區的描述性中繼資料。
ms.assetid: 19460437-5611-49A1-A7E7-704420C1DE8F
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 321e05ff2f65746ae2e555bf35b4aa8d298c20af
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488808"
---
# <a name="country-information-resources"></a>國家/地區資訊資源

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

下列資源是國家/地區的描述性中繼資料。

## <a name="countryinformation"></a>CountryInformation

| 屬性                      | 類型               | 描述                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | 字串             | 延伸模組資料。                                                                                |
| Iso2Code                      | 字串             | ISO-2 代碼。                                                                                     |
| Iso3Code                      | 字串             | ISO-3 代碼。                                                                                     |
| DefaultCulture                | 字串             | 預設的文化特性。                                                                               |
| IsStateRequired               | 布林值            | 指出是否需要州/省。                                             |
| SupportedStatesList           | 字串陣列   | 如果需要州/省，則會傳回該國家/地區的完整清單。                    |
| SupportedLanguagesList        | 字串陣列   | 支援的語言清單。                                                                     |
| SupportedCulturesList         | 字串陣列   | 支援的文化特性清單。                                                                      |
| IsPostalCodeRequired          | 布林值            | 指出郵遞區號是否為必要。                                    |
| PostalCodeRegex               | 字串             | 定義郵遞區號的正則運算式。                                          |
| IsCityRequired                | 布林值            | 指出是否需要城市。                                                       |
| IsVatIdSupported              | 布林值            | 指出是否需要 加值稅 識別碼。                                                     |
| TaxIdFormat                   | 字串             | 稅務識別碼格式。                                                                                 |
| TaxIdSample                   | 字串             | 稅務識別碼範例。                                                                                 |
| VatIdRegex                    | 字串             | 稅務識別碼正則運算式。                                                                     |
| PhoneNumberRegex              | 字串             | 電話號碼正則運算式。                                                               |
| IsRegistrationNumberSupported | 布林值            | 指出是否支援註冊編號。                                       |
| IsTaxIdSupported              | 布林值            | 指出是否支援稅務識別碼。 請注意，這與 IsVatIdSupported 不同。 |
| ResellerAgreementRegion       | 字串             | 轉售商合約區域。                                                                     |
| GeographicRegion              | 字串             | 地理區域。                                                                             |
| CountryCallingCodesList       | 字串陣列   | 國家/地區支援的呼叫碼。                                                 |
| 屬性                    | ResourceAttributes | 對應至 CountryInformation 資源的中繼資料屬性。                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

說明國家/地區的位址格式規則。

| 屬性                | 類型               | 描述                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | 字串             | ISO-2 代碼。                                                                                     |
| DefaultCulture          | 字串             | 預設的文化特性。                                                                               |
| IsStateRequired         | 布林值            | 指出是否需要州/省。                                             |
| SupportedStatesList     | 字串陣列   | 如果需要州/省，則會傳回該國家/地區的完整清單。                    |
| SupportedLanguagesList  | 字串陣列   | 支援的語言清單。                                                                     |
| SupportedCulturesList   | 字串陣列   | 支援的文化特性清單。                                                                      |
| IsPostalCodeRequired    | 布林值            | 指出郵遞區號是否為必要。                                    |
| PostalCodeRegex         | 字串             | 定義郵遞區號的正則運算式。                                          |
| IsCityRequired          | 布林值            | 指出是否需要城市。                                                       |
| IsVatIdSupported        | 布林值            | 指出是否需要 加值稅 識別碼。                                                     |
| TaxIdFormat             | 字串             | 稅務識別碼格式。                                                                                 |
| TaxIdSample             | 字串             | 稅務識別碼範例。                                                                                 |
| VatIdRegex              | 字串             | 稅務識別碼正則運算式。                                                                     |
| PhoneNumberRegex        | 字串             | 電話號碼正則運算式。                                                               |
| IsTaxIdSupported        | 布林值            | 指出是否支援稅務識別碼。 請注意，這與 IsVatIdSupported 不同。 |
| IsTaxIdOptional         | 布林值            | 指出是否為選擇性的稅務識別碼。                                                     |
| CountryCallingCodesList | 字串陣列   | 國家/地區支援的呼叫碼。                                                 |
| 屬性              | ResourceAttributes | 對應至 CountryInformation 資源的中繼資料屬性。                          |