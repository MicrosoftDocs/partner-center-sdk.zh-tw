---
title: 客戶合約的直接簽署（直接接受）狀態。
description: DirectSignedCustomerAgreementStatus 資源代表客戶合約直接簽署（直接接受）的狀態。
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 23397ab479f32879b00c04a817ef889221a6f091
ms.sourcegitcommit: 59ac8346af04aa34f5d342002909d0b203654bfe
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "81665988"
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

| 屬性       | 類型   | 描述                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | 指出客戶是否已直接簽署（接受）客戶合約。 |
