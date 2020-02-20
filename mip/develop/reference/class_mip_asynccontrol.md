---
title: 类 mip：： AsyncControl
description: 记录 Microsoft 信息保护（MIP） SDK 的 mip：： asynccontrol 类。
author: BryanLa
ms.service: information-protection
ms.topic: reference
ms.author: bryanla
ms.date: 02/14/2020
ms.openlocfilehash: afef25cef1363d5275581a774279c97d61239f4b
ms.sourcegitcommit: 2d3c638fb576f3f074330a33d077db0cf0e7d4e7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/20/2020
ms.locfileid: "77492760"
---
# <a name="class-mipasynccontrol"></a>类 mip：： AsyncControl 
用于取消异步操作的类。
  
## <a name="summary"></a>摘要
 Members                        | 说明                                
--------------------------------|---------------------------------------------
public bool Cancel （）  |  调用 "取消" 将导致尝试取消任务。如果成功，则将使用 mip：： OperationCancelledError 调用适当的 onFailure 回调。 此功能依赖于任务调度程序委托（。
  
## <a name="members"></a>Members
  
### <a name="cancel-function"></a>Cancel 函数
调用 "取消" 将导致尝试取消任务。如果成功，则将使用 mip：： OperationCancelledError 调用适当的 onFailure 回调。 此功能依赖于任务调度程序委托（。
  
**另请参阅**： mip：： TaskDispatcherDelegate）、

  
**返回**：如果无法调度取消信号，则返回 False; 否则返回 true。
不要在任务完成块中保留对 AsyncControl 对象的强引用。