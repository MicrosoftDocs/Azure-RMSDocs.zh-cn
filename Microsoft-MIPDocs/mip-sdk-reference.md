# <a name="mip-sdk-for-c-preview-reference"></a>MIP SDK for C++（预览版）参考

Microsoft 信息保护 (MIP) SDK for C++（预览版）允许开发人员管理数据保护策略，并将其应用于数据和其他数字资产。  

若要了解详细信息，请参阅 [MIP 开发人员博客](https://aka.ms/MIPDevelopers)和 [MIP 示例](https://aka.ms/mipsdksamples)。

MIP SDK for C++ 包括以下类：

| 类名称 | 描述 |
| :----------|:------------|
[mip::Action](class_mip_action.md) | 所有操作的基类。 |
[mip::AddContentFooterAction](class_mip_addcontentfooteraction.md) | 指定向文档添加内容页脚的操作类。
[mip::addContentHeaderAction](class_mip_addcontentheaderaction.md) | 指定添加内容头的操作类。
[mip::AddWatermarkAction](class_mip_addwatermarkaction.md) | 指定添加水印的操作类。
[mip::BadInputError](class_mip_badinputerror.md) | 无效输入错误，API 输入无效。
[mip::CommonRights](class_mip_commonrights.md) | 普遍支持的权限。
[mip::Consent](class_mip_consent.md) | 表示用户对准许操作的接受/拒绝。
[mip::ConsentCallback](class_mip_consentcallback.md) | 同意请求通知的接口。
[mip::ConsentResult](class_mip_consentresult.md) | 说明在用户交互后同意请求的结果。
[mip::ContentLabel](class_mip_contentlabel.md) | Microsoft 信息保护标签的抽象，应用于一段内容，通常是一个文档。
[mip::CustomAction](class_mip_customaction.md) | 泛型操作类，它捕获操作的所有子属性作为一个属性包。
[mip::CustomProtectedStream](class_mip_customprotectedstream.md) | 包装一个流，以提供对读写的透明加密和解密。
[mip::EditableDocumentRights](class_mip_editabledocumentrights.md) | 适用于可编辑文档的权限。
[mip::EmailRights](class_mip_emailrights.md) | 适用于电子邮件的权限。
[mip::Error](class_mip_error.md) | 将从 MIP SDK 报告（引发或返回）的所有错误的基类。
[mip::ExecutionState](class_mip_executionstate.md) | 执行引擎所需的所有状态的接口。
[mip::EileEngine](class_mip_fileengine.md) | 适用于所有引擎功能的接口。
[mip::FileEngine::Settings](class_mip_fileengine_settings.md) | 
[mip::FileHandler](class_mip_filehandler.md) | 适用于所有文件处理函数的接口。
[mip::FileHandler::Observer](class_mip_filehandler_observer.md) | Observer 接口，供客户端获取文件处理程序相关事件的通知。
[mip::FileIOError](class_mip_fileioerror.md) | 文件 IO 错误。
[mip::FileProfile](class_mip_fileprofile.md) | Microsoft 信息保护操作的根类。
[mip::FileProfile::Observer](class_mip_fileprofile_observer.md) | 用来接收与配置文件相关的事件通知的 Observer 接口。
[mip::FileProfile::Settings](class_mip_fileprofile_settings.md) | 用来管理文件配置文件设置的接口。
[mip::GetUserPolicyResult](class_mip_getuserpolicyresult.md) | 描述用户策略获取请求的结果。
[mip::InternalError](class_mip_internalerror.md) | 内部 SDK 错误。 出现意外情况。
[mip::IStream](class_mip_istream.md) | 受保护的流的 Base 接口。
[mip::JustificationRequiredError](class_mip_justificationrequirederror.md) | 请求的更改需要更改说明。
[mip::JustifyAction](class_mip_justifyaction.md) | 请求需要向标签降级提供合理理由并在执行状态下设置响应。
[mip::Label](class_mip_label.md) | 单个 Microsoft 信息保护标签的抽象。
[mip::LabelingOptions](class_mip_labelingoptions.md) | 用于为 SetLabel 方法配置标记选项的接口。
[mip::MetadataAction](class_mip_metadataaction.md) | 指定要添加到内容的元数据信息的操作。
[mip::NetworkError](class_mip_networkerror.md) | 网络错误。
[mip::NotSupportedError](class_mip_notsupportederror.md) | 不支持操作错误。
[mip::PolicyDescriptor](class_mip_policydescriptor.md) | 表示与受保护的内容关联的临时策略。
[mip::PolicyEngine](class_mip_policyengine.md) | 此类提供适用于所有引擎功能的接口。
[mip::PolicyEngine::Settings](class_mip_policyengine_settings.md) | 此类的一个实例带有适当的参数，应提供以启动引擎。
[mip::PrivilegedRequiredError](class_mip_privilegedrequirederror.md) | 通过 privilidge 分配方法设置的当前标签不能重写。
[mip::Profile](class_mip_profile.md) | Microsoft 信息保护操作的根类。
[mip::Profile::Observer](class_mip_profile_observer.md) | 用来接收与配置文件相关的事件通知的接口。
[mip::Profile::Settings](class_mip_profile_settings.md) | 配置配置文件设置。
[mip::ProtectAdhocAction](class_mip_protectadhocaction.md) | 指定向文档添加临时保护的操作类。  
[mip::ProtectbyTemplateAction](class_mip_protectbytemplateaction.md) | 指定向文档添加模板保护的操作类。
[mip::ProtectDoNotForwardAction](class_mip_protectdonotforwardaction.md) | 指定向文档添加不转发保护的操作类。
[mip::ProtectionProfile](class_mip_protectionprofile.md) | 用于执行保护操作的基类。
[mip::ProtectionProfile::Observer](class_mip_protectionprofile_observer.md) | 用于接收保护配置文件通知。
[mip::ProtectionProfile::Settings](class_mip_protectionprofile_settings.md) | 在实例的整个生存期使用的保护配置文件设置。
[mip::RemoveContentFooterAction](class_mip_removecontentfooteraction.md) | 指定从文档中删除内容页脚的操作类。
[mip::RemoveContentHeaderAction](class_mip_removecontentheaderaction.md) | 指定从文档中删除内容头的操作类。
[mip::RemoveProtectionAction](class_mip_removeprotectionaction.md) | 指定从文档中删除保护的操作类。
[mip::RemoveWatermarkAction](class_mip_removewatermarkaction.md) | 指定从文档中删除水印的操作类。
[mip::RMSCryptographyException](class_mip_rmscryptographyexception.md) | RMS 加密异常。
[mip::RMSException](class_mip_rmsexception.md) | 基本 RMS 异常。
[mip::RMSInvalidArgumentException](class_mip_rmsinvalidargumentexception.md) | RMS 无效参数异常。
[mip::RMSLogicException](class_mip_rmslogicexception.md) | RMS 逻辑异常。
[mip::RMSNetworkException](class_mip_rmsnetworkexception.md) | RMS 网络异常。
[mip::RMSNotFoundException](class_mip_rmsnotfoundexception.md) | RMS 未找到异常。
[mip::RMSNullPointerException](class_mip_rmsnullpointerexception.md) | RMS 空指针异常。
[mip::RMSOfficeFileException](class_mip_rmsofficefileexception.md) | RMS Office 文件异常。
[mip::RMSPFileException](class_mip_rmspfileexception.md) | RMS PFile 异常。
[mip::RMSRightsException](class_mip_rmsrightsexception.md) | RMS 权限异常。
[mip::RMSStreamException](class_mip_rmsstreamexception.md) | RMS 流异常。
[mip::Roles](class_mip_roles.md) | 定义保护数据的角色。
[mip::Stream](class_mip_stream.md) | 定义 mip sdk 和基于流的内容之间的接口的类。
[mip::TemplateDescriptor](class_mip_templatedescriptor.md) | 介绍 RMS 模板。
[mip::UserPolicy](class_mip_userpolicy.md) | 表示与受保护的内容关联的策略。
[mip::UserRights](class_mip_userrights.md) | 表示一组用户和与之关联的权限。
[mip::UserRoles](class_mip_userroles.md) | 表示一组用户和与之关联的角色。
 
