---
title: 開始使用
description: 合作夥伴中心 SDK 包含受控 API 和 REST API，可供合作夥伴用來管理客戶、訂用帳戶和訂單資料。
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9c2af1e11dbda19489a27e37c7f3de8ede90fd1c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86097568"
---
# <a name="get-started"></a>開始使用

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

合作夥伴中心 SDK 包含受控 API 和 REST API，可供合作夥伴用來管理客戶、訂用帳戶和訂單資料。

## <a name="get-the-code"></a>取得程式碼

[下載合作夥伴中心 SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681)

> [!NOTE]
> 適用於間接轉銷商的合作夥伴中心不支援 API 存取。

## <a name="determine-your-version-of-partner-center"></a>判斷您的合作夥伴中心版本

某些合作夥伴中心版本沒有完整的 SDK 可供使用。 如需詳細資訊，請參閱[針對 Microsoft 國家/地區雲端的合作夥伴中心進行開發](developing-for-partner-center-for-microsoft-national-cloud.md)。

## <a name="get-the-samples"></a>取得範例

如需有關 C# 程式碼片段、REST 範例和範例應用程式的詳細資訊，請參閱[合作夥伴中心範例](partner-center-samples.md)。

## <a name="test-vs-production"></a>測試環境與生產環境

開始撰寫和測試程式碼時，您應使用整合沙箱帳戶 (以及對應的權杖)，如此就不會意外產生公司需負責付費的新費用。 如需此測試環境的詳細資訊，請參閱[在合作夥伴中心設定 API 存取](set-up-api-access-in-partner-center.md)。

當您的解決方案經過測試並準備好在實際客戶帳戶上使用時，您必須更新您的權杖，以使用與主要合作夥伴中心帳戶對應的 Azure AD 用戶端應用程式和祕密。

如需有關測試和偵錯的秘訣和建議 (包括有關生產環境測試 (TiP) 和整合沙箱的詳細資訊)，請參閱[測試與偵錯](test-and-debug.md)。

## <a name="configure-your-authentication"></a>設定您的驗證

若要設定您的 Azure AD 驗證，讓您可以使用合作夥伴中心 API，請參閱[合作夥伴中心驗證](partner-center-authentication.md)。

> [!IMPORTANT]
> Microsoft 正在引進能透過 Microsoft Azure 多重要素驗證 (MFA) 架構來驗證雲端解決方案提供者 (CSP) 合作夥伴和控制台廠商 (CPV) 的安全可擴充架構。
合作夥伴中心會使用 Azure AD 進行驗證，並使用合作夥伴中心 API，確保您正確地完成驗證設定。
>
> 如需詳細資訊，請參閱[啟用安全應用程式模型](enable-secure-app-model.md)。

## <a name="get-help"></a>取得說明

合作夥伴可以在[合作夥伴中心 SDK Yammer 群組](https://go.microsoft.com/fwlink/p/?LinkID=717360)中取得支援。 若要取得更個人化的協助，開發人員可以使用其 MPN 支援權益或頂級支援。

## <a name="join-the-partner-center-api-and-sdk-early-adopter-program"></a>加入合作夥伴中心 API 及 SDK 早期採用者計畫

若要了解如何在開發合作夥伴功能上與 Microsoft 合作，請參閱[加入合作夥伴中心 API 及 SDK 早期採用者計畫](early-adopter-program.md)。
