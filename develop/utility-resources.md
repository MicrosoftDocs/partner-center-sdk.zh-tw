---
title: Utility resources
description: The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b19eb80c5be2cc07bd325681f9870a1af7fed481
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486248"
---
# <a name="utility-resources"></a>Utility resources


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The Partner Center REST API contains many resources which describe general-purpose data models used throughout the SDK.


## <a name="span-idaddressspan-idaddressaddress"></a><span id="address"/><span id="ADDRESS"/>Address

An address to use for the customer or for partner profiles. For more information about the supported formats and properties in different countries/regions, see [Get address formatting rules by market](get-market-specific-validation-data.md).

| 屬性     | 在工作列搜尋方塊中輸入   | Length (min, max) | 說明                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| 地址行 1 | 字串 | (1, 200)          | The first line of the address.                                                                   |
| 地址行 2 | 字串 | (0, 200)          | The second line of the address. 這個屬性為選擇性。                                       |
| 縣市         | 字串 | 不適用               | The city.                                                                                        |
| 州/省        | 字串 | (0, 2)            | The state.                                                                                       |
| 郵遞區號   | 字串 | 不適用               | The ZIP code or postal code.                                                                     |
| 國家/地區      | 字串 | (2, 2)            | The country/region in ISO country code format.                                                   |
| 地區       | 字串 | 不適用               | The region.                                                                                      |
| FirstName    | 字串 | (1, 50)           | The first name of a contact at the customer's company/organization.                              |
| LastName     | 字串 | (1, 50)           | The last name of a contact at the customer's company/organization.                               |
| PhoneNumber  | 字串 | 不適用               | The phone number of a contact at the customer's company/organization. 這個屬性為選擇性。 |
 

## <a name="span-idcontactspan-idcontactspan-idcontactcontact"></a><span id="Contact"/><span id="contact"/><span id="CONTACT"/>Contact

Describes contact information for a specific individual.

| 屬性    | 在工作列搜尋方塊中輸入   | 說明                  |
|-------------|--------|------------------------------|
| FirstName   | 字串 | The contact's first name.    |
| LastName    | 字串 | The contact's last name.     |
| 電子郵件       | 字串 | The contact's email address. |
| PhoneNumber | 字串 | The contact's phone number.  |
 

## <a name="span-idfieldfilterspan-idfieldfilterspan-idfieldfilterfieldfilter"></a><span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

Describes a filter that can be applied to search results.

| 屬性 | 在工作列搜尋方塊中輸入   | 說明                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 運算子 | 字串 | The filter operator: "equals", "not\_equals", "greater\_than", "greater\_than\_or\_equals", "less\_than", "less\_than\_or\_equals", "substring", "and", "or", "starts\_with", "not\_starts\_with". |
 

## <a name="span-idfileinfospan-idfileinfospan-idfileinfofileinfo"></a><span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

Represents an external file uploaded to Partner Center.

| 屬性                 | 在工作列搜尋方塊中輸入   | 說明                                   |
|--------------------------|--------|-----------------------------------------------|
| 留言                  | 字串 | A comment associated with the file upload.    |
| FileExtension            | 字串 | The file extension.                           |
| FileNameWithoutExtension | 字串 | The name of the file, extension not included. |
| FileSize                 | 長整數   | The size of the file.                         |
| Id                       | 字串 | The unique ID for the file upload.            |
 

## <a name="span-idlinkspan-idlinkspan-idlinklink"></a><span id="Link"/><span id="link"/><span id="LINK"/>Link

Contains a URI link and associated information.

| 屬性 | 在工作列搜尋方塊中輸入                   | 說明                        |
|----------|------------------------|------------------------------------|
| URI      | 字串                 | The URI.                           |
| 方法   | 字串                 | The method represented by the URI. |
| 標頭  | Array of KeyValuePairs | The headers for the link.          |
 

## <a name="span-idpasswordprofilespan-idpasswordprofilespan-idpasswordprofilepasswordprofile"></a><span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

Describes a specific password and if that password needs to be changed.

>[!NOTE]
>Unsupported on Partner Center operated by 21Vianet.

| 屬性            | 在工作列搜尋方塊中輸入                          | 說明                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| 密碼            | [SecureString](#securestring) | The password.                                                          |
| ForceChangePassword | boolean                       | Determines if the password needs to be forcibly changed on next login. |
 

## <a name="span-idresourcelinksspan-idresourcelinksspan-idresourcelinksresourcelinks"></a><span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

Contains a list of links for a resource.

| 屬性   | 在工作列搜尋方塊中輸入                                      | 說明                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [連結](#link)                             | The self URI.                                      |
| [下一步]       | [連結](#link)                             | The next page of items.                            |
| 上一則   | [連結](#link)                             | The previous page of items.                        |
| 屬性 | [ResourceAttributes](#resourceattributes) | The metadata attributes corresponding to the user. |
 

## <a name="span-idresourceattributesspan-idresourceattributesspan-idresourceattributesresourceattributes"></a><span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

Contains attribute metadata for a resource.

| 屬性   | 在工作列搜尋方塊中輸入   | 說明                                 |
|------------|--------|---------------------------------------------|
| Etag       | 字串 | The etag, also known as the object version. |
| ObjectType | 字串 | The type of object of the base resource.    |
 

## <a name="span-idsecurestringspan-idsecurestringspan-idsecurestringsecurestring"></a><span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

Stores secured information, such as a password.

| 屬性 | 在工作列搜尋方塊中輸入 | 說明                       |
|----------|------|-----------------------------------|
| 長度   | 整數  | The length of the secured string. |


## <a name="span-idvalidationcodespan-idvalidationcodespan-idvalidationcodevalidationcode"></a><span id="ValidationCode"/><span id="validationcode"/><span id="VALIDATIONCODE"/>ValidationCode

Represents a partner's Government Community Cloud validation code.

| 屬性         | 在工作列搜尋方塊中輸入         | 說明                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | Partner identifier                                                       |
| 組織名稱 | 字串       | The organization name provided during the validation process             |
| ValidationId     | 整數          | A unique identifier for validation                                       |
| MaxCreates       | nullable int | The maximum customers allowed to be created with this validation code    |
| RemainingCreates | nullable int | Remaining customer creates under this validation ID                      |
| ETag             | 字串       | The specific version of this resource. Changes when resource is changed. |
