---
title: 合作夥伴安全性需求資源
description: 瞭解多重要素驗證（MFA）採用詳細資料，以符合合作夥伴的安全性需求。
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/08/2020
ms.locfileid: "86094768"
---
# <a name="partner-security-requirements-resources"></a>合作夥伴安全性需求資源

**適用於：**

- 合作夥伴中心

本文可協助您瞭解多重要素驗證（MFA）採用詳細資料，以協助您的組織符合合作夥伴的安全性需求狀態。 

## <a name="portal-request-without-mfa"></a>沒有 MFA 的入口網站要求

指出存取合作夥伴中心入口網站但沒有 MFA 驗證的使用者。

| 屬性                            | 類型            | Description                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | 字串          | 使用者物件識別碼                        |
| TenantId                            | 字串          | CSP 租使用者識別碼                         |
| Upn                                 | 字串          | 使用者主體名稱                   |
| LastNonMfaCompliantLoginDateTime    | Datetime        | 使用者登入沒有 MFA 的最新時間 |


## <a name="api-request-summarized-by-application"></a>應用程式摘要的 API 要求

應用程式 + 使用者認證所提出之 API 要求的摘要，依要求日期和應用程式識別碼進行匯總。

| 屬性                            | 類型            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | Datetime        | API 要求日期          |
| MfaCompliantRequestCount            | long            | 具有 MFA 的要求計數    |
| TotalRequestCount                   | long            | 總要求數       |
| ApplicationId                       | 字串          | 應用程式識別碼        |
| ApplicationName                     | 字串          | 應用程式名稱      |


## <a name="api-request-details"></a>API 要求詳細資料

應用程式 + 使用者認證所提出的 API 要求。 

| 屬性                            | 類型            | 描述                              |
|-------------------------------------|-----------------|------------------------------------------|
| RequestId                           | 字串          | MS-RequestId                             |
| CorrelationId                       | 字串          | 毫秒-CorrelationId                         |
| OperationName                       | 字串          | 具有要求方法的 API 路徑         |
| RequestDateTime                     | Datetime        | API 要求時間                     |
| IpAddress                           | 字串          | 來源 IP 位址                        |
| ObjectId                            | 字串          | 使用者物件識別碼                           |
| TenantId                            | 字串          | CSP 租使用者識別碼                            |
| Upn                                 | 字串          | 使用者主體名稱                      |
| ApplicationId                       | 字串          | 您的應用程式                         |
| MfaCompliant                        | bool            | 指出包含或不含 MFA 的要求 |
