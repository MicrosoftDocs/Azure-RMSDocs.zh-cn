---
title: "从 AD RMS 迁移到 Azure 信息保护 - 阶段 2 | Azure 信息保护"
description: "从 AD RMS 迁移到 Azure 信息保护的阶段 2 涉及从 AD RMS 迁移到 Azure 信息保护中的步骤 5。"
author: cabailey
ms.author: cabailey
manager: mbaldwin
ms.date: 10/12/2016
ms.topic: article
ms.prod: 
ms.service: information-protection
ms.technology: techgroup-identity
ms.assetid: e3fd9bd9-3638-444a-a773-e1d5101b1793
ms.reviewer: esaggese
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7068e0529409eb783f16bc207a17be27cd5d82a8
ms.openlocfilehash: 197ff53d64889487c457f574a235c76821fcf61a


---
# <a name="migration-phase-2---client-side-configuration"></a>迁移阶段 2 - 客户端配置

>适用于：Active Directory Rights Management Services、Azure 信息保护、Office 365

使用以下信息，完成从 AD RMS 迁移到 Azure 信息保护的阶段 2。 这些过程涉及了[从 AD RMS 迁移到 Azure 信息保护](migrate-from-ad-rms-to-azure-rms.md)中的步骤 5。


## <a name="step-5-reconfigure-clients-to-use-azure-information-protection"></a>步骤 5. 重新配置客户端以使用 Azure 信息保护
对于 Windows 客户端：

1.  [下载迁移脚本](https://go.microsoft.com/fwlink/?LinkId=524619)：

    -   CleanUpRMS_RUN_Elevated.cmd

    -   Redirect_OnPrem.cmd

    这些脚本将重置 Windows 计算机上的配置，以使其使用 Azure 信息保护服务而不是 AD RMS。

2.  按照重定向脚本 (Redirect_OnPrem.cmd) 中的说明修改脚本，使其指向新的 Azure 信息保护租户。

    > [!IMPORTANT]
    > 说明包括将示例地址 **adrms** 和 **adrms.contoso.com** 替换为你自己的 AD RMS 服务器地址。 执行此操作时，请注意地址前后不要有多余空格，否则将中断迁移脚本，并且很难将其认定为问题的根本原因。 某些编辑工具会在粘贴文本后自动添加一个空格。
    >
    > 此外，如果 AD RMS 服务器使用 SSL/TLS 服务器证书，请检查字符串中许可 URL 值是否包括端口号 **443**。 例如：https:// rms.treyresearch.net:443/_wmcs/licensing。 单击群集名称并查看“群集详细信息”时，Active Directory Rights Management Services 中会显示此信息。 如果端口号 443 包含在此 URL 中，修改脚本时请将该值包括在内。 例如，https://rms.treyresearch.net**:443**。

3. 如果用户有 Office 2016：脚本尚未更新为包含 Office 2016 的配置，因此如果用户具有此版 Office，你需要手动更新脚本：

    - 对于 **CleanUpRMS.cmd** — 搜索行 `reg delete HKCU\Software\Microsoft\Office\15.0\Common\DRM /f`，并直接在它下面添加以下行：

            reg delete HKCU\Software\Microsoft\Office\16.0\Common\DRM /f

    - 对于 **Redirect_Onprem.cmd** — 搜索行 `reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F`，并直接在它下面添加以下两行：

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServerUrl" /d "https://%CloudRMS%/_wmcs/licensing" /F 

            reg add "HKEY_CURRENT_USER\Software\Microsoft\Office\16.0\Common\DRM" /t REG_SZ /v "DefaultServer" /d "%CloudRMS%" /F

    可选：脚本在注释中不引用 Office 2016。 如果你想更新注释以反映 Office 2016 的这些新增内容，请对 **Redirect_Onprem.cmd** 进行以下更改：

    - 搜索 `::     or MSIPC (Office 2013) with on-premises AD RMS`，并将其替换为以下行：
    
            ::     or MSIPC (Office 2013 and 2016) with on-premises AD RMS

    - 搜索 `echo Redirect SCP for Office 2013`，并将其替换为以下行：
    
            echo Redirect SCP for Office versions based on MSIPC

    - 搜索 `echo Redirect MSIPC for Office 2013` 并替换为以下行：
    
            echo Redirect MSIPC for Office versions based on MSIPC

4.  在 Windows 计算机上：

    - 使用提升的特权，在用户的上下文中运行这些脚本。

    对于移动设备客户端和 Mac 计算机：

    -  删除在部署 [AD RMS 移动设备扩展](http://technet.microsoft.com/library/dn673574.aspx)时创建的 DNS SRV 记录。

#### <a name="changes-made-by-the-migration-scripts"></a>由迁移脚本进行的更改
本节介绍迁移脚本进行的更改。 你只能将此信息出于参考目的，或用于故障排除，或者用于你想要自己进行这些更改的场合。

CleanUpRMS_RUN_Elevated.cmd：

-   删除 %userprofile%\AppData\Local\Microsoft\DRM 和 %userprofile%\AppData\Local\Microsoft\MSIPC 文件夹的内容，包括任何子文件夹以及具有长文件名的任何文件。

-   删除以下注册表项的内容：

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM

    -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\SOFTWARE\WoW6432Node\Microsoft\MSIPC\ServiceLocation

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\MSDRM\ServiceLocation

-   添加以下注册表值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServerURL

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Common\DRM\DefaultServer

Redirect_OnPrem.cmd：

-   为以下每个位置下作为参数提供的每个 URL 创建以下注册表值：

    -   HKEY_CURRENT_USER\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_LOCAL_MACHINE\Software\WoW6432Node\Microsoft\Office\(11.0|12.0|14.0)\Common\DRM\LicenseServerRedirection

    -   HKEY_CURRENT_USER\Software\Classes\Local Settings\Software\Microsoft\MSIPC\LicensingRedirection

    每一项均具有 REG_SZ 值 **https://OldRMSserverURL/_wmcs/licensing**，其数据采用以下格式：**https://&lt;YourTenantURL&gt;/_wmcs/licensing**。

    > [!NOTE]
    > *&lt;YourTenantURL&gt;* 采用以下格式：**{GUID}.rms.[Region].aadrm.com**。
    > 
    > 例如：5c6bb73b-1038-4eec-863d-49bded473437.rms.na.aadrm.com
    > 
    > 在对 Azure RMS 运行 **Get-AadrmConfiguration** cmdlet 时，可以通过标识 [RightsManagementServiceId](http://msdn.microsoft.com/library/windowsazure/dn629410.aspx) 值找到此值。


## <a name="next-steps"></a>后续步骤
要继续迁移，请转到[阶段 3 - 支持复制配置](migrate-from-ad-rms-phase3.md)。

[!INCLUDE[Commenting house rules](../includes/houserules.md)]


<!--HONumber=Jan17_HO4-->


