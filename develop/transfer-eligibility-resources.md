---
title: TransferEligibility 資源
description: 當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 739631a4870268001c14f95490985ba18896e418
ms.sourcegitcommit: 4b1c10f91962861244c9349d5b9a9ba354b35b24
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/12/2020
ms.locfileid: "81220714"
---
# <a name="transfereligibility-resources"></a>TransferEligibility 資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。

## <a name="transfereligibility"></a>TransferEligibility

描述 transferEligibility。

| 屬性              | 類型             | 描述                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | string           | 客戶的訂用帳戶識別碼。                                                  |
| isEligible            | bool             | 指出訂用帳戶是否符合傳送資格。                         |
| 原因                | string           | 當訂用帳戶不符合傳送資格時，說明 ineligiblity 的原因。 |