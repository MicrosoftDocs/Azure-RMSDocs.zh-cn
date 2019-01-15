---
title: 开发应用程序 - AIP
description: 有关基本控制台应用如何使用 AIP 实现文档保护的指南
keywords: ''
author: bryanla
ms.author: bryanla
manager: mbaldwin
ms.date: 03/13/2017
ms.topic: conceptual
ms.service: information-protection
ms.assetid: 396A2C19-3A00-4E9A-9088-198A48B15289
audience: developer
ms.reviewer: kartikk
ms.suite: ems
ms.openlocfilehash: 6f0fdcaf6d21047f28c470dc896a1cd64fee752d
ms.sourcegitcommit: bd2b31dd97c8ae08c28b0f5688517110a726e3a1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2019
ms.locfileid: "54071295"
---
# <a name="developing-your-application"></a>开发应用程序

本示例中将构建与 Azure信息保护服务 (AIP) 交互的简单控制台应用程序。  它将要保护的文件的路径作为输入，然后使用临时策略或 Azure 模板对其进行保护。 应用程序将根据输入应用正确的策略，创建信息受保护的文档。 你将使用的示例代码是 [Azure IP 测试应用程序](https://github.com/Azure-Samples/Azure-Information-Protection-Samples/tree/master/AzureIP_Test)，位于 Github 上。

## <a name="sample-app-prerequisites"></a>示例应用程序必备组件
- 操作系统：Windows 10、Windows 8、Windows 7、Windows Server 2008、Windows Server 2008 R2 或 Windows Server 2012
- 编程语言：C#（.NET Framework 3.0 及更高版本）
- 开发环境：Visual Studio 2015（及更高版本）

## <a name="setting-up-your-azure-configuration"></a>设置 Azure 配置

为此应用设置 Azure 需要创建租户 ID、对称密钥和应用程序主体 ID。

### <a name="azure-ad-tenant-configuration"></a>Azure AD 租户配置

若要为 Azure 信息保护配置 Azure AD 环境，请按照[激活 Azure Rights Management](https://docs.microsoft.com/information-protection/deploy-use/activate-service)中的指导进行操作。

激活服务后，你需要 PowerShell 组件来执行后续步骤。 请按照[使用 Windows PowerShell 管理 Azure Rights Management 服务](https://docs.microsoft.com/information-protection/deploy-use/administer-powershell)中的说明完成此操作。

### <a name="getting-your-tenant-id"></a>获取租户 ID

- 以管理员身份运行 PowerShell。
- 导入 RMS 模块：`Import-Module AADRM`
- 使用分配的用户凭据连接到服务：`Connect-AadrmService –Verbose`
- 确保已启用 RMS：`Enable-AADRM`
- 通过运行 `Get-AadrmConfiguration` 获取租户 ID

>记录 BPOSId（租户 ID）值。 后续步骤中需要此值。

*示例输出*
![cmdlet 输出](../media/develop/output-of-Get-AadrmConfiguration.png)

- 从服务断开连接：`Disconnect-AadrmService`

### <a name="create-a-service-principal"></a>创建服务主体
按照下列步骤来创建服务主体：
> 服务主体是全局配置以用于访问控制的凭据，允许服务使用 Microsoft Azure AD 进行身份验证，并使用 Microsoft Azure AD Rights Management 保护信息

- 以管理员身份运行 PowerShell
- 使用 `Import-Module MSOnline` 导入 Microsoft Azure AD 模块
- 使用分配的用户凭据 `Connect-MsolService` 连接到在线服务
- 通过运行 `New-MsolServicePrincipal` 创建新服务主体
- 为服务主体提供名称
> 记录对称密钥和应用程序主体 ID 以供将来使用。

*示例输出*
![cmdlet 输出](../media/develop/output-of-NewMsolServicePrincipal.png)

- 将应用程序主体 ID、对称密钥和租户 ID 添加到应用程序的 App.config 文件。

*App.config 文件示例*
![cmdlet 输出](../media/develop/example-App.config-file.png)

- 在 Azure 中注册应用程序后，你就可以使用 *ClientID* 和 *RedirectUri*。 有关如何在 Azure 中注册应用程序以及获取 *ClientID* 和 *RedirectUri* 的详细信息，请参阅[为 ADAL 身份验证配置 Azure RMS](adal-auth.md)。


## <a name="design-summary"></a>设计摘要
下图描述了你正在创建的应用的体系结构和流程，步骤如下。
![设计摘要](../media/develop/design-summary.png)

1. 用户输入：
  - 要保护的文件的路径
  - 选择模板或创建临时策略
2. 应用程序请求使用 AIP 进行身份验证。
3. AIP 确认身份验证
4. 应用程序从 AIP 请求模板。
5. AIP 返回预定义的模板。
6. 应用程序通过给定位置定位指定的文件。
7. 应用程序将 AIP 保护策略应用于文件。

## <a name="how-the-code-works"></a>该代码的工作原理

在示例中，Azure IP 测试（即解决方案）以文件 Iprotect.cs 开头。 这是一个 C# 控制台应用程序，与其他任何启用了 AIP 的应用程序相同，使用 `main()` 方法开始加载 *MSIPC.dll*。

    //Loads MSIPC.dll
    SafeNativeMethods.IpcInitialize();
    SafeNativeMethods.IpcSetAPIMode(APIMode.Server);

加载连接到 Azure 所需的参数

    //Loads credentials for the service principal from App.Config
    SymmetricKeyCredential symmetricKeyCred = new SymmetricKeyCredential();
    symmetricKeyCred.AppPrincipalId = ConfigurationManager.AppSettings["AppPrincipalId"];
    symmetricKeyCred.Base64Key = ConfigurationManager.AppSettings["Base64Key"];
    symmetricKeyCred.BposTenantId = ConfigurationManager.AppSettings["BposTenantId"];

在控制台应用程序中提供文件路径时，应用程序将检查文档是否已加密。 该方法属于 **SafeFileApiNativeMethods** 类。

    var checkEncryptionStatus = SafeFileApiNativeMethods.IpcfIsFileEncrypted(filePath);

如果文档未加密，则继续使用提示符上提供的选择来加密文档。

    if (!checkEncryptionStatus.ToString().ToLower().Contains(alreadyEncrypted))
    {
      if (method == EncryptionMethod1)
      {
        //Encrypt a file via AIP template
        ProtectWithTemplate(symmetricKeyCred, filePath);

      }
      else if (method == EncryptionMethod2)
      {
        //Encrypt a file using ad-hoc policy
        ProtectWithAdHocPolicy(symmetricKeyCred, filePath);
      }

“使用模板保护”选项继续从服务器获取模板列表，并为用户提供选项。
>如果没有修改模板，则将从 AIP 获取默认模板

     public static void ProtectWithTemplate(SymmetricKeyCredential symmetricKeyCredential, string filePath)
     {
       // Gets the available templates for this tenant             
       Collection<TemplateInfo> templates = SafeNativeMethods.IpcGetTemplateList(null, false, true,
           false, true, null, null, symmetricKeyCredential);

       //Requests tenant template to use for encryption
       Console.WriteLine("Please select the template you would like to use to encrypt the file.");

       //Outputs templates available for selection
       int counter = 0;
       for (int i = 0; i < templates.Count; i++)
       {
         counter++;
         Console.WriteLine(counter + ". " + templates.ElementAt(i).Name + "\n" +
             templates.ElementAt(i).Description);
       }

       //Parses template selection
       string input = Console.ReadLine();
       int templateSelection;
       bool parseResult = Int32.TryParse(input, out templateSelection);

       //Returns error if no template selection is entered
       if (parseResult)
       {
         //Ensures template value entered is valid
         if (0 < templateSelection && templateSelection <= counter)
         {
           templateSelection -= templateSelection;

           // Encrypts the file using the selected template             
           TemplateInfo selectedTemplateInfo = templates.ElementAt(templateSelection);

           string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(filePath,
               selectedTemplateInfo.TemplateId,
               SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST, true, false, true, null,
               symmetricKeyCredential);
          }
        }
      }

如果选择临时策略，应用程序的用户必须提供应具有权限的人员的电子邮件。 本节中使用 **IpcCreateLicenseFromScratch()** 方法创建许可证，并在模板上应用新策略。

    if (issuerDisplayName.Trim() != "")
    {
      // Gets the available issuers of rights policy templates.              
      // The available issuers is a list of RMS servers that this user has already contacted.
      try
      {
        Collection<TemplateIssuer> templateIssuers = SafeNativeMethods.IpcGetTemplateIssuerList(
                                                        null,
                                                        true,
                                                        false,
                                                        false, true, null, symmetricKeyCredential);

        // Creates the policy and associates the chosen user rights with it             
        SafeInformationProtectionLicenseHandle handle = SafeNativeMethods.IpcCreateLicenseFromScratch(
                                                            templateIssuers.ElementAt(0));
        SafeNativeMethods.IpcSetLicenseOwner(handle, owner);
        SafeNativeMethods.IpcSetLicenseUserRightsList(handle, userRights);
        SafeNativeMethods.IpcSetLicenseDescriptor(handle, new TemplateInfo(null, CultureInfo.CurrentCulture,
                                                                policyName,
                                                                policyDescription,
                                                                issuerDisplayName,
                                                                false));

        //Encrypts the file using the ad hoc policy             
        string encryptedFilePath = SafeFileApiNativeMethods.IpcfEncryptFile(
                                       filePath,
                                       handle,
                                       SafeFileApiNativeMethods.EncryptFlags.IPCF_EF_FLAG_KEY_NO_PERSIST,
                                       true,
                                       false,
                                       true,
                                       null,
                                       symmetricKeyCredential);
       }
    }

## <a name="user-interaction-example"></a>用户交互示例

创建和执行所有项后，应用程序的输出应如下所示：

1.系统会提示你选择一种加密方法。
![应用输出 - 步骤 1](../media/develop/app-output-1.png)

2. 你需要提供要保护的文件的路径。
![应用输出 - 步骤 2](../media/develop/app-output-2.png)

3. 系统将提示你输入许可证所有者的电子邮件（此所有者必须对 Azure AD 租户具有全局管理员权限）。
![应用输出 - 步骤 3](../media/develop/app-output-3.png)

4. 输入有权访问该文件的用户的电子邮件地址（电子邮件必须以空格分隔）。
![应用输出 - 步骤 4](../media/develop/app-output-4.png)

5. 从要向授权用户提供的权限列表中进行选择。
![应用输出 - 步骤 5](../media/develop/app-output-5.png)

6. 最后，输入一些策略元数据：策略名称、描述和发布者（Azure AD 租户）显示名称![应用输出 - 步骤6](../media/develop/app-output-6.png)

