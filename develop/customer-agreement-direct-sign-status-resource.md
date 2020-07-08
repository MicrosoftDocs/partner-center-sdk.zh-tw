---
title: 客戶合約的直接簽署（直接接受）狀態。
description: DirectSignedCustomerAgreementStatus 資源代表客戶合約直接簽署（直接接受）的狀態。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094318"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>客戶合約的直接簽署（直接接受）狀態

**適用於：**

- 合作夥伴中心

合作夥伴中心目前僅支援在 Microsoft 公用雲端中使用**DirectSignedCustomerAgreementStatus**資源。

此資源不適*用於：*

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

**DirectSignedCustomerAgreementStatus**資源代表直接接受客戶合約的狀態。

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

**DirectSignedCustomerAgreementStatus**資源包括下列屬性：

| 屬性       | 類型   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | 指出客戶是否已直接簽署（接受）客戶合約。 |
