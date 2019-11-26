---
title: Agreement resources
description: The Agreement resource represents a Microsoft cloud customer agreement.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2cf620d63da14e014a17017006346f80a7a3fe4c
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489258"
---
# <a name="agreement-resources"></a>Agreement resources

適用於：

- 合作夥伴中心

The **Agreement** resource is currently supported by Partner Center in the Microsoft public cloud only. It is not applicable to:

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

The **Agreement** resource represents a Microsoft cloud customer agreement.

## <a name="agreement"></a>合約

The **Agreement** resource represents the details of certification provided by the partner.

| 屬性       | 在工作列搜尋方塊中輸入   | 說明                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | 字串                         | Object identifier of the logged-in user in the partner tenant who is providing confirmation on behalf of the partner organization. When using App+User authentication to create an Agreement resource, Partner Center automatically derives the **userId** attribute value from the App+User token.                                                                             |
| primaryContact | [Contact](./utility-resources.md#contact) | Information about the user from the customer organization that accepted the Microsoft Cloud Agreement, including:  **firstName**, **lastName**, **email**, and **phoneNumber** (optional). |
| dateAgreed     | string in UTC date time format | The date when the customer accepted the agreement.                                 |
| templateId     |字串                          | Unique identifier of the agreement that the customer accepted. |
| type           |字串                          | Agreement type. Currently, supported values include **MicrosoftCloudAgreement** and **MicrosoftCustomerAgreement**.|
| agreementLink  | 字串                         | URL for the agreement template.                                                    |
