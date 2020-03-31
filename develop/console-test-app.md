---
title: 主控台測試應用程式
description: 此主控台測試應用程式會針對合作夥伴中心 Api 支援的所有案例提供範例程式碼。 您也可以使用它來進行測試。
ms.assetid: 56F5B4C6-CE87-4D13-9D8C-09F38E946292
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 35ebb92e8e9705cbce8c629d0a862613cc2f50b6
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412854"
---
# <a name="console-test-app"></a>主控台測試應用程式

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

主控台測試應用程式是在和C# JAVA 中提供，它會針對合作夥伴中心 api 支援的所有案例提供範例程式碼。 您也可以使用它來進行測試。

## <a name="get-the-code"></a>取得程式碼

下載主控台測試應用程式的範例程式碼。

## <a name="net"></a>.NET

[下載範例程式碼](https://go.microsoft.com/fwlink/p/?LinkId=746682)，並視需要加以修改。

> [!IMPORTANT]
> 建立應用程式之前，請更新*app.config*檔案中的值，以反映您在[合作夥伴中心驗證](partner-center-authentication.md)中建立的 Azure AD 驗證資訊。 具體而言，您應該在早期開發期間使用整合沙箱帳戶設定，或在生產環境中進行測試。

在*app.config*檔案的**ScenarioSettings**下，您可以設定將自動傳遞至您執行之案例的參數。

若要修改執行的案例清單，請將 IPartnerScenario\[中的程式程式碼批註 **\] mainScenarios** ，或在*Program.cs*檔案中找到的個別**Get 情節**方法中。

## <a name="java"></a>Java

[!INCLUDE [<Partner Center Java SDK support details>](<../includes/java-sdk-support.md>)]

[下載範例程式碼](https://go.microsoft.com/fwlink/p/?LinkId=2026887)，並視需要加以修改。

> [!IMPORTANT]
> 在您建立應用程式之前，請先更新*SamplesConfigurations*中的值，以反映您在[合作夥伴中心驗證](partner-center-authentication.md)中建立的 Azure AD 驗證資訊。 具體而言，您應該在早期開發期間使用整合沙箱帳戶設定，或在生產環境中進行測試。

在*SamplesConfiguration*檔案的**ScenarioSettings**下，您可以設定將自動傳遞至您執行之案例的參數。

若要修改執行的案例清單，請將 IPartnerScenario\[中的程式程式碼批註 **\] mainScenarios** ，或在*Program. java*檔案中找到的個別**Get 案例**方法中。

## <a name="what-to-change"></a>要變更的內容

使用下列清單來決定要在範例程式碼中變更或不變更的內容。

### <a name="partnerservicesettings"></a>PartnerServiceSettings

針對**PartnerServiceSettings**，請勿變更：

- **PartnerServiceApiEndpoint**
- **AuthenticationAuthorityEndpoint**
- **GraphEndpoint**
- **CommonDomain**

所有這些設定都是範例 API 呼叫正常運作所需的一切。

### <a name="userauthentication"></a>UserAuthentication

針對**UserAuthentication**，您必須變更：

- **ApplicationId** （您用來登入的 Azure Active Directory 應用程式識別碼）
- **Username** （您的 active directory 使用者名稱）
- **密碼**（您的 active directory 密碼）。

不要變更：

- **ResourceUrl**
- **RedirectUrl**

### <a name="appauthentication"></a>AppAuthentication

針對**AppAuthentication**，您必須變更：

- **ApplicationId** （您用於應用程式登入的 active directory 應用程式識別碼）
- **ApplicationSecret** （您用於應用程式登入的 active directory 應用程式秘密）
- **網域**（主控應用程式的 active directory 網域）

### <a name="scenariosettings"></a>ScenarioSettings

針對**ScenarioSettings**，請勿變更：

- **CustomerDomainSuffix** （建立新客戶時使用的網域尾碼）

選擇性設定。 如果保留空白，當您在必要時執行案例時，就必須輸入此資訊：

- **CustomerIdToDelete** （用來刪除的客戶識別碼）
- **DefaultCustomerId** （要在客戶相關案例中使用的客戶識別碼）
- **DefaultInvoiceID** （要在發票案例中使用的發票識別碼）
- **PartnerMpnId** （要在間接合作夥伴案例中使用的合作夥伴 MPN 識別碼）
- **DefaultServiceRequestId** （要在服務要求案例中使用的服務要求識別碼）
- **DefaultSupportTopicID** （要在服務要求案例中使用的支援主題識別碼）
- **DefaultOfferID** （供應專案案例中要使用的供應專案識別碼）
- **DefaultOrderID** （訂單識別碼，用於訂單案例）
- **DefaultSubscriptionID** （要在訂用帳戶案例中使用的訂用帳戶識別碼）

選擇性變更。 所有這些設定都會在抓取分頁內容時，指定每頁的專案數量：

- **CustomerPageSize**
- **InvoicePageSize**
- **ServiceRequestPageSize**
- **DefaultOfferPageSize**
- **SubscriptionPageSize**