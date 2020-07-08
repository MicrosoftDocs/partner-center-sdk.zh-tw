---
title: 合約檔資源
description: AgreementDocument 資源代表協定檔。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: a99af9ae8a3ba229c9d3fb1bb14e2cc9eeca6c5f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095432"
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
