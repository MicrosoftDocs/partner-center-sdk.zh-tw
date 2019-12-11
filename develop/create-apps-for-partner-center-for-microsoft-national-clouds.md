---
title: 為 Microsoft 國家雲端的合作夥伴中心註冊應用程式詳細資料
description: 開發人員必須透過 Azure 入口網站向 Azure AD 註冊其應用程式的詳細資料。 這有助於確保只有指定的應用程式能夠連接到合作夥伴和客戶資料。
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.assetid: 73C5926A-0DEB-42E5-8982-7E44A2031F0B
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ede0ba85851e4d450d4f28832cd46064d2786d2d
ms.sourcegitcommit: 7e5e3590931010eb0e0fef3e7f6d5d7d084a69ba
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/10/2019
ms.locfileid: "74995253"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud"></a>為 Microsoft 國家雲端的合作夥伴中心註冊應用程式詳細資料

適用於：

- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

開發人員必須透過 Azure 入口網站向 Azure AD 註冊其應用程式的詳細資料。 這有助於確保只有指定的應用程式能夠連接到合作夥伴和客戶資料。

針對適用于美國政府的 Microsoft Cloud 合作夥伴中心，您目前必須透過 PowerShell 管理應用程式。 如需詳細資訊，請參閱[Azure PowerShell 參考檔](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0#applications)。

[!INCLUDE [<Partner Center PowerShell module support details>](<../includes/powershell-module-support.md>)]

當您為美國政府的 Microsoft Cloud Microsoft Cloud 德國或合作夥伴中心建立適用于合作夥伴中心的應用程式時，請注意下列其他需求。

## <a name="web-apps"></a>Web 應用程式

針對 web 應用程式，請使用下列程式來註冊您的應用程式識別碼。

### <a name="create-or-update-web-app"></a>建立或更新 web 應用程式

1. 流覽至 [ [Azure 入口網站應用程式註冊](https://go.microsoft.com/fwlink/?linkid=2083908)] 頁面，註冊您的應用程式。 使用工作或學校帳戶或個人 Microsoft 帳戶登入 Azure 入口網站。

2. 選取 [新增註冊]。 如需詳細資訊，請參閱[快速入門：使用 Microsoft 身分識別平臺註冊應用程式](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app)。

### <a name="configure-api-access-permissions-for-web-app"></a>設定 web 應用程式的 API 存取權限

1. 選擇您的應用程式。 移至 Web 應用程式的 [**設定**]。
2. 在 [ **API 存取**] 區段中，選擇 [**必要許可權**]
3. 針對 Windows Azure Active directory 許可權：
    1. 選擇 [ **Windows Azure Active Directory 許可權**]。
    2. 在 [**應用程式許可權**] 中，選取 [讀取目錄資料]。
    3. 儲存許可權。
4. 請注意 web 應用程式的 [**屬性**] 區段中的 [應用程式識別碼]。

### <a name="add-a-secret-key-to-your-app"></a>將秘密金鑰新增到您的應用程式。

1. 移至 web 應用程式的 [**金鑰**] 區段。
2. 輸入 [金鑰描述]，並視需要選取 [持續時間] （1或2年）。
3. 儲存並複製 [秘密金鑰] 值。 **一旦您離開此頁面，就不會再顯示此值。**

您應該會有來自 web 應用程式設定的下列詳細資料：

- 應用程式識別碼
- 應用程式祕密

### <a name="register-the-web-app-in-partner-center"></a>在合作夥伴中心註冊 Web 應用程式

1. 登入 <https://partnercenter.microsoft.com>。
2. 選擇 [**儀表板**]，然後依序選擇 [**帳戶設定**] 和 [**應用程式管理**]。
3. 在 [ **Web 應用程式**] 區段中，選擇 [**註冊現有的應用程式**]。
4. 選取您在 Azure 管理入口網站中建立的 web 應用程式。
5. 選擇 [**註冊您的應用程式**]。

## <a name="native-apps"></a>原生應用程式

原生應用程式不需要註冊至合作夥伴中心。 但這些應用程式必須設定為提供合作夥伴中心 Api 的存取權。

>[!NOTE]
>在 Azure 管理入口網站中建立原生應用程式之前，請使用合作夥伴租使用者的系統管理員使用者認證登入合作夥伴中心。 這會在租使用者上建立設定以啟用應用程式許可權。

### <a name="create-native-app"></a>建立原生應用程式

1. 流覽至 [ [Azure 入口網站應用程式註冊](https://go.microsoft.com/fwlink/?linkid=2083908)] 頁面，註冊您的應用程式。 使用工作或學校帳戶或個人 Microsoft 帳戶登入 Azure 入口網站。

2. 選取 [新增註冊]。 如需詳細資訊，請參閱[快速入門：使用 Microsoft 身分識別平臺註冊應用程式](https://docs.microsoft.com/azure/active-directory/develop/quickstart-register-app)。

### <a name="configure-api-access-permissions-for-native-app"></a>設定原生應用程式的 API 存取權限

1. 選擇您的應用程式。 移至 [設定]。
2. 在 [API 存取] 中，選擇 [**必要許可權**]。
3. 選擇 [ **Windows Azure Active Directory 許可權**]。 在 [**委派的許可權**] 中，選取下列許可權：
    - **登入和讀取使用者設定檔**
    - **讀取目錄資料**
    - **以登入的使用者身分存取目錄**
    - **讀取所有群組**
4. 儲存許可權。
5. 選擇 [**新增**] [**必要許可權**]。
6. 選擇 [選取 API]。
    1. 在搜尋方塊中，輸入**Microsoft 合作夥伴中心**，然後從結果清單中選取它。
    2. 選擇 [選取]。
7. 選擇 [選取權限]。
    1. 選取 [**存取合作夥伴中心 PPE**]。
    2. 選擇 [選取]。
8. 選擇 [**完成**]。

>[!IMPORTANT]
> 請注意您應用程式屬性中的應用程式識別碼。

您不需要在合作夥伴中心註冊原生應用程式，但原生應用程式必須是系統管理員同意。 請記下原生應用程式的應用程式識別碼。