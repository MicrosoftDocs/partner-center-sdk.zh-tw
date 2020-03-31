---
title: 購買 Azure 保留
description: 您可以透過現有的 Microsoft Azure 訂用帳戶（MS-AZR-0017P-流程 ms-azr-0145p）或 Azure 方案，使用合作夥伴中心 API 為客戶購買 Azure 保留。
ms.assetid: 1BCDA7B8-93FC-4AAC-94E0-B15BFC95737F
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.localizationpriority: medium
ms.openlocfilehash: a3c0f64bf6bddb483a485cc4f1e1d96ed1599cb0
ms.sourcegitcommit: def3d4b9d7ba2bf5b1fd268d2e71dae5d5f65a6e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/31/2020
ms.locfileid: "80416300"
---
# <a name="purchase-azure-reservations"></a>購買 Azure 保留

適用於：

- 夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

若要使用合作夥伴中心 API 為客戶購買 Azure 保留專案，您必須擁有現有的 Microsoft Azure （**MS ms-azr-0017p-流程 ms-azr-0145p**）訂用帳戶或 azure 方案。

> [!NOTE]  
> 下列市場不提供 Azure 保留：
>  
> | 無法使用的市場            | &nbsp;                            | &nbsp;                                   |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | 奧蘭島                  | 格陵蘭                         | 巴布亞紐幾內亞                         |
> | 美屬薩摩亞                 | 格瑞那達                           | 皮特康群島                         |
> | 安道爾                        | 哥德普洛                        | 留尼旺                                  |
> | 安圭拉                       | 關島                              | 俄文同盟                       |
> | 南極大陸                     | 根息                          | 沙巴                                     |
> | 安地卡及巴布達            | 幾內亞                            | 聖巴瑟米                         |
> | 阿路巴                          | 幾內亞比索                     | 聖露西亞                              |
> | 貝南                          | 蓋亞納                            | 聖馬丁                             |
> | 不丹                         | 海地                             | 聖匹島                |
> | 波奈                        | 赫德島及麥當勞群島 | 聖文森及格瑞那丁         |
> | 布威島                  | 曼城島                       | 薩摩亞獨立國                                    |
> | 巴西                         | 尖棉                         | 聖馬利諾                               |
> | 英屬印度洋領土 | 澤西島                            | 聖多美普林西比                    |
> | 英屬維爾京群島         | 吉里巴斯                          | 塞席爾                               |
> | 布吉納法索                   | 科索沃                            | 獅子山                             |
> | 蒲隆地                        | 寮國                              | 聖佑達修斯                           |
> | 柬埔寨                       | 賴索托                           | 荷屬聖馬丁                             |
> | 中非共和國       | 賴比瑞亞                           | 索羅門群島                          |
> | 查德                           | 馬達加斯加                        | 索馬利亞                                  |
> | 中國                          | 馬拉威                            | 南喬治亞與南三明治群島 |
> | 聖誕島               | 馬爾地夫                          | 南蘇丹                              |
> | 可可斯群島        | 馬利                              | 聖赫勒拿、阿森松、特里斯坦達庫尼亞群島   |
> | 葛摩                        | 馬紹爾群島                  | 蘇利南                                 |
> | 剛果共和國                          | 馬丁尼克                        | 冷岸                                 |
> | 剛果民主共和國 (DRC)                    | 茅利塔尼亞                        | 史瓦濟蘭                                |
> | 柯克群島                   | 馬約特島                           | 東帝汶                              |
> | 吉布地                       | 密克羅尼西亞                        | 多哥                                     |
> | 多米尼克                       | 蒙特色拉特島                        | 托克勞群島                                  |
> | 赤道幾內亞              | 莫三比克                        | 東加                                    |
> | 厄利垂亞                        | 緬甸                           | 土克斯及開科斯群島                 |
> | 福克蘭群島               | 諾魯                             | 吐瓦魯                                   |
> | 法屬圭亞那                  | 新喀里多尼亞群島                     | 美國外島                    |
> | 法屬玻里尼西亞               | 尼日                             | 萬那杜                                  |
> | 法屬南半球領土    | 紐威島                              | 梵蒂岡                             |
> | 加彭                          | 諾福克島                    | 瓦利斯及福杜納                        |
> | 甘比亞                         | 北馬里安納群島          | 葉門                                    |
> | 直布羅陀                      | 帛琉                             | &nbsp;                                   |
>  

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 此案例支援使用獨立應用程式和應用程式 + 使用者認證來進行驗證。
- 客戶識別碼。 如果您沒有客戶的識別碼，您可以從 [客戶] 清單中選擇 [客戶]，然後選取 [帳戶]，然後儲存其 Microsoft 識別碼，以在合作夥伴中心查詢識別碼。
- Active CSP Azure 訂用帳戶或 Azure 方案的訂用帳戶識別碼。

