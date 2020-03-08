---
title: 關聯性資源
description: 描述與關聯性相關的資源。
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b1d6d41256c081f3ef5ce7b27d89498839d8f5c8
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899965"
---
# <a name="relationships-resources"></a>關聯性資源


**適用于**

- 夥伴中心

描述與關聯性相關的資源。

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


表示兩個夥伴之間的關聯性。

| 屬性         | 類型                                                           | 描述                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | string                                                         | 合作夥伴識別碼。 合作夥伴識別碼會指定位於關聯性的收件者（from）端之夥伴的租使用者識別碼。 |
| 位置         | string                                                         | 夥伴的位置。                                                                                                                   |
| mpnId            | string                                                         | 夥伴的 Microsoft 合作夥伴網路（MPN）識別碼。                                                                                 |
| 名稱             | string                                                         | 夥伴的名稱。                                                                                                                       |
| relationshipType | string                                                         | 關聯性的類型。                                                                                                                      |
| State            | string                                                         | 關聯性的狀態（例如「作用中」）。                                                                                                 |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                                                                                       |

 

## <a name="span-idrelationshiprequestspan-idrelationshiprequestspan-idrelationshiprequestrelationshiprequest"></a><span id="RelationshipRequest"/><span id="relationshiprequest"/><span id="RELATIONSHIPREQUEST"/>RelationshipRequest


提供客戶可以用來與夥伴建立關聯性的 URL。

| 屬性   | 類型                                                           | 描述                   |
|------------|----------------------------------------------------------------|-------------------------------|
| URL        | string                                                         | 關聯性要求 URL。 |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。      |

 

 

 




