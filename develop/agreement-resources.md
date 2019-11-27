---
title: 合約資源
description: 合約資源代表 Microsoft 雲端客戶合約。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2cf620d63da14e014a17017006346f80a7a3fe4c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489258"
---
# <a name="agreement-resources"></a>合約資源

適用於：

- 合作夥伴中心

**合約**資源目前僅由 Microsoft 公用雲端中的合作夥伴中心支援。 不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**合約**資源代表 Microsoft 雲端客戶合約。

## <a name="agreement"></a>合約

**協定**資源代表合作夥伴提供之認證的詳細資料。

| 屬性       | 類型   | 描述                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | 字串                         | 合作夥伴租使用者中已登入使用者的物件識別碼，代表夥伴組織提供確認。 使用 [應用程式 + 使用者驗證] 建立合約資源時，合作夥伴中心會自動從應用程式 + 使用者權杖衍生**userId**屬性值。                                                                             |
| primaryContact | [連絡人](./utility-resources.md#contact) | 客戶組織中接受 Microsoft Cloud 合約之使用者的相關資訊，包括： **firstName**、 **lastName**、 **email**和**phoneNumber** （選擇性）。 |
| dateAgreed     | UTC 日期時間格式的字串 | 客戶接受合約的日期。                                 |
| templateId     |字串                          | 客戶接受之合約的唯一識別碼。 |
| type           |字串                          | 合約類型。 目前支援的值包括**MicrosoftCloudAgreement**和**MicrosoftCustomerAgreement**。|
| agreementLink  | 字串                         | 合約範本的 URL。                                                    |
