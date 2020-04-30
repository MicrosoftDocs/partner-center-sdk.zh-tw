---
title: 關聯性資源
description: 描述與關聯性相關的資源。
ms.assetid: F6157FE3-7C9D-4A8F-AC11-6F4007594C3D
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 3e444653a8b5acd5dafbebe8e4526c50e7951155
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124437"
---
# <a name="relationships-resources"></a>關聯性資源

**適用于**

- 合作夥伴中心

描述與關聯性相關的資源。

## <a name="partnerrelationship"></a>PartnerRelationship

表示兩個夥伴之間的關聯性。

| 屬性         | 類型                                                           | 描述                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| id               | 字串                                                         | 合作夥伴識別碼。 合作夥伴識別碼會指定位於關聯性的收件者（from）端之夥伴的租使用者識別碼。 |
| location         | 字串                                                         | 夥伴的位置。                                                                                                                   |
| mpnId            | 字串                                                         | 夥伴的 Microsoft 合作夥伴網路（MPN）識別碼。                                                                                 |
| NAME             | 字串                                                         | 夥伴的名稱。                                                                                                                       |
| relationshipType | 字串                                                         | 關聯性的類型。                                                                                                                      |
| State            | 字串                                                         | 關聯性的狀態（例如`active`）。                                                                                                 |
| 屬性       | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

提供客戶可以用來與夥伴建立關聯性的 URL。

| 屬性   | 類型                                                           | 描述                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | 字串                                                         | 關聯性要求 URL。 |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。      |
