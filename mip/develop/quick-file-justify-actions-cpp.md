---
title: 如何降级/删除需要理由的标签 (C++)
description: 本文可帮助你了解如何降级或删除需要理由的标签。
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 04/14/2020
ms.author: mbaldwin
ms.openlocfilehash: d6ffccc19a5d2343fdb175b3c59ec52be5c7ad0f
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97865274"
---
# <a name="microsoft-information-protection-sdk-file-api---action-justification-for-lowering-a-sensitivity-label-on-a-file-c"></a>Microsoft 信息保护 SDK 文件 API - 降低文件上敏感度标签的级别的操作理由 (C++)

本快速入门介绍了在标签策略需要理由时如何处理对标签进行降级的操作。 本文使用 `mip::FileHandler` 类来更改文件的标签。 有关更多详细信息，请参阅 [API 参考](./reference/mip-sdk-reference.md)。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：设置/获取敏感度标签 (C++)](quick-file-set-get-label-cpp.md)，这可生成 Visual Studio 初学者解决方案（用于列出组织的敏感度标签），以便在文件中设置和读取敏感度标签。 本快速入门“如何降级/删除需要理由的标签 (C++)”建立在前一个快速入门的基础之上。
- 可选：查看 MIP SDK 概念中的[文件处理程序概念](concept-handler-file-cpp.md)。

## <a name="add-logic-to-set-a-lower-label-to-a-protected-file"></a>添加逻辑，向受保护的文件设置级别较低的标签

使用 `mip::FileHandler` 对象，添加逻辑以对文件设置敏感度标签。

1. 打开在前面的[快速入门：设置/获取敏感度标签 (C++)](quick-file-set-get-label-cpp.md) 中创建的 Visual Studio 解决方案。

2. 使用“解决方案资源管理器”，打开项目中包含 `main()` 方法的实现的 .cpp 文件。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

3. 在文件顶部的相应现有指令下面，添加以下 #include 和 using 指令：

    ```cpp

        #include "mip/file/file_error.h"

        using mip::JustificationRequiredError;
        using std::cin;

    ```

4. 将以前的快速入门中的 `<label-id>` 值更新为需要降级理由的敏感度标签。 在此快速入门中，首先设置此标签，然后尝试在后续步骤中通过代码片段降低此标签的级别。

5. 在 `main()` 正文的末尾，于 `system("pause");` 之下和关闭块之上（在上一快速入门中离开的位置），插入以下代码：

```cpp

// Downgrade label
// Set paths and lower label ID
// Set a new label on input file.

string lowerlabelId = "<lower-label-id>";
cout << "\nApplying new Label ID " << lowerlabelId << " to " << filePathOut << endl;
mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);

// Try to apply a label with lower sensitivity.
try
{
    handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
}

catch (const mip::JustificationRequiredError& e)
{
    // Request justification from user.
    cout<<"Please provide justification for downgrading a label: "<<endl;
    string justification;
    cin >> justification;

    // Set Justification provided flag
    bool isDowngradeJustified = true;
    mip::LabelingOptions labelingOptions(mip::AssignmentMethod::PRIVILEGED);
    labelingOptions.SetDowngradeJustification(isDowngradeJustified,justification);

    //Set new label.
    handler->SetLabel(engine->GetLabelById(lowerlabelId), labelingOptions, mip::ProtectionSettings());
}

catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}

// Commit changes, save as a different output file
string lowerFilePathOut = "<lower-output-file-path>";
try
{
    cout << "Committing changes" << endl;
    auto commitPromise = std::make_shared<std::promise<bool>>();
    auto commitFuture = commitPromise->get_future();
    handler->CommitAsync(lowerFilePathOut, commitPromise);
    if (commitFuture.get()) {
        cout << "\nLabel committed to file: " << lowerFilePathOut << endl;
    }
    else {
        cout << "Failed to label: " + lowerFilePathOut << endl;
        return 1;
    }
}
catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid commit file path?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}
system("pause");

// Set up async FileHandler for output file operations
string lowerActualFilePath = "<lower-content-identifier>";
try
{
    auto handlerPromise = std::make_shared<std::promise<std::shared_ptr<FileHandler>>>();
    auto handlerFuture = handlerPromise->get_future();
    engine->CreateFileHandlerAsync(
        lowerFilePathOut,
        lowerActualFilePath,
        true,
        std::make_shared<FileHandlerObserver>(),
        handlerPromise);

    handler = handlerFuture.get();
}
catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid output file path?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}

// Get the lowered label from output file
try
{
    cout << "\nGetting the label committed to file: " << lowerFilePathOut << endl;
    auto lowerLabel = handler->GetLabel();
    cout << "Name: " + lowerLabel->GetLabel()->GetName() << endl;
    cout << "Id: " + lowerLabel->GetLabel()->GetId() << endl;
}
catch (const std::exception& e)
{
    cout << "An exception occurred... did you specify a valid label ID?\n\n" << e.what() << "'\n";
    system("pause");
    return 1;
}
system("pause");

```

6. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<lower-label-id\> | 标签 ID，从上一快速入门中的控制台输出所复制。例如：`bb7ed207-046a-4caf-9826-647cff56b990`。 确保与之前受保护的文件标签相比，它的敏感度更低。 |
   | \<lower-output-file-path\> | 保存修改后的文件的输出文件路径。 |
   | \<lower-content-identifier\> | 内容的可读标识符。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireOAuth2Token()` 方法时，应用程序都会提示输入访问令牌。 

  ```console   
    Non-Business : 87ba5c36-17cf-14793-bbc2-bd5b3a9f95cz
    Public : 83867195-f2b8-2ac2-b0b6-6bb73cb33afz
    General : f42a3342-8706-4288-bd31-ebb85995028z
    Confidential : 074e457c-5848-4542-9a6f-34a182080e7z
    Highly Confidential : f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . .

    Applying Label ID f55c2dea-db0f-47cd-8520-a52e1590fb6z to c:\Test\Test.docx
    Committing changes


    Label committed to file: c:\Test\Test.docx
    Press any key to continue . . .

    Run the PowerShell script to generate an access token using the following values, then copy/paste it below:
    Set $authority to: https://login.windows.net/37f4583d-9985-4e7f-a1ab-71afd8b55ba0
    Set $resourceUrl to: https://aadrm.com
    Sign in with user account: user1@tenant.onmicrosoft.com
    Enter access token: <paste-access-token-here>
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_labeled.docx
    Name: Highly Confidential
    Id: f55c2dea-db0f-47cd-8520-a52e1590fb6z
    Press any key to continue . . . 

    Applying new Label ID f42a3342-8706-4288-bd31-ebb85995028z to c:\Test\Test_labeled.docx
    Please provide justification for downgrading a label:
    Need for sharing with wider audience.
    Committing changes

    Label committed to file: c:\Test\Test_downgraded.docx
    Press any key to continue . . .

    Getting the label committed to file: c:\Test\Test_downgraded.docx
    Name: General
    Id: f42a3342-8706-4288-bd31-ebb85995028z
    Press any key to continue . . .
   ```

请注意，若根据标签策略，要从文件中删除的标签需要一个理由，则 `DeleteLabel()` 操作应遵循类似方法。 `DeleteLabel()` 函数引发 `mip::JustificationRequiredError` 异常。 在成功删除该标签之前，应在异常处理中将 `isDowngradeJustified` 标记设置为 true。
