---
title: Agreement metadata resources
description: The AgreementMetadata resource collection describes agreement types that partners can use to provide confirmation of customer acceptance.
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
# <a name="agreement-metadata-resources"></a>Agreement metadata resources

適用於：

- 合作夥伴中心

The **AgreementMetaData** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource isn't applicable to:

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The **AgreementMetaData** collection provides metadata about all the agreement types. Partners can use this collection to provide confirmation of customer acceptance of agreements. Currently, the **AgreementMetaData** collection only returns metadata for one agreement type, which is the **Microsoft Cloud Agreement**.

## <a name="agreementmetadata"></a>AgreementMetaData

Agreement metadata returned includes the following:

| 屬性      | 在工作列搜尋方塊中輸入               | 說明                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | 字串             | Unique identifier of an agreement template.                                       |
| type          | 字串             | Agreement type. Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement** (preview). |
| agreementLink | 字串             | URL for the agreement template.                                                    |
