---
# required metadata

title: 配置客户端 | Azure RMS
description: 有关如何配置 Active Directory Rights Management Services 客户端 2.1 的说明。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 74C342BF-0F79-486D-AED7-C53230DE5FA7
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 配置客户端

本主题包含有关如何配置 Active Directory Rights Management Services 客户端 2.1 的说明。

**重要说明**  如果要通过在单框 RMS ISV 环境上运行来测试应用程序，则无需配置 AD RMS 客户端 2.1。 有关详细信息，请参阅 [测试启用权限的应用程序](running-your-first-application.md)。

 

### 先决条件

-   必须在要用于测试应用程序的计算机上安装具有 AD RMS 客户端 2.1。

    -   如果要在开发计算机上测试应用程序，则应该已安装了 Rights Management Services SDK 2.1。 AD RMS 客户端 2.1 当时会以无提示方式安装。

        有关如何安装 RMS SDK 2.1 的信息，请参阅 [安装 SDK](create-your-first-rights-aware-application.md)。

    -   如果要在开发计算机之外的计算机上测试应用程序，则可以通过 [AD RMS 客户端 2.1 下载页面](http://www.microsoft.com/en-us/download/details.aspx?id=38396) 在该计算机上安装 AD RMS 客户端 2.1。
        **注意** 如果你的应用程序使用服务器 API 模式 (**IPC\_API\_MODE\_SERVER**)，则无需使用应用程序清单。 你可以依据生产 RMS 服务器测试应用程序，且切换到生产环境时无需获取生产许可证。 有关服务器模式应用程序的详细信息，请参阅[应用程序类型](application-types.md)。

         

-   必须安装了 RMS 服务器并配置为在预生产环境中工作。 有关详细信息，请参阅 [安装并配置服务器](how-to-install-and-configure-an-rms-server.md)。

说明

### 步骤 1：如何为预生产证书层次结构设置 RMS 客户端 2.1

以下步骤介绍如何安装开发人员运行时、配置客户端以使用 ISV 证书（预生产）层次结构以及在客户端上设置服务发现。

1.  将开发人员运行时 Ipcsecproc\_isv.dll 从 %MSIPCSDKDIR%\\bin\\x86（对于 32 位版本的 Windows）或 %MSIPCSDKDIR\\bin\\x64（对于 64 位版本的 Windows）复制到 C:\\Program Files\\Active Directory Rights Management Services Client 2.1。

    **重要**  如果在 64 位版本的 Windows 上运行 32 位应用程序，则必须将 Ipcsecproc\_isv.dll 从 %MSIPCSDKDIR%\\bin\\x86 复制到 C:\\Program Files(x86)\\Active Directory Rights Management Services Client 2.1。

     

2.  通过将 **“Hierarchy”** 注册表项值为 1，来配置 AD RMS 客户端 2.1 以使用 ISV 证书（预生产）层次结构。

    ```
    HKEY_LOCAL_MACHINE
       SOFTWARE
          Microsoft
             MSIPC
                Hierarchy DWORD = 00000001
                Data type
                DWORD
    ```

    **注意**  注册表中不存在 **“Hierarchy”** 值在功能上等同于将其值设置为 0（零），这意味着 RMS SDK 2.1 会在生产模式下进行操作。 关于密钥和证书链的详细信息，请参阅[了解证书链](understanding-certificate-chains.md)。

    **重要**  
    如果在 64 位版本的 Windows 上运行 32 位应用程序，则必须在以下项位置设置 **“Hierarchy”** 值：

    ```
    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    ```
     

3.  配置服务器端发现或客户端发现，以使 AD RMS 客户端 2.1 可以发现预生产 RMS 服务器并与之建立通信。

    -   在服务器端发现中，管理员会向 Active Directory 注册预生产 RMS 根群集的服务连接点 (SCP)，客户端会查询 Active Directory 以发现该 SCP 并与服务器建立连接。
    -   在客户端发现中，会在运行 AD RMS 客户端 2.1 的计算机上，在注册表中配置 RMS 服务发现设置。 这些设置使 AD RMS 客户端 2.1 指向 RMS 服务器。 当它们存在时，不会执行服务器端发现。

    若要配置客户端发现，可以设置以下注册表项以指向预生产 RMS 服务器。 有关如何配置服务端发现的信息，请参阅 [RMS 客户端 2.0 部署说明](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)。

|Key|值|
|---|-----|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterpriseCertification`|（默认值）：<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Certification**|
|`HKEY_LOCAL_MACHINE\`<br>`SOFTWARE\`<br>`Microsoft\`<br>`MSIPC\`<br>`ServiceLocation\`<br>`EnterprisePublishing`|（默认值）：<br><br> [**http**&#124;**https**]**://** *RMSClusterName* **/_wmcs/Licensing**|


**注意**   默认情况下，这些项在注册表中不存在，必须创建。
     
**重要**  
    如果在 64 位版本的 Windows 上运行 32 位应用程序，则必须在以下项位置设置这些项：


    HKEY_LOCAL_MACHINE
        SOFTWARE
           Wow6432Node
              Microsoft
                MSIPC
    

### 备注

本主题中的指南并不全面。 有关如何配置 AD RMS 客户端 2.1 的详细信息，请参阅 [RMS 客户端 2.0 部署说明](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)。

## 相关主题


* [使用方法](how-to-use-msipc.md)
* [RMS 客户端 2.0 部署说明](https://TechNet.Microsoft.Com/en-us/library/jj159267(WS.10).aspx)
* [安装 SDK](create-your-first-rights-aware-application.md)
* [安装并配置服务器](how-to-install-and-configure-an-rms-server.md)
* [测试启用权限的应用程序](running-your-first-application.md)
* [了解证书链](understanding-certificate-chains.md)
 

 


<!--HONumber=Apr16_HO4-->


