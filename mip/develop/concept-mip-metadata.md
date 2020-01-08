---
title: 概念-在 MIP SDK 中标记元数据
description: 本文将帮助你了解 Microsoft 信息保护 SDK 生成的元数据。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 6713ba0d8b6727f3ed10e4b3846cbe2bb1b43f6e
ms.sourcegitcommit: 99eccfe44ca1ac0606952543f6d3d767088de425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/31/2019
ms.locfileid: "75555681"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft 信息保护 SDK-元数据

Microsoft 信息保护 SDK 生成应应用于文件的一组元数据。 此元数据是标签的表示形式。 本文档描述了 SDK 生成的元数据，以应用于邮件、文档和其他记录。

## <a name="labels"></a>标签

Microsoft 信息保护 SDK 中的标签应用于信息，以描述该信息的敏感性。 标签数据将保存到一组用于描述标签的键值对中的文件或记录。 元数据名称是根据以下结构生成的：

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

当应用于标记为 Microsoft 信息保护的数据时，结果为：

`MSIP_Label_GUID_Enabled = true`

GUID 是组织中每个标签的唯一标识符。

## <a name="microsoft-information-protection-sdk-metadata"></a>Microsoft 信息保护 SDK 元数据

MIP SDK 应用以下一组元数据。

| 属性 | 类型或值                 | Description                                                                                                                                                                                                                                        | 强制 |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **Enabled**   | True 或 False                 | 此属性指示是否为数据项启用这组键/值对所表示的分类。 DLP 产品通常会验证是否存在此密钥来识别分类标签。 | “是”       |
| **SiteId**    | GUID                          | Azure Active Directory 租户 ID                                                                                                                                                                                                                   | “是”       |
| **ActionId**  | GUID                          | 每次设置标签时，均会更改 ActionID。 审核日志将包括新旧的 actionID，以允许将标签活动链接到数据项。                                                                                 | “是”       |
| **方法**    | 标准或特权        | 通过[mip：： AssignmentMethod](reference/mip-enums-and-structs.md#assignmentmethod-enum)设置。 标准表示标签默认应用或自动应用。 特权意味着手动选择标签。                                                                                                                                                                                                                 | 否        |
| **SetDate**   | 延长 ISO 8601 日期格式 | 设置标签时的时间戳。                                                                                                                                                                                                              | 否        |
| **Name**      | 字符串                        | 标记租户内的唯一名称。 它不一定对应于显示名称。                                                                                                                                                              | 否      |
| **ContentBits** | integer | 用于描述应应用于文件的内容标记类型的位掩码。 CONTENT_HEADER = 0X1，CONTENT_FOOTER = 0X2，水印 = 0X4，加密 = 0x8
 | 否 |

当应用于某个文件时，结果与下表类似。

| Key                                                         | 值                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | 是                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21：13： 16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method      | 特权                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | 机密                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>用自定义特性扩展元数据

可以通过文件和策略 API 追加自定义元数据。 自定义属性必须保留基本 `MSIP_Label_GUID` 前缀。 

例如，Contoso Corporation 编写的应用程序必须应用元数据，指示哪个系统生成了标记文件。 应用程序可以创建一个新标签，以 `MSIP_Label_GUID`为前缀。 软件供应商名称和自定义属性将追加到前缀以生成自定义元数据。

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> 为了保持常见应用程序之间的兼容性，每个键和值的最大长度为255个字符。

## <a name="versioning"></a>版本控制

随着时间的推移，将引入、修改或停用属性。 应用程序应继续处理这些旧的或停用的属性，因为在企业范围内替换此值可能需要数年的时间。

在将属性替换为较新版本时，应将版本后缀添加到属性：

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>电子邮件

应用于电子邮件的元数据维护与文档类似的键/值对格式。 主要区别在于，所有属性都将被序列化到一个名为**MSIP_Labels**的电子邮件标头中。 键/值对由分号和空格分隔，并置于新标头中。

使用上面的示例元数据：

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
