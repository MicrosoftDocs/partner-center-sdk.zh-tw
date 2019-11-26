---
title: Country information resources
description: Descriptive metadata for a country/region.
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
# <a name="country-information-resources"></a>Country information resources

適用於：

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The following resources are descriptive metadata for a country/region.

## <a name="countryinformation"></a>CountryInformation

| 屬性                      | 在工作列搜尋方塊中輸入               | 說明                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | 字串             | The extension data.                                                                                |
| Iso2Code                      | 字串             | An ISO-2 code.                                                                                     |
| Iso3Code                      | 字串             | An ISO-3 code.                                                                                     |
| DefaultCulture                | 字串             | The default culture.                                                                               |
| IsStateRequired               | boolean            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList           | array of strings   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList        | array of strings   | A list of supported languages.                                                                     |
| SupportedCulturesList         | array of strings   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired          | boolean            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex               | 字串             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired                | boolean            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported              | boolean            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat                   | 字串             | The tax ID format.                                                                                 |
| TaxIdSample                   | 字串             | The tax ID sample.                                                                                 |
| VatIdRegex                    | 字串             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex              | 字串             | The phone number regular expression.                                                               |
| IsRegistrationNumberSupported | boolean            | Indicates whether a registration number is supported or not.                                       |
| IsTaxIdSupported              | boolean            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| ResellerAgreementRegion       | 字串             | The reseller agreement region.                                                                     |
| GeographicRegion              | 字串             | The geographic region.                                                                             |
| CountryCallingCodesList       | array of strings   | The calling codes supported in the country/region.                                                 |
| 屬性                    | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Describes the address formatting rules for a country/region.

| 屬性                | 在工作列搜尋方塊中輸入               | 說明                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | 字串             | An ISO-2 code.                                                                                     |
| DefaultCulture          | 字串             | The default culture.                                                                               |
| IsStateRequired         | boolean            | Indicates whether a state/province is required or not.                                             |
| SupportedStatesList     | array of strings   | If a state/province is required, returns the full list for that country/region.                    |
| SupportedLanguagesList  | array of strings   | A list of supported languages.                                                                     |
| SupportedCulturesList   | array of strings   | A list of supported cultures.                                                                      |
| IsPostalCodeRequired    | boolean            | Indicates whether a ZIP code or postal code is required or not.                                    |
| PostalCodeRegex         | 字串             | The regular expression that defines the ZIP/postal code .                                          |
| IsCityRequired          | boolean            | Indicates whether a city is required or not.                                                       |
| IsVatIdSupported        | boolean            | Indicates whether a VAT ID is required or not.                                                     |
| TaxIdFormat             | 字串             | The tax ID format.                                                                                 |
| TaxIdSample             | 字串             | The tax ID sample.                                                                                 |
| VatIdRegex              | 字串             | The tax ID regular expression.                                                                     |
| PhoneNumberRegex        | 字串             | The phone number regular expression.                                                               |
| IsTaxIdSupported        | boolean            | Indicates whether a tax ID is supported or not. Note that this is different than IsVatIdSupported. |
| IsTaxIdOptional         | boolean            | Indicates whether a tax ID is optional or not.                                                     |
| CountryCallingCodesList | array of strings   | The calling codes supported in the country/region.                                                 |
| 屬性              | ResourceAttributes | The metadata attributes corresponding to the CountryInformation resource.                          |