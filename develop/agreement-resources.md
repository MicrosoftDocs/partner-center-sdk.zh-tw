---
title: 合約資源
description: 合約資源代表 Microsoft 雲端客戶合約。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e59debb59700f7d2d4f0eba9dc156c325b3688d
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022665"
---
# <a name="agreement-resources"></a>合約資源

**適用於：**

- 合作夥伴中心

**合約**資源目前僅由 Microsoft 公用雲端中的合作夥伴中心支援。 不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**合約**資源代表 Microsoft 雲端客戶合約。

## <a name="agreement"></a>合約

**協定**資源代表合作夥伴提供之認證的詳細資料。

| 屬性       | 類型   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | 字串                         | 合作夥伴租使用者中已登入使用者的物件識別碼，代表夥伴組織提供確認。 使用 [應用程式 + 使用者驗證] 建立合約資源時，合作夥伴中心會自動從應用程式 + 使用者權杖衍生**userId**屬性值。                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | 來自已接受合約之客戶組織使用者的相關資訊，包括： **firstName**、 **lastName**、 **email**和**phoneNumber** （選擇性）。 |
| dateAgreed     | UTC 日期時間格式的字串 | 客戶接受合約的日期。                                 |
| templateId     |字串                          | 客戶接受之合約的唯一識別碼。 |
| type           |字串                          | 合約類型。 目前支援的值包括**MicrosoftCloudAgreement**和**MicrosoftCustomerAgreement**。|
| agreementLink  | 字串                         | 合約範本的 URL。                                                    |
