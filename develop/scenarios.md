---
title: 案例
description: 本節將說明雲端解決方案提供者計畫中的合作夥伴，可如何利用合作夥伴中心 API 以程式設計方式管理客戶帳戶、合作夥伴帳戶、訂單、訂用帳戶、支援及帳單。
ms.date: 02/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 12cd314c419e874225aed60f6a025f829098b37f
ms.sourcegitcommit: 57620e249e218edc4af7c83c2ce8a3008a4adf4e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/04/2020
ms.locfileid: "87557319"
---
# <a name="scenarios"></a>案例

**適用於：**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

本節將說明雲端解決方案提供者計畫中的合作夥伴，可如何利用合作夥伴中心 API 以程式設計方式管理客戶帳戶、合作夥伴帳戶、訂單、訂用帳戶、支援及帳單。

您可以使用不同的合作夥伴中心版本，其中包含不同的功能。 並非所有合作夥伴中心版本都支援所有案例。 若要深入了解，請參閱[針對 Microsoft 國家/地區雲端的合作夥伴中心進行開發](developing-for-partner-center-for-microsoft-national-cloud.md)。

## <a name="scenarios-supported-by-the-partner-center-sdk"></a>合作夥伴中心 SDK 支援的案例

下列所有案例都可以用三種不同的方式完成：

