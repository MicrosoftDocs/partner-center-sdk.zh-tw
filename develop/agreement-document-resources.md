---
title: 合約檔資源
description: AgreementDocument 資源代表協定檔。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 233277daece48cebe434ea3f458fd98fe6436de7
ms.sourcegitcommit: 33e48c19b6d05bacb1f8c2d8ce859e95c5373c61
ms.contentlocale: zh-TW
ms.lasthandoff: 07/06/2020
ms.locfileid: "86022596"
---
# <a name="agreement-document-resources"></a>合約檔資源

**適用於：**

- 合作夥伴中心

合作夥伴中心目前僅支援在*Microsoft 公用雲端*中使用**AgreementDocument**資源。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**AgreementDocument**資源代表可供預覽和下載的 Microsoft 合約檔。

## <a name="agreementdocument"></a>AgreementDocument

**AgreementDocument**資源包括下列屬性：

| 屬性       | 類型   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | 字串 | 本檔適用的國家或市場。 |
| 語言 | 字串 | 當地語系化此檔的語言。 |
| displayUri | 字串 | 在瀏覽器中預覽合約檔的連結。  |
| downloadUri |字串 | 下載合約檔的連結（以 Microsoft Word 格式）。 |
