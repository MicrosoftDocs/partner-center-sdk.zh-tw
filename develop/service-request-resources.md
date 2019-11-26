---
title: Service request resources
description: Partners can file service requests on behalf of their partners to report disruptions services provided by Microsoft or to request other technical support that they are incapable of providing.
ms.assetid: E9FBF7D8-A7E8-4DC6-B370-8339B9EE16B7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: e1fab576e69242a50549efc719f98eafad1ad9de
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488048"
---
# <a name="service-request-resources"></a>Service request resources


**Applies To**

- 合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Partners can file service requests on behalf of their partners to report disruptions services provided by Microsoft or to request other technical support that they are incapable of providing.

## <a name="span-idservicerequestspan-idservicerequestspan-idservicerequestservicerequest"></a><span id="ServiceRequest"/><span id="servicerequest"/><span id="SERVICEREQUEST"/>ServiceRequest


Describes a service request filed by a partner, including how that request is progressing.

| 屬性         | 在工作列搜尋方塊中輸入                                                          | 說明                                                                          |
|------------------|---------------------------------------------------------------|--------------------------------------------------------------------------------------|
| 標題            | 字串                                                        | The service request title.                                                           |
| 說明      | 字串                                                        | The description.                                                                     |
| 嚴重性         | 字串                                                        | The severity: "unknown", "critical", "moderate", or "minimal".                       |
| SupportTopicId   | 字串                                                        | The id of the support topic.                                                         |
| SupportTopicName | 字串                                                        | The name of the support topic.                                                       |
| Id               | 字串                                                        | The id of the service request.                                                       |
| 狀態           | 字串                                                        | The status of the service request: "none", "open", "closed", or "attention\_needed". |
| 組織     | [ServiceRequestOrganization](#servicerequestorganization)     | Organization for which the service request is created.                               |
| PrimaryContact   | [ServiceRequestContact](#servicerequestcontact)               | Primary Contact on the service request.                                              |
| LastUpdatedBy    | [ServiceRequestContact](#servicerequestcontact)               | "Last Updated By" contact for changes to the service request.                        |
| ProductName      | 字串                                                        | The name of the product that corresponds to the service request.                     |
| ProductId        | 字串                                                        | The id of the product.                                                               |
| CreatedDate      | date                                                          | The date of the service request's creation.                                          |
| LastModifiedDate | date                                                          | The date that the service request was last modified.                                 |
| LastClosedDate   | date                                                          | The date that the service request was last closed.                                   |
| FileLinks        | array of [FileInfo](utility-resources.md#fileinfo) resources | The collection of File Links that pertain to the service request.                    |
| NewNote          | [ServiceRequestNote](#servicerequestnote)                     | A note can be added to an existing service request.                                  |
| 備註            | array of [ServiceRequestNotes](#servicerequestnote)           | A collection of notes added to the service request.                                  |
| CountryCode      | 字串                                                        | The country corresponding to the service request.                                    |
| 屬性       | ResourceAttributes                                            | The metadata attributes corresponding to the service request.                        |

 

## <a name="span-idservicerequestcontactspan-idservicerequestcontactspan-idservicerequestcontactservicerequestcontact"></a><span id="ServiceRequestContact"/><span id="servicerequestcontact"/><span id="SERVICEREQUESTCONTACT"/>ServiceRequestContact


Describes a contact that creates or modifies a service request.

| 屬性     | 在工作列搜尋方塊中輸入                                                      | 說明                                            |
|--------------|-----------------------------------------------------------|--------------------------------------------------------|
| 組織 | [ServiceRequestOrganization](#servicerequestorganization) | Organization for which the service request is created. |
| ContactId    | 字串                                                    | The contact's unique id.                               |
| LastName     | 字串                                                    | The last name of the contact.                          |
| FirstName    | 字串                                                    | The first name of the contact.                         |
| 電子郵件        | 字串                                                    | The email of the contact.                              |
| PhoneNumber  | 字串                                                    | The phone number of the contact.                       |

 

## <a name="span-idservicerequestnotespan-idservicerequestnotespan-idservicerequestnoteservicerequestnote"></a><span id="ServiceRequestNote"/><span id="servicerequestnote"/><span id="SERVICEREQUESTNOTE"/>ServiceRequestNote


Describes a note attached to a service request.

| 屬性      | 在工作列搜尋方塊中輸入   | 說明                                  |
|---------------|--------|----------------------------------------------|
| CreatedByName | 字串 | The name of the creator of the note.         |
| CreatedDate   | date   | The date and time when the note was created. |
| 文字          | 字串 | The text of the note.                        |

 

## <a name="span-idservicerequestorganizationspan-idservicerequestorganizationspan-idservicerequestorganizationservicerequestorganization"></a><span id="ServiceRequestOrganization"/><span id="servicerequestorganization"/><span id="SERVICEREQUESTORGANIZATION"/>ServiceRequestOrganization


Describes the organization for which the service request is created.

| 屬性    | 在工作列搜尋方塊中輸入   | 說明                           |
|-------------|--------|---------------------------------------|
| Id          | 字串 | The unique id of the organization.    |
| 名稱        | 字串 | The name of the organization.         |
| PhoneNumber | 字串 | The phone number of the organization. |

 

## <a name="span-idsupporttopicspan-idsupporttopicspan-idsupporttopicsupporttopic"></a><span id="SupportTopic"/><span id="supporttopic"/><span id="SUPPORTTOPIC"/>SupportTopic


Describes a support topic. Service requests specify a support topic to ensure that they are processed quickly and effectively.

| 屬性    | 在工作列搜尋方塊中輸入               | 說明                                                   |
|-------------|--------------------|---------------------------------------------------------------|
| 名稱        | 字串             | The name of the support topic.                                |
| 說明 | 字串             | The description of the support topic.                         |
| Id          | 字串             | The unique id of the support topic.                           |
| 屬性  | ResourceAttributes | The metadata attributes corresponding to the service request. |

 

 

 




