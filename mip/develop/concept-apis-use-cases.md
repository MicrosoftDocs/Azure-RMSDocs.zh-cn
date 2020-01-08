---
title: 概念 - MIP SDK 中的 API。
description: 本文将帮助你了解 MIP SDK 中的三类 API、其关联方式及每种 API 的用例。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.date: 10/16/2018
ms.author: mbaldwin
ms.openlocfilehash: 580e2c14d60c60ccb42d5d8553d4f37a705b4c0f
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75556276"
---
# <a name="microsoft-information-protection-sdk---api-concepts"></a>Microsoft 信息保护 SDK - API 概念

Microsoft 信息保护 (MIP) SDK 由三个 API 组成，如以下关系图中所示：

[![MIP SDK API 关系图](media/concept-apis-use-cases/mip-sdk-components.png)](media/concept-apis-use-cases/mip-sdk-components.png#lightbox)

根据你的应用程序的需求，你可能需要文件 API 层中的接口，或可能需要直接使用策略或保护 API 层。

## <a name="file-api"></a>文件 API

文件 API 是保护 API 和策略 API 的抽象。 它提供易于使用的界面，可用于从服务中读取标签、将标签应用于定义的文件类型，以及从这些文件类型中读取标签。 文件 API 将在以下情况中由任何服务或应用程序使用：

- 涉及到支持的文件类型
- 必须读取或写入标签
- 必须保护或解密内容

### <a name="file-api-use-cases"></a>文件 API 用例

- 你是一家金融服务机构的软件工程师。 你希望确保来自 LOB 应用程序的数据（通常以 Excel 格式导出）在导出时根据内容进行标记。 文件 API 可用于列出可用的标签，然后将适当的标签应用于支持的文件格式。

- 你的组织开发了一款云访问安全代理 (CASB)。 你的客户要求能够将 MIP 标签应用于 Microsoft Office 和 PDF 文档。 借助文件 API，你能够显示已配置标签的列表，然后允许你的客户生成将应用给定标签的规则。 文件 API（采用标签 ID）将为符合客户标准的文件完成其余操作。

- 你的组织提供基于服务的数据丢失防护解决方案或用于监视 SaaS 应用程序的文件活动的 CASB。 若要降低使用 MIP 保护数据时的数据丢失或泄漏风险，你的服务必须扫描受保护文件的内容。 为支持的格式使用文件 API，当服务是特权用户时，它能够：

  1. 删除保护
  2. 扫描内容是否是受限制内容或敏感内容
  3. 放弃纯文本结果
  4. 将服务规则应用于报表或修正风险（如果发现）

## <a name="policy-api"></a>策略 API

借助策略 API（又称为通用策略引擎 (UPE)），软件开发人员能够为特定用户检索标签策略。 然后“计算”这些标签应采取的操作。

策略 API 主要由客户端应用程序使用，其中开发人员控制接口和文件格式。 当唯一要求是检索用户策略，而非直接检索标签文件时，也使用策略 API。 

### <a name="policy-api-use-cases"></a>策略 API 用例

- 你的组织开发了一个使用专有文件格式的 3D 设计软件。 你的客户使用 MIP，并希望通过你的应用程序在本机应用标签。 作为软件工程师，你使用策略 API 和自定义控件为经过身份验证的用户显示可用标签。 用户选择标签后，你调用 API 的计算操作方法。 API 告知你关于元数据、内容标记和保护方面应应用的具体内容。

- 你的组织开发了一项数据丢失防护 (DLP) 服务，该服务允许客户通过中央管理门户配置 DLP 策略。 你有使用 MIP 的客户，并需要读取或应用 AIP 标签，作为 DLP 策略的一部分。 作为软件工程师，你可以使用策略 API 来获取客户组织的标签列表。 然后，你可以将这些标签读取为 DLP 规则的一部分，或将标签信息应用为规则操作的一部分。

## <a name="protection-api"></a>保护 API

借助保护 API，软件开发人员能够将纯文本流转换为权限管理流，反之亦然。

### <a name="protection-api-use-cases"></a>保护 API 用例

- 你的组织开发了一个使用专有文件格式的 3D 打印软件。 你希望使用 MIP 保护文件，从而让文件只能由特定用户进行打印。 借助保护 API，你可以对文件应用保护，以便只有经过授权的客户才能打开和复印它。 

- 你的组织开发了一个处理 Exchange 邮箱和 .PST 文件的电子数据展示解决方案。 你的应用程序需要允许用户解密消息才能执行电子数据展示。 通过使用自定义消息/RPMSG 分析程序和足够的特权帐户，你可以使用 RMS API 执行以下操作：
  - 解密已加密的文件
  - 扫描内容
  - 如果超出作用域，则放弃，如果在作用域内，则打包

## <a name="next-steps"></a>后续步骤

你已经粗略了解可用的 MIP API 及其使用方法，请继续学习[配置文件和引擎对象概念](concept-profile-engine-cpp.md)。 这些概念是基本常识，适用于所有 MIP API 集。
