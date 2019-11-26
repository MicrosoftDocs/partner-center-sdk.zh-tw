---
title: Managed service resources
description: Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.
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
# <a name="managed-service-resources"></a>Managed service resources


**Applies To**

- 合作夥伴中心
- 由 21Vianet 營運的合作夥伴中心
- Microsoft Cloud 德國合作夥伴中心
- Microsoft Cloud for US Government 適用的合作夥伴中心

Managed services are services to which a partner has delegated admin privileges. Partners can provide support for and file service requests on the behalf of their managed services.

## <a name="span-idmanagedservicespan-idmanagedservicespan-idmanagedservicemanagedservice"></a><span id="ManagedService"/><span id="managedservice"/><span id="MANAGEDSERVICE"/>ManagedService


Describes a managed service.

| 屬性   | 在工作列搜尋方塊中輸入                | 說明                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | 字串              | The managed service id.                                  |
| 名稱       | 字串              | The name of the managed service.                         |
| GroupName  | 字串              | The name of the group to which the service belongs.      |
| 連結      | ManagedServiceLinks | The resource links corresponding to the managed service. |
| 屬性 | ResourceAttributes  | The metadata attributes corresponding to the agreement.  |

 

## <a name="span-idmanagedservicelinksspan-idmanagedservicelinksspan-idmanagedservicelinksmanagedservicelinks"></a><span id="ManagedServiceLinks"/><span id="managedservicelinks"/><span id="MANAGEDSERVICELINKS"/>ManagedServiceLinks


Contains the links that allow the partner with delegated admin permissions to provide support for the service.

| 屬性      | 在工作列搜尋方塊中輸入 | 說明                 |
|---------------|------|-----------------------------|
| AdminService  | Link | The admin service URI.      |
| ServiceHealth | Link | The service health URI.     |
| ServiceTicket | Link | The service ticket URI.     |
| Self          | Link | The self URI.               |
| [下一步]          | Link | The next page of items.     |
| 上一則      | Link | The previous page of items. |

 

 

 




