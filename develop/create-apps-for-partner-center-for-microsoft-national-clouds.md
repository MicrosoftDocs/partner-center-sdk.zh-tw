---
title: 註冊適用于 Microsoft 國家雲端合作夥伴中心的應用程式詳細資料
description: 開發人員必須透過 Azure 入口網站，向 Azure AD 註冊其應用程式的詳細資料。 這可協助確保只有指定的應用程式能夠連接到合作夥伴和客戶資料。
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 48eb5bf8c9fe473ae6fabe88ad2cc0767852dbe6
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90927860"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud"></a>註冊適用于 Microsoft 國家雲端合作夥伴中心的應用程式詳細資料

**適用於：**

- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

開發人員必須透過 Azure 入口網站，向 Azure AD 註冊其應用程式的詳細資料。 這可協助確保只有指定的應用程式能夠連接到合作夥伴和客戶資料。

針對 Microsoft Cloud for US Government 的合作夥伴中心，您目前必須透過 PowerShell 管理應用程式。 如需詳細資訊，請參閱 [Azure PowerShell 參考檔](/powershell/module/Azuread/?view=azureadps-2.0#applications)。

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

當您建立適用于 Microsoft Cloud 德國合作夥伴中心的應用程式，或 Microsoft Cloud for US Government 的合作夥伴中心時，請注意下列其他需求。

## <a name="web-apps"></a>Web 應用程式

針對 web 應用程式，請使用下列程式來註冊您的應用程式識別碼。

### <a name="create-or-update-web-app"></a>建立或更新 web 應用程式

1. 流覽至 [ [Azure 入口網站應用程式註冊](https://go.microsoft.com/fwlink/?linkid=2083908) ] 頁面以註冊您的應用程式。 使用工作或學校帳戶或個人 Microsoft 帳戶登入 Azure 入口網站。

2. 選取 [新增註冊]。 如需詳細資訊，請參閱 [快速入門：使用 Microsoft 身分識別平臺註冊應用程式](/azure/active-directory/develop/quickstart-register-app)。

### <a name="configure-api-access-permissions-for-web-app"></a>設定 web 應用程式的 API 存取權限

1. 選擇您的應用程式。 移至 Web 應用程式的 [ **設定** ]。

2. 在 [ **API 存取**] 區段中，選擇 [**必要許可權**]

3. 適用于 Windows Azure Active directory 許可權：

    1. 選擇 [ **Windows Azure Active Directory 許可權**。

    2. 在 [ **應用程式許可權**] 中，選取 [讀取目錄資料]。

    3. 儲存許可權。

4. 請記下 web 應用程式的 [ **屬性** ] 區段中的應用程式識別碼。

### <a name="add-a-secret-key-to-your-app"></a>將秘密金鑰新增到您的應用程式。

1. 移至 web 應用程式的 [ **金鑰** ] 區段。

2. 輸入金鑰描述，並依您的需求選取 [持續時間] 為1或2年。

3. 儲存並複製秘密金鑰值。 **一旦您離開此頁面，就不會再次顯示此值。**

您應該會有來自 web 應用程式設定的下列詳細資料：

- 應用程式識別碼
- 應用程式祕密

### <a name="register-the-web-app-in-partner-center"></a>在合作夥伴中心中註冊 Web 應用程式

1. 登入 [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) 。

2. 選擇 [ **儀表板**]，然後選擇 [ **帳戶設定**]，再選擇 [ **應用程式管理**]。

3. 在 [ **Web 應用程式** ] 區段中，選擇 [ **註冊現有的應用程式**]。

4. 選取您在 Azure 入口網站中建立的 web 應用程式。

5. 選擇 [ **註冊您的應用程式**]。

## <a name="native-apps"></a>原生應用程式

原生應用程式不需要註冊就能合作夥伴中心。 但這些應用程式必須設定為提供合作夥伴中心 Api 的存取權。

>[!NOTE]
>在 Azure 入口網站中建立原生應用程式之前，請使用合作夥伴租使用者中的系統管理使用者認證登入合作夥伴中心。 這會在租使用者上建立設定，以啟用應用程式許可權。

### <a name="create-native-app"></a>建立原生應用程式

1. 流覽至 [ [Azure 入口網站應用程式註冊](https://go.microsoft.com/fwlink/?linkid=2083908) ] 頁面以註冊您的應用程式。 使用工作或學校帳戶或個人 Microsoft 帳戶登入 Azure 入口網站。

2. 選取 [新增註冊]。 如需詳細資訊，請參閱 [快速入門：使用 Microsoft 身分識別平臺註冊應用程式](/azure/active-directory/develop/quickstart-register-app)。

### <a name="configure-api-access-permissions-for-native-app"></a>設定原生應用程式的 API 存取權限

1. 選擇您的應用程式。 移至 [設定] 。

2. 在 [API 存取] 中，選擇 [ **必要許可權**]。

3. 選擇 [ **Windows Azure Active Directory 許可權**。 在 [ **委派的許可權**] 中，選取下列許可權：

    - **登入和讀取使用者設定檔**
    - **讀取目錄資料**
    - **以登入的使用者身分存取目錄**
    - **讀取所有群組**

4. 儲存許可權。

5. 選擇**Add** [加入**必要的許可權**]。

6. 選擇 [選取 API]****。

    1. 在搜尋方塊中，輸入 **Microsoft 合作夥伴中心** ，然後從結果清單中選取它。

    2. 選擇 [選取]  。

7. 選擇 [選取權限]****。

    1. 選取 **合作夥伴中心 PPE 的存取權**。
    
    2. 選擇 [選取]  。

8. 選擇 [完成]。

>[!IMPORTANT]
> 請注意應用程式屬性中的應用程式識別碼。

您不需要在合作夥伴中心中註冊原生應用程式，但原生應用程式必須是系統管理員的同意。 請注意您原生應用程式的應用程式識別碼。
