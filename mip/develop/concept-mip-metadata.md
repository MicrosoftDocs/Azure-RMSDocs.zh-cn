---
title: 概念-标签 MIP SDK 中的元数据
description: 本文将帮助你了解 Microsoft 信息保护 SDK 生成的元数据。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.date: 11/08/2018
ms.author: tommos
ms.openlocfilehash: 990f729edaa0a2e212812f84fc5a4c63f82e37fb
ms.sourcegitcommit: a78d4236cbeff743703c44b150e69c1625a2e9f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56253963"
---
# <a name="microsoft-information-protection-sdk---metadata"></a>Microsoft 信息保护 SDK 的元数据

Microsoft 信息保护 SDK 生成元数据，应该应用于文件的组。 此元数据是标签的表示形式。 本文档介绍 SDK 生成要应用于邮件、 文档和其他记录的元数据。

## <a name="labels"></a>标签

Microsoft 信息保护 SDK 中的标签将应用于信息来描述该信息的敏感性。 标签数据保存到文件或一组描述标签的键 / 值对中的记录。 元数据名称是基于以下结构：

`DefinedPrefix_ElementType_GlobalIdentifier_AttributeName`

在应用于使用 Microsoft 信息保护标记的数据，结果是：

`MSIP_Label_GUID_Enabled = true`

GUID 是在组织中的每个标签的唯一标识符。

## <a name="microsoft-information-protection-sdk-metadata"></a>Microsoft 信息保护 SDK 元数据

MIP SDK 适用以下组的元数据。

| 属性 | 类型或值                 | 描述                                                                                                                                                                                                                                        | 必需 |
|-----------|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| **已启用**   | True 或 False                 | 此属性指示是否为数据项启用此组键 / 值对表示的分类。 DLP 产品通常会验证存在此项以识别分类标签。 | 是       |
| **SiteId**    | GUID                          | Azure Active Directory 租户 ID                                                                                                                                                                                                                   | 是       |
| **ActionId**  | GUID                          | ActionID 被更改每个时间设置一个标签。 审核日志将包含旧的和新允许的标记数据项目的活动链接的 actionID。                                                                                 | 是       |
| **方法**    | Standard、 特权或自动        | 通过 mip::AssignmentMethod 设置                                                                                                                                                                                                                 | 否        |
| **SetDate**   | 扩展的 ISO 8601 日期格式 | 设置标签时的时间戳。                                                                                                                                                                                                              | 否        |
| **名称**      | string                        | 标签在租户中的唯一名称。 它不一定与显示名称。                                                                                                                                                              | 否      |
| **ContentBits** | integer | 位掩码，用于描述标记的内容的类型应应用于文件。 CONTENT_HEADER = 0X1、 CONTENT_FOOTER = 0X2、 水印 = 0X4
 | 否 |

应用于一个文件时，结果是类似于下表。

| 键                                                         | 值                                |
|-------------------------------------------------------------|--------------------------------------|
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled     | true                                 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate     | 2018-11-08T21:13:16-0800             |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method      | 特权                           |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name        | 机密                         |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId      | cb46c030-1825-4e81-a295-151c039dbf02 |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits | 2                                    |
| MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId    | 88124cf5-1340-457d-90e1-0000a9427c99 |

## <a name="extending-metadata-with-custom-attributes"></a>扩展元数据使用自定义属性

通过文件和策略 API 都可以附加自定义元数据。 自定义特性必须维护基`MSIP_Label_GUID`前缀。 

例如，Contoso corporation 编写的应用程序必须应用，该值指示哪些系统生成的标记的文件的元数据。 应用程序可以创建一个新标签，前缀为`MSIP_Label_GUID`。 软件供应商名称和自定义属性添加到前缀以生成自定义元数据。

```
MSIP_Label_f048e7b8-f3aa-4857-bf32-a317f4bc3f29_ContosoCorp_GeneratedBy = HRReportingSystem
```

> [!Note]
> 为了保持兼容性之间常见的应用程序，最大长度为每个键和值为 255 个字符。

## <a name="versioning"></a>版本控制

随着时间推移，属性将会引入、 修改或已停用。 它被应为应用程序将继续处理这些旧或已停用的特性，如将值替换为整个企业内可能需要年。

当属性替换为较新版本，应将版本后缀添加到属性：

`MSIP_Label_GUID_EnabledV2 = True | False | Condition`

## <a name="email"></a>Email

元数据应用于电子邮件维护一个键/值对格式类似于文档。 主要区别在于，所有属性进行序列都化到名为单个电子邮件标头**MSIP_Labels**。 键/值对将由分号和空格分隔并放置在新的标头中。

使用上面的示例元数据：

```
MSIP_Labels: MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Enabled=true; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SetDate=2018-11-08T21:13:16-0800; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Method=Privileged; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_Name=Confidential; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_SiteId=cb46c030-1825-4e81-a295-151c039dbf02; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ContentBits=2; MSIP_Label_2096f6a2-d2f7-48be-b329-b73aaa526e5d_ActionId=88124cf5-1340-457d-90e1-0000a9427c99
```
