---
title: 公用程式資源
description: 合作夥伴中心 REST API 包含許多資源，其中說明整個 SDK 中使用的一般用途資料模型。
ms.assetid: C77219B9-FFDD-4779-AE15-5B15BA7BA863
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b19eb80c5be2cc07bd325681f9870a1af7fed481
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083075"
---
# <a name="utility-resources"></a>公用程式資源


**適用于**

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 REST API 包含許多資源，其中說明整個 SDK 中使用的一般用途資料模型。


## <a name="span-idaddressspan-idaddressaddress"></a><span id="address"/><span id="ADDRESS"/>位址

要用於客戶或夥伴設定檔的位址。 如需不同國家/地區中支援的格式和屬性的詳細資訊，請參閱[依市場取得位址格式規則](get-market-specific-validation-data.md)。

| 屬性     | 類型   | 長度（最小值、最大值） | 描述                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | （1，200）          | 第一行地址。                                                                   |
| AddressLine2 | string | （0，200）          | 第二行地址。 這個屬性為選擇性。                                       |
| 城市         | string | n/a               | 所在城市。                                                                                        |
| 狀態        | string | （0，2）            | 狀態。                                                                                       |
| PostalCode   | string | n/a               | 郵遞區號或郵遞區號。                                                                     |
| Country      | string | （2，2）            | ISO 國家（地區）代碼格式的國家/地區。                                                   |
| 地區       | string | n/a               | 所在區域。                                                                                      |
| FirstName    | string | （1，50）           | 客戶公司/組織的連絡人名字。                              |
| LastName     | string | （1，50）           | 客戶公司/組織中連絡人的姓氏。                               |
| PhoneNumber  | string | n/a               | 客戶公司/組織中連絡人的電話號碼。 這個屬性為選擇性。 |
 

## <a name="span-idcontactspan-idcontactspan-idcontactcontact"></a><span id="Contact"/><span id="contact"/><span id="CONTACT"/>連絡人

說明特定個人的連絡資訊。

| 屬性    | 類型   | 描述                  |
|-------------|--------|------------------------------|
| FirstName   | string | 連絡人的名字。    |
| LastName    | string | 連絡人的姓氏。     |
| 電子郵件       | string | 連絡人的電子郵件地址。 |
| PhoneNumber | string | 連絡人的電話號碼。  |
 

## <a name="span-idfieldfilterspan-idfieldfilterspan-idfieldfilterfieldfilter"></a><span id="FieldFilter"/><span id="fieldfilter"/><span id="FIELDFILTER"/>FieldFilter

描述可套用至搜尋結果的篩選準則。

| 屬性 | 類型   | 描述                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 運算子 | string | 篩選運算子：「等於」、「不\_equals」、「大於\_大於」、「\_大於\_或\_等於」、「小於\_」、「少於\_或\_等於」、「不\_」、「小於」、「」、「不\_」開始\_為「」。\_ |
 

## <a name="span-idfileinfospan-idfileinfospan-idfileinfofileinfo"></a><span id="FileInfo"/><span id="fileinfo"/><span id="FILEINFO"/>FileInfo

表示上傳至合作夥伴中心的外部檔案。

| 屬性                 | 類型   | 描述                                   |
|--------------------------|--------|-----------------------------------------------|
| 註解                  | string | 與檔案上傳相關聯的批註。    |
| FileExtension            | string | 副檔名。                           |
| FileNameWithoutExtension | string | 檔案的名稱，不包含副檔名。 |
| FileSize                 | long   | 檔案的大小。                         |
| Id                       | string | 檔案上傳的唯一識別碼。            |
 

## <a name="span-idlinkspan-idlinkspan-idlinklink"></a><span id="Link"/><span id="link"/><span id="LINK"/>連結

包含 URI 連結和相關聯的資訊。

| 屬性 | 類型                   | 描述                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | URI。                           |
| 方法   | string                 | URI 所表示的方法。 |
| 標頭  | KeyValuePairs 的陣列 | 連結的標頭。          |
 

## <a name="span-idpasswordprofilespan-idpasswordprofilespan-idpasswordprofilepasswordprofile"></a><span id="PasswordProfile"/><span id="passwordprofile"/><span id="PASSWORDPROFILE"/>PasswordProfile

描述特定的密碼，以及是否需要變更該密碼。

>[!NOTE]
>由世紀營運的合作夥伴中心不支援。

| 屬性            | 類型                          | 描述                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Password            | [SecureString](#securestring) | 密碼。                                                          |
| ForceChangePassword | boolean                       | 決定是否需要在下次登入時強制變更密碼。 |
 

## <a name="span-idresourcelinksspan-idresourcelinksspan-idresourcelinksresourcelinks"></a><span id="ResourceLinks"/><span id="resourcelinks"/><span id="RESOURCELINKS"/>ResourceLinks

包含資源的連結清單。

| 屬性   | 類型                                      | 描述                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Self       | [連結](#link)                             | 自我 URI。                                      |
| 下一步       | [連結](#link)                             | 下一個頁面的專案。                            |
| 上一步   | [連結](#link)                             | 前一頁的專案。                        |
| 屬性 | [ResourceAttributes](#resourceattributes) | 對應至使用者的中繼資料屬性。 |
 

## <a name="span-idresourceattributesspan-idresourceattributesspan-idresourceattributesresourceattributes"></a><span id="ResourceAttributes"/><span id="resourceattributes"/><span id="RESOURCEATTRIBUTES"/>ResourceAttributes

包含資源的屬性中繼資料。

| 屬性   | 類型   | 描述                                 |
|------------|--------|---------------------------------------------|
| Etag       | string | Etag，又稱為物件版本。 |
| ObjectType | string | 基底資源的物件類型。    |
 

## <a name="span-idsecurestringspan-idsecurestringspan-idsecurestringsecurestring"></a><span id="SecureString"/><span id="securestring"/><span id="SECURESTRING"/>SecureString

儲存安全的資訊，例如密碼。

| 屬性 | 類型 | 描述                       |
|----------|------|-----------------------------------|
| Length   | int  | 受保護字串的長度。 |


## <a name="span-idvalidationcodespan-idvalidationcodespan-idvalidationcodevalidationcode"></a><span id="ValidationCode"/><span id="validationcode"/><span id="VALIDATIONCODE"/>ValidationCode

代表合作夥伴的政府團體雲端驗證碼。

| 屬性         | 類型         | 描述                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| PartnerId        | GUID         | 合作夥伴識別碼                                                       |
| 組織名稱 | string       | 在驗證過程中提供的組織名稱             |
| ValidationId     | int          | 驗證的唯一識別碼                                       |
| MaxCreates       | 可為 null 的 int | 允許使用此驗證碼建立的最大客戶數    |
| RemainingCreates | 可為 null 的 int | 其餘客戶會在此驗證識別碼下建立                      |
| ETag             | string       | 此資源的特定版本。 變更資源時的變更。 |
