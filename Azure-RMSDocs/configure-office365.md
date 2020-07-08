---
title: 要使用的 Office 365 服务配置 Azure RMS-AIP
description: 管理员要将 Office 365 服务配置为使用 azure 信息保护中的 Azure Rights Management 服务的信息和说明。
author: cabailey
ms.author: cabailey
manager: barbkess
ms.date: 11/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 0a6ce612-1b6b-4e21-b7fd-bcf79e492c3b
ms.subservice: azurerms
ms.reviewer: esaggese
ms.suite: ems
ms.custom: admin
ms.openlocfilehash: ef5a4d9f270d111ead3a6d04c2b49e67e230eb6a
ms.sourcegitcommit: 223e26b0ca4589317167064dcee82ad0a6a8d663
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86047807"
---
# <a name="office365-configuration-for-online-services-to-use-the-azure-rights-management-service"></a>Office 365：用于联机服务的配置以使用 Azure Rights Management 服务

>*适用于： [Azure 信息保护](https://azure.microsoft.com/pricing/details/information-protection)、 [Office 365](https://download.microsoft.com/download/E/C/F/ECF42E71-4EC0-48FF-AA00-577AC14D5B5C/Azure_Information_Protection_licensing_datasheet_EN-US.pdf)*

使用下列部分来帮助你配置 Exchange Online、Microsoft SharePoint 和 Microsoft OneDrive 以使用 Azure 信息保护中的 Azure Rights Management 服务。

## <a name="exchangeonline-irm-configuration"></a>Exchange Online：IRM 配置

有关 Exchange Online 如何与 Azure Rights Management 服务协同工作的信息，请参阅[Office 应用程序和服务如何支持 azure Rights Management](office-apps-services-support.md)中的 " [Exchange Online 和 exchange Server](office-apps-services-support.md#exchange-online-and-exchange-server) " 部分。

为了使用 Azure 权限管理服务，可能已启用 Exchange Online。 要进行检查，请运行以下命令：

1. 如果这是你第一次在计算机上使用 Windows PowerShell for Exchange Online，必须配置 Windows PowerShell 以运行签名的脚本。 使用“以管理员身份运行”选项启动 Windows PowerShell 会话，然后键入****：

    ```md
    Set-ExecutionPolicy RemoteSigned
    ```

    按“Y”确认****。

2. 在 Windows PowerShell 会话中，使用为远程 Shell 访问启用的帐户登录到 Exchange Online。 默认情况下，将为 Exchange Online 中创建的所有帐户启用远程 Shell 访问，但可以使用[ &lt; UserIdentity &gt; -RemotePowerShellEnabled](https://technet.microsoft.com/library/jj984292%28v=exchg.160%29.aspx)命令禁用（和启用）此功能。

    若要登录，请首先键入：

    ```markdown
    $Cred = Get-Credential
    ```

    然后，在“Windows PowerShell 凭据请求”对话框中，提供你的 Office 365 用户名和密码 ****。

3. 首先，通过设置一个变量连接到 Exchange Online 服务：

    ```md
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://ps.outlook.com/powershell/ -Credential $Cred -Authentication Basic –AllowRedirection
    ```

    然后，运行以下命令：

    ```md
    Import-PSSession $Session
    ```

4. 运行[set-irmconfiguration](https://technet.microsoft.com/library/dd776120(v=exchg.160).aspx)命令，查看保护服务的 Exchange Online 配置：

    ```md
    Get-IRMConfiguration
    ```

    从输出中找到 AzureRMSLicensingEnabled 值****：

    - 如果 AzureRMSLicensingEnabled 设置为“True”，则已为 Azure 权限管理服务启用 Exchange Online****。

    - 如果 AzureRMSLicensingEnabled 设置为“False”，请运行以下命令，为 Azure Rights Management 服务启用 Exchange Online：`Set-IRMConfiguration -AzureRMSLicensingEnabled $true`****

5. 要测试 Exchange Online 是否已成功配置，请运行下列命令：

    ```md
    Test-IRMConfiguration -Sender <user email address>
    ```

    例如：**Test-IRMConfiguration -Sender  adams@contoso.com**

    此命令将运行一系列检查，包括验证与服务的连接，检索配置，检索 URI、许可证和任何模板。 在 Windows PowerShell 会话中，你将看到每一项的结果并在结束时看到是否所有内容均已通过这些检查： **总体结果：通过**

在启用 Exchange Online 以使用 Azure Rights Management 服务后，可以配置自动应用信息保护的功能，如[电子邮件流规则](https://support.office.com/article/define-mail-flow-rules-to-encrypt-email-messages-in-office-365-9b7daf19-d5f2-415b-bc43-a0f5f4a585e8)、[数据丢失防护 (DLP) 策略](https://technet.microsoft.com/library/jj150527%28v=exchg.150%29.aspx)和[受保护的语音邮件](https://technet.microsoft.com/library/dn198211%28v=exchg.150%29.aspx)（统一消息）。

## <a name="sharepoint-in-microsoft-365-and-onedrive-irm-configuration"></a>Microsoft 365 和 OneDrive 中的 SharePoint： IRM 配置

有关 SharePoint IRM 如何与 Azure Rights Management 服务一起工作的信息，请参阅本文档的 " **Rights Management 保护**" 部分[中的 sharepoint In Microsoft 365 和 sharepoint Server](office-apps-services-support.md#sharepoint-in-microsoft-365-and-sharepoint-server) 。

若要在 Microsoft 365 和 OneDrive 中配置 SharePoint 以支持 Azure Rights Management 服务，必须首先使用 SharePoint 管理中心为 SharePoint 启用信息权限管理（IRM）服务。 然后，站点所有者可以使用 IRM 保护其 SharePoint 列表和文档库，用户可以对其 OneDrive 库进行 IRM 保护，使保存在那里的文档和与他人共享的文档自动受到 Azure Rights Management 服务的保护。

> [!NOTE]
> Microsoft 365 和 OneDrive 中的受 IRM 保护的 SharePoint 库需要最新版本的新 OneDrive 同步客户端（OneDrive.exe）和 Microsoft 下载中心提供的[RMS 客户端](https://www.microsoft.com/download/details.aspx?id=38396)版本。 即使已经安装了 Azure 信息保护客户端，也要安装此版本的 RMS 客户端。 有关此部署方案的详细信息，请参阅[在企业环境中部署新的 OneDrive 同步客户端](https://support.office.com/article/Deploy-the-new-OneDrive-sync-client-in-an-enterprise-environment-3f3a511c-30c6-404a-98bf-76f95c519668)。

若要为 SharePoint 启用信息权限管理（IRM）服务，请参阅 Office 文档中的以下说明：

- [在 SharePoint 管理中心设置信息 Rights Management （IRM）](https://docs.microsoft.com/microsoft-365/compliance/set-up-irm-in-sp-admin-center)

由 Office 365 管理员进行此配置。

### <a name="configuring-irm-for-libraries-and-lists"></a>为库和列表配置 IRM

在你为 SharePoint 启用 IRM 服务后，站点所有者可以使用 IRM 保护其 SharePoint 文档库和列表。 有关说明，请参阅 Office 网站中的以下内容：

- [将信息权限管理应用于列表或库](https://office.microsoft.com/sharepoint-help/apply-information-rights-management-to-a-list-or-library-HA102891460.aspx)

由 SharePoint 站点管理员进行此配置。

### <a name="configuring-irm-for-onedrive"></a>为 OneDrive 配置 IRM

为 SharePoint 启用 IRM 服务后，可为用户的 OneDrive 文档库或单个文件夹配置 Rights Management 保护。 用户可以使用其 OneDrive 网站为自己配置此项。 虽然管理员不能使用 SharePoint 管理中心为他们配置此保护，但是你可以使用 Windows PowerShell 执行此操作。

> [!NOTE]
> 有关配置 OneDrive 的详细信息，请参阅 office 文档中的 Office [365 中的 "设置 onedrive](https://support.office.com/article/Set-up-OneDrive-for-Business-in-Office-365-3e21f8f0-e0a1-43be-aa3e-8c0236bf11bb)"。

#### <a name="configuration-for-users"></a>用户配置

为用户授予以下说明，以便他们可以配置其 OneDrive 来保护其业务文件。

1. 使用工作或学校帐户登录到 Office 365 并转到 [OneDrive 网站](https://admin.microsoft.com/onedrive)。

2. 在导航窗格的底部，选择“返回到经典 OneDrive”****。

3. 选择“设置”图标****。 在“设置”窗格中，如果“功能区”设置为“关”，请选择此设置以启用功能区************。

4. 若要将所有 OneDrive 文件配置为受保护，请从功能区中选择 "**库**" 选项卡，然后选择 "**库设置**"。

5. 在“文档”>“设置”页上的“权限和管理”部分中，单击“信息权限管理”************。

6. 在“信息权限管理设置”页上，选中“限制对此库的下载权限”复选框********。 为权限指定你选择的名称和描述，（可选）单击“显示选项”以配置可选配置，然后单击“确定”********。

    有关配置选项的详细信息，请参阅 Office 文档中的[将信息权限管理应用于列表或库](https://support.office.com/article/Apply-Information-Rights-Management-to-a-list-or-library-3bdb5c4e-94fc-4741-b02f-4e7cc3c54aa1)中的说明。

由于此配置依赖于用户（而不是管理员）来保护其 OneDrive 文件，因此，请告知用户保护其文件的好处以及如何执行此操作。 例如，说明当用户从 OneDrive 共享文档时，只有他们授权的人员可以使用其配置的任何限制访问它，即使该文件被重命名并复制到其他位置也是如此。

#### <a name="configuration-for-administrators"></a>管理员配置

尽管你无法使用 SharePoint 管理中心为用户的 OneDrive 配置 IRM，但是你可以使用 Windows PowerShell 执行此操作。 若要为这些库启用 IRM，请执行以下步骤：

1. 下载并安装[SharePoint 客户端组件 SDK](https://www.microsoft.com/download/details.aspx?id=42038)。

2. 下载并安装[SharePoint 命令行管理](https://www.microsoft.com/download/details.aspx?id=35588)程序。

3. 在计算机上复制以下脚本的内容，并将文件命名为 Set-IRMOnOneDriveForBusiness.ps1。

   *&#42;&#42;免责声明&#42;&#42;*：此示例脚本在任何 Microsoft 标准支持计划或服务下均不受支持。 此示例脚本按原样提供，不提供任何形式的保证。

   ```ps
   # Requires Windows PowerShell version 3

   <#
     Description:

       Configures IRM policy settings for OneDrive and can also be used for SharePoint libraries and lists

    Script Installation Requirements:

      SharePoint Client Components SDK
      https://www.microsoft.com/download/details.aspx?id=42038

      SharePoint Management Shell
      https://www.microsoft.com/download/details.aspx?id=35588

   ======
   #>

   # URL will be in the format https://<tenant-name>-admin.sharepoint.com
   $sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

   $tenantAdmin = "admin@contoso.com"

   $webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
                "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
                "https://contoso-my.sharepoint.com/personal/user3_contoso_com")

   <# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
      Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

   #>

   $listTitle = "Documents"

   function Load-SharePointOnlineClientComponentAssemblies
   {
       [cmdletbinding()]
       param()

       process
       {
           # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
           try
           {
               Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
               [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

               return $true
           }
           catch
           {
               if($_.Exception.Message -match "Could not load file or assembly")
               {
                   Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
               }
               else
               {
                   Write-Error -Exception $_.Exception
               }
               return $false
           }
       }
   }

   function Load-SharePointOnlineModule
   {
       [cmdletbinding()]
       param()

       process
       {
           do
           {
               # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
               $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

               if(-not $spoModule)
               {
                   try
                   {
                       Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                       return $true
                   }
                   catch
                   {
                       if($_.Exception.Message -match "Could not load file or assembly")
                       {
                           Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
                       }
                       else
                       {
                           Write-Error -Exception $_.Exception
                       }
                       return $false
                   }
               }
               else
               {
                   return $true
               }
           }
           while(-not $spoModule)
       }
   }

   function Set-IrmConfiguration
   {
       [cmdletbinding()]
       param(
           [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List,
           [parameter(Mandatory=$true)][string]$PolicyTitle,
           [parameter(Mandatory=$true)][string]$PolicyDescription,
           [parameter(Mandatory=$false)][switch]$IrmReject,
           [parameter(Mandatory=$false)][DateTime]$ProtectionExpirationDate,
           [parameter(Mandatory=$false)][switch]$DisableDocumentBrowserView,
           [parameter(Mandatory=$false)][switch]$AllowPrint,
           [parameter(Mandatory=$false)][switch]$AllowScript,
           [parameter(Mandatory=$false)][switch]$AllowWriteCopy,
           [parameter(Mandatory=$false)][int]$DocumentAccessExpireDays,
           [parameter(Mandatory=$false)][int]$LicenseCacheExpireDays,
           [parameter(Mandatory=$false)][string]$GroupName
       )

       process
       {
           Write-Verbose "Applying IRM Configuration on '$($List.Title)'"

           # reset the value to the default settings
           $list.InformationRightsManagementSettings.Reset()

           $list.IrmEnabled = $true

           # IRM Policy title and description

               $list.InformationRightsManagementSettings.PolicyTitle       = $PolicyTitle
               $list.InformationRightsManagementSettings.PolicyDescription = $PolicyDescription

           # Set additional IRM library settings

               # Do not allow users to upload documents that do not support IRM
               $list.IrmReject = $IrmReject.IsPresent

               $parsedDate = Get-Date
               if([DateTime]::TryParse($ProtectionExpirationDate, [ref]$parsedDate))
               {
                   # Stop restricting access to the library at <date>
                   $list.IrmExpire = $true
                   $list.InformationRightsManagementSettings.DocumentLibraryProtectionExpireDate = $ProtectionExpirationDate
               }

               # Prevent opening documents in the browser for this Document Library
               $list.InformationRightsManagementSettings.DisableDocumentBrowserView = $DisableDocumentBrowserView.IsPresent

           # Configure document access rights

               # Allow viewers to print
               $list.InformationRightsManagementSettings.AllowPrint = $AllowPrint.IsPresent

               # Allow viewers to run script and screen reader to function on downloaded documents
               $list.InformationRightsManagementSettings.AllowScript = $AllowScript.IsPresent

               # Allow viewers to write on a copy of the downloaded document
               $list.InformationRightsManagementSettings.AllowWriteCopy = $AllowWriteCopy.IsPresent

               if($DocumentAccessExpireDays)
               {
                   # After download, document access rights will expire after these number of days (1-365)
                   $list.InformationRightsManagementSettings.EnableDocumentAccessExpire = $true
                   $list.InformationRightsManagementSettings.DocumentAccessExpireDays   = $DocumentAccessExpireDays
               }

           # Set group protection and credentials interval

               if($LicenseCacheExpireDays)
               {
                   # Users must verify their credentials using this interval (days)
                   $list.InformationRightsManagementSettings.EnableLicenseCacheExpire = $true
                   $list.InformationRightsManagementSettings.LicenseCacheExpireDays   = $LicenseCacheExpireDays
               }

               if($GroupName)
               {
                   # Allow group protection. Default group:
                   $list.InformationRightsManagementSettings.EnableGroupProtection = $true
                   $list.InformationRightsManagementSettings.GroupName             = $GroupName
               }
       }
       end
       {
           if($list)
           {
               Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
               $list.InformationRightsManagementSettings.Update()
               $list.Update()
               $script:clientContext.Load($list)
               $script:clientContext.ExecuteQuery()
           }
       }
   }

   function Get-CredentialFromCredentialCache
   {
       [cmdletbinding()]
       param([string]$CredentialName)

       #if( Test-Path variable:\global:CredentialCache )
       if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
       {
           if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
           {
               Write-Verbose "Credential Cache Hit: $CredentialName"
               return $global:O365TenantAdminCredentialCache[$CredentialName]
           }
       }
       Write-Verbose "Credential Cache Miss: $CredentialName"
       return $null
   }

   function Add-CredentialToCredentialCache
   {
       [cmdletbinding()]
       param([System.Management.Automation.PSCredential]$Credential)

       if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
       {
           Write-Verbose "Initializing the Credential Cache"
           $global:O365TenantAdminCredentialCache = @{}
       }

       Write-Verbose "Adding Credential to the Credential Cache"
       $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
   }

   # load the required assemblies and Windows PowerShell modules

       if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

   # Add the credentials to the client context and SharePoint service connection

       # check for cached credentials to use
       $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

       if(-not $o365TenantAdminCredential)
       {
           # when credentials are not cached, prompt for the tenant admin credentials
           $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

           if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
           {
               Write-Error -Message "Could not validate the supplied tenant admin credentials"
               return
           }

           # add the credentials to the cache
           Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
       }

   # connect to Office365 first, required for SharePoint cmdlets to run

       Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

   # enumerate each of the specified site URLs

       foreach($webUrl in $webUrls)
       {
           $grantedSiteCollectionAdmin = $false

           try
           {
               # establish the client context and set the credentials to connect to the site
               $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
               $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

               # initialize the site and web context
               $script:clientContext.Load($script:clientContext.Site)
               $script:clientContext.Load($script:clientContext.Web)
               $script:clientContext.ExecuteQuery()

               # load and ensure the tenant admin user account if present on the target SharePoint site
               $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
               $script:clientContext.Load($tenantAdminUser)
               $script:clientContext.ExecuteQuery()

               # check if the tenant admin is a site admin
               if( -not $tenantAdminUser.IsSiteAdmin )
               {
                   try
                   {
                       # grant the tenant admin temporary admin rights to the site collection
                       Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                       $grantedSiteCollectionAdmin = $true
                   }
                   catch
                   {
                       Write-Error $_.Exception
                       return
                   }
               }

               try
               {
                   # load the list orlibrary using CSOM

                   $list = $null
                   $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                   $script:clientContext.Load($list)
                   $script:clientContext.ExecuteQuery()

                   # **************  ADMIN INSTRUCTIONS  **************
                   # If necessary, modify the following Set-IrmConfiguration parameters to match your required values
                   # The supplied options and values are for example only
                   # Example that shows the Set-IrmConfiguration command with all parameters: Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users" -IrmReject -ProtectionExpirationDate $(Get-Date).AddDays(180) -DisableDocumentBrowserView -AllowPrint -AllowScript -AllowWriteCopy -LicenseCacheExpireDays 25 -DocumentAccessExpireDays 90

                   Set-IrmConfiguration -List $list -PolicyTitle "Protected Files" -PolicyDescription "This policy restricts access to authorized users"  
               }
               catch
               {
                   Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
               }
          }
          finally
          {
               if($grantedSiteCollectionAdmin)
               {
                   # remove the temporary admin rights to the site collection
                   Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
               }
          }
       }

   Disconnect-SPOService -ErrorAction SilentlyContinue
   ```

4. 查看脚本，然后进行以下更改：

   1. 搜索 `$sharepointAdminCenterUrl` 并将示例值替换为自己的 SharePoint 管理中心 URL。

      进入 SharePoint 管理中心时，会发现此值作为基 URL，并且具有以下格式： https://* &lt; tenant_name &gt; *-admin.sharepoint.com

      例如，如果租户名称为 "contoso"，则应指定：**https://contoso-admin.sharepoint.com**

   2. 搜索 `$tenantAdmin` 并将示例值替换为自己的 Office 365 完全限定全局管理员帐户。

      此值与你用来以全局管理员身份登录到 Microsoft 365 管理中心的值相同，并具有以下格式： user_name@* &lt; 租户域名 &gt; *.com

      例如，如果 "contoso.com" 租户域的 Office 365 全局管理员用户名是 "admin"，则应指定：**admin@contoso.com**

   3. 搜索 `$webUrls` 并将示例值替换为用户的 OneDrive Web url，根据需要添加或删除任意数量的条目。

      或者，请参阅脚本中有关如何通过导入包含需要配置的所有 URL 的 .CSV 文件来替换此数组的注释。  我们提供了另一个示例脚本，用于自动搜索并提取 URL 以填充此 .CSV 文件。 准备好执行此操作时，请使用[其他脚本将所有 OneDrive url 输出到。"CSV 文件](#additional-script-to-output-all-onedrive-urls-to-a-csv-file)" 一节。

      用户的 OneDrive 的 web URL 采用以下格式： https://* &lt; 租户名称 &gt; *-my.sharepoint.com/personal/* &lt; &gt; user_name*_* &lt; 租户名称 &gt; *_com

      例如，如果 contoso 租户中的用户的用户名为 "rsimone"，则应指定：**https://contoso-my.sharepoint.com/personal/rsimone_contoso_com**

   4. 由于我们使用脚本来配置 OneDrive，因此请不要更改变量的**文档**值 `$listTitle` 。

   5. 搜索 `ADMIN INSTRUCTIONS`。 如果不更改此部分，则将为 IRM 配置用户的 OneDrive，策略标题为 "受保护的文件"，并且说明 "此策略限制授权用户的访问权限"。  不会设置任何其他 IRM 选项，这可能适用于大多数环境。 但是，可以更改建议的策略标题和说明，也可以添加适合环境的任何其他 IRM 选项。 请参阅脚本中带有注释的示例，以帮助构造自己的一组 Set-IrmConfiguration 命令参数。

5. 保存该脚本并为其签名。 如果未为脚本签名（更安全），则必须在计算机上配置 Windows PowerShell 才能运行未签名的脚本。 为此，请使用“以管理员身份运行”选项运行 Windows PowerShell 会话，然后键入 **Set-ExecutionPolicy Unrestricted**。**** 但是，此配置将允许所有未签名的脚本运行（较不安全）。

   有关为 Windows PowerShell 脚本签名的详细信息，请参阅 PowerShell 文档库中的 [about_Signing](https://technet.microsoft.com/library/hh847874.aspx)。

6. 运行该脚本，如果系统提示，请提供 Office 365 管理员帐户的密码。 如果修改了脚本，然后在同一个 Windows PowerShell 会话中运行该脚本，则系统不会提示输入凭据。

> [!TIP]
> 你还可以使用此脚本为 SharePoint 库配置 IRM。 对于此配置，你可能希望启用附加选项“不允许用户上载不支持 IRM 的文档”，以确保库只包含受保护的文档****。    为此，请将 `-IrmReject` 参数添加到脚本中的 Set-IrmConfiguration 命令。
>
> 你还需要修改 `$webUrls` 变量（例如， **https： \/ /contoso.sharepoint.com**）和 `$listTitle` 变量（例如 **$Reports**）。

如果需要为用户的 OneDrive 库禁用 IRM，请参阅[禁用 OneDrive 的 irm](#script-to-disable-irm-for-onedrive)部分中的脚本。

##### <a name="additional-script-to-output-all-onedrive-urls-to-a-csv-file"></a>用于将所有 OneDrive Url 输出到的其他脚本。CSV 文件

对于上面的步骤4c，你可以使用以下 Windows PowerShell 脚本提取所有用户的 OneDrive 库的 Url，然后可以根据需要对其进行检查、编辑（如有必要），然后将其导入到主脚本中。

此脚本还需要[Sharepoint 客户端组件 SDK](https://www.microsoft.com/download/details.aspx?id=42038)和[Sharepoint 命令行管理](https://www.microsoft.com/download/details.aspx?id=35588)程序。 按照相同的说明复制并粘贴它，本地保存文件（例如，“Report-OneDriveForBusinessSiteInfo.ps1”），如之前一样修改 `$sharepointAdminCenterUrl` 和 `$tenantAdmin` 值，然后运行该脚本。

*&#42;&#42;免责声明&#42;&#42;*：此示例脚本在任何 Microsoft 标准支持计划或服务下均不受支持。 此示例脚本按原样提供，不提供任何形式的保证。

```ps
# Requires Windows PowerShell version 3

<#
  Description:

    Queries the search service of an Office 365 tenant to retrieve all OneDrive sites.  
    Details of the discovered sites are written to a .CSV file (by default,"OneDriveForBusinessSiteInfo_<date>.csv").

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

======
#>

# URL will be in the format https://<tenant-name>-admin.sharepoint.com
$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.onmicrosoft.com"                           

$reportName = "OneDriveForBusinessSiteInfo_$((Get-Date).ToString("yyyy-MM-dd_hh.mm.ss")).csv"

$oneDriveForBusinessSiteUrls= @()
$resultsProcessed = 0

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# establish the client context and set the credentials to connect to the site

    $clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($sharepointAdminCenterUrl)
    $clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

# run a query against the Office 365 tenant search service to retrieve all OneDrive URLs

    do
    {
        # build the query object
        $query = New-Object Microsoft.SharePoint.Client.Search.Query.KeywordQuery($clientContext)
        $query.TrimDuplicates        = $false
        $query.RowLimit              = 500
        $query.QueryText             = "SPSiteUrl:'/personal/' AND contentclass:STS_Site"
        $query.StartRow              = $resultsProcessed
        $query.TotalRowsExactMinimum = 500000

        # run the query
        $searchExecutor = New-Object Microsoft.SharePoint.Client.Search.Query.SearchExecutor($clientContext)
        $queryResults = $searchExecutor.ExecuteQuery($query)
        $clientContext.ExecuteQuery()

        # enumerate the search results and store the site URLs
        $queryResults.Value[0].ResultRows | % {
            $oneDriveForBusinessSiteUrls += $_.Path
            $resultsProcessed++
        }
    }
    while($resultsProcessed -lt $queryResults.Value.TotalRows)

$oneDriveForBusinessSiteUrls | Out-File -FilePath $reportName
```

##### <a name="script-to-disable-irm-for-onedrive"></a>用于为 OneDrive 禁用 IRM 的脚本

如果需要为用户的 OneDrive 禁用 IRM，请使用以下示例脚本。

此脚本还需要[Sharepoint 客户端组件 SDK](https://www.microsoft.com/download/details.aspx?id=42038)和[Sharepoint 命令行管理](https://www.microsoft.com/download/details.aspx?id=35588)程序。 复制并粘贴内容，本地保存文件（例如，“Disable-IRMOnOneDriveForBusiness.ps1”），并修改 `$sharepointAdminCenterUrl` 和 `$tenantAdmin` 值。 手动指定 OneDrive Url 或使用上一部分中的脚本，以便可以导入这些 Url，然后运行该脚本。

*&#42;&#42;免责声明&#42;&#42;*：此示例脚本在任何 Microsoft 标准支持计划或服务下均不受支持。 此示例脚本按原样提供，不提供任何形式的保证。

```ps
# Requires Windows PowerShell version 3

<#
  Description:

    Disables IRM for OneDrive and can also be used for SharePoint libraries and lists

 Script Installation Requirements:

   SharePoint Client Components SDK
   https://www.microsoft.com/download/details.aspx?id=42038

   SharePoint Management Shell
   https://www.microsoft.com/download/details.aspx?id=35588

======
#>

$sharepointAdminCenterUrl = "https://contoso-admin.sharepoint.com"

$tenantAdmin = "admin@contoso.com"

$webUrls = @("https://contoso-my.sharepoint.com/personal/user1_contoso_com",
             "https://contoso-my.sharepoint.com/personal/user2_contoso_com",
             "https://contoso-my.sharepoint.com/personal/person3_contoso_com")

<# As an alternative to specifying the URLs as an array, you can import them from a CSV file (no header, single value per row).
   Then, use: $webUrls = Get-Content -Path "File_path_and_name.csv"

#>

$listTitle = "Documents"

function Load-SharePointOnlineClientComponentAssemblies
{
    [cmdletbinding()]
    param()

    process
    {
        # assembly location: C:\Program Files\Common Files\microsoft shared\Web Server Extensions\16\ISAPI
        try
        {
            Write-Verbose "Loading Assembly: Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.Policy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.Office.Client.TranslationServices, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.DocumentManagement, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Publishing, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Runtime, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search.Applications, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Search, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.Taxonomy, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            Write-Verbose "Loading Assembly: Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c"
            [System.Reflection.Assembly]::Load("Microsoft.SharePoint.Client.UserProfiles, Version=16.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c") | Out-Null

            return $true
        }
        catch
        {
            if($_.Exception.Message -match "Could not load file or assembly")
            {
                Write-Error -Message "Unable to load the SharePoint Server 2013 Client Components.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=42038"
            }
            else
            {
                Write-Error -Exception $_.Exception
            }
            return $false
        }
    }
}

function Load-SharePointOnlineModule
{
    [cmdletbinding()]
    param()

    process
    {
        do
        {
            # Installation location: C:\Program Files\SharePoint Online Management Shell\Microsoft.Online.SharePoint.PowerShell
            $spoModule = Get-Module -Name Microsoft.Online.SharePoint.PowerShell -ErrorAction SilentlyContinue

            if(-not $spoModule)
            {
                try
                {
                    Import-Module Microsoft.Online.SharePoint.PowerShell -DisableNameChecking
                    return $true
                }
                catch
                {
                    if($_.Exception.Message -match "Could not load file or assembly")
                    {
                        Write-Error -Message "Unable to load the SharePoint Online Management Shell.`nDownload Location: https://www.microsoft.com/download/details.aspx?id=35588"
                    }
                    else
                    {
                        Write-Error -Exception $_.Exception
                    }
                    return $false
                }
            }
            else
            {
                return $true
            }
        }
        while(-not $spoModule)
    }
}

function Remove-IrmConfiguration
{
    [cmdletbinding()]
    param(
        [parameter(Mandatory=$true)][Microsoft.SharePoint.Client.List]$List
    )

    process
    {
        Write-Verbose "Disabling IRM Configuration on '$($List.Title)'"

        $List.IrmEnabled = $false
        $List.IrmExpire  = $false
        $List.IrmReject  = $false
        $List.InformationRightsManagementSettings.Reset()
    }
    end
    {
        if($List)
        {
            Write-Verbose "Committing IRM configuration settings on '$($list.Title)'"
            $list.InformationRightsManagementSettings.Update()
            $list.Update()
            $script:clientContext.Load($list)
            $script:clientContext.ExecuteQuery()
        }
    }
}

function Get-CredentialFromCredentialCache
{
    [cmdletbinding()]
    param([string]$CredentialName)

    #if( Test-Path variable:\global:CredentialCache )
    if( Get-Variable O365TenantAdminCredentialCache -Scope Global -ErrorAction SilentlyContinue )
    {
        if($global:O365TenantAdminCredentialCache.ContainsKey($CredentialName))
        {
            Write-Verbose "Credential Cache Hit: $CredentialName"
            return $global:O365TenantAdminCredentialCache[$CredentialName]
        }
    }
    Write-Verbose "Credential Cache Miss: $CredentialName"
    return $null
}

function Add-CredentialToCredentialCache
{
    [cmdletbinding()]
    param([System.Management.Automation.PSCredential]$Credential)

    if(-not (Get-Variable CredentialCache -Scope Global -ErrorAction SilentlyContinue))
    {
        Write-Verbose "Initializing the Credential Cache"
        $global:O365TenantAdminCredentialCache = @{}
    }

    Write-Verbose "Adding Credential to the Credential Cache"
    $global:O365TenantAdminCredentialCache[$Credential.UserName] = $Credential
}

# load the required assemblies and Windows PowerShell modules

    if(-not ((Load-SharePointOnlineClientComponentAssemblies) -and (Load-SharePointOnlineModule)) ) { return }

# Add the credentials to the client context and SharePoint service connection

    # check for cached credentials to use
    $o365TenantAdminCredential = Get-CredentialFromCredentialCache -CredentialName $tenantAdmin

    if(-not $o365TenantAdminCredential)
    {
        # when credentials are not cached, prompt for the tenant admin credentials
        $o365TenantAdminCredential = Get-Credential -UserName $tenantAdmin -Message "Enter the password for the Office 365 admin"

        if(-not $o365TenantAdminCredential -or -not $o365TenantAdminCredential.UserName -or $o365TenantAdminCredential.Password.Length -eq 0 )
        {
            Write-Error -Message "Could not validate the supplied tenant admin credentials"
            return
        }

        # add the credentials to the cache
        Add-CredentialToCredentialCache -Credential $o365TenantAdminCredential
    }

# connect to Office365 first, required for SharePoint cmdlets to run

    Connect-SPOService -Url $sharepointAdminCenterUrl -Credential $o365TenantAdminCredential

# enumerate each of the specified site URLs

    foreach($webUrl in $webUrls)
    {
        $grantedSiteCollectionAdmin = $false

        try
        {
            # establish the client context and set the credentials to connect to the site
            $script:clientContext = New-Object Microsoft.SharePoint.Client.ClientContext($webUrl)
            $script:clientContext.Credentials = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($o365TenantAdminCredential.UserName, $o365TenantAdminCredential.Password)

            # initialize the site and web context
            $script:clientContext.Load($script:clientContext.Site)
            $script:clientContext.Load($script:clientContext.Web)
            $script:clientContext.ExecuteQuery()

            # load and ensure the tenant admin user account if present on the target SharePoint site
            $tenantAdminUser = $script:clientContext.Web.EnsureUser($o365TenantAdminCredential.UserName)
            $script:clientContext.Load($tenantAdminUser)
            $script:clientContext.ExecuteQuery()

            # check if the tenant admin is a site admin
            if( -not $tenantAdminUser.IsSiteAdmin )
            {
                try
                {
                    # grant the tenant admin temporary admin rights to the site collection
                    Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $true | Out-Null
                    $grantedSiteCollectionAdmin = $true
                }
                catch
                {
                    Write-Error $_.Exception
                    return
                }
            }

            try
            {
                # load the list orlibrary using CSOM

                $list = $null
                $list = $script:clientContext.Web.Lists.GetByTitle($listTitle)
                $script:clientContext.Load($list)
                $script:clientContext.ExecuteQuery()

               Remove-IrmConfiguration -List $list
            }
            catch
            {
                Write-Error -Message "Error setting IRM configuration on site: $webUrl.`nError Details: $($_.Exception.ToString())"
            }
       }
       finally
       {
            if($grantedSiteCollectionAdmin)
            {
                # remove the temporary admin rights to the site collection
                Set-SPOUser -Site $script:clientContext.Site.Url -LoginName $o365TenantAdminCredential.UserName -IsSiteCollectionAdmin $false | Out-Null
            }
       }
    }

Disconnect-SPOService -ErrorAction SilentlyContinue
```
