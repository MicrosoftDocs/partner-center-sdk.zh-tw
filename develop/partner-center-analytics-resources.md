---
title: 合作夥伴中心分析
description: 合作夥伴中心分析公用 API 檔。
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094710"
---
# <a name="partner-center-analytics---resources"></a>合作夥伴中心分析 - 資源

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

分析 API 可讓您以程式設計方式存取在使用者體驗中呈現的資料。

## <a name="prerequisites"></a>必要條件

- 認證，如[合作夥伴中心驗證](partner-center-authentication.md)所述。 這些案例僅支援使用使用者認證進行驗證。

## <a name="csp-program-azure-usage-analytics"></a>CSP 計畫： Azure 流量分析

下列案例示範如何流量分析 API 來抓取所有合作夥伴中心的 Azure 使用量分析資訊。

- [取得所有 Azure 使用情形的分析資訊](get-all-azure-usage-analytics.md)

此案例會在[Azure 使用量](#azure-usage-resource)資源的集合中傳回您的分析資訊。

## <a name="azure-usage-resource"></a>Azure 使用量資源

代表 Azure 使用量的所有分析資料。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| CustomerTenantId | 字串 | 客戶租使用者識別碼。 |
| customerName | 字串 | 客戶名稱。 |
| subscriptionId | 字串 | 訂用帳戶識別碼。 |
| subscriptionName | 字串 | 訂用帳戶名稱。 |
| usageDate | 字串 | 使用日期。 |
| resourceLocation | 字串 | 資料中心的位置，例如西歐。 |
| meterCategory | 字串 | 計量分類，例如 [資料管理]。 |
| meterSubcategory | 字串 | 「計量子類別」，例如「異地多餘」。 |
| meterUnit | 字串 | 計量單位，例如 gb 或小時。 |
| reservationOrderId | 字串 | Azure VM 保留實例的保留順序。 |
| reservationId | 字串 | 在特定 RI 訂單下的保留實例。 |
| serviceType | 字串 | 表示虛擬機器類型。 例如，Standard_E4s_v3。 |
| quantity | long | 指出計量單位中使用的數位。 |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP 計畫：間接轉銷商分析

下列案例示範如何流量分析 API 來抓取所有合作夥伴中心的間接轉售商分析資訊。

- [取得所有間接轉銷商的分析資訊](get-all-indirect-resellers-analytics.md)

此案例會在[間接轉售商](#indirect-resellers-resource)資源的集合中傳回您的分析資訊。

## <a name="indirect-resellers-resource"></a>間接轉銷商資源

代表間接轉銷商的所有分析資料。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| partnerTenantId | 字串 | 您要為其取得間接轉銷商資料之夥伴的租使用者識別碼。 |
| id | 字串 | 間接轉銷商識別碼。 |
| NAME | 字串 | 您要為其取得間接轉銷商資料的夥伴名稱。 |
| market | 字串 | 您想要為其取得間接轉銷商資料的合作夥伴市場。 |
| firstSubscriptionCreationDate | UTC 日期時間格式的字串 | 您要用來抓取間接轉銷商資料的第一個訂用帳戶建立日期。 |
| latestSubscriptionCreationDate | UTC 日期時間格式的字串 | 最新訂用帳戶的建立日期。 |
| firstSubscriptionEndDate | UTC 日期時間格式的字串 | 第一次結束任何訂用帳戶。 |
| latestSubscriptionEndDate | UTC 日期時間格式的字串 | 任何訂閱結束時的最新日期。 |
| firstSubscriptionSuspendedDate | UTC 日期時間格式的字串 | 第一次暫停任何訂用帳戶。 |
| latestSubscriptionSuspendedDate | UTC 日期時間格式的字串 | 任何訂用帳戶暫止的最新日期。 |
| firstSubscriptionDeprovisionedDate | UTC 日期時間格式的字串 | 第一次取消布建任何訂用帳戶。 |
| latestSubscriptionDeprovisionedDate | UTC 日期時間格式的字串 | 取消布建任何訂用帳戶的最新日期。 |
| subscriptionCount | double | 所有增值轉銷商的訂用帳戶計數 |
| licenseCount | double | 所有增值轉銷商的授權計數 |
| indirectResellerCount | double | 間接轉銷商計數 |

## <a name="csp-program-subscription-analytics"></a>CSP 方案：訂用帳戶分析

下列案例示範如何流量分析 API 來抓取您所有的合作夥伴中心訂用帳戶分析資訊、使用搜尋查詢進行篩選，或依日期或詞彙將它分組。

- [取得所有訂用帳戶的分析資訊](get-all-subscription-analytics.md)
- [取得根據搜尋查詢所篩選的訂用帳戶分析資訊](get-subscription-analytics-by-search-query.md)
- [取得根據日期或詞彙分組的訂用帳戶分析資訊](get-subscription-analytics-grouped-by-dates-or-terms.md)

所有這些案例都會在[訂](#subscription-resource)用帳戶資源的集合中傳回您的分析資訊。

## <a name="subscription-resource"></a>訂用帳戶資源

表示訂用帳戶的所有分析資料。

|         屬性          |              類型              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             字串             |                                              GUID 格式的字串，可識別客戶租使用者。                                              |
|       customerName        |             字串             |                                                               客戶的名稱。                                                                |
|      customerMarket       |             字串             |                                                 客戶執行業務的國家/地區。                                                 |
|            id             |             字串             |                                                              訂用帳戶識別碼。                                                              |
|          status           |             字串             |                                          訂用帳戶狀態：「作用中」、「已暫停」或「取消布建」。                                           |
|        productName        |             字串             |                                                                產品的名稱。                                                                |
|     subscriptionType      |             字串             |       訂閱類型。 **注意**：此欄位會區分大小寫。 支援的值為： "Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS"。       |
|     autoRenewEnabled      |            boolean             |                                         值，指出是否自動更新訂用帳戶。                                          |
|         partnerId         |             字串             | MPN 識別碼。 若為直接轉銷商，此參數將會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，此參數將會是間接轉銷商的 MPN 識別碼。 |
|       friendlyName        |             字串             |                                                             訂閱的名稱。                                                              |
|        partnerName        |             字串             |                                              購買訂閱之夥伴的名稱                                               |
|       providerName        |             字串             |            若為間接轉銷商的訂閱交易，提供者名稱就是購買訂閱的間接提供者。             |
|    effectiveStartDate     | UTC 日期時間格式的字串 |                                                           訂用帳戶開始的日期。                                                            |
|     commitmentEndDate     | UTC 日期時間格式的字串 |                                                            訂閱結束的日期。                                                             |
|    currentStateEndDate    | UTC 日期時間格式的字串 |                                           訂用帳戶的目前狀態將會變更的日期。                                            |
| trialToPaidConversionDate | UTC 日期時間格式的字串 |                                 訂用帳戶從試用版轉換成付費的日期。 預設值為 null。                                 |
|      trialStartDate       | UTC 日期時間格式的字串 |                                訂用帳戶的試用期開始日期。 預設值為 null。                                 |
|       trialEndDate        | UTC 日期時間格式的字串 |                                  訂用帳戶試用期結束的日期。 預設值為 null。                                  |
|       lastUsageDate       | UTC 日期時間格式的字串 |                                        上次使用訂用帳戶的日期。 預設值為 null。                                        |
|     deprovisionedDate     | UTC 日期時間格式的字串 |                                      取消布建訂用帳戶的日期。 預設值為 null。                                      |
|      lastRenewalDate      | UTC 日期時間格式的字串 |                                       上次更新訂用帳戶的日期，預設值為 null。                                       |
|       licenseCount        |             number             |                                                             授權總數。                                                              |
|     subscriptionCount     |             number             |                        訂閱數目。 注意：此值只會出現在匯總查詢的回應中。                         |

## <a name="search-analytics"></a>搜尋分析

> [!NOTE]
> 不需要 CSP 方案成員資格即可取得搜尋分析。

下列案例示範如何流量分析 API 來取得您所有的合作夥伴中心搜尋分析資訊。

- [取得所有搜尋的分析資訊](get-all-search-analytics.md)

此案例會在[搜尋](#search-resource)資源的集合中傳回您的分析資訊。

## <a name="search-resource"></a>搜尋資源

表示搜尋的所有分析資料。

| 屬性 | 類型 | Description |
|----------|------|-------------|
| companyName | 字串 | 帳單公司名稱。 |
| contactButtonClicked | Boolean | 指出是否已按下 [連絡人] 按鈕。 |
| keywordCountry | 字串 | 搜尋中指定的國家/地區。 |
| detailsViewed | Boolean | 指出是否已查看搜尋詳細資料。 |
| keywordIndustryFocus | 字串 | 要在其中進行搜尋的產業，例如醫療保健。 |
| mpnId | 字串 | Microsoft 合作夥伴網路（MPN）識別碼。 若為直接轉銷商，此參數將會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，此參數將會是間接轉銷商的 MPN 識別碼。 |
| partnerMarket | 字串 | 合作夥伴開展業務的地區設定。 |
| keywordProduct | 字串 | 搜尋中指定的產品。 |
| referralSubmitted | Boolean | 指出是否已提交參照。 |
| searchDate | UTC 日期時間格式的字串 | 搜尋查詢的發生日期。 |
| keywordSearchText | 字串 | 搜尋中指定的文字。 |
| searchResultPageViews | long | 合作夥伴在搜尋結果中的次數。 只有在匯總時才會包含回應的一部分。
| contactClicks | long | 按一下 [連絡人] 按鈕的次數。 只有在匯總時才會包含回應的一部分。
| referralCount | long | 從搜尋產生的參考數目。 只有在匯總時才會包含回應的一部分。
| profileViews | long | 夥伴設定檔的查看次數。 只有在匯總時才會包含回應的一部分。

## <a name="referrals-analytics"></a>參考分析

> [!NOTE]
> 不需要 CSP 方案成員資格即可取得參考分析。

下列案例示範如何流量分析 API 來抓取所有合作夥伴中心的參考分析資訊。

- [取得所有轉介的分析資訊](get-all-referrals-analytics.md)

此案例會在[參考](#referrals-resource)資源的集合中傳回您的分析資訊。

> [!NOTE]
> 由世紀營運的合作夥伴中心無法使用 [參考分析]。

## <a name="referrals-resource"></a>參考資源

代表參考的所有分析資料。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| id | 字串 | 客戶租使用者識別碼。  |
| status | 字串 | 指出參考是否導致客戶。  |
| customerMarket | 字串 | 客戶執行業務的國家/地區。 |
| customerName | 字串 | 客戶的名稱。 |
| customerOrgSize | 字串 | 範圍，指出客戶組織中的員工數目。 例如，"10to50employees"。 |
| acceptedDate | UTC 日期時間格式的字串 | 接受參考的日期。 |
| acknowledgedDate | UTC 日期時間格式的字串 | 認可參考的日期。 |
| archivedDate | UTC 日期時間格式的字串 | 封存參考的日期。 |
| declinedDate | UTC 日期時間格式的字串 | 拒絕參考的日期。 |
| expiredDate | UTC 日期時間格式的字串 | 參考到期的日期。 |
| lostDate | UTC 日期時間格式的字串 | 遺漏參考的日期。 |
| missedDate | UTC 日期時間格式的字串 | 遺漏參考的日期。 |
| createdDate | UTC 日期時間格式的字串 | 建立參考的日期。 |
| skippedDate | UTC 日期時間格式的字串 | 略過參考的日期。 |
| wonDate | UTC 日期時間格式的字串 | 進行參照的日期。 |
| partnerMarket | 字串 |  合作夥伴經營業務的國家/地區。 |
