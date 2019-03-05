---
title: 概念 - 分类标签
description: 本文将帮助你了解如何使用标签进行数据分类。
author: msmbaldwin
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 09/27/2018
ms.author: mbaldwin
ms.openlocfilehash: e1101bd505a35e02fdeeed032d5dec61364bfb8d
ms.sourcegitcommit: 471b3683367d93f0673c1cf276a15f83572aa80e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57333664"
---
# <a name="microsoft-information-protection-sdk---classification-label-concepts"></a>Microsoft 信息保护 SDK - 分类标签概念

作为全面数据保护战略的一部分，组织应实施数据分类系统来概述组织内数据的敏感程度，然后向这些分类映射文档属性。

如果该文档或数据丢失或被意外的使用者看到，则与分类相关的属性通常会给组织带来**风险**。 在为大众所熟知的美国政府分类系统中，一共有三个分类级别。 每个级别都有一个定义，描述了何时应该应用该分类：

* **排名靠前的机密**:应将应用于的未经授权的泄漏可能预计会导致灾难性损失的原始分类颁发机构是可以用于标识或描述国家安全的信息。
* **机密**:应将应用于的未经授权的泄漏可能预计会导致严重损失的原始分类颁发机构是可以用于标识或描述国家安全的信息。
* **机密**:应将应用于的未经授权的泄漏可能预计会导致损失的原始分类颁发机构是可以用于标识或描述国家安全的信息。
* **未分类**:这不是实际的分类，而不是上述三种之一不存在。

在商业或私营部门应用程序中，我们可以定义一个列表，类似于 Azure 信息保护服务中的默认列表，并附加货币值。

* **高度机密**:应将应用于信息，其中未经授权的泄漏可能预计会导致大于 USD 为 1 百万美元的损失。
* **机密**:应将应用于信息，其中未经授权的泄漏可能预计会导致比美元万美元奖金的更大的损害。
* **常规**:应将应用于信息，其中未经授权的泄漏可能预计会导致一些可衡量的损害。
* **公共**:应将应用于面向公共的、 外部消费的信息。 
* **非业务**:应将应用于不与公司业务，直接或间接相关的信息。

每个分类描述了在未经授权泄漏该信息的情况下对企业造成的风险。 在确定这些分类和条件后，应确定属性，以帮助数据所有者了解要应用的分类。

## <a name="labeling"></a>添加标签

将数据分类与一组信息相关联的行为称为**添加标签**。 由于 MIP SDK 正在向文档应用分类**标签**，因此我们所指的不是分类，而是标签。 用户或进程已经**分类**数据基于知识的信息：MIP SDK 将然后**标签**信息。

## <a name="labels-in-the-mip-sdk"></a>MIP SDK 中的标签

标签是 MIP SDK 的基本组件。 标签用于对 SDK 触及的所有文档进行标记、保护和内容标记。 SDK 可以：

* 向文档应用标签
* 读取文档上的现有标签
* 在策略要求下更改现有标签并强制说明理由
* 从文档中删除标签

标签将根据标签管理员在安全与合规中心定义的配置应用保护和内容标记。 

## <a name="miplabel-vs-mipcontentlabel"></a>mip::Label vs. mip::ContentLabel

MIP SDK 中存在两种标签。 `Label` 和`ContentLabel`。

* 标签：组织的策略中定义可由用户或进程应用标签。
* ContentLabel:已存在于文档或信息的标签。 可对其进行读取、更新或删除。 

换而言之，`ContentLabel` 是已应用于某条信息的 `Label`。

## <a name="metadata"></a>元数据

SDK 还支持以键/值对的形式向文档添加额外的元数据。 如果组织具有以更具体的方式描述信息的子分类或标记，则可以使用 SDK 应用该元数据。

## <a name="next-steps"></a>后续步骤

有关美国政府分类系统的更多详细信息，请参阅 https://www.gpo.gov/fdsys/pkg/FR-2010-01-05/html/E9-31418.htm。
