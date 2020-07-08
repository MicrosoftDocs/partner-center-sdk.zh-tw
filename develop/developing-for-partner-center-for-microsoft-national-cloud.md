---
title: 針對適用于 Microsoft 全國雲端的合作夥伴中心進行開發
description: 合作夥伴中心 SDK 在針對 Microsoft 全國雲端進行合作夥伴中心開發時的差異。
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6220b9f89f960f6d403e88e993c7e46444374cfc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094119"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>針對適用于 Microsoft 全國雲端的合作夥伴中心進行開發

**適用範圍：**

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心有一組 SDK 檔。 不過，某些功能可能無法在 Microsoft 國家雲端的合作夥伴中心版本中使用。

開發人員必須針對下列合作夥伴中心版本考慮 SDK 的變更：

- [由 21Vianet 營運的合作夥伴中心](#partner-center-operated-by-21vianet)
- [Microsoft Cloud 德國合作夥伴中心](#partner-center-for-microsoft-cloud-germany)
- [Microsoft Cloud for US Government 適用的合作夥伴中心](#partner-center-for-microsoft-cloud-for-us-government)

每個合作夥伴中心 SDK 文章都會列出適用的合作夥伴中心版本。 每個受控參考文章也會在 [**需求**] 區段中列出適用的合作夥伴中心版本。

## <a name="partner-center-operated-by-21vianet"></a>由 21Vianet 營運的合作夥伴中心

由世紀營運的*合作夥伴中心*與*合作夥伴中心*之間的合作夥伴差異如下：

- 您無法以程式設計方式重設客戶使用者或完整合作夥伴使用者的密碼。

- 無法使用 Azure 訂用帳戶。

- 您無法管理客戶的使用者授權。 相反地，您的客戶必須使用 Office 365 系統管理中心來管理其授權。

- 所有支援要求都是透過由世紀營運的合作夥伴中心來管理。 不適用服務要求和服務更新。

## <a name="partner-center-for-microsoft-cloud-germany"></a>Microsoft Cloud 德國合作夥伴中心

> [!IMPORTANT]
> 根據客戶需求的演進，我們的德國雲端策略將著重于在德國提供與我們的全球雲端服務一致的新雲端區域。 有了這個重點，我們就不會再接受新客戶，也不會從目前可用的 Microsoft Cloud 德國部署任何新的服務。 現有的客戶可以繼續使用目前提供的目前雲端服務，我們將會維護必要的安全性更新。
>
> 未來，新客戶可以選擇使用目前可用的歐洲地區或德國的新區域。 如需詳細資訊，請參閱[Microsoft 從德國的新資料中心傳遞雲端服務](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/)。

合作夥伴*中心*與*合作夥伴中心在 Microsoft Cloud 德國*之間的差異如下：

- 合作夥伴無法為其客戶的組織建立使用者，也無法指派角色。
  - 合作夥伴可以讀取欄位，但無法寫入或更新它們。
  - 合作夥伴必須在 Office 365 系統管理中心或透過 Azure 入口網站手動建立或更新其客戶的使用者。 請參閱[Azure Active Directory 檔](https://docs.microsoft.com/azure/active-directory/)。

- 您無法使用 Microsoft Cloud 德國入口網站或 Api 的合作夥伴中心，來管理客戶使用者的授權。 相反地，您必須使用 Office 365 系統管理中心或 Azure Active 直接群組授權管理（即將推出）來管理其授權。
  - （選擇性）您可以使用 Azure AD 圖形 API。 請參閱[新增或移除使用者的授權](https://msdn.microsoft.com/library/azure/ad/graph/api/functions-and-actions#assignLicense)。 針對 Microsoft Cloud 德國的合作夥伴中心，請務必使用圖形端點， `https://graph.cloudapi.de` 而不是 `https://graph.windows.net` 。

- 您無法以程式設計方式重設客戶使用者或完整合作夥伴使用者的密碼。 使用 Office 365 系統管理中心或 Azure 入口網站。 請參閱[在 Azure Active Directory 中重設使用者的密碼](https://azure.microsoft.com/documentation/articles/active-directory-users-reset-password-azure-portal/)。 針對步驟1，您必須登入 Microsoft Cloud 德國的 Azure 入口網站。

- 開發人員必須手動註冊其應用程式識別碼，以便將合作夥伴中心 API/SDK 功能整合到其應用程式中，以供 Microsoft Cloud 德國的合作夥伴中心。 如需詳細資訊，請參閱[註冊 Microsoft 國家雲端合作夥伴中心的應用程式詳細資料](https://docs.microsoft.com/partner-center/develop/create-apps-for-partner-center-for-microsoft-national-clouds)。

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴*中心*與*合作夥伴中心之間針對美國政府 Microsoft Cloud*的合作夥伴差異如下：

- Office 365 訂閱目前無法供美國政府的 Microsoft Cloud 合作夥伴中心使用。

- 支援美國政府 Microsoft Cloud 的現有合作夥伴，必須在合作夥伴中心為美國政府 Microsoft Cloud 建立新的帳戶。

- 適用于美國政府客戶的 Microsoft Cloud 必須與單一合作夥伴交易。
  - 在美國政府案例的 Microsoft Cloud 中，與現有客戶的多重通道和 multipartner 和要求關聯性不適用。 這項限制是因為目前無法使用 Office 365。

- 合作夥伴無法為其客戶的組織建立使用者，也無法指派角色。
  - 合作夥伴可以讀取欄位，但無法寫入或更新它們。 合作夥伴必須在 Azure 入口網站中手動建立或更新其客戶的使用者。 請參閱[Azure Active Directory 檔](https://docs.microsoft.com/azure/active-directory/)。

- 您無法以程式設計方式重設客戶使用者或完整合作夥伴使用者的密碼。 使用 Azure 入口網站。 請參閱[在 Azure Active Directory 中重設使用者的密碼](https://docs.microsoft.com/azure/active-directory/active-directory-users-reset-password-azure-portal)。 針對步驟1，您必須登入適用于美國政府 Microsoft Cloud 的 Azure 入口網站。

- 適用于美國政府之合作夥伴中心的 REST 端點，與合作夥伴中心的 Microsoft Cloud 相同： `https://api.partnercenter.microsoft.com` 。

- 開發人員必須手動註冊其應用程式識別碼，以便將合作夥伴中心 API/SDK 功能整合到其應用程式中，以供美國政府的 Microsoft Cloud 合作夥伴中心。 如需詳細資訊，請參閱[註冊 Microsoft 國家雲端合作夥伴中心的應用程式詳細資料](https://docs.microsoft.com/partner-center/develop/create-apps-for-partner-center-for-microsoft-national-clouds)。
