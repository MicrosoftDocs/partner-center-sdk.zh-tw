---
title: 合作夥伴中心 .NET SDK 版本資訊
description: 合作夥伴中心 .NET SDK 最新版本的版本資訊。
ms.date: 09/18/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7ba1e9f0fa090863fd52dc6a60cf7c6e1f9a9ba6
ms.sourcegitcommit: 9d85737f1baccb59c4321b22a69745dfeb336456
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/19/2020
ms.locfileid: "90813012"
---
# <a name="net-sdk-release-notes"></a>.NET SDK 版本資訊

下列版本資訊適用于 [Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)的新版本。 您可以在 GitHub 上找到 [.NET SDK 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples) 。 您可以在 .NET API 瀏覽器中找到 [合作夥伴中心 .NET api 參考](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest&preserve-view=true) 。

## <a name="version-1162"></a>版本1.16。2

[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.2) v 1.16.2 現已正式推出。 您也可以使用更新的 [GitHub 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples) 。 此版本包含下列變更：

* 更新 Audit 記錄支援的作業類型。 新加入的是：
  * CreateSelfServePolicy
  * UpdateSelfServePolicy
  * DeleteSelfServePolicy
  * RemovePartnerRelationship
  * DeleteTipCustomer
  * CreateRelatedReferral
  * UpdateRelatedReferral

* 現在已淘汰服務要求建立
* 支援主題現在已淘汰


## <a name="version-1161"></a>版本1.16。1

[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.16.1) v 1.16.1 現已正式推出。 您也可以使用更新的 [GitHub 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples) 。 此版本包含下列變更：

我們已將現有的 Microsoft 合作夥伴中心 SDK 從 .NET Framework 遷移至 .NET Standard 2.0 平臺。 這會使 SDK 與使用 .NET Framework 4.6.1 和更新版本的現有應用程式相容。 SDK 將支援 .NET Core 2.0 和更新版本。 先檢查 [.net 執行支援](/dotnet/standard/net-standard) ，再將其移植到現有的應用程式。   


## <a name="version-1153"></a>版本1.15。3
[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/1.15.3) v 1.15.3 現已正式推出。 您也可以使用更新的 REST Api 和 [GitHub 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples) 。 此版本包含下列變更：

* 夥伴協定
  * 已新增間接提供者的功能，以 [確認間接轉銷商的 Microsoft 合作夥伴合約狀態](verify-indirect-reseller-mpa-status.md)。
* 產品
  * 下列兩個介面不正確地放在 PartnerCenter 的命名空間底下。 現在，它們位於 PartnerCenter. Products 命名空間底下。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
