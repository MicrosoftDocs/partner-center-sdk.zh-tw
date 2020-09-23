---
title: 合作夥伴中心範例
description: 為了協助您使用合作夥伴中心 Api 快速啟動並執行，我們提供了範例程式、C 管理程式碼片段，以及 REST 範例要求和回應。
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 2a672826262e73856bffc1eefe85028d4e7cb130
ms.sourcegitcommit: 529b07030a874d644cf947790f4b53cdff438dd4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "91007636"
---
# <a name="partner-center-samples"></a>合作夥伴中心範例

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

為了協助您使用合作夥伴中心 Api 快速啟動並執行，我們提供了範例程式、c # managed 程式碼片段，以及 REST 範例要求和回應。

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<table>
  <thead>
    <th>範例</th>
    <th>詳細資料</th>
  </thead>
  <tbody>
    <tr>
      <td>程式碼片段</td>
      <td>針對指標和 .NET、JAVA 和 PowerShell 程式碼片段，示範如何使用合作夥伴中心受控 API 來管理客戶帳戶、取得分析、下訂單、管理帳單和訂用帳戶、提供支援，以及管理帳戶和設定檔，請參閱 <a href="scenarios.md">案例</a>。</td>
    </tr>
    <tr>
      <td>REST 範例</td>
      <td>如需示範如何使用合作夥伴中心 REST API 來管理客戶帳戶、取得分析、下訂單、管理帳單和訂用帳戶、提供支援，以及管理帳戶和設定檔的範例要求和回應，請參閱 <a href="scenarios.md">案例</a>。</td>
    </tr>
    <tr>
      <td><a href="console-test-app.md">主控台測試應用程式</a></td>
      <td>此應用程式可在 c # 和 JAVA 中使用，它會針對 [案例] 區段中所列的所有案例提供程式碼和一些錯誤處理。</td>
    </tr>
    <tr>
      <td><a href="csp-customer-web-storefront.md">CSP 客戶網路店面</a></td>
      <td>這個網站會顯示您的客戶可以用來購買 Microsoft 產品訂閱的工作線上商店。 您可以使用 <a href="csp-customer-storefront-builder-quick-start-guide-.md">CSP 客戶店面建立程式快速入門手冊</a>，輕鬆地為您的公司建立網站。</td>
    </tr>
    <tr>
      <td>Store 網站</td>
      <td><p><strong>描述：</strong></p>
          <p>此應用程式會示範如何根據雲端解決方案提供者合作夥伴提供的供應專案目錄，建立 web 存放區。 客戶可以建立商店帳戶，並透過您的網站訂購軟體訂閱。</p>
        <p><strong>取得程式碼：</strong></p>
        <p><a href="https://go.microsoft.com/fwlink/p/?LinkId=746683">下載範例程式碼</a></p>
        <p><strong>發行前的設定事項：</strong></p>
        <ul>
          <li><p>驗證：應用程式識別碼 & 秘密。</p></li>
          <li><p>商標：標誌和公司名稱。</p></li>
          <li><p>歡迎使用訊息。</p></li>
          <li><p>優惠，包括描述和價格。 應用程式會假設標價包含任何適用的稅金。 或者，您也可以新增其他邏輯，以在結帳時計算稅金。</p></li>
          <li><p>付款資訊：提供您自己的信用卡選項、PayPal 或其他付款類型。 在您設定此元件之前，請閱讀本指南的 <a href="/partner-center/non-payment-fraud-misuse">非付款、詐騙或誤用</a>。</p></li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>