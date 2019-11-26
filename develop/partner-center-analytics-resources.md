---
title: 合作夥伴中心分析
description: 合作夥伴中心分析公用 API 檔。
ms.assetid: B605C1CD-FC40-4393-8588-55C8F0CAA51A
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: ce7245e3a556b038b8f71ba5fef9ea96c13f4869
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486878"
---
# <a name="partner-center-analytics---resources"></a>合作夥伴中心分析-資源

**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心


分析 API 可讓您以程式設計方式存取在使用者體驗中呈現的資料。 

## <a name="span-idprerequisitesspan-idprerequisitesspan-idprerequisitesprerequisites"></a><span id="Prerequisites"/><span id="prerequisites"/><span id="PREREQUISITES"/>必要條件


- 如[合作夥伴中心驗證](partner-center-authentication.md)中所述的認證。 這些案例僅支援使用使用者認證進行驗證。


## <a name="span-idazure_usage_analyticsspan-idazure_usage_analyticsspan-idazure_usage_analyticscsp-program-azure-usage-analytics"></a><span id="Azure_Usage_Analytics"/><span id="azure_usage_analytics"/><span id="AZURE_USAGE_ANALYTICS"/>CSP 方案： Azure 使用量分析

下列案例示範如何流量分析 API 來抓取所有合作夥伴中心的 Azure 使用量分析資訊。  

- [取得所有 Azure 使用量分析資訊](get-all-azure-usage-analytics.md)  

