![快速入门教程步骤 1](../media/AzRMS_QuickStartSteps1.PNG)

即使你的订阅支持 Azure 权限管理，该服务在默认情况下也是禁用的。 你可以使用 Office 365 管理中心或 Azure 经典门户来激活它：

-   如果你有一个包含 Azure Rights Management 的 Office 365 订阅，或者虽然你的 Office 365 订阅不包含 Azure Rights Management，但你有一个包含 Azure RMS Premium 的订阅，则可执行以下操作：**使用 Office 365 管理中心**。

-   如果没有 Office 365 订阅：**使用 Azure 经典门户**。

![Azure 经典门户](../media/AzRMS_Tutorial_1_Screenshots.png)

#### <a name="to-activate-rights-management-from-the-office-365-admin-center"></a>从 Office 365 管理中心激活权限管理

1.  转到 [Office 365 门户](https://portal.office.com/)，使用你的工作或学校帐户登录。

2.  如果未自动显示 Office 365 管理中心，请选择左上方的“应用启动程序”图标，然后选择“管理”。 “管理”  磁贴只会向 Office 365 管理员显示。

    > [!TIP]
    > 有关管理中心的帮助，请参阅 [关于 Office 365 管理中心 - 管理员帮助](https://support.office.com/article/About-the-Office-365-admin-center-Admin-Help-58537702-d421-4d02-8141-e128e3703547)。

3.  在左窗格中，单击“服务设置” 。

4.  单击“权限管理” 。

5.  在 **“权限管理”** 页上，单击 **“管理”**。

6.  在“Rights Management”页上，单击“激活”。

7.  当提示 **“是否要激活权限管理?”**时，请单击 **“激活”**。

你现在应该看到 **“权限管理已激活”** 以及停用选项（可能需要手动刷新该页）。

此时请勿单击**高级功能**。 单击该选项会将你转到可在其中配置模板的 Azure 经典门户，这些模板不是本教程所必需的。 与之相反，你可以关闭 Office 365 管理中心。

#### <a name="to-activate-rights-management-from-the-azure-portal"></a>从 Azure 门户激活权限管理

1.  转到 [ Azure 经典门户](http://go.microsoft.com/fwlink/p/?LinkID=275081)并登录。

2.  在左窗格中，单击**ACTIVE DIRECTORY**。

3.  在 **“Active Directory”** 页中，单击 **“权限管理”**。

4.  选择要进行 [!INCLUDE[aad_rightsmanagement_2](../includes/aad_rightsmanagement_2_md.md)] 的待管理目录，单击“激活”，然后确认你的操作。

**“权限管理状态”** 现在应该显示 **“活动”** ，而 **“激活”** 选项将替换为 **“停用”**。

虽然你可以在门户中配置 Rights Management 的其他选项，但这些选项不是本教程所必需的，因此可关闭 Azure 经典门户。

此第一步只需执行这些操作。 激活此服务后，你组织中的所有用户就可以对重要的和敏感的文档进行保护。 在生产环境中，你可能需要对谁能在开始的时候执行此操作进行限制，以方便分阶段部署。 不过，本教程不需要这样。

进行生产部署时，你可能还需要配置自定义模板，当然本教程不包含此部分内容。 在需要对文件进行保护时，用户可以使用模板更快速、轻松地应用正确的设置。 激活权限管理时，你将自动获得 2 个默认的模板，而在生产环境中，你可能需要使用自己的自定义模板对这些模板进行补充。 但本教程不需要模板，因此你可以转到下一步。

|如果你想了解更多信息|其他信息|
|--------------------------------|--------------------------|
|关于如何激活权限管理以后如何在激活该服务后控制谁能对文件和电子邮件进行保护   →|[激活 Azure Rights Management](../deploy-use/activate-azure-classic.md)|
|关于默认模板以及如何创建新的自定义模板   →|[为 Azure Rights Management 配置自定义模板](../deploy-use/create-template.md)|
