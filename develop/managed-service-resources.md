---
title: 受控服務資源
description: 受控服務是夥伴具有委派系統管理員許可權的服務。 合作夥伴可以代表其受管理的服務，提供和檔案服務要求的支援。
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094793"
---
# <a name="managed-service-resources"></a>受控服務資源

**適用於**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

受控服務是夥伴具有委派系統管理員許可權的服務。 合作夥伴可以代表其受管理的服務，提供和檔案服務要求的支援。

## <a name="managedservice"></a>ManagedService

描述受管理的服務。

| 屬性   | 類型                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | 字串              | 受控服務識別碼。                                  |
| 名稱       | 字串              | 受控服務的名稱。                         |
| GroupName  | 字串              | 服務所屬之群組的名稱。      |
| 連結      | ManagedServiceLinks | 對應至受控服務的資源連結。 |
| 屬性 | ResourceAttributes  | 對應于協定的中繼資料屬性。  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

包含連結，可讓具有委派系統管理員許可權的夥伴提供服務的支援。

| 屬性      | 類型 | Description                 |
|---------------|------|-----------------------------|
| AdminService  | 連結 | 管理員服務 URI。      |
| 服務健康狀況 | 連結 | 服務健康情況 URI。     |
| ServiceTicket | 連結 | 服務票證 URI。     |
| Self          | 連結 | 自我 URI。               |
| 下一個          | 連結 | 下一個頁面的專案。     |
| 上一個      | 連結 | 前一頁的專案。 |

