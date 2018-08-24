---
title: iOS/OS X 代码示例 | Azure RMS
description: 本主题向你介绍 iOS/OS X 版 RMS SDK 的重要代码元素。
keywords: ''
author: lleonard-msft
ms.author: alleonar
manager: mbaldwin
ms.date: 02/23/2017
ms.topic: article
ms.service: information-protection
ms.assetid: 7E12EBF2-5A19-4A8D-AA99-531B09DA256A
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 714352afb1bade2b658486697cf5d943c89625be
ms.sourcegitcommit: 7ba9850e5bb07b14741bb90ebbe98f1ebe057b10
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2018
ms.locfileid: "42805800"
---
# <a name="iosos-x-code-examples"></a>iOS/OS X 代码示例

本主题向你介绍 iOS/OS X 版 RMS SDK 的重要代码元素。

**注意** 在示例代码以及随后的说明中，我们使用术语 MSIPC (Microsoft Information Protection and Control) 来引用客户端进程。



## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>使用 Microsoft Rights Management SDK 4.2 - 重要方案


以下是摘取自一个较大示例应用程序的 **Objective C** 代码示例，表示对你学习此 SDK 十分重要的开发方案。 这些示例演示 Microsoft 受保护的文件格式（称为受保护的文件）的使用、自定义受保护的文件格式的使用以及自定义 UI 控件的使用。

### <a name="scenario-consume-an-rms-protected-file"></a>方案：使用受 RMS 保护的文件


- **步骤 1**：创建 [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) 对象

 **说明**：通过 create 方法实例化 [MSProtectedData](https://msdn.microsoft.com/library/dn758348.aspx) 对象，该方法使用 [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) 实现服务身份验证，以便通过将 **MSAuthenticationCallback** 的实例作为参数 *authenticationCallback* 传递给 MSIPC API 来获取令牌。 请参阅以下示例代码部分中对 [MSProtectedData protectedDataWithProtectedFile](https://msdn.microsoft.com/library/dn758351.aspx) 的调用。

        + (void)consumePtxtFile:(NSString *)path authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // userId can be provided as a hint for authentication
            [MSProtectedData protectedDataWithProtectedFile:path
                                                 userId:nil
                                 authenticationCallback:authenticationCallback
                                                options:Default
                                        completionBlock:^(MSProtectedData *data, NSError *error)
            {
                //Read the content from the ProtectedData, this will decrypt the data
                NSData *content = [data retrieveData];
            }];
        }

- **步骤 2**：使用 Active Directory 身份验证库 (ADAL) 设置身份验证。

  **说明**：此步骤中会介绍用于通过示例身份验证参数来实现 [MSAuthenticationCallback](https://msdn.microsoft.com/library/dn758312.aspx) 的 ADAL。 若要深入了解如何使用 ADAL，请参阅 Azure AD 身份验证库 (ADAL)。

      // AuthenticationCallback holds the necessary information to retrieve an access token.
      @interface MsipcAuthenticationCallback : NSObject<MSAuthenticationCallback>

      @end

      @implementation MsipcAuthenticationCallback

      - (void)accessTokenWithAuthenticationParameters:
             (MSAuthenticationParameters *)authenticationParameters
                                    completionBlock:
             (void(^)(NSString *accessToken, NSError *error))completionBlock
      {
          ADAuthenticationError *error;
          ADAuthenticationContext* context = [
              ADAuthenticationContext authenticationContextWithAuthority:authenticationParameters.authority
                                                                error:&error
          ];
          NSString *appClientId = @”com.microsoft.sampleapp”;
          NSURL *redirectURI = [NSURL URLWithString:@"local://authorize"];
          // Retrieve token using ADAL
          [context acquireTokenWithResource:authenticationParameters.resource
                                 clientId:appClientId
                              redirectUri:redirectURI
                                   userId:authenticationParameters.userId
                          completionBlock:^(ADAuthenticationResult *result) {
                              if (result.status != AD_SUCCEEDED)
                              {
                                  NSLog(@"Auth Failed");
                                  completionBlock(nil, result.error);
                              }
                              else
                              {
                                  completionBlock(result.accessToken, result.error);
                              }
                          }];
       }

-   **步骤 3**：通过 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) 对象的 [MSUserPolicy accessCheck](https://msdn.microsoft.com/library/dn790789.aspx) 方法，检查此用户对于该内容是否具有 Edit 权限。

        - (void)accessCheckWithProtectedData:(MSProtectedData *)protectedData
        {
            //check if user has edit rights and apply enforcements
            if (!protectedData.userPolicy.accessCheck(EditableDocumentRights.Edit))
            {
                // enforce on the UI
                textEditor.focusableInTouchMode = NO;
                textEditor.focusable = NO;
                textEditor.enabled = NO;
            }
        }

### <a name="scenario-create-a-new-protected-file-using-a-template"></a>方案：使用模板创建新的受保护文件

此方案首先获取模板列表 [MSTemplateDescriptor](https://msdn.microsoft.com/library/dn790785.aspx)，再选择第一个模板以创建策略，然后创建和写入新的受保护文件。

-   **步骤 1**：获取模板列表

        + (void)templateListUsageWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSTemplateDescriptor templateListWithUserId:@"user@domain.com"
                            authenticationCallback:authenticationCallback
                                   completionBlock:^(NSArray/*MSTemplateDescriptor*/ *templates, NSError *error)
                                   {
                                     // use templates array of MSTemplateDescriptor (Note: will be nil on error)
                                   }];
        }

