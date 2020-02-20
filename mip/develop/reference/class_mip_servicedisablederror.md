---
title: 类 mip：： ServiceDisabledError
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： servicedisablederror 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: 1481e81707e84d7ba977d36bec152ba86b5e60b6
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77489412"
---
# <a name="class-mipservicedisablederror"></a>类 mip：： ServiceDisabledError 
由于服务被禁用，用户无法访问内容。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
公共区 GetExtent （） const  |  获取服务的禁用范围。
枚举范围  |  描述服务的禁用范围。
  
## <a name="members"></a>Members
  
### <a name="getextent-function"></a>GetExtent 函数
获取服务的禁用范围。

  
**返回**：禁用服务的范围
  
### <a name="extent-enum"></a>区枚举
 值                         | 说明                                
--------------------------------|---------------------------------------------
用户            | 已为用户禁用服务。
设备            | 设备的服务已禁用。
平台            | 平台已禁用服务。
租户            | 租户的服务已禁用。
描述服务的禁用范围。