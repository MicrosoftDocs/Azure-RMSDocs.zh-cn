---
title: Microsoft 信息保护 (MIP) SDK 版本发行历史记录和支持策略
description: 快速入门教程，演示如何为 Microsoft 信息保护 (MIP) SDK 客户端应用程序编写初始化逻辑。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 01/08/2019
ms.author: mbaldwin
manager: barbkess
ms.openlocfilehash: c2a5d89bf318d9e685d00033ba3ad53915659cdb
ms.sourcegitcommit: fcde8b31f8685023f002044d3a1d1903e548d207
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2019
ms.locfileid: "69882668"
---
# <a name="microsoft-information-protection-mip-sdk-version-release-history-and-support-policy"></a>Microsoft 信息保护 (MIP) SDK 版本发行历史记录和支持策略

## <a name="servicing"></a>服务 

每个正式发布 (GA) 版本在下一正式发行版发布后的六个月内受支持。 文档可能不包含有关不支持的版本的信息。 修补程序和新功能仅适用于最新的 GA 版本。

不应在生产中部署预览版本。 请改用最新的预览版本来测试新功能或即将推出的新功能或修补程序。 仅支持最新的预览版本。

## <a name="release-history"></a>版本历史

使用以下信息可查看受支持版本的新增功能或更改内容。 最新版本会最先列出。 

> [!NOTE]
> 不会列出小修补程序, 因此, 如果您在使用 SDK 时遇到问题, 我们建议您检查是否已通过最新的 GA 版本修复了此问题。 如果问题仍然存在，请检查当前预览版。
>  
> 若要获得技术支持, 请访问[Microsoft 信息保护论坛 Stack Overflow](https://stackoverflow.com/questions/tagged/microsoft-information-protection)。 


## <a name="version-130"></a>版本1.3。0

**发布日期**:TBD

## <a name="version-120"></a>版本1.2。0

**发布日期**:2019年4月15日

## <a name="version-110"></a>版本1.1。0

**发布日期**:2019年1月15日

此版本引入了对以下平台的支持:

  - .NET
  - iOS SDK (策略 API)
  - Android SDK (策略 API 和保护 API)

**新功能：**

- ADRMS 支持
- 保护 API 操作真正是异步的 (在 Win32 上), 允许同时进行非阻塞加密/解密操作
  - 现在可以在*任何*后台线程上调用应用程序回调 (AuthDelegate、HTTPDelegate 等)
- IT 管理员设置的自定义标签属性现在可以通过 mip:: Label:: GetCustomSettings 进行读取
- 现在可以直接从文件中检索序列化发布许可证, 无需通过 mip:: FileHandler:: GetSerializedPublishingLicense 进行任何 HTTP 操作
- 当完成通过 mip:: FileProfile:::P FileEngine olicyEngine via mip:::: Observer:: OnAddPolicyEngineStarting/mip::P olicyProfile:: Observer:: OnAddEngineStarting 创建 mip:::: 时, 将通知应用程序是否需要 HTTP 操作
- 检测到受保护的内容是否有过期日期, 或未使用便利方法 mip 进行简化::P rotectionDescriptor::D oesContentExpire
- 分类
  - 可从 SCC 服务获取敏感度类型 (用于 CC #、passport # 等的正则表达式)
    - 通过设置 mip:: FileEngine:: Settings/mip::P olicyEngine:: Settings 标志来启用功能
    - 通过 mip:: FileEngine:: ListSensitivityTypes/mip::P olicyEngine:: ListSensitivityTypes 读取类型
  - 可以将外部文档扫描程序实用工具的分类结果送入到 MIP, 以根据文档内容来驱动推荐/必需的标签
    - 通过 mip:: FileExecutionState:: GetClassificationResults/MIP:: Executionstate&:: GetClassificationResults 将结果传递给 MIP
    - 当分类结果与指示必需/推荐标签的策略规则匹配时, mip:: ApplyLabelAction 和 mip:: RecommendLabelAction 可以由 mip::P olicyEngine:: ComputeActions 返回

- 新要求:
  - 已强制填充 ID/名称/版本字段 mip:: ApplicationInfo 创建 mip:: FileProfile、mip::P olicyProfile 和 mip::P rotectionProfile
  - 创建 mip:: FileHandlers 时, 应用程序必须实现新的 mip:: FileExecutionState 接口
  
- 更新的异常:
  - mip:: NoAuthTokenError 在应用程序的 AuthDelegate 返回空标记时引发 (因为取消)
    - 适用于创建:
      - mip::FileEngine
      - mip::FileHandler
      - mip::PolicyEngine
      - mip::ProtectionHandler
  - 如果未为标签配置租户, 则引发 mip:: NoPolicyError
    - 适用于创建:
      - mip::FileEngine
      - mip::PolicyEngine
  - 如果为特定用户/设备/平台/租户禁用了 RMS 服务, 则引发 mip:: ServiceDisabledError
    - 适用于创建:
      - mip::FileHandler
      - mip::ProtectionHandler
  - 如果用户无权解密文档或内容已过期, 则引发 mip:: NoPermissionsError
    - 适用于创建:
      - mip::FileHandler
      - mip::ProtectionHandler

**修补程序**：

TBD

## <a name="next-steps"></a>后续步骤

- 有关支持的平台等的信息, 请参阅[MIP SDK faq 和问题](faqs-known-issues.md)。
- 有关如何开始利用 MIP SDK 的信息, 请参阅[MIP sdk 设置和配置](setup-configure-mip.md)。
