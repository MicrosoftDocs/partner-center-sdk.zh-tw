---
title: 購買類別目錄專案
description: 如何使用合作夥伴中心 API 購買類別目錄專案。
ms.assetid: B9B1B66A-D1AD-44E8-85AA-49D9C2A94BE5
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ff4f04bc53f96e6e7670922093bca830456de921
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486738"
---
# <a name="purchase-catalog-items"></a>購買類別目錄專案


**適用于**

- 合作夥伴中心


下列案例示範使用合作夥伴中心 API 從目錄購買專案的一般程式。


## <a name="span-iddiscoveryspan-iddiscoveryspan-iddiscoverydiscovery"></a><span id="Discovery"/><span id="discovery"/><span id="DISCOVERY"/>探索

選取 [產品和 Sku]，然後使用下列合作夥伴中心 API 模型來檢查其可用性： 

- [產品](product-resources.md#product)-可購買商品或服務的群組結構。 產品本身並不是可購買專案。
- [SKU](product-resources.md#sku) -產品下的可購買庫存單位（SKU）。 這些代表產品的不同形狀。
- [可用性](product-resources.md#availability)-SKU 可供購買的設定（例如國家/地區、貨幣和產業區段）。

若要從目錄購買專案，請完成下列步驟：

1.  識別並取得您想要購買的產品和 SKU。

    - [取得產品清單](get-a-list-of-products.md)
    - [使用產品識別碼取得產品](get-a-product-by-id.md)
    - [取得產品的 Sku 清單](get-a-list-of-skus-for-a-product.md)
    - [使用 SKU 識別碼取得 SKU](get-a-sku-by-id.md)

2.  檢查 SKU 的清查。 只有在[purchasePrerequisites](product-resources.md#sku)屬性中以**InventoryCheck**值標記的 sku 才需要此步驟。

    - [檢查清查](check-inventory.md) 

3.  取得[SKU](product-resources.md#sku)的[可用性](product-resources.md#availability)。 您將需要在放置訂單時的可用性**CatalogItemId** 。 若要取得此值，請使用下列其中一個 Api： 

    - [取得 SKU 的 hdinsight 清單](get-a-list-of-availabilities-for-a-sku.md)
    - [使用可用性識別碼取得可用性](get-an-availability-by-id.md)


## <a name="span-idorder_submissionspan-idorder_submissionspan-idorder_submissionorder-submission"></a><span id="Order_submission"/><span id="order_submission"/><span id="ORDER_SUBMISSION"/>訂單提交

若要提交您的類別目錄專案順序，請執行下列動作：

1.  建立[購物車](cart-resources.md)，以保存您想要購買的類別目錄專案集合。 當您建立購物車時，[購物車明細專案](cart-resources.md#cartlineitem)會自動根據可依相同[順序](order-resources.md)購買的內容進行分組。

    - [建立購物車](create-a-cart.md)
    - [更新購物車](update-a-cart.md)

2.  查看購物車。 簽出購物車會導致[訂單](order-resources.md)的建立。 

    - [結帳購物車](checkout-a-cart.md)

## <a name="span-idget_order_detailsspan-idget_order_detailsspan-idget_order_detailsget-order-details"></a><span id="Get_order_details"/><span id="get_order_details"/><span id="GET_ORDER_DETAILS"/>取得訂單詳細資料



您可以使用訂單識別碼來抓取個別訂單的詳細資料，或取得客戶的訂單清單。 請注意，提交訂單的時間和出現在客戶訂單清單中的時間，最多會有15分鐘的延遲。 

- 如需使用訂單識別碼取得個別訂單的詳細資料，請參閱[依識別碼取得訂單](get-an-order-by-id.md)。

- 請參閱[取得客戶的所有訂單](get-all-of-a-customer-s-orders.md)，以取得使用客戶識別碼之客戶的訂單清單。      

-  請參閱[依客戶和計費週期類型取得訂單清單](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)，以依據[計費週期類型](product-resources.md#billingcycletype)來取得客戶的訂單清單，讓您分別列出目錄專案訂單（一次性費用）和年度或每月計費訂單。 

## <a name="span-idlifecycle_managementspan-idlifecycle_managementspan-idlifecycle_managementlifecycle-management"></a><span id="Lifecycle_management"/><span id="lifecycle_management"/><span id="LIFECYCLE_MANAGEMENT"/>生命週期管理



在合作夥伴中心管理目錄專案的生命週期時，您可以取得有關目錄專案[權利](entitlement-resources.md)的資訊，並使用保留訂單識別碼取得保留詳細資料。 如需如何執行這項操作的範例，請參閱[取得權利](get-a-collection-of-entitlements.md)。   

## <a name="span-idinvoice_and_reconciliationspan-idinvoice_and_reconciliationspan-idinvoice_and_reconciliationinvoice-and-reconciliation"></a><span id="Invoice_and_reconciliation"/><span id="invoice_and_reconciliation"/><span id="INVOICE_AND_RECONCILIATION"/>發票和對帳



下列案例示範如何以程式設計方式來查看您的客戶[發票](invoice-resources.md)，並取得您的帳戶餘額和摘要，其中包含類別目錄專案的一次性費用。  

**餘額和付款**    
若要取得預設貨幣類型的目前帳戶餘額，這是週期性和一次性（類別目錄專案）費用的餘額，請參閱[取得您目前的帳戶餘額](get-the-reseller-s-current-account-balance.md)

**多貨幣餘額和付款**    
若要取得目前的帳戶餘額和發票摘要的集合，其中包含具有每個客戶貨幣類型的週期性和一次性費用，請參閱[取得發票](get-invoice-summaries.md)摘要。

**發票**    
若要取得同時顯示週期性和一次性費用的發票集合，請參閱[取得發票集合](get-a-collection-of-invoices.md)。 

**單一發票**    
若要使用發票識別碼來抓取特定發票，請參閱[依識別碼取得發票](get-invoice-by-id.md)。  

**對帳**    
若要取得特定發票識別碼的發票明細專案詳細資料（對帳明細專案）集合，請參閱[取得發票明細專案](get-invoiceline-items.md)。  

**下載發票做為 PDF**    
若要使用發票識別碼來抓取 PDF 格式的發票語句，請參閱[取得發票聲明](get-invoice-statement.md)。

