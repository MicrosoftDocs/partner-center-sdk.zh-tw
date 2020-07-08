---
title: 審核資源
description: 搭配合作夥伴中心審核作業使用的資源。
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5a9cb01af9d0ea027ed55716515dcbad251dacdb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86095380"
---
# <a name="auditing-resources"></a>審核資源

**適用於：**

- 合作夥伴中心

您可以搭配使用下列資源與審核作業。

## <a name="auditrecord"></a>AuditRecord

代表合作夥伴使用者或應用程式所執行之作業的記錄。

| 屬性 | 類型 | Description |
| --- | --- | ---|
| customerId | 字串 | 用來識別客戶的 GUID 格式字串。 |
| customerName | 字串 | 客戶名稱。 |
| userPrincipalName | 字串 | 使用者主體名稱或使用者識別碼。 一般來說，此屬性是以網際網路標準 RFC 822 為基礎之電子郵件地址格式使用者的網際網路樣式登入名稱。 |
| applicationId | 字串 | 識別執行作業之應用程式的字串。 |
| resourceType | 字串 | 作業所採取的資源類型。 可能的值： `customer` 、 `customer_user` 、 `order` 、 `subscription` 、、 `license` `third_party_add_on` `mpn_association` `transfer` `application` `application_credential` `partner_user` `partner_relationship` 、、、、、、。 |
| resourceOldValue | 字串 | 資源的舊值。 |
| resourceNewValue | 字串 | 資源的新值。 |
| operationType | 字串 | 執行的作業類型。 可能的值： `update_customer_qualification` 、 `update_subscription` 、 `upgrade_subscription` 、 `convert_trial_subscription` 、 `add_customer` 、 `update_customer_billing_profile` 、 `update_customer_partner_contract_company_name` 、 `update_customer_spending_budget` 、 `delete_customer` （僅限沙箱整合帳戶）、、 `remove_partner_customer_relationship` `create_order` `update_order` `create_customer_user` `delete_customer_user` `update_customer_user` `update_customer_user_licenses` `reset_customer_user_password` `update_customer_user_principal_name` `restore_customer_user` `create_mpn_association` `update_mpn_association` `update_sfb_customer_user_licenses` `update_transfer` `create_partner_relationship` `register_application` `unregister_application` `add_application_credential` `remove_application_credential` `create_partner_user` `update_partner_user` `remove_partner_user` 、、、、、、、、、、、、、、、、、、、、、、、、、、、、。 |
| operationDate | UTC 日期時間格式的字串 | 作業的執行日期和時間。 |
| operationStatus | 字串 | 正在進行審核之作業的狀態。 可能的值： `succeeded` 、 `failed` 或 `progress` ，這表示作業仍在進行中。 |
| customizedData  | 物件的陣列 | 其他資訊。 每個物件都包含兩個 JSON 索引鍵/值組：第一個是 `key` 和字串值，第二個是 `value` 和字串值。 陣列中的物件數目取決於所執行的作業類型。 |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 |
