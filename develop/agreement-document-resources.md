---
title: 合約檔資源
description: AgreementDocument 資源代表協定檔。
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 917bb25ab5cb20b5148af056c5f433a8b62e9cc9
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412675"
---
# <a name="agreement-document-resources"></a>合約檔資源

適用於：

- 夥伴中心

合作夥伴中心目前僅支援在*Microsoft 公用雲端*中使用**AgreementDocument**資源。 此資源不適用於：

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**AgreementDocument**資源代表可供預覽和下載的 Microsoft 合約檔。

## <a name="agreementdocument"></a>AgreementDocument

**AgreementDocument**資源包括下列屬性：

| 屬性       | 類型   | 描述                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| 國家/地區 | string | 本檔適用的國家或市場。 |
| 語言 | string | 當地語系化此檔的語言。 |
| displayUri | string | 在瀏覽器中預覽合約檔的連結。  |
| downloadUri |string | 下載合約檔的連結（以 Microsoft Word 格式）。 |
