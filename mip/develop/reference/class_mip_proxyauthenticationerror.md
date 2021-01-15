---
title: 类 ProxyAuthenticationError
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 proxyauthenticationerror：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 01/13/2021
ms.openlocfilehash: 04915e74cc09f271a2ca3bb256b906bc442bb3fd
ms.sourcegitcommit: 76926b357bbfc8772ed132ce5f2426fbea59e98b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2021
ms.locfileid: "98214297"
---
# <a name="class-proxyauthenticationerror"></a>类 ProxyAuthenticationError 
代理身份验证失败。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共类别 GetCategory ( # A1 const  |  获取网络故障的类别。
public int32_t GetResponseStatusCode ( # A1 const  |  获取 HTTP 响应状态代码。
枚举类别  |  网络错误类别。
  
## <a name="members"></a>成员
  
### <a name="getcategory-function"></a>GetCategory 函数
获取网络故障的类别。

  
**返回**：网络失败类别
  
### <a name="getresponsestatuscode-function"></a>GetResponseStatusCode 函数
获取 HTTP 响应状态代码。

  
**返回**： HTTP 响应状态代码，0（如果没有）
  
### <a name="category-enum"></a>类别枚举

网络错误类别。

 值                         | 说明                                
--------------------------------|---------------------------------------------
Unknown            | 未知的网络故障
FailureResponseCode            | HTTP 响应代码指示失败
BadResponse            | 无法读取 HTTP 响应
UnexpectedResponse            | HTTP 响应已完成，但包含意外数据
NoConnection            | 未能建立连接
Proxy (代理)            | 代理失败
SSL            | SSL 故障
超时            | 连接超时
Offline            | 操作需要网络连接
已中止            | 由于服务器流量中止，HTTP 操作失败
已取消            | 应用程序已取消 HTTP 操作
