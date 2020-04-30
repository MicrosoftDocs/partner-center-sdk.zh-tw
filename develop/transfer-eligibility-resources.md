---
title: TransferEligibility 資源
description: 當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: cb0ba6a4ff0daf6fa3ed04561aeb997822b5bc2b
ms.sourcegitcommit: 45094b6fb1437bca51f97e193ac2957747dbea27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/24/2020
ms.locfileid: "82124316"
---
# <a name="transfereligibility-resources"></a>TransferEligibility 資源

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。

## <a name="transfereligibility"></a>TransferEligibility

描述 transferEligibility。

| 屬性              | 類型             | 描述                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | 字串           | 客戶的訂用帳戶識別碼。                                                  |
| isEligible            | bool             | 指出訂用帳戶是否符合傳送資格。                         |
| 原因                | 字串           | 原因屬性會說明訂用帳戶不符合傳輸資格的原因。 |