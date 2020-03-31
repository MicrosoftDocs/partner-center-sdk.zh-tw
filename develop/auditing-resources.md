---
title: 審核資源
description: 搭配合作夥伴中心審核作業使用的資源。
ms.assetid: FEF0BED4-2CEB-46D2-9365-D7D3C50AF0E3
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 719ddd1b2e5003842ea85e0f4710c2cf01970564
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80413646"
---
# <a name="auditing-resources"></a>審核資源

適用於：

- 夥伴中心

您可以搭配使用下列資源與審核作業。

## <a name="auditrecord"></a>AuditRecord

代表合作夥伴使用者或應用程式所執行之作業的記錄。

| 屬性 | 類型 | 描述 |
| --- | --- | ---|
| Id | string | 識別客戶的 GUID 格式字串。 |
| customerName | string | 客戶名稱。 |
| userPrincipalName | string | 使用者主體名稱或使用者識別碼。 一般來說，這是以網際網路標準 RFC 822 為基礎之電子郵件地址格式使用者的網際網路樣式登入名稱。 |
| applicationId | string | 識別執行作業之應用程式的字串。 |
| resourceType | string | 作業所採取的資源類型。 可能的值： &quot;客戶&quot;、&quot;customer_user&quot;、&quot;訂單&quot;、&quot;訂閱&quot;、&quot;授權&quot;、&quot;third_party_add_on&quot;、&quot;mpn_association&quot;、&quot;傳輸&quot;、&quot;應用程式&quot;、&quot;application_credential&quot;、&quot;partner_user&quot;、&quot;partner_relationship&quot;。 |
| resourceOldValue | string | 資源的舊值。 |
| resourceNewValue | string | 資源的新值。 |
| operationType | string | 執行的作業類型。 可能的值： &quot;update_customer_qualification&quot;，&quot;update_subscription&quot;，&quot;upgrade_subscription&quot;，&quot;convert_trial_subscription&quot;，&quot;add_customer&quot;，&quot;update_customer_billing_profile&quot;，&quot;update_customer_partner_contract_company_name&quot;，&quot;update_customer_spending_budget&quot;，&quot;delete_customer&quot; （沙箱整合帳戶僅限）、&quot;remove_partner_customer_relationship&quot;、&quot;create_order&quot;、&quot;update_order&quot;、&quot;create_customer_user&quot;、&quot;delete_customer_user&quot;、&quot;update_customer_user&quot;、&quot;update_customer_user_licenses&quot;、&quot;reset_customer_user_password&quot;、&quot;update_customer_user_principal_name&quot;、&quot;restore_customer_user&quot;，&quot;create_mpn_association&quot;，&quot;update_mpn_association&quot;，&quot;update_sfb_customer_user_licenses&quot;，&quot;update_transfer&quot;，&quot;create_partner_relationship&quot;，&quot;register_application&quot;，&quot;unregister_application&quot;，&quot;add_application_credential&quot;，&quot;remove_application_credential&quot;，&quot;create_partner_user&quot;，&quot;update_partner_user&quot;，&quot;remove_partner_user&quot;。 |
| operationDate | UTC 日期時間格式的字串 | 執行作業的日期和時間。 |
| operationStatus | string | 正在進行審核之作業的狀態。 可能的值： &quot;成功&quot;、&quot;失敗的&quot;，或 &quot;進度&quot;，這表示作業仍在進行中。 |
| customizedData  | 物件的陣列 | 其他資訊。 每個物件都包含兩個 JSON 索引鍵/值組：第一個是 &quot;索引鍵&quot; 和字串值，第二個是 &quot;值&quot; 和字串值。 陣列中的物件數目取決於所執行的作業類型。 |
| 屬性 | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。 |