---
title: 快速入门 - 使用 C# MIP SDK 保护 API 加密/解密文本
description: 本快速入门介绍如何使用 Microsoft 信息保护 SDK .NET 包装器，通过保护模板来加密和解密临时文本 (C#)
services: information-protection
author: msmbaldwin
ms.service: information-protection
ms.topic: quickstart
ms.date: 03/30/2020
ms.author: mbaldwin
ms.custom: has-adal-ref
ms.openlocfilehash: 6b0ff0faabe8ebb1776cb95e411fe6ee08d39c9f
ms.sourcegitcommit: 8e48016754e6bc6d051138b3e3e3e3edbff56ba5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97864986"
---
# <a name="quickstart-encryptdecrypt-text-using-mip-sdk-c"></a>快速入门：使用 MIP SDK (C#) 加密/解密文本

本快速入门介绍如何使用更多的 MIP 保护 API。 使用上一快速入门中列出的其中一个保护模板，通过保护处理程序来加密临时文本。 保护处理程序类公开用于应用/删除保护的各种操作。

## <a name="prerequisites"></a>必备条件

如果尚未操作，请务必在继续之前完成以下先决条件：

- 首先完成[快速入门：首先列出保护模板 (C#)](quick-protection-list-templates-csharp.md)，这可生成 Visual Studio 初学者解决方案，以列出经身份验证的用户可用的保护模板。 此“加密/解密文本”快速入门以上一快速入门为基础。
- 可选：查看 [MIP SDK 中的保护处理程序](concept-handler-protection-cpp.md)概念。

## <a name="add-logic-to-set-and-get-a-sensitivity-label"></a>添加逻辑以设置和获取敏感度标签

使用保护引擎对象添加逻辑以加密临时文本。

1. 使用“解决方案资源管理器”，打开项目中包含 Main()` 方法的实现的 .cs 文件  。 它默认与包含它的项目同名，即在项目创建期间指定的名称。

2. 在 `Main()` 正文的末尾（在上一快速入门中离开的位置），插入以下代码：

   ```csharp
   //Set text to encrypt and template ID
   string inputText = "<Sample-text>";
   string templateId = "<template-id>";
   //Create a template based publishing descriptor
   ProtectionDescriptor protectionDescriptor = new ProtectionDescriptor(templateId);

   //Create publishing settings using protection descriptor
   PublishingSettings publishingSettings = new PublishingSettings(protectionDescriptor);

   //Generate Protection Handler for publishing
   var publishingHandler = Task.Run(async() => await protectionEngine.CreateProtectionHandlerForPublishingAsync(publishingSettings)).Result;

   //Encrypt text using Publishing handler
   long bufferSize = publishingHandler.GetProtectedContentLength(inputText.Length, true);
   byte[] inputTextBuffer = Encoding.ASCII.GetBytes(inputText);
   byte[] encryptedTextBuffer = new byte[bufferSize];
   publishingHandler.EncryptBuffer(0, inputTextBuffer, encryptedTextBuffer, true);
   Console.WriteLine("Original text: {0}", inputText);
   Console.WriteLine("Encrypted text: {0}", Encoding.UTF8.GetString(encryptedTextBuffer));

   //Create a Protection handler for consumption using the same publishing licence
   var serializedPublishingLicense = publishingHandler.GetSerializedPublishingLicense();
   PublishingLicenseInfo plInfo = PublishingLicenseInfo.GetPublishingLicenseInfo(serializedPublishingLicense);
   ConsumptionSettings consumptionSettings = new ConsumptionSettings(plInfo);
   var consumptionHandler = protectionEngine.CreateProtectionHandlerForConsumption(consumptionSettings);

   //Use the handler to decrypt the encrypted text
   long buffersize = encryptedTextBuffer.Length;
   byte[] decryptedBuffer = new byte[bufferSize];
   var bytesDecrypted = consumptionHandler.DecryptBuffer(0, encryptedTextBuffer, decryptedBuffer, true);
   byte[] OutputBuffer = new byte[bytesDecrypted];
   for (int i = 0; i < bytesDecrypted; i++){
      OutputBuffer[i] = decryptedBuffer[i];
   }

   Console.WriteLine("Decrypted content: {0}", Encoding.UTF8.GetString(OutputBuffer));
   Console.WriteLine("Press a key to quit.");
   Console.ReadKey();

   ```

3. 在靠近 `Main()` 的末尾处，查找在第一个快速入门中创建的应用程序关闭块，并添加处理程序行：

   ```csharp
   // Application Shutdown
   publishingHandler = null;
   consumptionHandler = null;
   protectionEngine = null;
   protectionProfile = null;
   mipContext = null;
   ```

4. 使用以下值替换源代码中的占位符值：

   | 占位符 | 值 |
   |:----------- |:----- |
   | \<sample-text\> | 要加密的示例文本，例如：`My secure text`。 |
   | \<template-id\> | 模板 ID，从上一快速入门中的控制台输出所复制，例如：`bb7ed207-046a-4caf-9826-647cff56b990`。 |

## <a name="build-and-test-the-application"></a>生成和测试应用程序

生成和测试客户端应用程序。

1. 使用 CTRL-SHIFT-B（“生成解决方案”）来生成客户端应用程序。 如果没有生成错误，请使用 F5（开始调试）来运行应用程序。

2. 如果项目成功生成并运行，则每次 SDK 调用 `AcquireToken()` 方法时，应用程序都可能提示通过 ADAL 进行身份验证。 如果已有缓存凭据，你就不会看到登录和查看标签列表的提示（后跟已应用标签和已修改文件的相关信息）。

  ```console
   Original content: My secure text
   Encrypted content: c?_hp???Q??+<?
   Decrypted content: My secure text
   Press a key to quit.
   ```
