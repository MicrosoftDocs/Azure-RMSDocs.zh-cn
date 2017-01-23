---
title: "使用 Azure 门户对 RMS 身份验证进行配置 | Azure RMS"
description: "使用 ADAL 进行身份验证的过程概述"
keywords: "身份验证、RMS、ADAL"
author: bruceperlerms
ms.author: bruceper
manager: mbaldwin
ms.date: 09/25/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: 2680b399-febb-4bd6-b844-ac3d1e69aca4
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 9a777b9a13c5ecff3083f4552a8c81f4e42c5cb2


---

# <a name="how-to-use-azure-portal-to-configure-for-rms-authentication"></a>操作方法：使用 Azure 门户对 RMS 身份验证进行配置

使用 Azure Active Directory 身份验证库 (ADAL) 为应用向 Azure RMS 进行身份验证。

使用此方法要求你的应用程序管理自己的 OAuth 身份验证。 使用此方法，RMS 客户端将在需要进行身份验证时执行应用程序定义的回调。

## <a name="configure-via-azure-portal"></a>通过 Azure 门户进行配置
首先按照此指南开始通过 Azure 门户进行配置，如[为 ADAL 身份验证配置 Azure RMS](adal-auth.md) 中所述。 请务必从此过程复制并保存*客户端 ID* 和*重定向 URI* 以便稍后使用。

## <a name="code-sample"></a>代码示例
以下是摘取自移动客户端代码的较大示例、用于启用 Azure ADAL 的代码段。 有关详细信息，请参阅 [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp) 中的完整示例

       /**
       * Instantiates a new rms authentication callback.
       *
       * @param parentActivity the parent activity
       * @throws NoSuchAlgorithmException the no such algorithm exception
       * @throws InvalidKeySpecException the invalid key spec exception
       * @throws UnsupportedEncodingException the unsupported encoding exception
       */

       public MsipcAuthenticationCallback(Activity parentActivity) throws NoSuchAlgorithmException, InvalidKeySpecException, UnsupportedEncodingException
       {
         mParentActivity = parentActivity;
         setADALKeyStore();

         /**
         * Note: Following values of are client_id and redirect_uri are for demo purpose only.
         * Your values will come from the preceeding Azure Portal process.
         */
         mClientId = "com.microsoft.rightsmanagement.sampleapp";
         mRedirectURI = mClientId + "://authorize";
       }


## <a name="related-topics"></a>相关主题

- [MSIPCSampleApp](https://github.com/AzureAD/rms-sdk-ui-for-android/tree/master/samples/MsipcSampleApp)
- [为 ADAL 身份验证配置 Azure RMS](adal-auth.md)

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO1-->


