---
title: TransferEligibility 資源
description: 當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac5724a1f708bc540a3aac7ce74b2eda60a296
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095980"
---
# <a name="transfereligibility-resources"></a>TransferEligibility 資源

**適用於：**

- 合作夥伴中心

當客戶想要將合作夥伴的訂用帳戶轉移給另一個夥伴時，合作夥伴會建立轉移。

## <a name="transfereligibility"></a>TransferEligibility

描述 transferEligibility。

| 屬性              | 類型             | 描述                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| id                    | 字串           | 客戶的訂用帳戶識別碼。                                                  |
| isEligible            | bool             | 指出訂用帳戶是否符合傳送資格。                         |
| 原因                | 字串           | 原因屬性會說明訂用帳戶不符合傳輸資格的原因。 |