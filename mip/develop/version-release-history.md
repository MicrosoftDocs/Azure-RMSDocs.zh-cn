---
title: Microsoft 信息保护 (MIP) SDK 版本发行历史记录和支持策略
description: 快速入门教程，演示如何为 Microsoft 信息保护 (MIP) SDK 客户端应用程序编写初始化逻辑。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 01/08/2019
ms.author: bryanla
manager: barbkess
ms.openlocfilehash: 1d7b30832441180f8673e7430d7d32e8a58a5205
ms.sourcegitcommit: 8c2de5119105cf5d5bc91fcc2202b64e5a779e7c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2019
ms.locfileid: "56082779"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft 信息保护 (MIP) SDK 版本发行历史记录和支持策略

## <a name="servicing"></a>维护服务 

6 个月后的下一 GA 版本是版本支持每个公开发行 (GA) 版本。 文档可能不包括有关不受支持版本的信息。 修补程序和新功能仅适用于最新 GA 版本。

不应在生产环境中部署预览版本。 相反，使用最新预览版本来测试新功能或修补程序的下一 GA 版本中将出现。 支持仅最新预览版本。

## <a name="release-history"></a>版本历史

使用以下信息查看新增功能或在受支持的版本已更改。 最新版本会最先列出。 

> [!NOTE]
> 因此，如果遇到与 SDK 问题，我们建议您检查它是否具有固定，不会列出小修补程序最新 GA 版本。 如果问题仍然存在，请检查当前预览版。
>  
> 有关技术支持，请访问[Stack Overflow Microsoft 信息保护论坛](https://stackoverflow.com/questions/tagged/microsoft-information-protection)。 

## <a name="version-110"></a>版本 1.1.0

**发布日期**:TBD

此版本引入了对以下平台的支持：

  - .NET
  - iOS SDK (策略 API)
  - Android SDK （API 和保护 API 策略）

**新功能：**

- ADRMS 支持
- 保护 API 操作都是真正异步 （Win32)，从而允许同时进行非阻止加密/解密操作
  - 应用程序回调 （AuthDelegate、 HTTPDelegate 等） 可能会立即调用*任何*后台线程
- 现在可以通过 mip::Label::GetCustomSettings 读取由 IT 管理员设置的自定义标签属性
- 现在可直接从无 mip::FileHandler::GetSerializedPublishingLicense 通过任何 HTTP 操作的文件检索序列化的发布许可证
- 应用程序将收到通知是否完成 mip::FileEngine/mip::PolicyEngine mip::FileProfile::Observer::OnAddPolicyEngineStarting 通过创建所需的 HTTP 操作 / mip::PolicyProfile::Observer::OnAddEngineStarting
- 检测到的或不受保护的内容是否具有到期日期已得到简化了便捷方法 mip::ProtectionDescriptor::DoesContentExpire
- 分类：
  - 敏感类型 (对于 CC # 的正则表达式表达式 passport #，等等) 可以获取从源代码管理服务
    - 通过设置 mip::FileEngine::Settings 启用功能 / mip::PolicyEngine::Settings 标志
    - 读取类型通过 mip::FileEngine::ListSensitivityTypes / mip::PolicyEngine::ListSensitivityTypes
  - 分类结果从外部文档扫描程序实用程序可以提供给 MIP 来驱动根据文档内容的建议/所需的标签
    - 通过 mip::FileExecutionState::GetClassificationResults 将结果传递到 MIP / mip::ExecutionState::GetClassificationResults
    - 当分类结果匹配，该值指示所需/建议标签的策略规则时可由 mip::PolicyEngine::ComputeActions 返回 mip::ApplyLabelAction 和 mip::RecommendLabelAction

- 新的要求：
  - 已强制实施的 ID/名称/版本字段 mip::ApplicationInfo 创建 mip::FileProfile、 mip::PolicyProfile 和 mip::ProtectionProfile 时填充
  - 创建 mip::FileHandlers 时，应用程序必须实现新 mip::FileExecutionState 接口
  
- 更新后的异常：
  - 如果应用程序的 AuthDelegate 返回 （由于取消） 的空令牌，则引发 mip::NoAuthTokenError
    - 适用于创建的：
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - 如果租户未配置的标签，则引发 mip::NoPolicyError
    - 适用于创建的：
      - mip::FileEngine
      - mip::PolicyEngine
  - 如果为特定用户/设备/平台/租户禁用 RMS service，则引发 mip::ServiceDisabledError
    - 适用于创建的：
      - mip::FileHandler
      - mip::ProtectionHandler
  - 如果用户没有权限来解密内容或文档引发 mip::NoPermissionsError 已过期
    - 适用于创建的：
      - mip::FileHandler
      - mip::ProtectionHandler

**修补程序**：

TBD

## <a name="next-steps"></a>后续步骤

- 请参阅[MIP SDK 常见问题解答和问题](faqs-known-issues.md)有关受支持的平台和的详细信息。
- 请参阅[MIP SDK 设置和配置](setup-configure-mip.md)有关如何开始使用 MIP SDK 的信息。