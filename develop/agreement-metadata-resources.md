---
title: 合約中繼資料資源
description: AgreementMetadata 資源集合會描述合作夥伴可用來提供確認客戶接受的合約類型。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094589"
---
# <a name="agreement-metadata-resources"></a>合約中繼資料資源

**適用於：**

- 合作夥伴中心

合作夥伴中心目前僅支援在*Microsoft 公用雲端*中使用**AgreementMetaData**資源。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**AgreementMetaData**集合會提供有關所有合約類型的中繼資料。 合作夥伴可以使用此集合來確認客戶接受合約。 **AgreementMetaData**集合會針對這兩種合約類型（**Microsoft Cloud 合約**和**Microsoft 客戶合約**）傳回中繼資料。

## <a name="agreementmetadata"></a>AgreementMetaData

傳回的合約中繼資料包括下列屬性：

| 屬性      | 類型               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | 字串             | 協定範本的唯一識別碼。                                       |
| type          | 字串             | 合約類型。 目前支援的值包括**MicrosoftCloudAgreement**和**MicrosoftCustomerAgreement** （預覽）。 |
| agreementLink | 字串             | 合約範本的 URL。                                                    |
