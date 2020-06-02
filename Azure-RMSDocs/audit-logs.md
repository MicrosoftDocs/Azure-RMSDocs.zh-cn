---
title: Azure 信息保护生成的审核日志-AIP
description: 了解 Azure 信息保护生成的审核日志-AIP。
author: batamig
ms.author: bagol
manager: rkarlin
ms.date: 06/01/2020
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: information-protection
ms.subservice: prereqs
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: b851372494a3215a1db3f118809ec2bdf438affd
ms.sourcegitcommit: fa16364879823b86b4e56ac18a1fc8de5a5dae57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/01/2020
ms.locfileid: "84250428"
---
# <a name="azure-information-protection-audit-log-reference-public-preview"></a>Azure 信息保护审核日志参考（公共预览版）

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

Microsoft Azure 信息保护在以下活动事件中生成审核日志：
* [访问](#access-audit-logs)
* [访问被拒绝](#access-denied-audit-logs)
* [更改保护](#change-protection-audit-logs)
* [发现](#discover-audit-logs)
* [降级标签](#downgrade-label-audit-logs)
* [文件已删除](#file-removed-audit-logs)
* [新标签](#new-label-audit-logs)
* [新保护](#new-protection-audit-logs)
* [删除标签](#remove-label-audit-logs)
* [删除保护](#remove-protection-audit-logs)
* [升级标签](#upgrade-label-audit-logs)




## <a name="access-audit-logs"></a>访问审核日志
为以下活动生成**访问**审核日志：

|报告者  |平台  |应用程序  |操作/说明  |
|---------|---------|---------|---------|
|Azure 信息保护：</br>-经典客户端</br>-统一标签客户端     | Windows        | Office        |在每个会话中对标记或受保护的文件进行第一次生成。<br>日志文件包含任何信息类型匹配项。  <!-- plan to be removed -->    |
|Azure 信息保护：</br>-经典客户端</br>-统一标签客户端     |Windows         |Office         |每次创建标记文件或受保护的文件时生成。<!-- plan to be removed -->       |
|Azure 信息保护：</br>-经典客户端</br>-统一标签客户端     | Windows、SharePoint、OneDrive        | Office        | 每次打开标记或受保护的文件时生成。         |
|Microsoft 信息保护（MIP） SDK     | 任意        | 第三方应用程序        | 每次通过支持该文件的第三方应用程序访问标记或受保护的文件时生成。       |
|RMS 服务     | Windows        | Office         |每次访问标记或受保护的文档时生成。<!-- plan to be removed -->       |

## <a name="access-denied-audit-logs"></a>拒绝访问审核日志
对于以下活动，会生成 "**拒绝访问**" 审核日志：

|报告者  |平台  |应用程序  |操作/说明   |
|---------|---------|---------|---------|
|RMS 服务     | Windows        | Office         |用户每次尝试访问不具有访问权限的受保护文档时生成。|

## <a name="change-protection-audit-logs"></a>更改保护审核日志
为以下活动生成**更改保护**审核日志：

|报告者  |平台  |应用程序  |操作/说明   |
|---------|---------|---------|---------|
|Azure 信息保护：</br>-经典客户端</br>-统一标签客户端     | Windows、SharePoint、OneDrive        | Office        | 每次手动更改保护时，如果没有标签，则会生成。  |
|Microsoft 信息保护（MIP） SDK     | 任意        | 第三方应用程序        | 每次手动更改保护时，如果没有标签，则会生成。<br>仅当第三方应用程序支持时才生成。 |

## <a name="discover-audit-logs"></a>发现审核日志
为以下活动**生成审核日志**：

|报告者  |平台  |应用程序  |操作/说明   |
|---------|---------|---------|---------|
|Azure 信息保护：</br>-经典扫描程序 </br>-统一标记扫描器     | Windows        | Office        |每次 AIP 扫描程序扫描文件时生成。<br>日志文件包含以下详细信息：<br>-匹配的信息类型<br>-标签 |
|Microsoft 信息保护（MIP） SDK | 任意 | 第三方应用程序 | 每次由支持该文件的第三方应用程序扫描文件时生成。 </br>日志文件包含以下详细信息：</br>-匹配的信息类型</br>-标签|

## <a name="downgrade-label-audit-logs"></a>降级标签审核日志
为以下活动生成**降级标签**审核日志：

| 报告者      | 平台                       | 应用程序              | 操作/说明      |
| ---------------- | ------------------------------ | ------------------------ | --------------- |
|Azure 信息保护：</br>-经典客户端</br>-统一标签客户端 | Windows、SharePoint、一个驱动器 | Office                   | 每次用不太敏感的标签更新文档标签时生成。|
| Microsoft Defender ATP            | Windows                        | (OS)                       | 每次用不太敏感的标签更新文档标签时生成。 |
| Microsoft 信息保护（MIP） SDK          | 任意                            | 第三方应用程序 | 每次用不太敏感的标签更新文档标签时生成。<br>仅当第三方应用程序支持时才生成。 |

## <a name="file-removed-audit-logs"></a>文件已删除审核日志

> [!NOTE]
> 仅在 Azure 信息保护扫描程序版本[2.7.95.0](rms-client/unifiedlabelingclient-version-release-history.md#version-27950-public-preview)和更高版本中支持文件删除审核日志。

为以下活动生成**文件已删除**审核日志：

| 报告者                                                                              | 平台 | 应用程序                     | 操作/说明                                                          |
| ---------------------------------------------------------------------------------------- | -------- | ------------------------------- | ------------------------------------------------------------------------------ |
| Azure 信息保护扫描程序，统一标签客户端 | Windows  | Office 和支持的文件类型 | 每次扫描程序检测到以前已被扫描的文件现在已被删除。 |


## <a name="new-label-audit-logs"></a>新标签审核日志
为以下活动生成**新的标签**审核日志：

| 报告者                                                                      | 平台                       | 应用程序              | 操作/说明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure 信息保护：</br>-经典客户端</br>-统一标签客户端 | Windows、SharePoint、一个驱动器 | Office                   | 每次应用新标签时生成。                                                                  |
| Microsoft Defender ATP                                                                            | Windows                        | (OS)                       | 每次应用新文档标签时生成。                                                                  |
| Microsoft 信息保护（MIP） SDK                                                                          | 任意                            | 第三方应用程序 | 每次应用新文档标签时生成。<br>仅当第三方应用程序支持时才生成。 |

## <a name="new-protection-audit-logs"></a>新保护审核日志
为以下活动生成**新的保护**审核日志：

| 报告者                                                                      | 平台                       | 应用程序              | 操作/说明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure 信息保护：</br>-经典客户端</br>-统一标签客户端 | Windows、SharePoint、一个驱动器 | Office                   | 每次手动添加保护时，如果没有标签，则会生成。                                                                  |
| Microsoft 信息保护（MIP） SDK                                                                          | 任意                            | 第三方应用程序 | 每次手动添加保护时，如果没有标签，则会生成。<br>仅当第三方应用程序支持时才生成。 |

## <a name="remove-label-audit-logs"></a>删除标签审核日志
为以下活动生成 "**删除标签**" 审核日志：


| 报告者                                                                      | 平台                       | 应用程序              | 操作/说明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure 信息保护：</br>-经典客户端</br>-统一标签客户端 | Windows、SharePoint、一个驱动器 | Office                   | 每次删除标签时生成。                                                                  |
| Microsoft Defender ATP                                                                            | Windows                        | (OS)                       | 每次删除标签时生成。                                                                  |
| Microsoft 信息保护（MIP） SDK                                                                          | 任意                            | 第三方应用程序 | 每次删除标签时生成。<br>仅当第三方应用程序支持时才生成。 |

## <a name="remove-protection-audit-logs"></a>删除保护审核日志
为以下活动生成**删除保护**审核日志：

| 报告者                                                                      | 平台                       | 应用程序              | 操作/说明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure 信息保护：</br>-经典客户端</br>-统一标签客户端 | Windows、SharePoint、一个驱动器 | Office                   | 每次手动删除保护时，如果没有标签，则生成。                                                                  |
| Microsoft 信息保护（MIP） SDK                                                                          | 任意                            | 第三方应用程序 | 每次手动删除保护时，如果没有标签，则生成。<br>仅当第三方应用程序支持时才生成。 |

## <a name="upgrade-label-audit-logs"></a>升级标签审核日志
为以下活动生成**升级标签**审核日志：

| 报告者                                                                      | 平台                       | 应用程序              | 操作/说明                                                                                      |
| -------------------------------------------------------------------------------- | ------------------------------ | ------------------------ | ---------------------------------------------------------------------------------------------------------- |
| Azure 信息保护：</br>-经典客户端</br>-统一标签客户端 | Windows、SharePoint、一个驱动器 | Office                   | 每次用更敏感的标签更新文档标签时生成。                                                                   |
| Microsoft Defender ATP                                                                            | Windows                        | (OS)                       | 每次用更敏感的标签更新文档标签时生成。                                                                   |
| Microsoft 信息保护（MIP） SDK                                                                          | 任意                            | 第三方应用程序 | 每次用更敏感的标签更新文档标签时生成。<br>仅当第三方应用程序支持时才生成。 |
