---
title: 概念 - MIP SDK 中的 API。
description: 本文将帮助你了解 MIP SDK 中的三类 API、其关联方式及每种 API 的用例。
author: BryanLa
ms.service: information-protection
ms.topic: conceptual
ms.date: 09/27/2018
ms.author: bryanla
ms.openlocfilehash: a625df159a00a955d155850ff4e326d1e0d204e5
ms.sourcegitcommit: 823a14784f4b34288f221e3b3cb41bbd1d5ef3a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2018
ms.locfileid: "47453326"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>Microsoft 信息保护 SDK - API 概念

MIP SDK 由三个 API 组成：

- [保护 API](#protection-api)
- [策略 API](#policy-api)
- [文件 API](#file-api)

## <a name="protection-api"></a>保护 API

借助保护 API，软件开发人员能够将纯文本流转换为权限管理流，反之亦然。

### <a name="protection-api-use-cases"></a>保护 API 用例

- 你的组织开发了一个使用专有文件格式的 3D 打印软件。 你希望使用 MIP 保护文件，从而让文件只能由特定用户进行打印。 借助保护 API，你可以对文件应用保护，以便只有经过授权的使用者才能打开和/或打印。 

- 你的组织开发了一个处理 Exchange 邮箱和 PST 文件的电子数据展示解决方案。 你的应用程序必须能够为用户解密消息才能完全执行电子数据展示。 借助自定义消息/RPMSG 分析程序和拥有足够特权的帐户，你可以利用 RMS API 来解密加密的文件、扫描内容，以及在超出范围时丢弃或在属于范围内时打包。

## <a name="policy-api"></a>策略 API

借助策略 API（又称为通用策略引擎 [UPE]），软件开发人员能够为特定用户获取标签策略，然后“计算”这些标签应采取的操作。

策略 API 主要由开发人员控制接口和文件格式的客户端应用程序使用，或者由唯一的要求是获取用户策略而不必直接标记文件的客户端应用程序使用。 

### <a name="policy-api-use-cases"></a>策略 API 用例

- 你的组织开发了一个使用专有文件格式的 3D 设计软件。 你的客户使用 Microsoft 信息保护，并希望能够通过你的应用程序在本机应用标签。 作为软件工程师，你可以使用策略 API 和自定义控件来为经过身份验证的用户显示可用标签。 一旦用户选择了标签，你就可以调用 API 的计算操作方法来具体了解应该应用的内容，包括元数据、内容标记和保护信息。

- 你的组织开发了一项 DLP 服务，该服务允许客户通过中央管理门户配置 DLP 策略。 你的客户使用 Microsoft 信息保护，并希望能够通过 DLP 策略读取或应用 AIP 标签。 作为软件工程师，你可以使用策略 API 获取客户组织的标签列表，然后在 DLP 规则的一部分中读取这些标签，或在规则操作的一部分中应用标签信息。

## <a name="file-api"></a>文件 API

文件 API 是保护 API 和策略 API 的抽象。 它提供易于使用的界面，可用于从服务中读取标签、将标签应用于定义的文件类型，以及从这些文件类型中读取标签。 文件 API 可由任何服务或应用程序使用，前提是涉及支持的文件类型，并且必须读取或写入标签，或者保护或解密内容。

### <a name="file-api-use-cases"></a>文件 API 用例

- 你是一家金融服务机构的软件工程师。 你希望确保来自 LOB 应用程序的数据（通常以 Excel 格式导出）在导出时根据内容进行标记。 文件 API 可用于列出可用的标签，然后将适当的标签应用于支持的文件格式。

- 你的组织开发了一款云访问安全代理 (CASB)。 你的客户要求能够将 MIP 标签应用于 Microsoft Office 和 PDF 文档。 借助文件 API，你能够显示已配置标签的列表，然后允许你的客户生成将应用所需标签的规则。 文件 API（采用标签 ID）将为符合客户标准的文件完成其余操作。

- 你的组织提供基于服务的数据丢失防护解决方案和/或用于监视 SaaS 应用程序的文件活动的 CASB。 若要降低使用 MIP 保护数据时的数据丢失或泄漏风险，你的服务必须能够扫描受保护文件的内容。 如果为支持的格式使用文件 API，当服务为特权用户时，你可以删除保护信息、扫描内容以查找是否存在受限制内容或敏感内容、放弃纯文本结果，以及应用服务规则来报告风险或对风险进行补救（如找到）。

## <a name="next-steps"></a>后续步骤

你已经粗略了解可用的 MIP API 及其使用方法，请继续学习[配置文件和引擎对象概念](concept-profile-engine-cpp.md)。 这些概念是基本常识，适用于所有 MIP API 集。