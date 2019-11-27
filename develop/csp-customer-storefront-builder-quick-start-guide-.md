---
title: CSP 客戶店面 Builder 快速入門手冊
description: 建立線上 marketplace，使用 CSP 客戶店面 Builder 來銷售雲端解決方案提供者（CSP）供應專案。
ms.assetid: 333EE80D-E49E-4E89-87FB-3F02AC48C236
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 2b36d1f64a9ab02483832674997c66e3fbffd36e
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74489728"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>CSP 客戶店面 Builder 快速入門手冊

適用於：

- 合作夥伴中心

建立線上 marketplace，使用 CSP 客戶店面 Builder 來銷售雲端解決方案提供者（CSP）供應專案。

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>CSP 客戶店面 Builder 簡介

CSP 客戶店面產生器可協助合作夥伴輕鬆地建立線上 marketplace，將 CSP 供應專案銷售給客戶。 大部分的合作夥伴和小型銷售組織都想要專注于銷售，而不是開發線上 marketplace。 合作夥伴中心 SDK 範例應用程式需要軟體發展技能，才能建立及部署網站。 有了 CSP 客戶店面 Builder，您就可以快速且輕鬆地建立自己的網站。 您也可以將網站下載為範例程式碼，或使用準備好交易的網站直接部署到 Azure 訂用帳戶。

