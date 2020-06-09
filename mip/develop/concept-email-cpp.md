---
title: 如何使用 MIP SDK 处理电子邮件（c + +）
description: 本文将帮助你了解如何使用 MIP SDK 文件 API 处理 .msg 和 .rpmsg 文件的方案。
author: Pathak-Aniket
ms.service: information-protection
ms.topic: conceptual
ms.date: 04/08/2020
ms.author: v-anikep
ms.openlocfilehash: 5014367637d2b52256e2d68d3e524bf31286d106
ms.sourcegitcommit: a1feede30ac1f54e900e52eb45b3e6634e0f13f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2020
ms.locfileid: "84548269"
---
# <a name="file-api-email-message-file-processing-c"></a>文件 API 电子邮件文件处理（c + +）

MIP SDK 支持解密和加密电子邮件。 尽管在此方案中将会涉及到的方式略有不同，但由 Outlook 或 Exchange 生成的 .msg 文件以及 .rpmsg 文件也受支持。

此方案的一些常用用例包括：

- 电子数据展示的解密消息
- 解密用于 DLP 检查的邮件和附件
- 直接从业务线应用程序发布受保护的消息
- 解密、修改和重新保护传输中的消息

## <a name="file-api-operations-for-msg-files"></a>.Msg 文件的文件 API 操作

文件 API 支持对 .msg 文件的保护操作，并且与其他任何文件类型的操作方式相同，不同之处在于，SDK 需要应用程序启用 MSG 功能标志。 不支持对 .msg 文件执行标记操作。

如前文所述，的实例化 `mip::FileEngine` 需要设置对象 `mip::FileEngineSettings` 。 `mip::FileEngineSettings`可用于为自定义设置传递参数，应用程序需要为特定实例设置该参数。 FileEngineSettings 的 CustomSettings 属性用于将的标志设置为 `enable_msg_file_type` ，以启用对 .msg 文件的处理。

.Msg 文件保护操作伪代码可能如下所示：

- `enable_msg_file_type`在中设置标志 `mip::FileEngineSettings` 并将添加 `mip::FileEngine` 到 `mip::FileProfile` 。
- 使用保护 API 列出可供用户使用的保护模板。
- `mip::FileHandler`指向要保护的文件的构造。
- 选择要保护的模板，并使用的方法将保护设置为文件 `mip::FileHandler` `SetProtection` 。

请参阅保护 API[快速入门：列出模板](quick-protection-list-templates-cpp.md)了解有关如何列出保护模板的信息。

## <a name="file-api-operations-for-rpmsg-files"></a>.Rpmsg 文件的文件 API 操作

MIP SDK 不支持符合 MIME （通常为 .EML）的消息。 相反，SDK 公开检查函数，该函数能够对嵌入的 **.rpmsg**文件进行解密，并将一组字节流呈现为输出。 由 SDK 使用者提取 * .rpmsg * （或 message_v2、_v3 或 v4）文件，并将其传递给 API。

通常，在电子邮件传输过程中，邮件网关和数据丢失防护（DLP）服务会处理 MIME 兼容的消息。 当邮件受到保护时，邮件的内容将存储在附件 *.rpmsg*中。 此附件包含加密的电子邮件正文和任何属于原始邮件的附件。 *.Rpmsg*文件附加到纯文本包装电子邮件，然后发送到邮件服务。 一旦该消息离开 Exchange 或 Exchange Online 边界，就会采用符合 MIME 标准的格式，以便可以将其发送到其目标。

在大多数情况下，DLP 合作伙伴需要能够从消息中获取附件和纯文本字节，以对照 DLP 策略进行检查和评估。 检查 API 采用 .rpmsg 作为输入并返回字节流作为输出。 这些字节流包含消息的纯文本字节以及附件。 应用程序开发人员负责处理这些流，并对它们执行一些有用的操作（检查、递归解密，等等）。

`Inspect`API 是通过类实现的，该类 `mip::FileInspector` 公开用于检查受支持的文件类型的操作。 `mip::MsgInspector`这种扩展会 `mip::FileInspector` 公开特定于 .rpmsg 文件格式的解密操作。 MIP SDK 不支持 *.rpmsg*文件的任何发布方案。

`mip::MsgInspector`类公开以下成员：

```cpp
public const std::vector<uint8_t>& GetBody()
public BodyType GetBodyType() const
public BodyType GetBodyType() const
public InspectorType GetInspectorType() const
public std::shared_ptr<Stream> GetFileStream() const
```

有关更多详细信息，请参阅[API 参考](./reference/mip-sdk-reference.md)。

## <a name="next-steps"></a>后续步骤

- 查看[文件 API-处理电子邮件文件（c + +）快速入门](quick-email-msg-cpp.md)
- 查看[文件 API-处理电子邮件文件（c #）快速入门](quick-email-msg-csharp.md)