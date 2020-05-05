---
title: 合作夥伴中心 .NET SDK 版本資訊
description: 最新版合作夥伴中心 .NET SDK 的版本資訊。
ms.date: 12/09/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: e11e5d6f7f2372b3230d8ac26e02d00b2b554edc
ms.sourcegitcommit: 506c69986f3d1ea650c935c42880048d6c4241f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82784703"
---
# <a name="net-sdk-release-notes"></a>.NET SDK 版本資訊

下列版本資訊適用于新版本的[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter)。 您可以在 GitHub 上找到[.NET SDK 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)。 您可以在 .NET API 瀏覽器中找到[合作夥伴中心 .NET API 參考](https://docs.microsoft.com/dotnet/api/?view=partnercenter-dotnet-latest)。

## <a name="version-1153"></a>版本1.15。3

[Microsoft 合作夥伴中心 .NET SDK](https://www.nuget.org/packages/Microsoft.Store.PartnerCenter/) v 1.15.3 現已正式推出。 此外，也提供更新的 REST Api 和[GitHub 範例](https://github.com/Microsoft/Partner-Center-DotNet-Samples)。 此版本包含下列變更：

* 夥伴協定
  * 新增間接提供者[驗證間接轉銷商的 Microsoft 合作夥伴合約狀態](verify-indirect-reseller-mpa-status.md)的功能。
* Products
  * 下列兩個介面不正確地放在 PartnerCenter. Products 命名空間底下。 現在，它們位於 PartnerCenter 的 [Products] 命名空間底下。
    * ICustomerProductByReservationScope
    * ICustomerSkuByReservationScope
