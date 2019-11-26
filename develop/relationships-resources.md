---
title: Relationships resources
description: Describes resources related to relationships.
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b1d6d41256c081f3ef5ce7b27d89498839d8f5c8
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488098"
---
# <a name="relationships-resources"></a>Relationships resources


**Applies To**

- 合作夥伴中心

Describes resources related to relationships.

## <a name="span-idpartnerrelationshipspan-idpartnerrelationshipspan-idpartnerrelationshippartnerrelationship"></a><span id="PartnerRelationship"/><span id="partnerrelationship"/><span id="PARTNERRELATIONSHIP"/>PartnerRelationship


Represents a relationship between two partners.

| 屬性         | 在工作列搜尋方塊中輸入                                                           | 說明                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | 字串                                                         | The partner identifier. The partner identifier specifies the tenant id of the partner who is in the recipient (from) side of the relationship. |
| location         | 字串                                                         | The location of the partner.                                                                                                                   |
| mpnId            | 字串                                                         | The Microsoft Partner Network (MPN) identifier of the partner.                                                                                 |
| name             | 字串                                                         | The name of the partner.                                                                                                                       |
| relationshipType | 字串                                                         | The type of relationship.                                                                                                                      |
| state            | 字串                                                         | The state of the relationship (e.g. "active").                                                                                                 |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.                                                                                                                       |

 

## <a name="span-idrelationshiprequestspan-idrelationshiprequestspan-idrelationshiprequestrelationshiprequest"></a><span id="RelationshipRequest"/><span id="relationshiprequest"/><span id="RELATIONSHIPREQUEST"/>RelationshipRequest


Provides the URL by which a customer can establish a relationship with a partner.

| 屬性   | 在工作列搜尋方塊中輸入                                                           | 說明                   |
|------------|----------------------------------------------------------------|-------------------------------|
| URL        | 字串                                                         | The relationship request URL. |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | The metadata attributes.      |

 

 

 




