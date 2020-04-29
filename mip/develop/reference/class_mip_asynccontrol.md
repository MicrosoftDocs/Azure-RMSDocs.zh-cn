---
title: 类 AsyncControl
description: 记录 Microsoft 信息保护（MIP） SDK 的 asynccontrol：：未定义的类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 04/16/2020
ms.openlocfilehash: d032abf9fe7192cfe6ccfd5890d6585aaa2ba645
ms.sourcegitcommit: f54920bf017902616589aca30baf6b64216b6913
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2020
ms.locfileid: "81763657"
---
# <a name="class-asynccontrol"></a>类 AsyncControl 
用于取消异步操作的类。
  
## <a name="summary"></a>“摘要”
 成员                        | 说明                                
--------------------------------|---------------------------------------------
public bool Cancel （）  |  调用 "取消" 将导致尝试取消任务。如果成功，则将使用 mip：： OperationCancelledError 调用适当的 onFailure 回调。 此功能依赖于任务调度程序委托（。
  
## <a name="members"></a>成员
  
### <a name="cancel-function"></a>Cancel 函数
调用 "取消" 将导致尝试取消任务。如果成功，则将使用 mip：： OperationCancelledError 调用适当的 onFailure 回调。 此功能依赖于任务调度程序委托（。
  
**另请参阅**： mip：： TaskDispatcherDelegate）、

  
**返回**：如果无法调度取消信号，则返回 False; 否则返回 true。
不要在任务完成块中保留对 AsyncControl 对象的强引用。