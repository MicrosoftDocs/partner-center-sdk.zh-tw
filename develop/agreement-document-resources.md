---
title: Agreement document resources
description: The AgreementDocument resource represents an agreement document.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 9ac079822a2ddb45310148c16101fa25a38ec492
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74488928"
---
# <a name="agreement-document-resources"></a>Agreement document resources

適用於：

- 合作夥伴中心

The **AgreementDocument** resource is currently supported by Partner Center only in the *Microsoft public cloud*. This resource not applicable to:

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The **AgreementDocument** resource represents a Microsoft agreement document that is available for preview and download.

## <a name="agreementdocument"></a>AgreementDocument

An **AgreementDocument** resource includes the following properties:

| 屬性       | 在工作列搜尋方塊中輸入   | 說明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| 國家/地區 | 字串 | The country or market to which this document applies. |
| language | 字串 | The language in which this document is localized. |
| displayUri | 字串 | A link to preview the agreement document in a browser.  |
| downloadUri |字串 | A link to download the agreement document (in Microsoft Word format). |
