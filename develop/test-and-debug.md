---
title: 測試與偵錯
description: 若要測試您的程式碼，您應該在合作夥伴中心使用您的整合沙箱帳戶（和對應的權杖），如此您就不會意外產生貴公司負責支付的新費用。
ms.assetid: 0A84F92F-CE66-42DF-B686-4D9E6FFECB16
ms.date: 09/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: d24becdaf89798fd99ca0ed3fe0ea60d75d0d2f9
ms.sourcegitcommit: 58fecbc8e6f20dae7cde34ae44b72d5d37ae09b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2020
ms.locfileid: "82869062"
---
# <a name="test-and-debug"></a>測試與偵錯

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

若要測試您的程式碼，您應該在合作夥伴中心使用您的整合沙箱帳戶（和對應的權杖），如此您就不會意外產生貴公司負責支付的新費用。 如需這項測試生產（TiP）環境的詳細資訊，請參閱[在合作夥伴中心設定 API 存取](set-up-api-access-in-partner-center.md)。

## <a name="integration-sandbox-constraints"></a>整合沙箱條件約束

如果您執行自動化組建驗證測試、在生產環境中進行測試，或在整合沙箱中執行手動測試，您可能會達到整合沙箱的最大限制。 這些限制為75客戶、每個客戶5個訂用帳戶，以及每個訂用帳戶25個基座。

- 25個基座的限制表示您無法在具有超過25個基座的最小基座需求的沙箱中取得供應專案。 這項限制包括試用版。

- 無法取得沙箱帳戶的使用量摘要，因為這些帳戶適用于測試用途。

- 與帳單和發票相關的 Api 將無法在沙箱中使用，因為測試帳戶不會產生任何發票。


### <a name="azure-plan"></a>Azure 方案

根據預設，合作夥伴無法使用其沙箱帳戶布建 Azure 方案。 需要使用其沙箱帳戶來執行此動作的合作夥伴必須申請存取權。 若要申請存取，請聯繫您的 Microsoft 帳戶經理或商務連絡人。 先前已申請在其沙箱帳戶中存取布建 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂閱的合作夥伴，不需要再次申請存取。 系統會授與他們自動布建 Azure 方案的存取權。

針對已核准其沙箱帳戶以布建 Azure 方案的合作夥伴，適用下列限制：

- 每個沙箱合作夥伴帳戶在所有客戶租使用者中最多可以有10個 Azure 方案（不論方案在客戶之間的散發方式為何）。

- 直接帳單合作夥伴最多可以為每個客戶租使用者建立一個 Azure 方案。

- 間接提供者可以為每個客戶租使用者建立最多三個 Azure 方案（針對指定為夥伴記錄的不同間接轉售商）。

- 每個 Azure 方案最多可以有三個 Azure 訂用帳戶。

- 每個資料中心的每個 CSP Azure 訂用帳戶都限制為四部虛擬機器（VM）核心。 因此，您無法布建需要超過四個 VM 核心的 VM Sku。 某些特製化 VM Sku （例如 GPU 核心）也會被排除。

- 每個沙箱合作夥伴帳戶在所有 Azure 方案中，每個計費週期的消費限制為 $2000 （美元）。 當合作夥伴達到支出限制之後，所有 Azure 方案將會暫時停用，直到下一個計費週期為止。

### <a name="cloud-solution-provider-csp-azure-subscription-offers"></a>雲端解決方案提供者（CSP） Azure 訂用帳戶優惠

CSP Azure 訂用帳戶供應專案預設已不再提供給沙箱帳戶。 這些包括適用于 Microsoft 公用雲端、德國雲端和政府雲端中 CSP Azure 訂用帳戶的 MS-AZR-0017P-Ms-azr-0146p、MS-MS-AZR-0017P-Ms-azr-0146p 和 MS-MS-AZR-0017P-USGOV-ms-azr-0146p。 需要使用其沙箱帳戶來存取這些供應專案的合作夥伴，必須申請以取得存取權。 若要申請存取，請與您的 Microsoft 帳戶經理或業務連絡人進行討論。

針對已針對 CSP Azure 訂用帳戶供應專案核准其沙箱帳戶的合作夥伴，適用下列限制：

- 最多可以有375個作用中的訂用帳戶（每位客戶75個客戶 x 5 個訂用帳戶）。 不過，只有10個可以是 CSP Azure 訂用帳戶。

- 當 CSP Azure 訂用帳戶達到 $200 的 Azure 使用量時，其資源會暫時停用，直到其下一個計費週期為止。 它仍然被視為有效的訂用帳戶，且會計入10個作用中的 Azure 訂用帳戶限制。

- 每個資料中心的每個 CSP Azure 訂用帳戶都限制為四部虛擬機器（VM）核心。 因此，您無法布建需要超過四個 VM 核心的 VM Sku。 某些特製化 VM Sku （例如 GPU 核心）也會被排除。

