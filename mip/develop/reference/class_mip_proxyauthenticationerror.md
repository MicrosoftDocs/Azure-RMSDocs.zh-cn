---
title: 类 mip：:P roxyAuthenticationError
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：:p roxyauthenticationerror 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: c0289f9b2f2a8a1163e62e6c6a96e3023f297194
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489616"
---
# <a name="class-mipproxyauthenticationerror"></a>类 mip：:P roxyAuthenticationError 
代理身份验证失败。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
公共类别 GetCategory （） const  |  获取网络故障的类别。
public int32_t GetResponseStatusCode （） const  |  获取 HTTP 响应状态代码。
枚举类别  |  网络错误类别。
  
## <a name="members"></a>Members
  
### <a name="getcategory-function"></a>GetCategory 函数
获取网络故障的类别。

  
**返回**：网络失败类别
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode 函数
获取 HTTP 响应状态代码。

  
**返回**： HTTP 响应状态代码，0（如果没有）
  
### <a name="category-enum"></a>类别枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
未知            | 未知的网络故障
FailureResponseCode            | HTTP 响应代码指示失败
BadResponse            | 无法读取 HTTP 响应
UnexpectedResponse            | HTTP 响应已完成，但包含意外数据
NoConnection            | 未能建立连接
代理            | 代理失败
SSL            | SSL 故障
超时            | 连接超时
脱机            | 操作需要网络连接
Throttled            | 由于服务器流量中止，HTTP 操作失败
已取消            | 应用程序已取消 HTTP 操作
网络错误类别。