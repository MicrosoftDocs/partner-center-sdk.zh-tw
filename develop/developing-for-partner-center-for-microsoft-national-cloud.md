---
title: 適用于 Microsoft 國家雲端的合作夥伴中心開發
description: 針對 Microsoft 國家雲端的合作夥伴中心進行開發時合作夥伴中心 SDK 差異。
MS-HAID:
- pc\_apiv2.developing\_with\_different\_partner\_center\_versions
- pc\_apiv2.developing\_for\_partner\_center\_for\_microsoft\_national\_cloud
ms.date: 06/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8ba9b639b56333bf4a8c2ebc259a67c89de79cee
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927328"
---
# <a name="developing-for-partner-center-for-microsoft-national-clouds"></a>適用于 Microsoft 國家雲端的合作夥伴中心開發

**適用於：**

- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心有一組 SDK 檔。 不過，某些功能可能無法在 Microsoft 國家雲端的合作夥伴中心版本中使用。

開發人員必須考慮下列合作夥伴中心版本的 SDK 變更：

- [由 21Vianet 營運的合作夥伴中心](#partner-center-operated-by-21vianet)
- [Microsoft Cloud 德國合作夥伴中心](#partner-center-for-microsoft-cloud-germany)
- [Microsoft Cloud for US Government 適用的合作夥伴中心](#partner-center-for-microsoft-cloud-for-us-government)

每篇合作夥伴中心 SDK 文章會列出適用的合作夥伴中心版本。 每個受控參考文章也會列出 [ **需求** ] 區段中適用的合作夥伴中心版本。

## <a name="partner-center-operated-by-21vianet"></a>由 21Vianet 營運的合作夥伴中心

*由世紀**合作夥伴中心*與合作夥伴中心之間的夥伴之間的差異如下：

- 您無法以程式設計方式重設客戶使用者或完整夥伴使用者的密碼。

- 無法使用 Azure 的訂用帳戶。

- 您無法為客戶的使用者管理授權。 相反地，您的客戶必須使用 Office 365 系統管理中心來管理他們的授權。

- 所有支援要求都是透過由世紀經營的合作夥伴中心來管理。 服務要求和服務更新不適用。

## <a name="partner-center-for-microsoft-cloud-germany"></a>Microsoft Cloud 德國合作夥伴中心

> [!IMPORTANT]
> 根據客戶的需求演進，我們的德國雲端策略將著重于在德國與全球雲端供應專案一致的新雲端區域。 透過此焦點，我們將不再接受新的客戶，或從目前可用的 Microsoft Cloud 德國部署任何新的服務。 現有的客戶可以繼續使用目前可用的雲端服務，我們將會維護必要的安全性更新。
>
> 未來，新客戶可以選擇使用目前可用的歐洲地區或德國的新區域（當其可用時）。 如需詳細資訊，請參閱 [Microsoft 從德國的新資料中心提供雲端服務](https://news.microsoft.com/europe/2018/08/31/microsoft-to-deliver-cloud-services-from-new-datacentres-in-germany-in-2019-to-meet-evolving-customer-needs/)。

*Microsoft Cloud 德國**合作夥伴中心*與合作夥伴中心之間的夥伴差異如下：

- 合作夥伴無法為其客戶的組織建立使用者或指派角色。
  - 夥伴可以讀取欄位，但無法寫入或更新它們。
  - 合作夥伴必須在 Office 365 系統管理中心或透過 Azure 入口網站手動建立或更新客戶的使用者。 請參閱 [Azure Active Directory 檔](/azure/active-directory/)。

- 您無法使用 Microsoft Cloud 德國入口網站或 Api 的合作夥伴中心來管理客戶使用者的授權。 相反地，您必須立即使用 Office 365 系統管理中心或 Azure Active 直接群組授權管理 (即將推出) 管理其授權。
  -  (選擇性) 您可以使用 Azure AD 圖形 API。 請參閱 [新增或移除使用者的授權](https://msdn.microsoft.com/library/azure/ad/graph/api/functions-and-actions#assignLicense)。 針對 Microsoft Cloud 德國的合作夥伴中心，請務必使用圖形端點， `https://graph.cloudapi.de` 而不是 `https://graph.windows.net` 。

- 您無法以程式設計方式重設客戶使用者或完整夥伴使用者的密碼。 使用 Office 365 系統管理中心或 Azure 入口網站。 請參閱 [在 Azure Active Directory 中重設使用者的密碼](https://azure.microsoft.com/documentation/articles/active-directory-users-reset-password-azure-portal/)。 在步驟1中，您必須登入 Microsoft Cloud 德國的 Azure 入口網站。

- 開發人員必須手動註冊其應用程式識別碼，以在其應用程式中整合合作夥伴中心 API/SDK 功能，以供 Microsoft Cloud 德國合作夥伴中心。 如需詳細資訊，請參閱 [註冊 Microsoft 國家雲端合作夥伴中心的應用程式詳細資料](/partner-center/develop/create-apps-for-partner-center-for-microsoft-national-clouds)。

## <a name="partner-center-for-microsoft-cloud-for-us-government"></a>Microsoft Cloud for US Government 適用的合作夥伴中心

Microsoft Cloud for US Government 的 *合作夥伴中心* 和 *合作夥伴中心* 之間的夥伴差異如下：

- Office 365 訂閱目前無法用於 Microsoft Cloud for US Government 的合作夥伴中心。

- 支援 Microsoft Cloud for US Government 的現有合作夥伴必須在合作夥伴中心中為 Microsoft Cloud for US Government 建立新的帳戶。

- Microsoft Cloud for US Government 客戶必須與單一夥伴交易。
  - 在 Microsoft Cloud for US Government 案例中，與現有客戶的多重通道和 multipartner 和要求關聯性並不適用。 這項限制是因為目前無法使用 Office 365。

- 合作夥伴無法為其客戶的組織建立使用者或指派角色。
  - 夥伴可以讀取欄位，但無法寫入或更新它們。 合作夥伴必須在 Azure 入口網站中手動建立或更新客戶的使用者。 請參閱 [Azure Active Directory 檔](/azure/active-directory/)。

- 您無法以程式設計方式重設客戶使用者或完整夥伴使用者的密碼。 使用 Azure 入口網站。 請參閱 [在 Azure Active Directory 中重設使用者的密碼](/azure/active-directory/active-directory-users-reset-password-azure-portal)。 在步驟1中，您必須登入 Microsoft Cloud for US Government 的 Azure 入口網站。

- Microsoft Cloud for US Government 的合作夥伴中心 REST 端點與合作夥伴中心：相同 `https://api.partnercenter.microsoft.com` 。

- 開發人員必須手動註冊其應用程式識別碼，才能在其應用程式中整合合作夥伴中心 API/SDK 功能，以進行 Microsoft Cloud for US Government 的合作夥伴中心。 如需詳細資訊，請參閱 [註冊 Microsoft 國家雲端合作夥伴中心的應用程式詳細資料](/partner-center/develop/create-apps-for-partner-center-for-microsoft-national-clouds)。