> [!Important]
> 2018年8月1日前所有以沙箱帳戶布建的現有 CSP Azure 訂用帳戶已不再受到支援，Microsoft 將在2018年10月16日之間取消布建。 取消布建訂閱之後，就無法重新啟用這些訂用帳戶，而且也無法再存取相關聯的資料。 在這些訂用帳戶下儲存寶貴資料的合作夥伴，必須在2018年10月16日前備份資料。

### <a name="azure-reserved-vm-instance"></a>Azure 保留的 VM 實例

如果您要使用您的沙箱帳戶[購買 Azure 保留的 vm 實例](purchase-azure-reservations.md)，您的每位客戶只能有兩個 VM 實例。 您也只能從下列 Azure 保留的 VM 實例產品 Sku 中選取：

| 產品標題  | 生效日期  | Sku 標題                                               | 區域 [ArmRegionName] | 實例索引鍵 [ArmSkuName] | Duration | 耗用量計量識別碼       |
|----------------|-----------------|---------------------------------------------------------|------------------------|--------------|----------|----------------------------|
| B 系列       | 12/1/2017 0:00  | 保留的 VM 實例，Standard_B1s，KR 南部，1年    | KoreaSouth             | `Standard_B1s` | `1Year`    | 3f913071-0dd7-4258-8ec4-6fad05bd976d |
| B 系列       | 12/1/2017 0:00  | 保留的 VM 實例，Standard_B1s，美國東部，1年     | eastus                 | `Standard_B1s` | `1Year`    | f4d7a5a5-1b67-45ea-b1a0-282fbdd34b05 |
| B 系列       | 12/1/2017 0:00  | 保留的 VM 實例，Standard_B1s，美國西部2，1年   | westus2                | `Standard_B1s` | `1Year`    | 222e39f5-e99f-4fa3-a323-f46402977888 |
| B 系列       | 12/1/2017 0:00  | 保留的 VM 實例，Standard_B1s，美國中北部，1年    | northcentralus | `Standard_B1s` | `1Year`    | 4e1716fc-4842-43f1-aa96-7c1b1b1395a7 |
| B 系列       | 12/1/2017 0:00  | 保留的 VM 實例，Standard_B1s，CA 東部，1年     | CanadaEast             | `Standard_B1s` | `1Year`    | ab8a5993-5db7-47c8-b3b1-2e1365b353fb |

### <a name="subscriptions-for-commercial-marketplace-products"></a>商用 marketplace 產品的訂閱

在生產環境中，[建立商業 Marketplace SaaS 產品的訂](create-subscription-azure-marketplace-products.md)用帳戶之後，您需要從合作夥伴中心抓取個人化啟用連結，並造訪發行者的網站以完成安裝程式。 只有在安裝完成後，訂用帳戶才會開始計費。

在 CSP 沙箱環境中，沒有與 Isv 的整合。 如果您嘗試從合作夥伴中心抓取啟用連結，則會傳回虛擬連結。 您無法使用此虛擬連結完成發行者網站上的安裝程式。 若要使用整合沙箱帳戶來測試對商業 marketplace SaaS 產品的訂閱計費，請參閱[啟用商業 marketplace 產品的沙箱訂閱](activate-sandbox-subscription-azure-marketplace-products.md)。 訂用帳戶會在成功啟用後開始計費。

若要在測試回合結束時清除，以便下一輪測試的空間，請參閱下列文章：

- [從整合沙箱中刪除客戶帳戶](delete-a-customer-account-from-the-integration-sandbox.md)

- [減少訂用帳戶的數量](change-the-quantity-of-a-subscription.md)

- [暫止訂用](suspend-a-subscription.md)帳戶，讓您可以將它移除。

## <a name="best-practices-for-rest-development"></a>REST 開發的最佳做法

- 使用網路追蹤工具，讓您可以看到您的要求、回應，以及回應中的 HTTP 狀態碼是否有任何錯誤。 如需有關錯誤處理的詳細資訊，請參閱[合作夥伴中心的 REST 錯誤碼](error-codes.md)。

- 針對對合作夥伴中心 REST API 進行的每個呼叫，使用新的相互關聯識別碼。 這種作法可確保更好的記錄功能，並在進行調試時提供協助。 如需詳細資訊，請參閱[合作夥伴中心 REST 標頭](headers.md)。

## <a name="troubleshooting-tips-for-common-rest-problems"></a>常見 REST 問題的疑難排解秘訣

- 檢查所有標頭屬性，包括 URL 和 API 版本。

- 必要時，請確定已包含屬性，且格式正確。

- 不正確的陣列格式是常見的錯誤。

- **Etag**是暫時性的，因此不應該儲存。 當函式呼叫需要**etag**時，請再次取得資源，以使用最新的**etag**值。 **Etag**值應該包含在雙引號中，就像字串：

   ```rest
   If-Match : "eyJpZCI6IjUwMWE4NjBjLTE2OTgtNDQyYi04MDhjLTRiNjEyY2NmMzVmMiIsInZlcnNpb24iOjF9"
   ```
