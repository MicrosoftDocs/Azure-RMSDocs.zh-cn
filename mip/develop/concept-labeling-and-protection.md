---
title: 标签和保护-Microsoft 信息保护 SDK
description: Microsoft 信息保护软件开发工具包操作。
author: msmbaldwin
ms.author: mbaldwin
ms.date: 08/20/2020
ms.topic: conceptual
ms.service: information-protection
ms.openlocfilehash: 2e18b9ae65a4915807fdcb8fc37dd18396270fee
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865003"
---
# <a name="labeling-and-pre-existing-protection-in-microsoft-information-protection-sdk"></a>Microsoft 信息保护 SDK 中的标签和预先存在的保护

Microsoft 信息保护支持标记和分类服务。 用户和应用程序可将以下内容应用于支持的文件：

- 仅通过应用标签进行分类

- 通过应用标签来分类和保护

- 仅保护

本文讨论 SDK 如何处理将标签应用于具有预先存在的保护的文件的尝试。 当文档通过应用标签或其他方式预先存在保护时，SDK 会在应用场景中处理新标签的应用，如下所示。

## <a name="label-based-protection-when-label-metadata-has-been-stripped"></a>去除标签元数据时基于标签的保护

如果文件已应用标签，并且该标签应用了保护，则 SDK 应该能够将文件保护解析为特定标签。 如果对该文件具有 "编辑" 权限的用户将不小心或恶意地删除标签元数据，则仍将保留该保护。 当下一次 SDK 与文件交互时，它会查看保护数据，将该保护模板解析为原始标签，并重新应用该标签。 这是 SDK 中内置的安全机制，用于信息保护以防标签元数据被篡改。

## <a name="custom-protection-and-label-applications"></a>自定义保护和标签应用程序

如果该文件采用某种形式的保护，则通过 RMS 模板和用户尝试将标签应用到该文件时，SDK 首先需要能够对标签解析原始保护。 如果无法执行此操作，SDK 将无法评估新保护敏感度级别是否比原始保护敏感度更严格或更宽松，因此 SDK 不会将新标签应用于文件。

## <a name="user-defined-permissions"></a>用户定义的权限

如果文件应用了标签，并且该标签应用了用户定义的保护，则会将保护应用到文件，但 SDK 无法将该文件解析为 RMS 模板。 在这种情况下，当用户尝试对文件应用新标签时，SDK 会将操作视为类似于上述操作，而不会将新标签应用于文件。
