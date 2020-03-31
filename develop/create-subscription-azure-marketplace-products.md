---
title: 建立商業 marketplace 產品的訂用帳戶
description: 開發人員可以使用合作夥伴中心 Api 來建立及管理商業 marketplace 產品的訂用帳戶。
ms.assetid: ''
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: 1db279b2e377ee5e24bf80709a7e84755fc2f132
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80412231"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>建立商業 marketplace 產品的訂用帳戶

適用於：

* 夥伴中心

您可以使用合作夥伴中心 API 來建立商業市集產品的訂用帳戶。 您必須[取得市場](#get-a-list-of-offers-for-a-market)供應專案的清單、[建立並提交](#create-and-submit-an-order)商業 marketplace 訂用帳戶的訂單，然後[取得啟用連結](#get-activation-link)。

您也可以[執行生命週期管理](#lifecycle-management)，並管理這些訂閱的[發票](#invoice-and-reconciliation)。

## <a name="prerequisites"></a>必要條件

* [合作夥伴中心驗證認證](partner-center-authentication.md)。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
* 客戶識別碼。 如果您沒有客戶的識別碼：請登入合作夥伴中心，從 [客戶] 清單中選擇 [客戶]，選取 [**帳戶**]，然後儲存其**Microsoft 識別碼**。

## <a name="get-a-list-of-offers-for-a-market"></a>取得市場供應專案清單

您可以使用下列合作夥伴中心 API 模型，來查看市場的供應專案：

* **[Product](product-resources.md#product)** ：可購買商品或服務的群組結構。 產品本身不是可購買專案。
* **[SKU](product-resources.md#sku)** ：產品下的可購買庫存單位（SKU）。 這些代表產品的不同形狀。
* **[可用性](product-resources.md#availability)** ：可供購買 SKU 的設定（例如國家/地區、貨幣或產業區段）。

購買 Azure 保留區之前，請先完成下列步驟：

1. 識別並取得您想要購買的產品和 SKU。 如果您已經知道產品識別碼和 SKU 識別碼，請選取它們。

    * [取得產品清單](get-a-list-of-products.md)
    * [使用產品識別碼取得產品](get-a-product-by-id.md)
    * [取得產品的 SKU 清單](get-a-list-of-skus-for-a-product.md)
    * [使用 SKU 識別碼取得 SKU](get-a-sku-by-id.md)

    > [!NOTE]
    > 您可以依據其 **"Azure"** 的**ProductType**屬性及其「 **SaaS**」的**子類型**屬性來識別商用 marketplace 產品。

2. 如果 Sku 標記為**InventoryCheck**必要條件，請[檢查 sku 的清查](check-inventory.md)。

    > [!NOTE]
    > 目前沒有支援清查檢查或以**InventoryCheck**必要條件標記的商用 marketplace 產品。

3. 取得 SKU 的可用性。 在下訂單時，您將需要可用性的**CatalogItemId** ，您可以透過下列 api 來取得：

    * [取得 SKU 的可用性清單](get-a-list-of-availabilities-for-a-sku.md)
    * [使用可用性識別碼取得可用性](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>建立並提交訂單

若要提交您的 Azure 保留訂單，請執行下列動作：

1. [建立購物車](create-a-cart.md)，以保存您想要購買的類別目錄專案集合。 當您建立[購物車](cart-resources.md#cart)時，[購物車明細專案](cart-resources.md#cartlineitem)會自動根據可依相同[順序](order-resources.md#order)購買的內容進行分組。 （您也可以[更新購物車](update-a-cart.md)）。
2. [查看購物車](checkout-a-cart.md)，這會導致建立[訂單](order-resources.md#order)。

### <a name="get-order-details"></a>取得訂單詳細資料

您可以[使用訂單識別碼來抓取個別訂單的詳細資料](get-an-order-by-id.md)。 您也可以[取得特定客戶的所有訂單清單](get-all-of-a-customer-s-orders.md)。

> [!NOTE]
> 提交訂單後，會有最多15分鐘的延遲，訂單才會出現在該客戶的訂單清單中。

## <a name="get-activation-link"></a>取得啟用連結

合作夥伴或客戶必須啟用 Azure Markeplace 產品的訂用帳戶。 您可以[依訂單明細專案取得啟用連結](get-activation-link-by-order-line-item.md)。 您也可以[依識別碼取得訂用](get-a-subscription-by-id.md)帳戶，然後列舉其**Links**屬性來建立啟用連結。

## <a name="lifecycle-management"></a>生命週期管理

您可以使用下列方法來管理商用 marketplace 產品訂閱的生命週期：

* [取消商業市集訂用帳戶](cancel-an-azure-marketplace-subscription.md)
* [啟用或停用商業 marketplace 訂用帳戶的 autorenew](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>數量管理

商業 marketplace 訂用帳戶的數量必須在其相關[SKU](product-resources.md#sku)所定義的限制內（請參閱**minimumQuantity**和**maximumQuantity**屬性）。 若要更新商業 marketplace 訂用帳戶的數量，請使用下列方法：

* [變更訂用帳戶的數量](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>發票和對帳

您可以使用下列方法來管理客戶[發票](invoice-resources.md)（包括商用 marketplace 產品的訂閱費用）：

* [取得已開立發票的商業市集取用量明細](get-invoice-billed-consumption-lineitems.md)
* [取得發票估算連結](get-invoice-estimate-links.md)
* [取得未開立發票的商業市集取用量明細](get-invoice-unbilled-consumption-lineitems.md)
* [取得發票未開立帳單對帳明細專案](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>使用整合沙箱帳戶進行測試

在生產環境中，建立商業 marketplace SaaS 產品的訂用帳戶之後，您需要從合作夥伴中心抓取個人化啟用連結，並造訪發行者的網站以完成安裝程式。 只有在安裝完成後，訂用帳戶才會開始計費。

在 CSP 沙箱環境中，沒有與 Isv 的整合。 如果您嘗試從合作夥伴中心抓取啟用連結，則會傳回虛擬連結。 您無法使用此虛擬連結完成發行者網站上的安裝程式。 若要使用整合沙箱帳戶來測試對商業 marketplace SaaS 產品的訂閱計費，請使用下列方法來改為啟用訂閱。 成功啟用之後，訂用帳戶計費將會開始：

* [啟用商業市集產品的沙箱訂用帳戶](activate-sandbox-subscription-azure-marketplace-products.md)

