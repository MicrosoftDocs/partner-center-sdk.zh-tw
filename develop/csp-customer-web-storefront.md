---
title: CSP 客戶網路店面
description: 這個範例網站程式碼會顯示可供客戶購買 Microsoft 產品訂閱的工作線上商店。
ms.assetid: 0726B1CA-97A1-42E6-92AD-25787BFE0C67
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: b8e8a87e0ed22d1703b65085cf6eb9e1743c9f09
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489738"
---
# <a name="csp-customer-web-storefront"></a>CSP 客戶網路店面

適用於：

- 合作夥伴中心

> [!NOTE]
> 這個範例應用程式僅適用于合作夥伴中心的全域實例。 不適用於 Microsoft Cloud 德國的合作夥伴中心，或適用于美國政府 Microsoft Cloud 的合作夥伴中心。

[合作夥伴中心店面](https://github.com/Microsoft/Partner-Center-Storefront)是線上商店的**範例網站**，可供客戶用來購買 Microsoft 產品的訂閱。 您可以修改此**範例程式碼**，供您自己用來[設定](#configure-offers)供應專案、[新增商標](#configure-branding)並[新增付款方法](#configure-payment-types)。

## <a name="sample-code"></a>範例程式碼

從 GitHub 下載[合作夥伴中心店面範例程式碼](https://github.com/Microsoft/Partner-Center-Storefront)。

## <a name="configure-authentication"></a>設定驗證

建立應用程式之前，請先更新 Web.config 檔案中的下列值，以反映您在[合作夥伴中心驗證](partner-center-authentication.md)中建立的 Azure AD 驗證資訊。 您應該在早期開發期間使用整合沙箱帳戶設定，或在生產環境中進行測試（TiP）。

- **partnerCenter. applicationId**
- **partnerCenter. applicationSecret**
- **partnerCenter. domain**
- **Microsoft.office365.webportal. clientId**
- **Microsoft.office365.webportal. clientSecret**
- **Microsoft.office365.webportal. domain**
- **Microsoft.office365.webportal. azureStorageConnectionString**

## <a name="configure-offers"></a>設定供應專案

您可以在**OfferCatalogViewModel**中設定供應專案集（**MicrosoftOffer**）。

## <a name="configure-branding"></a>設定商標

這個範例網站會在*BrandingConfiguration.cs*和*PortalBranding.cs*中追蹤下列公司和品牌資訊：

- 組織名稱
- 組織標誌
- 標頭影像
- 隱私權合約
- 連絡人電子郵件
- 連絡人電話號碼
- 支援電子郵件
- 支援電話號碼

### <a name="configure-payment-types"></a>設定付款類型

應用程式目前使用*PayPalGateway.cs*中所實行的 PayPal 閘道。