此案例會在[Azure 使用量](#azure_usage)資源的集合中傳回您的分析資訊。 

## <a name="span-idazure_usagespan-idazure_usagespan-idazure_usageazure-usage-resource"></a><span id="Azure_Usage"/><span id="azure_usage"/><span id="AZURE_USAGE"/>Azure 使用量資源

代表 Azure 使用量的所有分析資料。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| customerTenantId | 字串 | 客戶租使用者識別碼。 |
| customerName | 字串 | 客戶名稱。 |
| 訂閱 | 字串 | 訂用帳戶識別碼。 |
| subscriptionName | 字串 | 訂用帳戶名稱。 |
| usageDate | 字串 | 使用日期。 |
| resourceLocation | 字串 | 資料中心的位置，例如西歐。 |
| MeterCategory | 字串 | 計量分類，例如 [資料管理]。 |
| meterSubcategory | 字串 | 「計量子類別」，例如「異地多餘」。 |
| meterUnit | 字串 | 計量單位，例如 gb 或小時。 | 
| reservationOrderId | 字串 | Azure VM 保留實例的保留順序。 |
| reservationId | 字串 | 在特定 RI 訂單下的保留實例。 |
| serviceType | 字串 | 表示虛擬機器類型。 例如，Standard_E4s_v3。 |
| quantity | 長整數 | 指出計量單位中使用的數位。 |


## <a name="span-idindirect_resellers_analyticsspan-idindirect_resellers_analyticsspan-idindirect_resellers_analyticscsp-program-indirect-resellers-analytics"></a><span id="Indirect_Resellers_Analytics"/><span id="indirect_resellers_analytics"/><span id="INDIRECT_RESELLERS_ANALYTICS"/>CSP 方案：間接轉銷商分析

下列案例示範如何流量分析 API 來抓取所有合作夥伴中心的間接轉售商分析資訊。  

- [取得所有間接轉售商分析資訊](get-all-indirect-resellers-analytics.md)  

此案例會在[間接轉售商](#indirect_resellers)資源的集合中傳回您的分析資訊。 


## <a name="span-idindirect_resellersspan-idindirect_resellersspan-ididirect_resellersindirect-resellers-resource"></a><span id="Indirect_Resellers"/><span id="indirect_resellers"/><span id="IDIRECT_RESELLERS"/>間接轉售商資源

代表間接轉銷商的所有分析資料。

| 屬性 | 類型 | 描述 |
|----------|------|-------------|
| partnerTenantId | 字串 | 您要為其取得間接轉銷商資料之夥伴的租使用者識別碼。 |
| id | 字串 | 間接轉銷商識別碼。 |
| name | 字串 | 您要為其取得間接轉銷商資料的夥伴名稱。 |
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


## <a name="span-idsubscription_analyticsspan-idsubscription_analyticsspan-idsubscription_analyticscsp-program-subscription-analytics"></a><span id="Subscription_Analytics"/><span id="subscription_analytics"/><span id="SUBSCRIPTION_ANALYTICS"/>CSP 方案：訂閱分析

下列案例示範如何流量分析 API 來抓取您所有的合作夥伴中心訂用帳戶分析資訊、使用搜尋查詢進行篩選，或依日期或詞彙將它分組。  

- [取得所有訂用帳戶分析資訊](get-all-subscription-analytics.md)  
- [取得搜尋查詢所篩選的訂用帳戶分析資訊](get-subscription-analytics-by-search-query.md)  
- [取得依日期或詞彙分組的訂用帳戶分析資訊](get-subscription-analytics-grouped-by-dates-or-terms.md)  

所有這些案例都會在[訂](#subscription)用帳戶資源的集合中傳回您的分析資訊。 


## <a name="span-idsubscriptionspan-idsubscriptionspan-idsubscriptionsubscription-resource"></a><span id="Subscription"/><span id="subscription"/><span id="SUBSCRIPTION"/>訂用帳戶資源


表示訂用帳戶的所有分析資料。


|         屬性          |              類型              |                                                                      描述                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     customerTenantId      |             字串             |                                              GUID 格式的字串，可識別客戶租使用者。                                              |
|       customerName        |             字串             |                                                               客戶的名稱。                                                                |
|      customerMarket       |             字串             |                                                 客戶執行業務的國家/地區。                                                 |
|            id             |             字串             |                                                              訂用帳戶識別碼。                                                              |
|          status           |             字串             |                                          訂用帳戶狀態：「作用中」、「已暫停」或「取消布建」。                                           |
|        productName        |             字串             |                                                                產品的名稱。                                                                |
|     subscriptionType      |             字串             |       訂用帳戶類型。 **注意**：此欄位會區分大小寫。 支援的值為： "Office"、"Azure"、"Microsoft365"、"Dynamics"、"EMS"。       |
|     autoRenewEnabled      |            布林值             |                                         值，指出是否自動更新訂用帳戶。                                          |
|         partnerId         |             字串             | MPN 識別碼。 若為直接轉銷商，這會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，這將是間接轉銷商的 MPN 識別碼。 |
|       friendlyName        |             字串             |                                                             訂用帳戶的名稱。                                                              |
|        partnerName        |             字串             |                                              購買訂閱之夥伴的名稱                                               |
|       providerName        |             字串             |            若為間接轉銷商的訂閱交易，提供者名稱就是購買訂閱的間接提供者。             |
|    RateplaNcharge.effectivestartdate     | UTC 日期時間格式的字串 |                                                           訂用帳戶開始的日期。                                                            |
|     commitmentEndDate     | UTC 日期時間格式的字串 |                                                            訂閱結束的日期。                                                             |
|    currentStateEndDate    | UTC 日期時間格式的字串 |                                           訂用帳戶的目前狀態將會變更的日期。                                            |
| trialToPaidConversionDate | UTC 日期時間格式的字串 |                                 訂用帳戶從試用版轉換成付費的日期。 預設值為 null。                                 |
|      trialStartDate       | UTC 日期時間格式的字串 |                                訂用帳戶的試用期開始日期。 預設值為 null。                                 |
|       trialEndDate        | UTC 日期時間格式的字串 |                                  訂用帳戶試用期結束的日期。 預設值為 null。                                  |
|       lastUsageDate       | UTC 日期時間格式的字串 |                                        上次使用訂用帳戶的日期。 預設值為 null。                                        |
|     deprovisionedDate     | UTC 日期時間格式的字串 |                                      取消布建訂用帳戶的日期。 預設值為 null。                                      |
|      lastRenewalDate      | UTC 日期時間格式的字串 |                                       上次更新訂用帳戶的日期，預設值為 null。                                       |
|       licenseCount        |             數字             |                                                             授權總數。                                                              |
|     subscriptionCount     |             數字             |                        訂閱數目。 注意：此值只會出現在匯總查詢的回應中。                         |

## <a name="span-idsearch_analyticsspan-idsearch_analyticsspan-idsearch_analyticssearch-analytics"></a><span id="Search_Analytics"/><span id="search_analytics"/><span id="SEARCH_ANALYTICS"/>搜尋分析

> [!NOTE]  
> 不需要 CSP 方案成員資格就能取得搜尋分析。

下列案例示範如何流量分析 API 來取得您所有的合作夥伴中心搜尋分析資訊。  

- [取得所有搜尋分析資訊](get-all-search-analytics.md)  

此案例會在[搜尋](#search_resource)資源的集合中傳回您的分析資訊。 


## <a name="span-idsearch_resourcespan-idsearch_resourcespan-idsearch_resourcesearch-resource"></a><span id="Search_Resource"/><span id="search_resource"/><span id="SEARCH_RESOURCE"/>搜尋資源

表示搜尋的所有分析資料。

| 屬性 | 類型 | 描述 |  
|----------|------|-------------|  
| 公司 | 字串 | 帳單公司名稱。 |
| contactButtonClicked | 布林值 | 指出是否已按下 [連絡人] 按鈕。 |
| keywordCountry | 字串 | 搜尋中指定的國家/地區。 |
| detailsViewed | 布林值 | 指出是否已查看搜尋詳細資料。 |
| keywordIndustryFocus | 字串 | 要在其中進行搜尋的產業，例如醫療保健。 |
| mpnId | 字串 | Microsoft 合作夥伴網路（MPN）識別碼。 若為直接轉銷商，這會是合作夥伴的 MPN 識別碼。 若為間接轉銷商，這將是間接轉銷商的 MPN 識別碼。 |
| partnerMarket | 字串 | 合作夥伴開展業務的地區設定。 |
| keywordProduct | 字串 | 搜尋中指定的產品。 |
| referralSubmitted | 布林值 | 指出是否已提交參照。 |
| searchDate | UTC 日期時間格式的字串 | 搜尋查詢的發生日期。 |
| keywordSearchText | 字串 | 搜尋中指定的文字。 |
| searchResultPageViews | 長整數 | 合作夥伴在搜尋結果中的次數。 只有在匯總時才會包含回應的一部分。
| contactClicks | 長整數 | 按一下 [連絡人] 按鈕的次數。 只有在匯總時才會包含回應的一部分。
| referralCount | 長整數 | 從搜尋產生的參考數目。 只有在匯總時才會包含回應的一部分。
| profileViews | 長整數 | 夥伴設定檔的查看次數。 只有在匯總時才會包含回應的一部分。


## <a name="span-idreferral_analyticsspan-idreferral_analyticsspan-idreferral_analyticsreferrals-analytics"></a><span id="Referral_Analytics"/><span id="referral_analytics"/><span id="REFERRAL_ANALYTICS"/>的參考分析

> [!NOTE]  
> 不需要 CSP 方案成員資格即可取得參考分析。

下列案例示範如何流量分析 API 來抓取所有合作夥伴中心的參考分析資訊。  

- [取得所有推薦的分析資訊](get-all-referrals-analytics.md)  

此案例會在[參考](#referrals)資源的集合中傳回您的分析資訊。 

> [!NOTE]  
> 由世紀營運的合作夥伴中心無法使用 [參考分析]。 


## <a name="span-idreferralsspan-idreferralsspan-idreferralsreferrals-resource"></a><span id="Referrals"/><span id="referrals"/><span id="REFERRALS"/>參考資源

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
