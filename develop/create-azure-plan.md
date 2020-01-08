---
title: 建立 Azure 方案
description: 開發人員可以使用合作夥伴中心 Api，以程式設計方式購買、建立和管理 Azure 方案。
ms.assetid: ''
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 65d7e33d5a05cbf0b6ca938ea45f0ba03dfefd2e
ms.sourcegitcommit: efffee16923d06f37d24cd50cbce9bdc82a56a5e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/03/2020
ms.locfileid: "75621660"
---
# <a name="create-an-azure-plan"></a>建立 Azure 方案

適用於：

* 合作夥伴中心

您可以使用合作夥伴中心 Api 來購買、建立和管理 Azure 方案。 此程式類似于建立 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶。 您必須[取得 Azure 方案的類別目錄專案](#get-the-catalog-item-for-azure-plan)，然後[建立並提交訂單](#create-and-submit-an-order)。

## <a name="prerequisites"></a>先決條件

* [合作夥伴中心驗證認證](partner-center-authentication.md)。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
* 客戶識別碼。 如果您沒有客戶的識別碼，請依照[取得客戶清單](get-a-list-of-customers.md)或登入合作夥伴中心中的步驟，從 [客戶] 清單中選擇 [客戶]，選取 [**帳戶**]，然後儲存其**Microsoft 識別碼**。
* [確認客戶接受 Microsoft 客戶合約](https://docs.microsoft.com/partner-center/confirm-customer-agreement)。

## <a name="get-the-catalog-item-for-azure-plan"></a>取得 Azure 方案的類別目錄專案

您必須先取得對應的類別目錄專案，才能為客戶建立 Azure 方案。 您可以使用現有的合作夥伴中心目錄 Api 和下列資源模型來抓取類別目錄專案。

* **[Product](product-resources.md#product)** ：可購買商品或服務的群組結構。 產品本身不是可購買專案。
* **[SKU](product-resources.md#sku)** ：產品下的可購買庫存單位（SKU）。 Sku 代表產品的不同形狀。
* **[可用性](product-resources.md#availability)** ：可供購買 SKU 的設定（例如國家/地區、貨幣或產業區段）。

若要取得 Azure 方案的類別目錄專案，請完成下列步驟：

1. 識別並取得 Azure 方案的*產品*識別碼。 依照[取得產品清單](get-a-list-of-products.md)中的步驟，並將**TargetView**指定為**microsoftazure.mobileengagement**。 （如果您已經知道 Azure 方案的*產品*識別碼，您可以依照[使用產品識別碼 取得產品](get-a-product-by-id.md)中的步驟進行。）

2. 從 Azure 方案的產品取得**SKU** 。 請依照[取得產品的 sku 清單](get-a-list-of-skus-for-a-product.md)中的步驟進行。 如果您已經知道 Azure 方案的 SKU 識別碼，您可以依照[使用 sku 識別碼取得 sku](get-a-sku-by-id.md)中的步驟來進行。

3. 從 Azure 方案的 SKU 取得**可用性**。 依照[取得 SKU 的 hdinsight 清單](get-a-list-of-availabilities-for-a-sku.md)中的步驟進行。 如果您已經知道所需可用性的識別碼，可以改為遵循[使用可用性識別碼取得可用性](get-an-availability-by-id.md)中的步驟。 *請務必記下 Azure 方案可用性的**CatalogItemId**屬性值。您將需要此值來建立訂單。*

## <a name="create-and-submit-an-order"></a>建立並提交訂單

若要提交您的 Azure 方案訂單，請執行下列動作：

1. [建立購物車](create-a-cart.md)，以保存您想要購買的類別目錄專案集合。 當您建立[購物車](cart-resources.md#cart)時，[購物車明細專案](cart-resources.md#cartlineitem)會自動根據可依相同[順序](order-resources.md#order)購買的內容進行分組。 （您也可以[更新購物車](update-a-cart.md)）。

2. [查看購物車](checkout-a-cart.md)，這會導致建立[訂單](order-resources.md#order)。

## <a name="get-order-details"></a>取得訂單詳細資料

您可以[使用訂單識別碼來抓取個別訂單的詳細資料](get-an-order-by-id.md)。 您也可以[取得特定客戶的所有訂單清單](get-all-of-a-customer-s-orders.md)。

>[!NOTE]
>提交訂單後，會有最多15分鐘的延遲，訂單才會出現在該客戶的訂單清單中。

## <a name="manage-azure-plans"></a>管理 Azure 方案

成功處理訂單之後，將會為 Azure 方案建立合作夥伴中心**訂**用帳戶資源。 您可以使用下列方法來管理合作夥伴中心**訂**用帳戶資源，以管理 Azure 方案：

* [取得客戶的訂用帳戶](get-all-of-a-customer-s-subscriptions.md)
* [依訂單取得訂用帳戶清單](get-a-list-of-subscriptions-by-order.md)

在合作夥伴中心建立 Azure 方案時，也會在 Azure 中建立對應的 Azure 使用量訂用帳戶。 您也可以使用 Azure 入口網站和 Azure Api，在相同的 Azure 方案底下建立額外的 Azure 使用量訂用帳戶。 您可以遵循[取得合作夥伴中心訂用帳戶的 azure 權利清單](get-a-list-of-azure-entitlements-for-subscription.md)中的步驟，取得與 azure 方案相關聯的所有 azure 使用量訂閱的識別碼

## <a name="lifecycle-management"></a>生命週期管理

您可以遵循[暫止訂用](suspend-a-subscription.md)帳戶中的步驟來暫停現有的 Azure 方案。

*如果現有的 Azure 方案不再具有任何相關聯的使用中資產（包括 Azure 使用量訂用帳戶和 Azure 保留專案），您就只能將其暫止。*

如需如何停用 Azure 使用量訂閱的詳細資訊，請參閱訂用帳戶[生命週期管理上的 AZURE API](https://docs.microsoft.com/rest/api/resources/subscriptions)。

若要移除現有的 Azure 保留專案，您必須[取消保留](https://docs.microsoft.com/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)。  
暫止 Azure 方案之後，您可以重新啟用它。

如需如何重新啟用 Azure 方案的詳細資訊，請參閱重新啟用已[暫停的訂用](reactivate-a-suspended-a-subscription.md)帳戶

## <a name="transition-existing-csp-offers-to-azure-plan"></a>將現有的 CSP 供應專案轉換為 Azure 方案

您無法為具有 Microsoft Azure （MS-AZR-0017P-流程 ms-azr-0145p）訂用帳戶的現有客戶建立 Azure 方案。 不過，您可以透過合作夥伴中心內的 CSP 方案新商務體驗，將[客戶從現有的 Csp azure 供應專案轉換為 azure 服務](https://docs.microsoft.com/partner-center/azure-plan-transition)。 若要轉換現有的客戶，請使用產品升級 Api 來執行下列動作：

* [檢查客戶是否符合轉換至 Azure 方案的資格](get-eligibility-for-product-upgrade.md)
* [起始客戶的產品升級](create-product-upgrade-entity.md)
* [檢查產品升級的狀態](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Azure 費用

您可以使用下列方法來查詢使用量摘要和詳細使用量記錄，以追蹤[Azure 費用](azure-spending.md)：

* [取得合作夥伴的使用摘要](get-a-partner-usage-summary.md)
* [取得合作夥伴的所有客戶使用記錄](get-a-customer-s-usage-records.md)
* [取得客戶的使用摘要](get-a-customer-usage-summary.md)
* [取得客戶的所有訂用帳戶使用記錄](get-a-customer-subscription-s-usage-records.md)
* [取得訂用帳戶使用資料](get-a-customer-subscription-usage-summary.md)
* [取得訂用帳戶的所有每月使用記錄](get-all-monthly-usage-records-for-a-subscription.md)
* [依照資源取得訂用帳戶的使用資料](get-a-customer-subscription-resource-usage-records.md)
* [依照計量取得訂用帳戶的使用資料](get-a-customer-subscription-meter-usage-records.md)
* [取得計量的使用記錄資源](meter-usage-resources.md)
* [取得資源的使用記錄資源](resource-usage-resources.md)

您也可以使用下列方法來設定及管理客戶使用量預算：

* [取得客戶的使用量預算](get-a-customer-s-usage-spending-budget.md)
* [更新客戶的使用量預算](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>發票和對帳

您可以使用下列方法來管理發票和對帳資料：

* [取得發票的集合](get-a-collection-of-invoices.md)
* [取得發票估算連結](get-invoice-estimate-links.md)
* [依識別碼取得發票](get-invoice-by-id.md)
* [取得發票對帳單](get-invoice-statement.md)
* [取得發票摘要](get-invoice-summaries.md)
* [取得已開立發票的取用明細項目](get-invoice-billed-consumption-lineitems.md)
* [取得未開立發票的取用明細項目](get-invoice-unbilled-consumption-lineitems.md)
* [取得發票計費的偵察明細專案](get-invoiceline-items.md)
* [取得未開立發票的對帳明細項目](get-invoice-unbilled-recon-lineitems.md)
