---
title: 發票資源
description: 透過合作夥伴中心 Api 可取得多個發票相關資源。 這些資源與發票和明細專案詳細資料相關。
ms.assetid: FDD151CC-3473-46DF-A422-265DCBC8A498
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 6540af51e462974592ec18d7dd9ede8517ba1725
ms.sourcegitcommit: 07153b06dae146418ca5213c7e6fe1c869ba164d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/21/2020
ms.locfileid: "80083105"
---
# <a name="invoice-resources"></a>發票資源

適用於：

- 夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

下列發票相關資源可透過合作夥伴中心 Api 取得。

## <a name="invoice"></a>發票

| 屬性 | 類型 | 描述 |
| -------- | ---- | ----------- |
| id | string | 發票識別碼。 |
| invoiceDate | UTC 日期時間格式的字串 | 產生發票的日期。 |
| billingPeriodStartDate | UTC 日期時間格式的字串 | 計費循環開始日期（UTC）。 |
| billingPeriodEndDate | UTC 日期時間格式的字串   | 計費循環結束日期（UTC）。 |
| totalCharges | 數字 | 總費用。 包含交易和任何調整的費用。     |
| paidAmount | 數字  | 合作夥伴所支付的金額。 如果收到付款，則為負數。  |
| currencyCode | string  | 指出用於所有發票專案金額和總計之貨幣的程式碼。 |
| currencySymbol  | string | 用於所有發票專案金額和總計的貨幣符號。 |
| pdfDownloadLink | string  | 以 PDF 格式下載發票的連結。 此連結不會作為搜尋結果的一部分傳回，而且只有在發票是由識別碼存取時才會填入。 此連結會在30分鐘內自動過期。 |
| invoiceDetails  | [InvoiceDetail](#invoicedetail)物件的陣列  | 發票詳細資料。  |
| 條款      | [發票](#invoice)物件的陣列   | 此發票的改正。  |
| documentType    | string | 發票的檔案類型：「點數附注」、「發票」。 |
| amendsOf        | string | 本檔為修訂檔的參考編號。  |
| invoiceType     | string  | 發票的類型：「週期性」、「一\_時間」。   |
| 連結           | [ResourceLinks](utility-resources.md#resourcelinks)  | 資源連結。  |
| 屬性      | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。  |

## <a name="invoicedetail"></a>InvoiceDetail

發票包含計費專案的集合，且每個專案都以 InvoiceDetail 資源表示。

| 屬性            | 類型                                                           | 描述                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | 發票詳細資料的類型：「無」、「使用量\_行\_專案」、「帳單\_行\_專案」。 |
| billingProvider     | string                                                         | 計費提供者： [無]、[office]、[azure] 或 [azure\_資料\_市場]。         |
| 連結               | [ResourceLinks](utility-resources.md#resourcelinks)           | 資源連結。                                                               |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

發票中的每個個別費用都會以 InvoiceLineItem 表示。

| 屬性            | 類型                                                           | 描述                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | 發票明細專案的類型： [無]、[使用量\_行\_專案]、[帳單\_行\_專案]。 |
| billingProvider     | string                                                         | 計費提供者： [無]、[office]、[azure] 或 [azure\_資料\_市場]。            |
| 屬性          | [ResourceAttributes](utility-resources.md#resourceattributes) | 中繼資料屬性。                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

描述發票的餘額和總費用的摘要。

| 屬性                 | 類型                                                           | 描述                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | 數字                                                         | 發票的餘額。 這是未付款帳單的總金額。 |
| currencyCode             | string                                                         | 指出用於餘額金額之貨幣的程式碼。       |
| currencySymbol           | string                                                         | 使用的貨幣符號。                                             |
| accountingDate           | UTC 日期時間格式的字串                                 | 上次更新餘額金額的日期。                         |
| firstInvoiceCreationDate | UTC 日期時間格式的字串                                 | 建立客戶第一張發票的日期。              |
| lastPaymentDate          | UTC 日期時間格式的字串                                 | 上次付款的日期。                                         |
| lastPaymentAmount        | 數字                                                         | 上一個付款的金額。                                       |
| latestInvoiceDate        | UTC 日期時間格式的字串                                 | 建立客戶之最後發票的日期。               |
| 詳細資料                  | [InvoiceSummaryDetail](#invoicesummarydetail)物件的陣列 | 發票摘要詳細資料。                                           |
| 連結                    | [ResourceLinks](utility-resources.md#resourcelinks)            | 資源連結。                                                   |
| 屬性               | [ResourceAttributes](utility-resources.md#resourceattributes)  | 中繼資料屬性。                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

表示發票類型的個別詳細資料摘要（例如，週期性、一\_時間）。

| 屬性            | 類型                                                           | 描述                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceType         | string                                                         | 發票的類型：「週期性」、「一\_時間」。                                       |
| 摘要             | [InvoiceSummary](#invoicesummary)物件                       | 每張發票類型的發票摘要。                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

代表[InvoiceSummary](#invoicesummary)類型的集合，其中包含每個貨幣之發票類型的個別詳細資料。  

| 屬性            | 類型                                                           | 描述                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | [InvoiceSummary](#invoicesummary)物件的陣列             | 每筆發票類型的發票摘要（依貨幣）。                            |

## <a name="licensebasedlineitem"></a>LicenseBasedLineItem

表示以授權為基礎之訂用帳戶的發票計費明細專案。

| 屬性                 | 類型                                                           | 描述                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 銷售額                   | string                                                         | 取得或設定總金額。 總金額 = 單位價格 * 數量。  |
| 屬性               | string                                                         | 取得屬性。                                                  |
| 為 billingcycletype         | string                                                         | 取得或設定計費週期類型。                                  |
| billingProvider          | string                                                         | 取得帳單提供者。                                            |
| chargeEndDate            | UTC 日期時間格式的字串                                 | 取得或設定費用的結束日期。                             |
| chargeStartDate          | UTC 日期時間格式的字串                                 | 取得或設定費用的開始日期。                           |
| chargeType               | string                                                         | 取得或設定費用的類型。                                      |
| 貨幣                 | string                                                         | 取得或設定此行專案所使用的貨幣。                    |
| Id               | string                                                         | 取得或設定 Microsoft 計費平臺中的客戶唯一識別碼。  |
| customerName             | UTC 日期時間格式的字串                                 | 取得或設定客戶名稱。                                       |
| domainName               | string                                                         | 取得或設定功能變數名稱。                                             |
| durableOfferId           | string                                                         | 取得或設定持久性供應專案的唯一識別碼。                     |
| invoiceLineItemType      | string                                                         | 取得發票明細專案的類型。                                   |
| mpnId                    | 數字                                                         | 取得或設定與此行專案相關聯的 MPN 識別碼。 對於直接轉銷商，這是轉銷商的 MPN 識別碼。 對於間接轉銷商，這是已新增轉銷商（VAR）之值的 MPN 識別碼。                                   |
| offerId                  | string                                                         | 取得或設定供應專案唯一識別碼。                             |
| offerName                | string                                                         | 取得或設定供應專案名稱。                                          |
| orderId                  | string                                                         | 取得或設定訂單的唯一識別碼。                             |
| partnerId                | string                                                         | 取得或設定合作夥伴的 Azure active directory 租使用者識別碼。            |
| quantity                 | 數字                                                         | 取得或設定與此行專案相關聯的單位數。      |
| subscriptionDescription  | string                                                         | 取得或設定訂用帳戶描述。                            |
| Subscription.subscriptionenddate      | UTC 日期時間格式的字串                                 | 取得或設定訂閱到期的日期。                      |
| subscriptionId           | string                                                         | 取得或設定訂用帳戶的唯一識別碼。                      |
| subscriptionName         | string                                                         | 取得或設定訂用帳戶名稱。                                   |
| And subscription.subscriptionstartdate    | UTC 日期時間格式的字串                                 | 取得或設定訂閱開始的日期。                   |
| 進行                 | 數字                                                         | 取得或設定折扣後的金額。                               |
| syndicationPartnerSubscriptionNumber | string                                             | 取得或設定新聞訂閱合作夥伴訂用帳戶號碼。             |
| 銷                      | 數字                                                         | 取得或設定收取的稅金。                                       |
| tier2MpnId               | 數字                                                         | 取得或設定與此明細專案相關聯之第2層合作夥伴的 MPN 識別碼。 |
| totalForCustomer         | 數字                                                         | 取得或設定折扣和稅金後的總金額。                 |
| totalOtherDiscount       | 數字                                                         | 取得或設定與此購買相關聯的折扣。              |
| unitPrice                | 數字                                                         | 取得或設定單價。                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

表示以使用量為基礎之訂用帳戶的發票計費明細專案。

| 屬性                 | 類型                                                           | 描述                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| 屬性               | string                                                         | 取得屬性。                                                  |
| 為 billingcycletype         | string                                                         | 取得或設定計費週期類型。                                  |
| billingProvider          | string                                                         | 取得帳單提供者。                                            |
| chargeEndDate            | UTC 日期時間格式的字串                                 | 取得或設定費用的結束日期。                             |
| chargeStartDate          | UTC 日期時間格式的字串                                 | 取得或設定費用的開始日期。                           |
| chargeType               | string                                                         | 取得或設定費用的類型。                                      |
| consumedQuantity         | 數字                                                         | 取得或設定耗用的總單位數。                                |
| consumptionDiscount      | string                                                         | 取得或設定耗用量的折扣。                             |
| consumptionPrice         | string                                                         | 取得或設定所耗用數量的價格。                          |
| 貨幣                 | string                                                         | 取得或設定與價格相關聯的貨幣。                 |
| customerName             | string                                                         | 取得或設定客戶名稱。                                       |
| Id               | string                                                         | 取得或設定客戶的唯一識別碼。                          |
| detailLineItemId         | 數字                                                         | 取得或設定詳細資料行專案識別碼。 唯一識別適用于所耗用單位之計算不同案例的明細專案。 範例：已使用的總計 = 1338，1024以一種費率計費，314以不同的費率收費。        |
| domainName               | string                                                         | 取得或設定功能變數名稱。                                             |
| includedQuantity         | 數字                                                         | 取得或設定訂單中包含的單位。                         |
| invoiceLineItemType      | string                                                         | 取得發票明細專案的類型。                                   |
| invoiceNumber            | string                                                         | 取得或設定發票編號。                                      |
| listPrice                | 數字                                                         | 取得或設定每個單位的價格。                                  |
| mpnId                    | 數字                                                         | 取得或設定與此行專案相關聯的 MPN 識別碼。 對於直接轉銷商，這是轉銷商的 MPN 識別碼。 對於間接轉銷商，這是已新增轉銷商（VAR）之值的 MPN 識別碼。                                   |
| orderId                  | string                                                         | 取得或設定訂單的唯一識別碼。                             |
| overageQuantity          | 數字                                                         | 取得或設定超過允許使用量的耗用數量。               |
| partnerBillableAccountId | string                                                         | 取得或設定合作夥伴的可計費帳戶識別碼。                         |
| partnerId                | string                                                         | 取得或設定合作夥伴的 Azure active directory 租使用者識別碼。            |
| partnerName              | string                                                         | 取得或設定夥伴的名稱。                                      |
| postTaxEffectiveRate     | 數字                                                         | 取得或設定稅金後的有效價格。                         |
| postTaxTotal             | 數字                                                         | 取得或設定稅金後的總費用。 稅前費用 + 稅金金額 |
| 計算 pretaxcharges            | 數字                                                         | 取得或設定稅金前的費用。                          |
| preTaxEffectiveRate      | 數字                                                         | 取得或設定稅金前的有效價格。                        |
| 區內                   | string                                                         | 取得或設定與資源實例相關聯的區域。        |
| resourceGuid             | string                                                         | 取得或設定資源識別碼。                                 |
| resourceName             | string                                                         | 取得或設定資源名稱。 範例：資料庫（GB/月）。         |
| serviceName              | string                                                         | 取得或設定服務名稱。 範例： Azure 資料服務。           |
| serviceType              | string                                                         | 取得或設定服務類型。 範例： Azure SQL Azure DB。           |
| sku                      | string                                                         | 取得或設定服務 SKU。                                         |
| subscriptionDescription  | string                                                         | 取得或設定訂用帳戶描述。                            |
| subscriptionId           | string                                                         | 取得或設定訂用帳戶的唯一識別碼。                      |
| subscriptionName         | string                                                         | 取得或設定訂用帳戶名稱。                                   |
| taxAmount                | 數字                                                         | 取得或設定收取的稅金金額。                               |
| tier2MpnId               | 數字                                                         | 取得或設定與此明細專案相關聯之第2層合作夥伴的 MPN 識別碼。 |
| 單位                     | string                                                         | 取得或設定 Azure 使用量的測量單位。                     |

## <a name="invoicestatement"></a>InvoiceStatement

表示應用程式/pdf 中發票語句上可用的作業。

| 屬性                 | 類型                                                           | 描述                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| HTTPResponseMessage      | object                                                         | 具有 contentType 的 ByteArrayContent = 應用程式/pdf。                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

代表授權型訂用帳戶的發票計費明細專案。

| 屬性 | 類型 | 描述 |
| --- | --- | --- |
| PartnerId | string | 取得或設定合作夥伴租使用者識別碼。 |
| CustomerId | string | 取得或設定客戶租使用者識別碼。 |
| CustomerName | string | 取得或設定客戶名稱。 |
| CustomerDomainName | string | 取得或設定客戶功能變數名稱。 |
| CustomerCountry | string | 取得或設定客戶國家/地區。 |
| InvoiceNumber | string | 取得或設定發票編號。 |
| MpnId | string | 取得或設定與此行專案相關聯的 MPN 識別碼。 |
| ResellerMpnId | int | 取得或設定訂單的唯一識別碼。 |
| OrderDate | DateTime | 取得或設定建立訂單的日期。 |
| ProductId | string | 取得或設定產品的唯一識別碼。 |
| SkuId | string | 取得或設定 SKU 的唯一識別碼。 |
| AvailabilityId | string | 取得或設定可用性唯一識別碼。 |
| ProductName | string | 取得或設定產品名稱。 |
| SkuName | string | 取得或設定 SKU 名稱。 |
| ChargeType | string | 取得或設定費用的類型。 |
| UnitPrice | decimal | 取得或設定單價。 |
| EffectiveUnitPrice | decimal | 取得或設定有效的單位價格。 |
| Unittype.pixel 表示 | string | 取得或設定單位類型。 |
| 數量 | int | 取得或設定與此行專案相關聯的單位數。 |
| 小計 | decimal | 取得或設定折扣後的金額。 |
| TaxTotal | decimal | 取得或設定收取的稅金。 |
| TotalForCustomer | decimal | 取得或設定折扣和稅金後的總金額。 |
| Currency | string | 取得或設定此行專案所使用的貨幣。 |
| PublisherName | string | 取得或設定與此購買相關聯的發行者名稱。 |
| PublisherId | string | 取得或設定與此購買相關聯的發行者識別碼。 |
| SubscriptionDescription | string | 取得或設定與此購買相關聯的訂用帳戶描述。 |
| SubscriptionId | string | 取得或設定與此購買相關聯的訂用帳戶識別碼。 |
| ChargeStartDate | DateTime | 取得或設定與此購買相關聯的費用開始日期。 |
| ChargeEndDate | DateTime | 取得或設定與此購買相關聯的費用結束日期。 |
| TermAndBillingCycle | string | 取得或設定與此購買相關聯的詞彙和計費週期。 |
| 替代識別碼 | string | 取得或設定替代識別碼（報價識別碼）。 |
| PriceAdjustmentDescription | string | 取得或設定價格調整描述。 |
| DiscountDetails | string |  **過時**。 取得或設定與此購買相關聯的折扣詳細資料。 |
| PricingCurrency | string | 取得或設定定價貨幣代碼。 |
| PCToBCExchangeRate | decimal | 取得或設定計費貨幣匯率的定價貨幣。 |
| PCToBCExchangeRateDate | DateTime | 取得或設定決定計費貨幣匯率之定價貨幣的匯率日期。 |
| BillableQuantity | decimal | 取得或設定購買的單位。 針對名為**BillableQuantity**的每個設計資料行。 |
| MeterDescription | string | 取得或設定耗用量明細專案的計量描述。 |
| ReservationOrderId | string | 取得或設定 Azure RI 購買的保留訂單識別碼。 |
| BillingFrequency | string | 取得或設定計費頻率。 |
| InvoiceLineItemType | InvoiceLineItemType | 傳回發票明細專案的類型。 |
| BillingProvider | BillingProvider | 傳回計費提供者。 |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

代表每日評等使用量的未開立帳單、計費的對帳明細專案。

| 屬性 | 類型 | 描述 |
| --- | --- | --- |
| PartnerId | string | 取得或設定合作夥伴租使用者識別碼。 |
| PartnerName | string | 取得或設定夥伴名稱。 |
| CustomerId | string | 取得或設定使用方式所屬客戶的租使用者識別碼。 |
| CustomerName | string | 取得或設定使用所屬客戶公司的名稱。 |
| CustomerDomainName | string | 取得或設定使用所屬客戶的功能變數名稱。 |
| InvoiceNumber | string | 取得或設定使用量所屬發票的識別碼。 |
| ProductId | string | 取得或設定產品的唯一識別碼。 |
| SkuId | string | 取得或設定 SKU 的唯一識別碼。 |
| AvailabilityId | string | 取得或設定可用性唯一識別碼。 |
| SkuName | string | 取得或設定服務的 SKU 名稱。 |
| ProductName | string | 取得或設定產品的名稱。 |
| PublisherName | string | 取得或設定發行者的名稱。 |
| PublisherId | string | 取得或設定發行者的識別碼。 |
| SubscriptionId | string | 取得或設定訂閱識別碼。 |
| SubscriptionDescription | string | 取得或設定訂用帳戶描述。 |
| ChargeStartDate | DateTime | 取得或設定費用開始日期。 |
| ChargeEndDate | DateTime | 取得或設定收費結束日期。 |
| UsageDate | DateTime | 取得或設定使用日期。 |
| MeterType | string | 取得或設定計量類型。 |
| MeterCategory | string | 取得或設定計量類別目錄。 |
| 計量識別碼 | string | 取得或設定計量識別碼（GUID）。 |
| MeterSubCategory | string | 取得或設定計量子類別目錄。 |
| MeterName | string | 取得或設定計量名稱。 |
| MeterRegion | string | 取得或設定計量區域。 |
| UnitOfMeasure | string | 取得或設定測量單位。 |
| ResourceLocation | string | 取得或設定資源的位置。 |
| ConsumedService | string | 取得或設定已使用的服務名稱。 |
| ResourceGroup | string | 取得或設定資源群組的名稱。 |
| ResourceUri | string | 取得或設定使用方式的資源實例 uri。 |
| 標記 | string | 取得或設定客戶已新增的標記。 |
| AdditionalInfo | string | 取得或設定服務特定的中繼資料。 例如，虛擬機器的映射類型。 |
| ServiceInfo1 | string | 取得或設定內部 Azure 服務中繼資料。 |
| ServiceInfo2 | string | 取得或設定服務資訊，例如虛擬機器的映射類型和 ExpressRoute 的 ISP 名稱。 |
| CustomerCountry | string | 取得或設定客戶的國家/地區。 |
| MpnId | string | 取得或設定與此行專案相關聯的 MPN 識別碼。 |
| ResellerMpnId | string | 取得或設定與此明細專案相關聯之第2層合作夥伴的轉售商 MPN 識別碼。 |
| ChargeType | string | 取得或設定費用的類型。 |
| UnitPrice | decimal | 取得或設定單位的價格。 |
| 數量 | decimal | 取得或設定使用量的數量。 |
| Unittype.pixel 表示 | string | 取得或設定單位類型（例如1小時）。 |
| BillingPreTaxTotal | decimal | 取得或設定客戶或帳單貨幣的當地貨幣中，所需的延長成本或總成本。 |
| BillingCurrency | string | 取得或設定 ISO 貨幣，其中計量會以客戶或帳單貨幣的當地貨幣來計費。 |
| PricingPreTaxTotal | decimal | 取得或設定用來評等之稅金或目錄貨幣之前的延長成本或總成本。 |
| PricingCurrency | string | 取得或設定 ISO 貨幣，其中計量會以美元或用來評等的目錄貨幣來計費。 |
| entitlementId | string | 取得或設定權利（Azure 訂用帳戶）識別碼。 |
| EntitlementDescription | string | 取得或設定權利（Azure 訂用帳戶）的描述。 |
| PCToBCExchangeRate | string | 取得或設定計費貨幣匯率的定價貨幣。 |
| PCToBCExchangeRateDate | DateTime | 取得或設定計費貨幣匯率日期的定價貨幣。 |
| EffectiveUnitPrice | decimal | 取得或設定有效的單位價格。 |
| RateOfPartnerEarnedCredit | decimal | 取得或設定合作夥伴取得信用額度的速率。 |
| hasPartnerEarnedCredit | bool | 取得或設定是已套用的合作夥伴獲額。 |
| InvoiceLineItemType | InvoiceLineItemType | 傳回發票明細專案的類型。 |
| BillingProvider | BillingProvider | 傳回計費提供者。 |