-   **步骤 2**：使用列表中的第一个模板创建 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)。

        + (void)userPolicyCreationFromTemplateWithAuthenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            [MSUserPolicy userPolicyWithTemplateDescriptor:[templates objectAtIndex:0]
                                            userId:@"user@domain.com"
                                     signedAppData:nil
                            authenticationCallback:authenticationCallback
                                           options:None
                                   completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
            // use userPolicy (Note: will be nil on error)
            }];
        }

-   **步骤 3**：创建 [MSMutableProtectedData](https://msdn.microsoft.com/library/dn758325.aspx) 并向其中写入内容。

        + (void)createPtxtWithUserPolicy:(MSUserPolicy *)userPolicy contentToProtect:(NSData *)contentToProtect
        {
            // create an MSMutableProtectedData to write content
            [contentToProtect protectedDataInFile:filePath
                        originalFileExtension:kDefaultTextFileExtension
                               withUserPolicy:userPolicy
                              completionBlock:^(MSMutableProtectedData *data, NSError *error)
            {
             // use data (Note: will be nil on error)
            }];
        }

### <a name="scenario-open-a-custom-protected-file"></a>方案：打开自定义受保护的文件


-   **步骤 1**：通过 *serializedContentPolicy* 创建 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)。

        + (void)userPolicyWith:(NSData *)protectedData
        authenticationCallback:(id<MSAuthenticationCallback>)authenticationCallback
        {
            // Read header information from protectedData and extract the  PL
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger serializedPolicySize;
            NSMutableData *serializedPolicy;
            [protectedData getBytes:&serializedPolicySize length:sizeof(serializedPolicySize)];
            [protectedData getBytes:[serializedPolicy mutableBytes] length:serializedPolicySize];

            // Get the user policy , this is an async method as it hits the REST service
            // for content key and usage restrictions
            // userId provided as a hint for authentication
            [MSUserPolicy userPolicyWithSerializedPolicy:serializedPolicy
                                              userId:@"user@domain.com"
                              authenticationCallback:authenticationCallback
                                             options:Default
                                     completionBlock:^(MSUserPolicy *userPolicy,
                                                       NSError *error)
            {

            }];
         }

-   **步骤 2**：使用**步骤 1** 中的 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx) 创建 [MSCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx)，并从中读取信息。

        + (void)customProtectedDataWith:(NSData *)protectedData
        {
            // Read header information from protectedData and extract the  protectedContentSize
            /*-------------------------------------------
            | PL length | PL | ContetSizeLength |
            -------------------------------------------*/
            NSUInteger protectedContentSize;
            [protectedData getBytes:&protectedContentSize
                         length:sizeof(protectedContentSize)];

            // Create the MSCustomProtector used for decrypting the content
            // The content start position is the header length
            [MSCustomProtectedData customProtectedDataWithPolicy:userPolicy
                                               protectedData:protectedData
                                        contentStartPosition:sizeof(NSUInteger) + serializedPolicySize
                                                 contentSize:protectedContentSize
                                             completionBlock:^(MSCustomProtectedData *customProtector,
                                                               NSError *error)
            {
             //Read the content from the custom protector, this will decrypt the data
             NSData *content = [customProtector retrieveData];
             NSLog(@"%@", content);
            }];
         }