## <a name="how-to-purchase-microsoft-azure-reservations"></a>如何購買 Microsoft Azure 保留

一旦您識別出您想要新增 Azure 保留的 active CSP Azure 訂用帳戶，請使用下列步驟來購買它：

1. [啟用-註冊](#enablement)使用中的 CSP Azure 訂用帳戶，以將其用於購買 Azure 保留。
2. [探索](#discovery)-尋找並選取您想要購買的 Azure 保留產品和 sku，並檢查其可用性。
3. [訂單提交](#order-submission)-使用訂單中的專案建立購物車，並提交。
4. [取得訂單詳細資料](#get-order-details)-檢查訂單的詳細資料、客戶的所有訂單，或依計費週期類型來查看訂單。

購買 Azure 保留之後，下列案例會示範如何藉由取得 Azure 保留權利的相關資訊來管理其生命週期，以及如何取得餘額聲明、發票和發票摘要。

- [生命週期管理](#lifecycle-management)
- [發票和對帳](#invoice-and-reconciliation)

## <a name="enablement"></a>啟用

啟用表示藉由註冊訂用帳戶，讓現有的 Microsoft Azure （**ms-azr-0017p-流程 ms-azr-0145p**）訂用帳戶與 azure 保留的 VM 實例產生關聯，以供 azure 保留區使用。 註冊是購買 Azure 保留的 VM 執行個體的必要條件。

需要訂用帳戶，原因如下：

1. 若要檢查客戶是否有資格部署資源，因此在某個區域中購買 Azure 保留的 VM 執行個體。
2. 為訂用帳戶上的部署提供容量優先順序。 這僅適用于已選取**容量優先順序**選項的單一範圍 Azure 保留的 VM 執行個體。

一旦識別出您想要新增 Azure 保留的作用中訂用帳戶之後，您必須註冊訂用帳戶，才能啟用 Azure 保留。 若要註冊現有的[訂](subscription-resources.md)用帳戶資源，以啟用它來排序 Azure 保留專案，請參閱[註冊訂用](register-a-subscription.md)帳戶。

註冊訂用帳戶之後，您應該藉由檢查註冊狀態來確認註冊程式已完成。 若要這麼做，請參閱[取得訂用帳戶註冊狀態](get-subscription-registration-status.md)。

> [!NOTE]  
> 為具有 Azure 方案的客戶購買 Microsoft Azure 保留時，您必須先註冊 Azure 方案。 類似于 Microsoft Azure （**ms-azr-0017p-流程 ms-azr-0145p**）訂用帳戶，Azure 方案會以合作夥伴中心[訂](subscription-resources.md)用帳戶資源來表示。 因此，您可以使用相同的[註冊訂](register-a-subscription.md)用帳戶方法來註冊 Azure 方案。

## <a name="discovery"></a>探索

啟用訂用帳戶以購買 Azure 保留之後，您就可以選取產品和 Sku，並使用下列合作夥伴中心 API 模型來檢查其可用性：

- [產品](product-resources.md#product)-可購買商品或服務的群組結構。 產品本身並不是可購買專案。
- [SKU](product-resources.md#sku) -產品下的可購買庫存單位（SKU）。 這些代表產品的不同形狀。
- [可用性](product-resources.md#availability)-SKU 可供購買的設定（例如國家/地區、貨幣和產業區段）。

購買 Azure 保留區之前，請先完成下列步驟：

1. 識別並取得您想要購買的產品和 SKU。 若要這麼做，您可以先列出產品和 Sku，或如果您已經知道產品和 SKU 的識別碼，請選取它們。

    - [取得產品清單 (以國家/地區為基礎)](get-a-list-of-products.md)
    - [使用產品識別碼取得產品](get-a-product-by-id.md)
    - [取得產品的 SKU 清單 (以國家/地區為基礎)](get-a-list-of-skus-for-a-product.md)
    - [使用 SKU 識別碼取得 SKU](get-a-sku-by-id.md)

2. 檢查 SKU 的清查。 只有以**InventoryCheck**必要條件標記的 sku 才需要此步驟。

    - [確認存貨](check-inventory.md)

3. 取得[SKU](product-resources.md#sku)的[可用性](product-resources.md#availability)。 您將需要在放置訂單時的可用性**CatalogItemId** 。 若要取得此值，請使用下列其中一個 Api：

    - [取得 SKU 的可用性清單 (以國家/地區為基礎)](get-a-list-of-availabilities-for-a-sku.md)
    - [使用可用性識別碼取得可用性](get-an-availability-by-id.md)

> [!IMPORTANT]  
> 每個 Microsoft Azure 保留產品都有不同的 Microsoft Azure （**ms-azr-0017p-流程 ms-azr-0145p**）訂用帳戶和 Azure 方案的 hdinsight。 若要[取得產品清單（依國家/地區](get-a-list-of-products.md)），或[取得產品的 sku 清單（依據國家/地區）](get-a-list-of-skus-for-a-product.md)，或取得僅適用于 Azure 方案之 sku 的[hdinsight 清單](get-a-list-of-availabilities-for-a-sku.md)，請指定 "reservationScope = AzurePlan" 參數。

## <a name="order-submission"></a>訂單提交

若要提交您的 Azure 保留訂單，請執行下列動作：

1. 建立購物車，以保存您想要購買的類別目錄專案集合。 當您建立[購物車](cart-resources.md)時，[購物車明細專案](cart-resources.md#cartlineitem)會自動根據可依相同[順序](order-resources.md)購買的內容進行分組。

    - [建立購物車](create-a-cart.md)
    - [更新購物車](update-a-cart.md)

2. 查看購物車。 簽出購物車會導致[訂單](order-resources.md)的建立。

    - [結帳購物車](checkout-a-cart.md)

## <a name="get-order-details"></a>取得訂單詳細資料

建立您的 Azure 保留訂單之後，您可以使用訂單識別碼來抓取個別訂單的詳細資料，或取得客戶的訂單清單。 請注意，提交訂單的時間和出現在客戶訂單清單中的時間，最多會有15分鐘的延遲。

- 使用訂單識別碼取得個別訂單的詳細資料。 請參閱[依識別碼取得訂單](get-an-order-by-id.md)。

- 使用客戶識別碼取得客戶的訂單清單。 請參閱[取得客戶的所有訂單](get-all-of-a-customer-s-orders.md)。

- 若要依[計費週期類型](product-resources.md#billingcycletype)取得客戶的訂單清單，可讓您分別列出 Azure 保留訂單（一次性費用）和年度或每月計費訂單。 請參閱[依客戶和計費週期類型取得訂單清單](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)。

## <a name="lifecycle-management"></a>生命週期管理

在合作夥伴中心管理 Azure 保留週期的過程中，您可以取得 Azure 保留[權利](entitlement-resources.md)的相關資訊，並使用保留訂單識別碼取得保留詳細資料。 如需如何執行這項操作的範例，請參閱[取得權利](get-a-collection-of-entitlements.md)。   

## <a name="invoice-and-reconciliation"></a>發票和對帳

下列案例示範如何以程式設計方式來查看您的客戶[發票](invoice-resources.md)，並取得您的帳戶餘額和摘要，包括 Azure 保留的一次性費用。  

**餘額與付款**若要取得預設貨幣類型的目前帳戶餘額，這是週期性和一次性（Azure 保留）費用的餘額，請參閱[取得您目前的帳戶餘額](get-the-reseller-s-current-account-balance.md)

**多貨幣餘額和付款**若要取得目前的帳戶餘額和發票摘要的集合，其中包含具有每個客戶貨幣類型的週期性和一次性費用，請參閱[取得發票](get-invoice-summaries.md)摘要。

**發票**若要取得同時顯示週期性和一次性費用的發票集合，請參閱[取得發票集合](get-a-collection-of-invoices.md)。 

**單一發票**若要使用發票識別碼來抓取特定發票，請參閱[依識別碼取得發票](get-invoice-by-id.md)。  

**對帳**若要取得特定發票識別碼的發票明細專案詳細資料（對帳明細專案）集合，請參閱[取得發票明細專案](get-invoiceline-items.md)。  

**以 PDF 格式下載發票**若要使用發票識別碼來抓取 PDF 格式的發票語句，請參閱[取得發票聲明](get-invoice-statement.md)。
