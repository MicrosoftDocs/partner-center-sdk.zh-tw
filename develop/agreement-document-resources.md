---
title: 合約檔資源
description: AgreementDocument 資源代表協定檔。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 21035d465094ab306d65ce3f24a006a97bf96354
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81665155"
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

| 屬性       | 類型   | 描述                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| country | 字串 | 本檔適用的國家或市場。 |
| 語言 | 字串 | 當地語系化此檔的語言。 |
| displayUri | 字串 | 在瀏覽器中預覽合約檔的連結。  |
| downloadUri |字串 | 下載合約檔的連結（以 Microsoft Word 格式）。 |
