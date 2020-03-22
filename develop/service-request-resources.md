---
title: 服務要求資源
description: 合作夥伴可以代表他們的合作夥伴提出服務要求，以報告 Microsoft 所提供的中斷服務，或要求他們無法提供的其他技術支援。
ms.assetid: E9FBF7D8-A7E8-4DC6-B370-8339B9EE16B7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e1fab576e69242a50549efc719f98eafad1ad9de
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80082875"
---
# <a name="service-request-resources"></a>服務要求資源


**適用于**

- 夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴可以代表他們的合作夥伴提出服務要求，以報告 Microsoft 所提供的中斷服務，或要求他們無法提供的其他技術支援。

## <a name="span-idservicerequestspan-idservicerequestspan-idservicerequestservicerequest"></a><span id="ServiceRequest"/><span id="servicerequest"/><span id="SERVICEREQUEST"/>ServiceRequest


描述由合作夥伴記載的服務要求，包括該要求的進度。

| 屬性         | 類型                                                          | 描述                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 標題            | string                                                        | 服務要求標題。                                                           |
| 描述      | string                                                        | 描述。                                                                     |
| Severity         | string                                                        | 嚴重性：「不明」、「重大」、「適中」或「最小」。                       |
| SupportTopicId   | string                                                        | 支援主題的識別碼。                                                         |
| SupportTopicName | string                                                        | 支援主題的名稱。                                                       |
| Id               | string                                                        | 服務要求的識別碼。                                                       |
| 狀態           | string                                                        | 服務要求的狀態： [無]、[開啟]、[已關閉] 或 [\_需要注意]。 |
| 組織     | [ServiceRequestOrganization](#servicerequestorganization)     | 建立服務要求的組織。                               |
| primaryContact   | [ServiceRequestContact](#servicerequestcontact)               | 服務要求的主要連絡人。                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | 「上次更新者」連絡人，以瞭解服務要求的變更。                        |
| ProductName      | string                                                        | 對應至服務要求的產品名稱。                     |
| ProductId        | string                                                        | 產品的識別碼。                                                               |
| CreatedDate      | date                                                          | 服務要求建立的日期。                                          |
| lastModifiedDate | date                                                          | 上次修改服務要求的日期。                                 |
| LastClosedDate   | date                                                          | 上次關閉服務要求的日期。                                   |
| FileLinks        | [FileInfo](utility-resources.md#fileinfo)資源的陣列 | 與服務要求相關之檔案連結的集合。                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | 附注可以加入至現有的服務要求。                                  |
| 注意事項            | [ServiceRequestNotes](#servicerequestnote)的陣列           | 加入至服務要求的附注集合。                                  |
| CountryCode      | string                                                        | 對應至服務要求的國家/地區。                                    |
| 屬性       | ResourceAttributes                                            | 對應至服務要求的中繼資料屬性。                        |

 

## <a name="span-idservicerequestcontactspan-idservicerequestcontactspan-idservicerequestcontactservicerequestcontact"></a><span id="ServiceRequestContact"/><span id="servicerequestcontact"/><span id="SERVICEREQUESTCONTACT"/>ServiceRequestContact


描述建立或修改服務要求的連絡人。

| 屬性     | 類型                                                      | 描述                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| 組織 | [ServiceRequestOrganization](#servicerequestorganization) | 建立服務要求的組織。 |
| ContactId    | string                                                    | 連絡人的唯一識別碼。                               |
| LastName     | string                                                    | 連絡人的姓氏。                          |
| FirstName    | string                                                    | 連絡人的名字。                         |
| 電子郵件        | string                                                    | 連絡人的電子郵件。                              |
| PhoneNumber  | string                                                    | 連絡人的電話號碼。                       |

 

## <a name="span-idservicerequestnotespan-idservicerequestnotespan-idservicerequestnoteservicerequestnote"></a><span id="ServiceRequestNote"/><span id="servicerequestnote"/><span id="SERVICEREQUESTNOTE"/>ServiceRequestNote


描述附加至服務要求的附注。

| 屬性      | 類型   | 描述                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | string | 便箋的建立者名稱。         |
| CreatedDate   | date   | 建立便箋的日期和時間。 |
| Text          | string | 便箋的文字。                        |

 

## <a name="span-idservicerequestorganizationspan-idservicerequestorganizationspan-idservicerequestorganizationservicerequestorganization"></a><span id="ServiceRequestOrganization"/><span id="servicerequestorganization"/><span id="SERVICEREQUESTORGANIZATION"/>ServiceRequestOrganization


描述建立服務要求的組織。

| 屬性    | 類型   | 描述                           |
|-------------|--------|---------------------------------------|
| Id          | string | 組織的唯一識別碼。    |
| 名稱        | string | 組織的名稱。         |
| PhoneNumber | string | 組織的電話號碼。 |

 

## <a name="span-idsupporttopicspan-idsupporttopicspan-idsupporttopicsupporttopic"></a><span id="SupportTopic"/><span id="supporttopic"/><span id="SUPPORTTOPIC"/>SupportTopic


描述支援主題。 服務要求會指定支援主題，以確保能快速且有效地處理它們。

| 屬性    | 類型               | 描述                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| 名稱        | string             | 支援主題的名稱。                                |
| 描述 | string             | 支援主題的描述。                         |
| Id          | string             | 支援主題的唯一識別碼。                           |
| 屬性  | ResourceAttributes | 對應至服務要求的中繼資料屬性。 |

 

 

 