- 在[合作夥伴中心](https://partner.microsoft.com/dashboard)儀表板中手動進行。

- 以程式設計方式使用合作夥伴中心受控 API。

- 以程式設計方式使用合作夥伴中心 REST API。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr>
<td><p><a href="usage-analytics.md">分析</a></p></td>
<td><p>擷取分析</p>
<ul>
<li><p><a href="partner-center-analytics-resources.md">合作夥伴中心分析 - 資源</a></p></li>
<li><p><a href="get-all-azure-usage-analytics.md">取得所有 Azure 使用情形的分析資訊</a></p></li>
<li><p><a href="get-all-indirect-resellers-analytics.md">取得所有間接轉銷商的分析資訊</a></p></li>
<li><p><a href="get-all-referrals-analytics.md">取得所有轉介的分析資訊</a></p></li>
<li><p><a href="get-all-search-analytics.md">取得所有搜尋的分析資訊</a></p></li>
<li><p><a href="get-all-subscription-analytics.md">取得所有訂用帳戶的分析資訊</a></p></li>
<li><p><a href="get-subscription-analytics-by-search-query.md">取得根據搜尋查詢所篩選的訂用帳戶分析資訊</a></p></li>
<li><p><a href="get-subscription-analytics-grouped-by-dates-or-terms.md">取得根據日期或詞彙分組的訂用帳戶分析資訊</a></p></li>
<li><p><a href="get-licenses-deployment-information.md">取得授權部署資訊</a></p></li>
<li><p><a href="get-licenses-usage-information.md">取得授權使用資訊</a></p></li>
<li><p><a href="get-customer-licenses-deployment-information.md">取得客戶授權部署資訊</a></p></li>
<li><p><a href="get-customer-licenses-usage-information.md">取得客戶授權使用資訊</a></p></li>
<li><p><a href="get-partner-licenses-deployment-information.md">取得合作夥伴授權部署資訊</a></p></li>
<li><p><a href="get-partner-licenses-usage-information.md">取得合作夥伴授權使用資訊</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="device-deployment.md">裝置部署</a></p></td>
<td><p>設定原則</p>
<p>新增、刪除、更新和擷取裝置設定原則。</p>
<ul>
<li><p><a href="create-a-new-configuration-policy-for-the-specified-customer.md">為指定客戶建立新的設定原則</a></p></li>
<li><p><a href="delete-a-configuration-policy-for-the-specified-customer.md">為指定客戶刪除設定原則</a></p></li>
<li><p><a href="get-a-list-of-a-customer-s-policies.md">取得客戶的原則清單</a></p></li>
<li><p><a href="retrieve-a-customer-s-configuration-policy.md">擷取客戶的設定原則</a></p></li>
<li><p><a href="update-a-configuration-policy-for-the-specified-customer.md">為指定客戶更新設定原則</a></p></li>
</ul>
<p>裝置</p>
<p>使用和上傳裝置批次和裝置中繼資料。</p>
<ul>
<li><p><a href="get-the-status-of-a-device-batch-upload.md">取得裝置批次上傳的狀態</a></p></li>
<li><p><a href="get-the-list-of-device-batches-for-the-specified-customer.md">取得指定客戶的裝置批次清單</a></p></li>
<li><p><a href="get-a-list-of-devices-for-the-specified-batch-and-customer.md">取得指定批次和客戶的裝置清單</a></p></li>
<li><p><a href="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer.md">上傳裝置清單，為指定的客戶建立新的批次</a></p></li>
<li><p><a href="upload-a-list-of-devices-for-the-specified-customer.md">將裝置清單上傳至指定客戶的現有批次</a></p></li>
<li><p><a href="delete-a-device-for-the-specified-customer.md">為指定客戶刪除裝置</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-profiles-and-information.md">管理帳戶和設定檔</a></p></td>
<td><p>使用帳戶和設定檔</p>
<ul>
<li><p><a href="get-legal-business-profile.md">取得合作夥伴的合法商務設定檔</a></p></li>
<li><p><a href="get-an-organization-profile.md">取得組織設定檔</a></p></li>
<li><p><a href="get-partner-billing-profile.md">取得合作夥伴的帳單設定檔</a></p></li>
<li><p><a href="get-partner-network-profile.md">取得 Microsoft 合作夥伴網路設定檔</a></p></li>
<li><p><a href="get-support-profile.md">取得支援設定檔</a></p></li>
<li><p><a href="update-legal-business-profile.md">更新合作夥伴的合法商務設定檔</a></p></li>
<li><p><a href="update-partner-billing-profile.md">更新合作夥伴的帳單設定檔</a></p></li>
<li><p><a href="update-support-profile.md">更新支援設定檔</a></p></li>
<li><p><a href="update-an-organization-profile.md">更新組織設定檔</a></p></li>
<li><p><a href="get-partner-by-mpn-id.md">確認合作夥伴的 MPN 識別碼</a></p></li>
<li><p><a href="get-all-subscriptions-by-partner.md">依合作夥伴 MPN 識別碼取得客戶的訂用帳戶</a></p></li>
<li><p><a href="get-customers-of-an-indirect-reseller.md">取得間接轉銷商的客戶</a></p></li>
<li><p><a href="get-indirect-resellers-of-a-customer.md">取得客戶的間接轉銷商</a></p></li>
<li><p><a href="retrieve-a-list-of-indirect-resellers.md">擷取間接轉銷商清單</a></p></li>
</ul></td>
</tr>
<tr>
<td>
<p><a href="manage-billing.md">管理計費</a></p></td>
<td><p>計費週期</p>
<ul>
<li><p><a href="change-the-billing-cycle.md">變更計費擁週期</a></p></li>
</ul>
<p>Azure 費率和使用率記錄</p>
<ul>
<li><p><a href="get-prices-for-microsoft-azure.md">取得 Microsoft Azure 定價</a></p></li>
<li><p><a href="get-a-customer-s-utilization-record-for-azure.md">取得客戶的 Azure 使用率記錄</a></p></li>
</ul>
<p>發票</p>
<ul>
<li><p><a href="get-a-collection-of-invoices.md">取得發票的集合</a></p></li>
<li><p><a href="get-invoice-estimate-links.md">取得發票估算連結</a></p></li>
<li><p><a href="get-invoice-billed-consumption-lineitems.md">取得已開立發票的商業市集取用量明細</a></p></li>
<li><p><a href="get-invoice-by-id.md">依照識別碼取得發票</a></p></li>
<li><p><a href="get-invoiceline-items.md">取得發票明細項目</a></p></li>
<li><p><a href="get-invoice-receipt-statement.md">取得發票收據對帳單</a></p></li>
<li><p><a href="get-invoice-statement.md">取得發票對帳單</a></p></li>
<li><p><a href="get-invoice-summaries.md">取得發票摘要</a></p></li>
<li><p><a href="get-invoice-unbilled-consumption-lineitems.md">取得未開立發票的商業市集取用量明細</a></p></li>
<li><p><a href="get-invoice-unbilled-recon-lineitems.md">取得未開立發票的對帳明細項目</a></p></li>
<li><p><a href="get-the-reseller-s-current-account-balance.md">取得合作夥伴的目前帳戶餘額</a></p></li>
</ul>
<p>Azure 費用預算</p>
<ul>
<li><p><a href="get-all-monthly-usage-records-for-a-subscription.md">取得訂用帳戶的使用量資料</a></p></li>
<li><p><a href="get-a-customer-usage-summary.md">取得所有客戶的訂用帳戶使用量摘要</a></p></li>
</ul>
<p>服務成本</p>
<ul>
<li><p><a href="get-a-customer-s-service-costs-summary.md">取得客戶的服務成本摘要</a></p></li>
<li><p><a href="get-a-customer-s-service-costs-line-items.md">取得客戶的服務成本明細項目</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-customers.md">管理客戶帳戶</a></p></td>
<td><p>建立客戶</p>
<ul>
<li><p><a href="create-a-customer.md">建立客戶</a></p></li>
<li><p><a href="create-a-customer-for-an-indirect-reseller.md">建立間接轉銷商的客戶</a></p></li>
<li><p><a href="request-reseller-relationship.md">擷取關聯性的要求 URL</a></p></li>
<li><p><a href="remove-a-reseller-relationship-with-a-customer.md">移除與客戶的經銷商關係</a></p></li>
</ul>
<p>查閱客戶</p>
<ul>
<li><p><a href="get-a-customer-by-id.md">依照識別碼取得客戶</a></p></li>
<li><p><a href="get-a-customer-by-name.md">取得依搜尋欄位篩選的客戶清單</a></p></li>
<li><p><a href="get-a-list-of-customers.md">取得客戶清單</a></p></li>
</ul>
<p>管理客戶訂單和訂用帳戶</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-orders.md">取得客戶的所有訂單</a></p></li>
<li><p><a href="get-a-list-of-orders-by-customer-and-billing-cycle-type.md">依照客戶和計費週期類型取得訂單清單</a></p></li>
<li><p><a href="get-a-collection-of-entitlements.md">取得權利的集合</a></p></li>
<li><p><a href="get-all-of-a-customer-s-subscriptions.md">取得客戶的訂用帳戶</a></p></li>
<li><p><a href="update-the-nickname-for-a-subscription.md">更新訂用帳戶的暱稱</a></p></li>
</ul>
<p>管理客戶帳戶詳細資料</p>
<ul>
<li><p><a href="get-all-of-a-customer-s-billing-profiles.md">取得客戶的帳單設定檔</a></p></li>
<li><p><a href="update-a-customer-s-billing-profile.md">更新客戶的帳單設定檔</a></p></li>
<li><p><a href="get-a-customer-s-company-profile.md">取得客戶的公司設定檔</a></p></li>
<li><p><a href="update-a-customer-s-usage-spending-budget.md">更新客戶的使用量支出預算</a></p></li>
<li><p><a href="add-a-verified-domain-for-a-customer.md">為客戶新增已驗證的網域</a></p></li>
<li><p><a href="confirm-customer-consent-customer-agreement.md">確認客戶接受 Microsoft 客戶合約</a></p></li>
<li><p><a href="get-agreement-metadata.md">取得 Microsoft Cloud 合約的合約中繼資料</a></p></li>
<li><p><a href="get-confirmation-of-customer-consent.md">取得客戶接受 Microsoft Cloud 合約的確認</a></p></li>
<li><p><a href="get-direct-sign-status-of-customer-agreement.md">取得 Microsoft 客戶合約的直接簽署 (直接接受) 狀態</a></p></li>
<li><p><a href="get-customer-agreement-metadata.md">取得 Microsoft 客戶合約的合約中繼資料</a></p></li>
<li><p><a href="get-a-partner-s-validation-codes.md">取得合作夥伴的驗證碼</a></p></li>
<li><p><a href="get-a-customer-s-qualification.md">取得客戶資格</a></p></li>
<li><p><a href="update-a-customer-s-qualification.md">更新客戶的資格</a></p></li>
</ul>
<p>管理使用者帳戶和指派授權</p>
<ul>
<li><p><a href="get-a-user-account-by-id.md">依識別碼取得使用者帳戶</a></p></li>
<li><p><a href="create-user-accounts-for-a-customer.md">為客戶建立使用者帳戶</a></p></li>
<li><p><a href="delete-user-accounts-for-a-customer.md">為客戶刪除使用者帳戶</a></p></li>
<li><p><a href="update-user-accounts-for-a-customer.md">為客戶更新使用者帳戶</a></p></li>
<li><p><a href="view-a-deleted-user.md">為客戶檢視已刪除的使用者</a></p></li>
<li><p><a href="restore-a-user-for-a-customer.md">為客戶還原已刪除的使用者</a></p></li>
<li><p><a href="get-a-list-of-all-user-accounts-for-a-customer.md">為客戶取得所有使用者帳戶的清單</a></p></li>
<li><p><a href="reset-user-password-for-a-customer.md">為客戶重設使用者密碼</a></p></li>
<li><p><a href="get-user-roles-for-a-customer.md">為客戶取得使用者角色</a></p></li>
<li><p><a href="set-user-roles-for-a-customer.md">為客戶設定使用者角色</a></p></li>
<li><p><a href="remove-customer-user-from-a-role.md">從角色中移除客戶使用者</a></p></li>
<li><p><a href="get-a-list-of-available-licenses.md">取得可用授權的清單</a></p></li>
<li><p><a href="assign-licenses-to-a-user.md">指派授權給使用者</a></p></li>
<li><p><a href="check-which-licenses-are-assigned-to-a-user.md">取得指派給使用者的授權</a></p></li>
<li><p><a href="get-licenses-assigned-to-a-user-by-license-group.md">依照授權群組取得指派給使用者的授權</a></p></li>
<li><p><a href="get-a-list-of-available-licenses-by-license-group.md">依照授權群組取得可用授權的清單</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="manage-orders.md">管理訂單</a></p></td>
<td><p>購買 Azure 保留的 VM 執行個體</p>
<ul>
<li><p><a href="purchase-azure-reservations.md">購買 Azure 保留</a></p></li>
</ul>
<p>進行一次性購買</p>
<ul>
<li><p><a href="make-a-one-time-purchase.md">進行一次性購買</a></p></li>
</ul>
<p>從目錄取得供應項目</p>
<ul>
<li><p><a href="get-a-list-of-offer-categories-by-country-and-locale.md">依照市場取得供應項目類別的清單</a></p></li>
<li><p><a href="get-a-list-of-offers-for-a-market.md">取得市場的供應項目清單</a></p></li>
<li><p><a href="get-an-offer-by-id.md">依識別碼取得供應項目</a></p></li>
<li><p><a href="get-addon-offers-by-offer-id.md">取得應用程式識別碼的附加元件</a></p></li>
<li><p><a href="get-a-list-of-products.md">取得產品清單</a></p></li>
<li><p><a href="get-a-product-by-id.md">依照識別碼取得產品</a></p></li>
<li><p><a href="get-a-list-of-skus-for-a-product.md">取得產品的 SKU 清單</a></p></li>
<li><p><a href="get-a-sku-by-id.md">取得 SKU 的可用性清單</a></p></li>
<li><p><a href="get-an-availability-by-id.md">依照識別碼取得可用性</a></p></li>
<li><p><a href="check-inventory.md">確認存貨</a></p></li>
</ul>
<p>管理訂單</p>
<ul>
<li><p><a href="cancel-an-order-from-the-integration-sandbox.md">從整合沙箱中取消訂單</a></p></li>
<li><p><a href="checkout-a-cart.md">購物車結帳</a></p></li>
<li><p><a href="create-a-cart.md">建立購物車</a></p></li>
<li><p><a href="create-a-cart-with-add-ons.md">使用附加元件建立購物車</a></p></li>
<li><p><a href="create-an-order.md">建立訂單</a></p></li>
<li><p><a href="create-an-order-for-a-customer-of-an-indirect-reseller.md">為間接轉銷商的客戶建立訂單</a></p></li>
<li><p><a href="get-activation-link-by-order-line-item.md">依照訂單明細項目取得啟用連結</a></p></li>
<li><p><a href="get-an-order-by-id.md">依識別碼取得供應項目</a></p></li>
<li><p><a href="purchase-an-add-on-to-a-subscription.md">購買要加入訂用帳戶的附加元件</a></p></li>
<li><p><a href="purchase-catalog-items.md">購買目錄項目</a></p></li>
<li><p><a href="update-a-cart.md">更新購物車</a></p></li>
</ul>
<p>啟用訂用帳戶以用於購買 Azure 保留的 VM 執行個體</p>
<ul>
<li><p><a href="register-a-subscription.md">註冊訂用帳戶</a></p></li>
<li><p><a href="get-subscription-registration-status.md">取得訂用帳戶的註冊狀態</a></p></li>
</ul>
<p>試用版轉換</p>
<ul>
<li><p><a href="get-a-list-of-trial-conversion-offers.md">取得試用版轉換方案的清單</a></p></li>
<li><p><a href="convert-a-trial-subscription-to-paid.md">將試用版訂用帳戶轉換成付費版</a></p></li>
</ul>
<p>取得訂用帳戶詳細資料</p>
<ul>
<li><p><a href="get-a-subscription-by-id.md">依照識別碼取得訂用帳戶</a></p></li>
<li><p><a href="get-a-list-of-subscriptions-by-order.md">依訂單取得訂用帳戶清單</a></p></li>
<li><p><a href="get-a-list-of-add-ons-for-a-subscription.md">取得訂用帳戶的附加元件清單</a></p></li>
<li><p><a href="get-subscription-provisioning-status.md">取得訂用帳戶的佈建狀態</a></p></li>
</ul>
<p>管理訂用帳戶</p>
<ul>
<li><p><a href="change-the-quantity-of-a-subscription.md">變更訂用帳戶的數量</a></p></li>
<li><p><a href="update-autorenew-for-an-azure-marketplace-subscription.md">更新商業市集訂用帳戶的自動續約</a></p></li>
<li><p><a href="suspend-a-subscription.md">暫停訂閱</a></p></li>
<li><p><a href="reactivate-a-suspended-a-subscription.md">重新啟用暫止的訂用帳戶</a></p></li>
<li><p><a href="transition-a-subscription.md">轉換訂用帳戶</a></p></li>
<li><p><a href="cancel-an-azure-marketplace-subscription.md">取消商業市集訂用帳戶</a></p></li>
</ul></td>
</tr>
<tr>
<td><p><a href="provide-support.md">提供支援</a></p></td>
<td><p>管理客戶的服務</p>
<ul>
<li><p><a href="get-the-managed-services-for-a-customer-by-id.md">依照識別碼取得客戶的受控服務</a></p></li>
</ul>
<p>管理支援連絡人</p>
<ul>
<li><p><a href="get-a-subscription-s-support-contact.md">取得訂用帳戶的支援連絡人</a></p></li>
<li><p><a href="update-a-subscription-s-support-contact.md">更新訂用帳戶的支援連絡人</a></p></li>
</ul>
<p>管理服務要求</p>
<ul>
<li><p><a href="create-a-service-request-.md">建立服務要求</a></p></li>
<li><p><a href="get-service-request-support-topics--pending-.md">取得服務要求支援主題的清單</a></p></li>
<li><p><a href="get-all-service-requests-for-a-customer.md">為客戶取得所有服務要求</a></p></li>
<li><p><a href="get-service-request-details-by-id.md">依照識別碼取得服務要求詳細資料</a></p></li>
<li><p><a href="update-a-service-request.md">更新服務要求</a></p></li>
</ul></td>
</tr>
<tr>
  <td><p><a href="https://docs.microsoft.com/partner/develop/referrals">轉介</a></p></td>
  <td><p>轉介</p>
    <ul>
      <li><p><a href="https://docs.microsoft.com/partner/develop/create-a-referral">建立轉介</a></p></li>
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-list-of-referrals">取得轉介清單</a></p></li>
      <li><p><a href="https://docs.microsoft.com/partner/develop/get-a-referral-by-id">依照識別碼取得轉介</a></p></li>
      <li><p><a href="https://docs.microsoft.com/partner/develop/update-a-referral">更新轉介</a></p></li>
    </ul>
  </td>
</tr>
<tr>
<td><p><a href="utilities.md">公用程式</a></p></td>
<td><p>公用程式</p>
<ul>
<li><p><a href="validate-an-address.md">驗證位址</a></p></li>
<li><p><a href="get-market-specific-validation-data.md">依市場取得位址格式化規則</a></p></li>
<li><p><a href="verify-domain-availability.md">驗證網域可用性</a></p></li>
<li><p><a href="delete-a-customer-account-from-the-integration-sandbox.md">從整合沙箱中刪除客戶帳戶</a></p></li>
<li><p><a href="get-a-record-of-partner-center-activity-by-user.md">取得合作夥伴中心活動的記錄</a></p></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="background"></a>背景

### <a name="who-is-involved-in-the-order-process"></a>訂購程序中包含哪些人員？

Microsoft、散發者、轉銷商和客戶。 散發者和轉銷商通常稱為**合作夥伴**。

有時候，Microsoft 會直接與銷售給客戶的轉售商合作。 或者，Microsoft 也會與散發者合作，而那些散發者會使用自己的一組轉銷商或轉銷商通路來銷售給客戶。

### <a name="whats-getting-sold"></a>銷售項目為何？

Microsoft 會提供**供應項目**清單。 這些是 Office 365 或 Intune 等產品的特定 SKU。 供應項目會以**授權為基礎** (成本取決於安裝的機器數目)，或是**以使用量為基礎** (成本取決於所使用的記憶體和計算數量)。 如需詳細資訊，請參閱[雲端解決方案提供者計畫中的合作夥伴供應項目](https://docs.microsoft.com/partner-center/csp-offers)。

CSP 合作夥伴是擁有客戶的轉銷商，他們會對客戶銷售目前供應項目清單中的 Microsoft 產品。 在客戶簽署其合約後，轉銷商會針對一個或多個供應項目下**訂單**。 某些供應項目會包括**附加元件**，例如更多的空間或額外功能，這些功能會與父系供應項目一起追蹤。 訂單會進入處理程序，然後客戶就可以使用其**訂用帳戶**。 Microsoft 會根據授權數目和每個客戶的使用量，每月向轉銷商或散發者收費。

您可以新增訂用帳戶，以及增加或減少授權或附加元件數目。 如果客戶無法支付費用、誤用訂用帳戶或參與詐騙，則 Microsoft、散發者或轉銷商皆能夠暫停訂用帳戶。 如果未在 CSP 計畫的限制內重新啟動，將會永久停用。

您可以查看客戶**有權**使用的訂用帳戶 (也就是目前需付費、未暫停且尚未由新訂單取代的訂用帳戶)。