### <a name="scenario-create-a-custom-protected-file-using-a-custom-ad-hoc-policy"></a>方案：使用自定义（临时）策略创建自定义受保护的文件


-   **步骤 1**：在用户提供了电子邮件地址的情况下，创建策略描述符。

    **说明**：实际上，会使用来自设备接口的用户输入创建以下对象；[MSUserRights](https://msdn.microsoft.com/library/dn790811.aspx) 和 [MSPolicyDescriptor](https://msdn.microsoft.com/library/dn758339.aspx)。

        + (void)policyDescriptor
        {
            MSUserRights *userRights = [[MSUserRights alloc] initWithUsers:[NSArray arrayWithObjects: @"user1@domain.com", @"user2@domain.com", nil] rights:[MSEmailRights all]];

            MSPolicyDescriptor *policyDescriptor = [[MSPolicyDescriptor alloc] initWithUserRights:[NSArray arrayWithObjects:userRights, nil]];
            policyDescriptor.contentValidUntil = [[NSDate alloc] initWithTimeIntervalSinceNow:NSTimeIntervalSince1970 + 3600.0];
            policyDescriptor.offlineCacheLifetimeInDays = 10;
        }

-   **步骤 2**：通过策略描述符 *selectedDescriptor* 创建自定义 [MSUserPolicy](https://msdn.microsoft.com/library/dn790796.aspx)。

        + (void)userPolicyWithPolicyDescriptor:(MSPolicyDescriptor *)policyDescriptor
        {
            [MSUserPolicy userPolicyWithPolicyDescriptor:policyDescriptor
                                          userId:@"user@domain.com"
                          authenticationCallback:authenticationCallback
                                         options:None
                                 completionBlock:^(MSUserPolicy *userPolicy, NSError *error)
            {
              // use userPolicy (Note: will be nil on error)
            }];
        }

-   **步骤 3**：创建 [MSMutableCustomProtectedData](https://msdn.microsoft.com/library/dn758321.aspx) 并向其写入内容，然后关闭。

        + (void)mutableCustomProtectedData:(NSMutableData *)backingData policy:(MSUserPolicy *)policy contentToProtect:(NSString *)contentToProtect
        {
            //Get the serializedPolicy from a given policy
            NSData *serializedPolicy = [policy serializedPolicy];

            // Write header information to backing data including the PL
            // ------------------------------------
            // | PL length | PL | ContetSizeLength |
            // -------------------------------------
            NSUInteger serializedPolicyLength = [serializedPolicy length];
            [backingData appendData:[NSData dataWithBytes:&serializedPolicyLength length:sizeof(serializedPolicyLength)]];
            [backingData appendData:serializedPolicy];
            NSUInteger protectedContentLength = [MSCustomProtectedData getEncryptedContentLengthWithPolicy:policy contentLength:unprotectedData.length];
            [backingData appendData:[NSData dataWithBytes:&protectedContentLength length:sizeof(protectedContentLength)]];

            NSUInteger headerLength = sizeof(serializedPolicyLength) + serializedPolicyLength + sizeof(protectedContentLength);

            // Create the MSMutableCustomProtector used for encrypting content
            // The content start position is the current length of the backing data
            // The encryptedContentSize content size is 0 since there is no content yet
            [MSMutableCustomProtectedData customProtectorWithUserPolicy:policy
                                                        backingData:backingData
                                             protectedContentOffset:headerLength
                                                    completionBlock:^(MSMutableCustomProtectedData *customProtector,
                                                                      NSError *error)
            {
                //Append data to the custom protector, this will encrypt the data and write it to the backing data
                [customProtector appendData:[contentToProtect dataUsingEncoding:NSUTF8StringEncoding] error:&error];

                //close the custom protector so it will flush and finalise encryption
                [customProtector close:&error];

            }];
          }
