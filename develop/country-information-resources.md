---
title: 國家/地區資訊資源
description: 國家/地區的描述性中繼資料。
ms.assetid: 19460437-5611-49A1-A7E7-704420C1DE8F
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1675db6dcb09301f86436bb0b9c8dbb785fcde17
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413544"
---
# <a name="country-information-resources"></a>國家/地區資訊資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

下列資源是國家/地區的描述性中繼資料。

## <a name="countryinformation"></a>CountryInformation

| 屬性                      | 類型               | 描述                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | 延伸模組資料。                                                                                |
| Iso2Code                      | string             | ISO-2 代碼。                                                                                     |
| Iso3Code                      | string             | ISO-3 代碼。                                                                                     |
| DefaultCulture                | string             | 預設的文化特性。                                                                               |
| IsStateRequired               | 布林值            | 指出是否需要州/省。                                             |
| SupportedStatesList           | 字串的陣列   | 如果需要州/省，則會傳回該國家/地區的完整清單。                    |
| SupportedLanguagesList        | 字串的陣列   | 支援的語言清單。                                                                     |
| SupportedCulturesList         | 字串的陣列   | 支援的文化特性清單。                                                                      |
| IsPostalCodeRequired          | 布林值            | 指出郵遞區號是否為必要。                                    |
| PostalCodeRegex               | string             | 定義郵遞區號的正則運算式。                                          |
| IsCityRequired                | 布林值            | 指出是否需要城市。                                                       |
| IsVatIdSupported              | 布林值            | 指出是否需要 加值稅 識別碼。                                                     |
| TaxIdFormat                   | string             | 稅務識別碼格式。                                                                                 |
| TaxIdSample                   | string             | 稅務識別碼範例。                                                                                 |
| VatIdRegex                    | string             | 稅務識別碼正則運算式。                                                                     |
| PhoneNumberRegex              | string             | 電話號碼正則運算式。                                                               |
| IsRegistrationNumberSupported | 布林值            | 指出是否支援註冊編號。                                       |
| IsTaxIdSupported              | 布林值            | 指出是否支援稅務識別碼。 請注意，這與 IsVatIdSupported 不同。 |
| ResellerAgreementRegion       | string             | 轉售商合約區域。                                                                     |
| GeographicRegion              | string             | 地理區域。                                                                             |
| CountryCallingCodesList       | 字串的陣列   | 國家/地區支援的呼叫碼。                                                 |
| 屬性                    | ResourceAttributes | 對應至 CountryInformation 資源的中繼資料屬性。                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

說明國家/地區的位址格式規則。

| 屬性                | 類型               | 描述                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | ISO-2 代碼。                                                                                     |
| DefaultCulture          | string             | 預設的文化特性。                                                                               |
| IsStateRequired         | 布林值            | 指出是否需要州/省。                                             |
| SupportedStatesList     | 字串的陣列   | 如果需要州/省，則會傳回該國家/地區的完整清單。                    |
| SupportedLanguagesList  | 字串的陣列   | 支援的語言清單。                                                                     |
| SupportedCulturesList   | 字串的陣列   | 支援的文化特性清單。                                                                      |
| IsPostalCodeRequired    | 布林值            | 指出郵遞區號是否為必要。                                    |
| PostalCodeRegex         | string             | 定義郵遞區號的正則運算式。                                          |
| IsCityRequired          | 布林值            | 指出是否需要城市。                                                       |
| IsVatIdSupported        | 布林值            | 指出是否需要 加值稅 識別碼。                                                     |
| TaxIdFormat             | string             | 稅務識別碼格式。                                                                                 |
| TaxIdSample             | string             | 稅務識別碼範例。                                                                                 |
| VatIdRegex              | string             | 稅務識別碼正則運算式。                                                                     |
| PhoneNumberRegex        | string             | 電話號碼正則運算式。                                                               |
| IsTaxIdSupported        | 布林值            | 指出是否支援稅務識別碼。 請注意，這與 IsVatIdSupported 不同。 |
| IsTaxIdOptional         | 布林值            | 指出是否為選擇性的稅務識別碼。                                                     |
| CountryCallingCodesList | 字串的陣列   | 國家/地區支援的呼叫碼。                                                 |
| 屬性              | ResourceAttributes | 對應至 CountryInformation 資源的中繼資料屬性。                          |