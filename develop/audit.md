---
title: 稽核作業
description: 使用審核作業來取得合作夥伴中心活動的記錄。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e31990df06a67d4f02b97dab8422ee498a09b43
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095397"
---
# <a name="audit-operations"></a>稽核作業

合作夥伴中心 Api 提供了審核功能，讓您可以取得合作夥伴中心活動的記錄。

您可以從目前的日期，或透過包含開始日期和/或結束日期的日期範圍，抓取過去30天的審核記錄。 不過，請注意，基於效能的考慮，活動記錄資料可用性受限於前90天。 開始日期超過目前日期之前90天的要求將會收到不正確的要求例外狀況（錯誤碼：400）和適當的訊息。

## <a name="retrieve-audit-records"></a>取出 audit 記錄

取得合作夥伴使用者或應用程式所執行作業的詳細歷程記錄審核記錄：

- [取得合作夥伴中心活動的記錄](get-a-record-of-partner-center-activity-by-user.md)
- [審核資源](auditing-resources.md)