此網站是由合作夥伴完整擁有、支援及維護，而且 Microsoft 不會從網站收集任何資料或遙測。 CSP 客戶店面 Builder 會為合作夥伴建立一個與[支付卡產業資料安全標準](https://www.pcisecuritystandards.org/)（PCI DSS）完全相容的網站。

CSP 客戶店面產生器程式碼受限於[合作夥伴中心 SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)中提供的授權。

>[!NOTE]
>您必須負責店面網站管理、維護，以及任何可能因網站建立而產生的問題。 閱讀並瞭解[合作夥伴中心 SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)中的條款。

如需其他資訊，另請參閱下列主題： [CSP 客戶 web 店面](csp-customer-web-storefront.md)和[主控台測試應用程式](console-test-app.md)。

## <a name="considerations"></a>考量

CSP 客戶店面產生器是用來建立網站的快速方式。 在規劃期間，請注意下列考慮：

- 一旦部署後，Microsoft 和合作夥伴中心不會維護合作夥伴網站的複本，或任何新增至 CSP 客戶店面建立器的資訊。
- 合作夥伴中心只能將 CSP 客戶店面網站部署至合作夥伴的 Azure 訂用帳戶。
- 此網站一經部署，就完全由合作夥伴所擁有及管理。 Microsoft 無法存取此網站或任何與網站相關的資料。 合作夥伴負責維護及管理網站。 Microsoft 不會提供任何即時網站或其他與 CSP 客戶店面建立者相關的支援，或使用 CSP 客戶店面產生器所建立的任何網站。
- 合作夥伴中心無法使用新的或已變更的 SDK 或 API 功能，直接存取或升級此網站。 所有新功能或增強功能都必須由合作夥伴所擁有、開發及管理，包括新增合作夥伴中心 SDK 或 API 功能。
- 此 CSP 客戶店面產生器目前提供設定 PayPal Pro/PayU Money （印度）帳戶付款的功能。 如果合作夥伴需要變更付款處理器，他們將需要變更程式碼，以支援其慣用的付款方法。
- CSP 客戶店面產生器中新增的任何付款相關資訊，都不會儲存或保留在合作夥伴中心。
- PayPal 付款設定適用于任何可使用 PayPal 的地理位置。 PayPal 可用性和支援僅由 PayPal 控制，並可隨時因 PayPal 而中止。
- PayU 付款設定目前僅適用于印度。 PayU 可用性和支援僅由 PayU 控制，並可在 PayU 時隨時停止。
- 閱讀並瞭解[合作夥伴中心 SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)中的條款。

## <a name="using-the-csp-customer-storefront-builder"></a>使用 CSP 客戶店面 Builder

合作夥伴中心的 CSP 合作夥伴管理員可以直接從合作夥伴中心部署 CSP 客戶店面。 有了最少的工作，就可以在合作夥伴的租使用者上部署新的網站。 一旦部署後，合作夥伴可以使用網站來設定商標、供應專案和付款相關資訊，然後與客戶共用網站 URL 位址。

建立店面網站的流程是：

1. [部署網站](#deploy)
2. [設定店面](#configure)
3. [店面上的交易](#transact)

### <a name="deploy"></a>部署

部署選項：

- 從合作夥伴中心部署您的網站
- 與 Azure 整合以部署已設定的網站
- 在現有的訂用帳戶上部署或攜帶您自己的訂用帳戶

### <a name="configure"></a>設定

自訂店面不需要任何開發技能。

使用您的合作夥伴中心系統管理員認證登入，以設定：

- **商標**：公司名稱、標誌、連絡人等等。
- 供應**專案：查看**所有 CSP 供應專案。 您可以選取您的客戶可以查看和購買的供應專案。 您也可以將供應專案資訊個人化，並增加您的價格。
- **Paypal 付款**設定：新增您的 PayPal 付款帳戶資訊。 如果您沒有 PayPal 帳戶，可以造訪 <https://www.paypal.com> 並建立新的帳戶。 此帳戶將用於 PayPal，以取得客戶的付款。 *Microsoft 對於合作夥伴和 PayPal 之間的關係概不負責。使用 PayPal 可能需要合作夥伴或合作夥伴的客戶同意其他條款。*
- （*印度*）**PayU 付款**設定：新增您的 PayU Money 付款帳戶資訊。 如果您沒有 PayU Money 帳戶，可以造訪 <https://www.payumoney.com/> 並建立新的帳戶。 此帳戶將用於 PayU，以取得客戶的付款。 *Microsoft 對於合作夥伴和 PayU 之間的關係概不負責。使用 PayU 可能需要合作夥伴或合作夥伴的客戶同意其他條款。*

### <a name="transact"></a>辦理

- 部署之後，客戶可以立即購買和交易。
- 客戶可以直接從與合作夥伴中心 SDK 整合的合作夥伴入口網站購買。

#### <a name="customer-countries"></a>客戶國家/地區

客戶可以隸屬于這些國家/地區：

| 國碼 (地區碼) | 國家/地區名稱   |
|--------------|----------------|
| AU           | 澳大利亞      |
| AT           | 奧地利        |
| BE           | 比利時        |
| BG           | 保加利亞       |
| CA           | 加拿大         |
| HR           | 克羅埃西亞        |
| CY           | 賽普勒斯         |
| CZ           | 捷克共和國 |
| DK           | 丹麥        |
| EE           | 愛沙尼亞        |
| FI           | 芬蘭        |
| FR           | 法國         |
| DE           | 德國        |
| GR           | 希臘         |
| HU           | 匈牙利        |
| IS           | 冰島        |
| IN           | 印度          |
| IE           | 愛爾蘭        |
| IT           | 義大利          |
| JP           | 日本          |
| LV           | 拉脫維亞         |
| L           | 列支敦斯登  |
| LT           | 立陶宛      |
| LU           | 盧森堡     |
| MT           | 馬爾他          |
| [MC]           | 摩納哥         |
| NL           | 荷蘭    |
| NZ           | 紐西蘭    |
| 否           | 挪威         |
| 郵政           | 波蘭         |
| PT           | 葡萄牙       |
| RO           | 羅馬尼亞        |
| SK           | 斯洛伐克       |
| SL           | 斯洛維尼亞       |
| ES           | 西班牙          |
| SE           | 瑞典         |
| CH           | 瑞士    |
| GB           | 英國 |
| 美國           | 美國  |

### <a name="additional-resources"></a>其他資源

若要增強或自訂您的 CSP 客戶店面：

- 下載[合作夥伴中心店面範例程式碼](https://github.com/Microsoft/Partner-Center-Storefront)以進行其他自訂。
- 使用 Microsoft Visual Studio 2015 （或更新版本）進行開發。
- 建立額外的變更和增強功能（包括授權、認證、資訊清單變更和其他專案）。

## <a name="partner-experience-scenarios"></a>合作夥伴體驗案例

### <a name="deployment-scenario"></a>部署案例

- 合作夥伴系統管理員可以使用合作夥伴中心來部署網站。 在 [帳戶設定] 中，選擇 [ **Web 店面**] 部署新的網站。
- 在此頁面上，合作夥伴可以查看新網站名稱的可用性，並加以變更（如果有的話）。
- 此頁面會顯示與此合作夥伴租使用者相關聯的所有作用中 Azure 訂用帳戶，以及合作夥伴可以選擇用來部署網站的訂用帳戶。
- 如果合作夥伴沒有與此合作夥伴中心帳戶相關聯的作用中訂用帳戶，他們可以將此帳戶新增為現有 Azure 訂用帳戶的系統管理員，然後重新整理以在此清單中看到該訂用帳戶。
- 合作夥伴會選擇要部署此網站的資料中心位置。
- [**部署您的存放區**] 連結會根據所提供的資訊來部署這個新網站，並顯示 URL。
- 請務必複製此 URL，因為合作夥伴中心不會維護這些網站的狀態或歷程記錄。 如果您關閉瀏覽器頁面，將會遺失網站名稱。
- 在部署期間，將會使用在合作夥伴中心建立的 web 應用程式認證來部署網站。 如果您沒有註冊 web 應用程式，這會在部署期間註冊。

### <a name="configuration-scenario"></a>設定案例

- 新建立的網站會連結至合作夥伴租使用者，並可存取此合作夥伴租使用者的所有系統管理員帳戶。
  -合作夥伴可以使用合作夥伴中心的系統管理員認證來登入這個新網站。
- 店面應用程式目前支援法文、西班牙文、荷蘭文、德文、日文和英文。 （英文作為備用語言）。
  - 店面會使用合作夥伴在合作夥伴中心的設定檔中的預設地區設定，來設定地區設定。 此地區設定是用來在存放庫中設定貨幣、日期格式和當地語系化的供應專案。
- 合作夥伴可以設定商標、供應專案和 PayPal 或 PayU （印度）付款資訊。
- 合作夥伴可以更新 [公司名稱]、[公司標誌]、[標頭影像]、[銷售] 和 [支援連絡人] 等等。
- 合作夥伴可以根據其領域查看所有可用的 CSP 供應專案。
  - 合作夥伴可以選擇他們想要對所有客戶顯示的供應專案。
  - CSP 合作夥伴可以選取一或多個供應專案，並更新名稱、數量、功能描述和價格。
  - 價格為年度費用。 客戶每年訂閱。
- 合作夥伴隨時都可以為（a）所有目前和未來的客戶或（b）特定客戶設定預先核准的交易。
  - 預先核准的客戶在新增訂閱、向現有訂用帳戶購買額外的基座或續訂訂閱時，不需要在入口網站上付費。
  - 預先核准的客戶將不會被重新導向至 PayPal 或 PayU （印度），以便在這些交易期間進行付款。
  - 預先核准的客戶交易可讓合作夥伴對預先核准的客戶執行離線計費和發票處理。
- CSP 合作夥伴可以輸入其 PayPal 帳戶資訊，例如 PayPal 用戶端識別碼和密碼。 CSP 合作夥伴也可以選取要使用沙箱或 live 帳戶進行測試。
  - 合作夥伴可以在 **& 認證的應用程式**<https://developer.paypal.com/> 中找到這項資訊。 您也可以從目前的應用程式取得這項資訊，或在 PayPal 中建立新的應用程式。
  - 建立新的 PayPal 帳戶（如果您還沒有的話）。 此帳戶將用於 PayPal，以取得客戶的付款。
    - 若要開啟 PayPal 企業帳戶，請參閱 <https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register>。
    - 若要建立 PayPal 沙箱帳戶，請參閱 <https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/>。
- （印度） CSP 合作夥伴可以輸入其 PayU Money 帳戶資訊，例如 PayU 用戶端識別碼和密碼。 合作夥伴可以在 <https://developer.payumoney.com/>中找到詳細資訊。
  - 建立新的 PayU Money 帳戶（如果您還沒有的話）。 若要開啟 PayU Money 帳戶，請造訪 <https://www.payumoney.com/merchant-account/#/>。 此帳戶將用於 PayU，以取得客戶的付款。

## <a name="customer-experience-scenarios"></a>客戶體驗案例

### <a name="new-customer-signup-scenario"></a>新客戶註冊案例

- 根據預設，網站可公開使用，並在首頁上顯示合作夥伴的目錄。
- 客戶現在可以屬於大量的[客戶國家/地區](#customer-countries)。
- 重點在於歐洲自由貿易聯盟（EFTA）國家/地區、北美洲、日本、印度、澳大利亞和紐西蘭地區。
  - 這項功能會使用合作夥伴中心 SDK 中的區域授權支援。
- 客戶可以從要購買的類別目錄中選取供應專案。
  - 他們可以新增其客戶名稱、位址和網域相關資訊。
- 客戶將會被導向至 PayPal 或 PayU （印度）結帳的經驗。 客戶可以使用下列其中一種方式來提供付款：
  - 其現有的 PayPal 或 PayU （適用于印度）帳戶
  - 由 PayPal 或 PayU （印度）在其國家/地區支援的資金補助。 這些可能包括信用卡、金融卡和銀行帳戶（適用的話）。
- 會為此客戶建立客戶租使用者。 成功建立租使用者訂單之後，系統會提供客戶使用者名稱、密碼和訂用帳戶詳細資料。
  - 客戶可以儲存使用者名稱和密碼以保持登入，以供進一步購買。
  - 每個訂用帳戶會購買一年，而客戶可以在訂用帳戶結束日期之前的30天內更新。

### <a name="view-prior-purchases-scenario"></a>查看先前購買案例

- 客戶可以使用客戶租使用者使用者名稱和密碼登入，並移至 [**我的訂單**] 區段。
- 客戶可以流覽至 [**我的訂單**] 頁面，他們可以在其中查看已購買的訂閱，並在必要時進行更新。
- 客戶可以流覽至 [**我的訂閱**] 頁面，他們可以在其中查看所有訂用帳戶（授權型和以使用量為基礎），包括在合作夥伴中心維護的訂閱。

### <a name="add-seats-to-existing-subscriptions-scenario"></a>將基座新增至現有的訂用帳戶案例

- 從 [**我的訂單**] 區段中，客戶可以將更多基座新增至現有的訂用帳戶。 客戶可以在訂閱年度期間隨時新增更多基座。
- 每個新增的基座都不會變更訂用帳戶的結束日期。 不過，訂用帳戶的價格會根據您新增基座的日期，以及該日期在年份中的位置而變更。 定價會按日按比例計費，只收取一年的剩餘天數。

### <a name="add-more-subscriptions-scenario"></a>新增更多訂閱案例

- 客戶可以隨時從 [**我的訂單**] 底下的 [**新增**訂用帳戶] 區段購買任意數目的訂閱。
- 客戶可以選取訂用帳戶、新增數量，並支付完成交易的費用，並立即開始使用訂用帳戶。 如果客戶是預先核准的客戶，訂用帳戶就可以立即使用，而發票會傳送給客戶進行付款。

### <a name="renew-subscription-scenario"></a>續訂訂閱案例

- 客戶可以在訂用帳戶結束日期之前的30天內更新訂用帳戶。
- 這僅適用于過去30天。
- 如果未在過去30天內更新，則會從這個客戶租使用者的訂用帳戶清單中移除訂用帳戶。
- 您無法在續約期間更新數量。

### <a name="payments-scenario"></a>付款案例

- 如果客戶已預先核准系統管理員的交易，則不會針對上述案例顯示付款體驗。 相反地，合作夥伴可以將付款的發票傳送給預先核准的客戶。
- 針對所有新購買專案，您可以新增更多基座、新增訂閱和續訂。 客戶可以透過 PayPal 或 PayU （印度）使用此網站來支付合作夥伴。
- 此網站已與 PayPal 或 PayU （印度）整合，並可讓合作夥伴接受其客戶的付款。 PayPal 或 PayU （印度）會在合作夥伴的帳戶中取得此金額的信用額度。 PayPal 或 PayU （適用于印度）銀行帳戶管理不在此網站的範圍內，而且會分別在 PayPal.com 或 PayUmoney.com 上管理。
- 這取決於在 PayPal.com 或 PayUmoney.com 設定其 PayPal orPayU （印度）付款設定的夥伴。 Microsoft 不會儲存此資訊，或使用此選項所產生的實際付款交易。

### <a name="prorated-pricing-scenario"></a>按比例計算的定價案例

- 當客戶在現有的訂用帳戶中新增更多基座時，此網站支援按比例計算的價格。
- 每個訂用帳戶會在一年後到期，且在購買訂閱之後就無法變更。
- 新增額外基座不會變更訂用帳戶的結束日期。 客戶會在結束日期之前的剩餘天數向您收費。 例如，如果第一天的訂用帳戶成本為 $365，而您在第二天增加了一個基座，新基座的價格將會是 $364。 如果您稍後再新增一個10天，價格將會是 $354。