---
title: 类 AsyncControl
description: 记录 (MIP) SDK 的 Microsoft 信息保护的 asynccontrol：：未定义的类。
author: msmbaldwin
ms.service: information-protection
ms.topic: reference
ms.author: mbaldwin
ms.date: 09/21/2020
ms.openlocfilehash: 7058ccdcac0133bc708a81d5e7342f61c48994f9
ms.sourcegitcommit: 3f5f9f7695b9ed3c45e9230cd8b8cb39a1c5a5ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "95565228"
---
# <a name="class-asynccontrol"></a>类 AsyncControl 
用于取消异步操作的类。
  
## <a name="summary"></a>总结
 成员                        | 说明                                
--------------------------------|---------------------------------------------
公共 bool 取消 ( # A1  |  调用 "取消" 将导致尝试取消任务。如果成功，则将使用 mip：： OperationCancelledError 调用适当的 onFailure 回调。 此功能依赖于任务调度程序委托 (。
  
## <a name="members"></a>成员
  
### <a name="cancel-function"></a>Cancel 函数
调用 "取消" 将导致尝试取消任务。如果成功，则将使用 mip：： OperationCancelledError 调用适当的 onFailure 回调。 此功能依赖于任务调度程序委托 (。
  
**另请参阅**： mip：： TaskDispatcherDelegate) 

  
**返回**：如果无法调度取消信号，则返回 False; 否则返回 true。
不要在任务完成块中保留对 AsyncControl 对象的强引用。