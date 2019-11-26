---
title: 合約中繼資料資源
description: AgreementMetadata 資源集合會描述合作夥伴可用來提供確認客戶接受的合約類型。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b147b44d4f4c1d986f7e3290c71ddbf0af54de70
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488708"
---
# <a name="agreement-metadata-resources"></a>合約中繼資料資源

適用於：

- 合作夥伴中心

合作夥伴中心目前僅支援在*Microsoft 公用雲端*中使用**AgreementMetaData**資源。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**AgreementMetaData**集合會提供有關所有合約類型的中繼資料。 合作夥伴可以使用此集合來確認客戶接受合約。 目前， **AgreementMetaData**集合只會傳回一個合約類型的中繼資料，也就是**Microsoft Cloud 協定**。

## <a name="agreementmetadata"></a>AgreementMetaData

傳回的合約中繼資料包括下列各項：

| 屬性      | 類型               | 描述                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | 字串             | 協定範本的唯一識別碼。                                       |
| type          | 字串             | 合約類型。 目前支援的值包括**MicrosoftCloudAgreement**和**MicrosoftCustomerAgreement** （預覽）。 |
| agreementLink | 字串             | 合約範本的 URL。                                                    |
