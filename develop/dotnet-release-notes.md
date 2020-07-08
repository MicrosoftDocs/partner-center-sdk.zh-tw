---
title: 合作夥伴中心 .NET SDK 版本資訊
description: 最新版合作夥伴中心 .NET SDK 的版本資訊。
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fe63c5bf5a7d3114f8914d432a64099e009698e6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86098409"
---
# <a name="net-sdk-release-notes"></a>.NET SDK 版本資訊

下列版本資訊適用于新版本的[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)。 您可以在 GitHub 上找到[.NET SDK 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)。 您可以在 .NET API 瀏覽器中找到[合作夥伴中心 .NET API 參考](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest)。

## <a name="version-1153"></a>版本1.15。3

[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.3 現已正式推出。 此外，也提供更新的 REST Api 和[GitHub 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)。 此版本包含下列變更：

* 夥伴協定
  * 新增間接提供者[驗證間接轉銷商的 Microsoft 合作夥伴合約狀態](verify-indirect-reseller-mpa-status.md)的功能。
* 產品
  * 下列兩個介面不正確地放在 PartnerCenter. Products 命名空間底下。 現在，它們位於 PartnerCenter 的 [Products] 命名空間底下。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
