---
title: 合約中繼資料資源
description: AgreementMetadata 資源集合會描述合作夥伴可用來提供確認客戶接受的合約類型。
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 7ba318054d9df22023564fe3796833e49f87282e
ms.sourcegitcommit: 98ec47d226a0b56f329e55ba881e476e2afff971
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/07/2020
ms.locfileid: "78899648"
---
# <a name="agreement-metadata-resources"></a>合約中繼資料資源

適用於：

- 夥伴中心

合作夥伴中心目前僅支援在*Microsoft 公用雲端*中使用**AgreementMetaData**資源。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**AgreementMetaData**集合會提供有關所有合約類型的中繼資料。 合作夥伴可以使用此集合來確認客戶接受合約。 **AgreementMetaData**集合會針對這兩種合約類型（**Microsoft Cloud 合約**和**Microsoft 客戶合約**）傳回中繼資料。

## <a name="agreementmetadata"></a>AgreementMetaData

傳回的合約中繼資料包括下列各項：

| 屬性      | 類型               | 描述                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | 協定範本的唯一識別碼。                                       |
| 類型          | string             | 合約類型。 目前支援的值包括**MicrosoftCloudAgreement**和**MicrosoftCustomerAgreement** （預覽）。 |
| agreementLink | string             | 合約範本的 URL。                                                    |
