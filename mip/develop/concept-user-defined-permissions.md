---
title: 概念-MIP SDK 中的核心概念-用户定义的权限。
description: 本文将帮助你了解称为用户定义的权限的核心 SDK 概念。
author: tommoser
ms.service: information-protection
ms.topic: conceptual
ms.date: 02/02/2021
ms.author: tommos
ms.openlocfilehash: 47939a37616173c456d1588e95e36f8a978ed32d
ms.sourcegitcommit: 7420cf0200c90687996124424a254c289b11a26f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "101844177"
---
# <a name="microsoft-information-protection-sdk---user-defined-permissions"></a>Microsoft 信息保护 SDK-用户定义的权限

Microsoft 信息保护 SDK 支持两种主要类型的标签驱动权限：基于模板和用户定义。

- **基于模板的权限：** 这些权限由 "安全性和符合性中心" 中的 "标签管理员" 定义。 这些标签是集中管理的，配置中的更改将影响已有文件副本的用户。 例如，如果管理员从授权用户列表中删除某个用户，则该用户将不再有权访问受保护的数据。

- **用户定义的权限**：这些权限是在最终用户或应用程序进行 **标记时** 定义的。 权限以用户对角色或用户到权限映射集合的形式传递到 MIP SDK。 这些权限将写入受保护文档的发布许可证，与基于模板的权限不同，无法在共享时集中管理或修改这些权限，而无需直接访问和修改文档。

## <a name="users-rights-and-roles"></a>用户、权限和角色

由于在标记时用户会定义权限，因此你的应用程序必须提供一个接口，以允许用户或服务提供该用户将拥有的电子邮件地址和权限的输入。 此配置的实现方法是：传入 `UserRoles` 或 `UserRights` 对象的集合，这些对象专门定义哪些用户应该拥有文档的哪一级别的访问权限。

```csharp
// Create a List<string> of the first set of permissions. 
List<string> users = new List<string>()
{
    "alice@contoso.com",
    "bob@contoso.com"
};

// Create a List<string> of the Rights the above users should have. 
List<string> rights = new List<string>()
{
    Rights.View,
    Rights.Edit                
};

// Create a UserRights object containing the defined users and rights.
UserRights userRights = new UserRights(users, rights);

// Add them to a new List<UserRights>
List<UserRights> userRightsList = new List<UserRights>()
{
    userRights
};
```

结果是，你将具有一个集合，该 `List<UserRights>` 集合指定 Alice 和 Bob 都对受保护的文件具有 "查看" 和 "编辑"。 若要添加具有 *不同* 权限集的多个用户，请重复此过程以创建第二个 `UserRights` 对象，传递新用户和权限，然后通过调用将添加到 `List<UserRights>` 集合 `userRightsList.Add(userRights2)` 。

此模式也适用于 `UserRoles` ，只需将 **权限** 替换为 **角色** 并创建集合即可实现 `List<UserRoles>` 。

### <a name="apply-protection"></a>应用保护

可以通过 `ProtectionDescriptor` 从 `List<UserRights>` 或 `List<UserRoles>` 对象创建，然后将其传递到来实现设置保护 `FileHandler.SetProtection()` 。 最后，将更改提交到文件以写入新文件。 

### <a name="when-to-apply-protection-to-files"></a>何时将保护应用于文件

通过 MIP SDK 设置标签时， `FileHandler.SetLabel()` 它需要执行操作并应用任何保护。 如果为 (UDP) 的用户定义权限配置标签，则应用程序无法提前知道标签为 UDP 标签。 MIP SDK 通过引发类型的异常来显示此信息 `Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException` 。 你的 `FileHandler` 代码应该捕获此异常，并触发你的用户或服务接口来定义自定义权限。 完成后，你将能够设置保护。 下面的示例演示了端到端模式，但假定已经实现了用于生成对象的函数 `List<UserRights>` 。

```csharp
try
{
    // Attempt to set the label. If it's a UDP label, this will throw. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());
}

catch (Microsoft.InformationProtection.Exceptions.AdhocProtectionRequiredException)
{
    // Assumes you've create a function that returns the List<UserRights> as previously detailed. 
    List<UserRights> userRightsList = GetUserRights();

    // Create a ProtectionDescriptor using the set of UserRights.
    ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(userRightsList);
    
    // Apply protection to the file using the new ProtectionDescriptor. 
    handler.SetProtection(protectionDescriptor, new ProtectionSettings());

    // Set the label. This will now succeed as protection has been defined. 
    handler.SetLabel(engine.GetLabelById(options.LabelId), labelingOptions, new ProtectionSettings());

    // Commit the change. 
    var result = Task.Run(async () => await handler.CommitAsync("myFileOutput.xlsx")).Result;
}
```

## <a name="custom-protection"></a>自定义保护

此过程也可用于设置保护，并跳过该 `SetLabel()` 步骤。 如果你的应用程序不需要应用标签，则不需要异常处理程序，并且可以按照模式来设置保护 `ProtectionDescriptor`  ->  `SetProtection()`  ->  `CommitAsync()` 。

## <a name="next-steps"></a>后续步骤

- [查看 Microsoft 365 文档中的标签加密配置。](/microsoft-365/compliance/encryption-sensitivity-labels?view=o365-worldwide#understand-how-the-encryption-works)