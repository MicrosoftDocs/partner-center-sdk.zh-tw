---
title: 合作夥伴中心 .NET SDK 版本資訊
description: 最新版合作夥伴中心 .NET SDK 的版本資訊。
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b98c6ef23b08947a7dec219ba40b7e19a3e5026
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995615"
---
# <a name="net-sdk-release-notes"></a>.NET SDK 版本資訊

下列版本資訊適用于新版本的[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)。 您可以在 GitHub 上找到[.NET SDK 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)。 您可以在 .NET API 瀏覽器中找到[合作夥伴中心 .NET API 參考](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest)。

## <a name="version-1152"></a>版本1.15。2

[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.2 現已正式推出。 此外，也提供更新的 REST Api 和[GitHub 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)。 此版本包含下列變更：

* 夥伴協定
  * 新增間接提供者[驗證間接轉銷商的 Microsoft 合作夥伴合約狀態](verify-indirect-reseller-mpa-status.md)的功能。
* 產品
  * 下列兩個介面不正確地放在 PartnerCenter. Products 命名空間底下。 現在，它們位於 PartnerCenter 的 [Products] 命名空間底下。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
