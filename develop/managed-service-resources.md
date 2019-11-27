---
title: 受控服務資源
description: 受控服務是夥伴具有委派系統管理員許可權的服務。 合作夥伴可以代表其受管理的服務，提供和檔案服務要求的支援。
ms.assetid: B05E9585-72E4-4330-8721-A88EC4C193D7
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.localizationpriority: medium
ms.openlocfilehash: 32cc11190425c2cdfdbf6c793ef75091915e5d69
ms.sourcegitcommit: fbfad1ae706c8e4bdae080e5d79bc158d6b55d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2019
ms.locfileid: "74486898"
---
# <a name="managed-service-resources"></a>受控服務資源


**適用于**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

受控服務是夥伴具有委派系統管理員許可權的服務。 合作夥伴可以代表其受管理的服務，提供和檔案服務要求的支援。

## <a name="span-idmanagedservicespan-idmanagedservicespan-idmanagedservicemanagedservice"></a><span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


描述受管理的服務。

| 屬性   | 類型                | 描述                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | 字串              | 受控服務識別碼。                                  |
| 名稱       | 字串              | 受控服務的名稱。                         |
| GroupName  | 字串              | 服務所屬之群組的名稱。      |
| 連結      | ManagedServiceLinks | 對應至受控服務的資源連結。 |
| 屬性 | ResourceAttributes  | 對應于協定的中繼資料屬性。  |

 

## <a name="span-idmanagedservicelinksspan-idmanagedservicelinksspan-idmanagedservicelinksmanagedservicelinks"></a><span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


包含連結，可讓具有委派系統管理員許可權的夥伴提供服務的支援。

| 屬性      | 類型 | 描述                 |
|---------------|------|-----------------------------|
| AdminService  | Link | 管理員服務 URI。      |
| ServiceHealth | Link | 服務健康情況 URI。     |
| ServiceTicket | Link | 服務票證 URI。     |
| Self          | Link | 自我 URI。               |
| 下一則          | Link | 下一個頁面的專案。     |
| 上一則      | Link | 前一頁的專案。 |

 

 

 




