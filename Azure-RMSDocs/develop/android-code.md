---
title: Android 代码示例 | Azure RMS
description: 本主题向你介绍 Android 版本的 RMS SDK 的重要代码元素。
keywords: ''
author: msmbaldwin
ms.author: mbaldwin
manager: barbkess
ms.date: 12/10/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: information-protection
ms.assetid: 58CC2E50-1E4D-4621-A947-25312C3FF519
audience: developer
ms.reviewer: shubhamp
ms.suite: ems
ms.openlocfilehash: 7ae70446b932d9f78c2dccc99b2f5727c2e9418e
ms.sourcegitcommit: fff4c155c52c9ff20bc4931d5ac20c3ea6e2ff9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2019
ms.locfileid: "60178879"
---
# <a name="android-code-examples"></a>Android 代码示例

本文介绍了如何为 Android 版 RMS SDK 编码元素。

**注意：** 在本文中，MSIPC (Microsoft Information Protection and Control) 一词是指客户端流程。


## <a name="using-the-microsoft-rights-management-sdk-42---key-scenarios"></a>使用 Microsoft Rights Management SDK 4.2 - 重要方案

这些代码示例摘自较大的示例应用，即对熟悉此 SDK 十分重要的开发方案。 它们展示了如何使用以下对象：

- Microsoft 受保护的文件格式（亦称为“受保护的文件”。
- 自定义受保护的文件格式
- 自定义用户界面 (UI) 控件

MSIPCSampleApp 示例应用可与适用于 Android 操作系统的此 SDK 配合使用。 若要了解详细信息，请参阅 [rms-sdk-ui-for-android](https://github.com/AzureAD/rms-sdk-ui-for-android)。

### <a name="scenario-consume-an-rms-protected-file"></a>方案：使用受 RMS 保护的文件

- **步骤 1**：创建 [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx)。

    **源**：*MsipcAuthenticationCallback.java*

    **说明**：实例化 [ProtectedFileInputStream](https://msdn.microsoft.com/library/dn790851.aspx) 对象，并实现服务身份验证。  使用 [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758250.aspx) 获取令牌，具体是通过将 AuthenticationRequestCallback 实例作为参数 mRmsAuthCallback 传递到 MSIPC API。 请参阅以下示例代码节结尾附近的 [ProtectedFileInputStream.create](https://msdn.microsoft.com/library/dn790851.aspx) 调用。

    ``` java
        public void startContentConsumptionFromPtxtFileFormat(InputStream inputStream)
        {
            CreationCallback<ProtectedFileInputStream> protectedFileInputStreamCreationCallback =
              new CreationCallback<ProtectedFileInputStream>()
            {
                @Override
                public Context getContext()
                {
                   …
               }

                @Override
                public void onCancel()
                {
                   …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                   …
                }

                @Override
                public void onSuccess(ProtectedFileInputStream protectedFileInputStream)
                {
                   …
                   …
                    byte[] dataChunk = new byte[16384];
                    try
                    {
                        while ((nRead = protectedFileInputStream.read(dataChunk, 0,
                                dataChunk.length)) != -1)
                        {
                            …
                        }
                         …
                        protectedFileInputStream.close();
                    }
                    catch (IOException e)
                    {
                      …
                    }  
              }
            };
            try
            {
               …
                ProtectedFileInputStream.create(inputStream, null, mRmsAuthCallback,
                                                PolicyAcquisitionFlags.NONE,
                                                protectedFileInputStreamCreationCallback);
            }
            catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
            {
                …
            }
        }
    ```

- **步骤 2**：使用 Active Directory 身份验证库 (ADAL) 设置身份验证。

    **源**：*MsipcAuthenticationCallback.java*。

    **说明**：此步骤中需要使用 ADAL 来实现具有示例身份验证参数的 [AuthenticationRequestCallback](https://msdn.microsoft.com/library/dn758255.aspx)。 若要了解详细信息，请参阅 [Azure AD Authentication Library (ADAL)](https://msdn.microsoft.com/library/jj573266.aspx)。


~~~
``` java
    class MsipcAuthenticationCallback implements AuthenticationRequestCallback
    {

    …

    @Override
    public void getToken(Map<String, String> authenticationParametersMap,
                         final AuthenticationCompletionCallback authenticationCompletionCallbackToMsipc)
    {
        String authority = authenticationParametersMap.get("oauth2.authority");
        String resource = authenticationParametersMap.get("oauth2.resource");
        String userId = authenticationParametersMap.get("userId");
        final String userHint = (userId == null)? "" : userId;
        AuthenticationContext authenticationContext = App.getInstance().getAuthenticationContext();
        if (authenticationContext == null || !authenticationContext.getAuthority().equalsIgnoreCase(authority))
        {
            try
            {
                authenticationContext = new AuthenticationContext(App.getInstance().getApplicationContext(), authority, …);
                App.getInstance().setAuthenticationContext(authenticationContext);
            }
            catch (NoSuchAlgorithmException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
            catch (NoSuchPaddingException e)
            {
                …
                authenticationCompletionCallbackToMsipc.onFailure();
            }
       }
        App.getInstance().getAuthenticationContext().acquireToken(mParentActivity, resource, mClientId, mRedirectURI, userId, mPromptBehavior,
                       "&USERNAME=" + userHint, new AuthenticationCallback<AuthenticationResult>()
                        {
                            @Override
                            public void onError(Exception exc)
                            {
                                …
                                if (exc instanceof AuthenticationCancelError)
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onCancel();
                                }
                                else
                                {
                                     …
                                    authenticationCompletionCallbackToMsipc.onFailure();
                                }
                            }

                            @Override
                            public void onSuccess(AuthenticationResult result)
                            {
                                …
                                if (result == null || result.getAccessToken() == null
                                        || result.getAccessToken().isEmpty())
                                {
                                     …
                                }
                                else
                                {
                                    // request is successful
                                    …
                                    authenticationCompletionCallbackToMsipc.onSuccess(result.getAccessToken());
                                }
                            }
                        }

                        );
                  }
```
~~~

- **步骤 3**：通过 [UserPolicy.accessCheck](https://msdn.microsoft.com/library/dn790885.aspx) 方法检查此用户对于此内容是否具有 Edit 权限。

    **源**：*TextEditorFragment.java*

    ``` java
         //check if user has edit rights and apply enforcements
                if (!mUserPolicy.accessCheck(EditableDocumentRights.Edit))
                {
                    mTextEditor.setFocusableInTouchMode(false);
                    mTextEditor.setFocusable(false);
                    mTextEditor.setEnabled(false);
                    …
                }
    ```


### <a name="scenario-create-a-new-protected-file-using-a-template"></a>方案：使用模板创建新的受保护文件

此方案首先获取模板列表，选择第一个模板以创建策略，然后创建并写入新的受保护的文件。

- **步骤 1**：通过 [TemplateDescriptor](https://msdn.microsoft.com/library/dn790871.aspx) 对象获取模板列表。

    **源**：*MsipcTaskFragment.java*

    ``` java
    CreationCallback<List<TemplateDescriptor>> getTemplatesCreationCallback = new CreationCallback<List<TemplateDescriptor>>()
      {
          @Override
          public Context getContext()
          {
              …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(List<TemplateDescriptor> templateDescriptors)
          {
             …
          }
      };
      try
      {
              …
          mIAsyncControl = TemplateDescriptor.getTemplates(emailId, mRmsAuthCallback, getTemplatesCreationCallback);
      }
      catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
      {
              …
      }
    ```

- **步骤 2**：使用列表中的第一个模板创建 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx)。

    **源**：*MsipcTaskFragment.java*

    ``` java
      CreationCallback<UserPolicy> userPolicyCreationCallback = new CreationCallback<UserPolicy>()
      {
          @Override
          public Context getContext()
          {
              …
          }

          @Override
          public void onCancel()
          {
              …
          }

          @Override
          public void onFailure(ProtectionException e)
          {
              …
          }

          @Override
          public void onSuccess(final UserPolicy item)
          {
              …
          }
      };
      try
      {
           …
          mIAsyncControl = UserPolicy.create((TemplateDescriptor)selectedDescriptor, mEmailId, mRmsAuthCallback,
                            UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
           …
      }
      catch (InvalidParameterException e)
      {
              …
      }
    ```

-  **步骤 3**：创建 [ProtectedFileOutputStream](https://msdn.microsoft.com/library/dn790855.aspx) 并向其中写入内容。

    **源**：*MsipcTaskFragment.java*

    ``` java
    private void createPTxt(final byte[] contentToProtect)
        {
             …
            CreationCallback<ProtectedFileOutputStream> protectedFileOutputStreamCreationCallback = new CreationCallback<ProtectedFileOutputStream>()
            {
                @Override
                public Context getContext()
                {
                 …
                }

                @Override
                public void onCancel()
                {
                 …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                 …
                }

                @Override
                public void onSuccess(ProtectedFileOutputStream protectedFileOutputStream)
                {
                    try
                    {
                        // write to this stream
                        protectedFileOutputStream.write(contentToProtect);
                        protectedFileOutputStream.flush();
                        protectedFileOutputStream.close();
                        …
                    }
                    catch (IOException e)
                    {
                        …
                    }
                }
            };
            try
            {
                File file = new File(filePath);
                outputStream = new FileOutputStream(file);
                mIAsyncControl = ProtectedFileOutputStream.create(outputStream, mUserPolicy, originalFileExtension,
                        protectedFileOutputStreamCreationCallback);
            }
            catch (FileNotFoundException e)
            {
                 …
            }
            catch (InvalidParameterException e)
            {
                 …
            }
        }
    ```


### <a name="scenario-open-a-custom-protected-file"></a>方案：打开自定义受保护的文件

- **步骤 1**：从 serializedContentPolicy 创建 [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx)。

    **源**：*MsipcTaskFragment.java*

    ``` java
    CreationCallback<UserPolicy> userPolicyCreationCallbackFromSerializedContentPolicy = new CreationCallback<UserPolicy>()
            {
                @Override
                public void onSuccess(UserPolicy userPolicy)
                {
                  …
                }

                @Override
                public void onFailure(ProtectionException e)
                {
                  …
                }

                @Override
                public void onCancel()
                {
                  …
                }

                @Override
                public Context getContext()
                {
                  …
                }
            };


~~~
try
{
  ...

  // Read the serializedContentPolicyLength from the inputStream.
  long serializedContentPolicyLength = readUnsignedInt(inputStream);

  // Read the PL bytes from the input stream using the PL size.
  byte[] serializedContentPolicy = new byte[(int)serializedContentPolicyLength];
  inputStream.read(serializedContentPolicy);

  ...

  UserPolicy.acquire(serializedContentPolicy, null, mRmsAuthCallback, PolicyAcquisitionFlags.NONE,
          userPolicyCreationCallbackFromSerializedContentPolicy);
}
catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
{
  ...
}
catch (IOException e)
{
  ...
}
```
~~~


- **Step 2**: Create a [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) using the [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) from **Step 1**.

    **Source**: *MsipcTaskFragment.java*

    ``` java
      CreationCallback<CustomProtectedInputStream> customProtectedInputStreamCreationCallback = new CreationCallback<CustomProtectedInputStream>()
      {
         @Override
         public Context getContext()
         {
             …
         }

         @Override
         public void onCancel()
         {
             …
         }

         @Override
         public void onFailure(ProtectionException e)
         {
             …
         }

         @Override
         public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
         {
            …

             byte[] dataChunk = new byte[16384];
             try
             {
                 while ((nRead = customProtectedInputStream.read(dataChunk, 0, dataChunk.length)) != -1)
                 {
                      …
                 }
                  …
                 customProtectedInputStream.close();
             }
             catch (IOException e)
             {
                …
             }
             …
         }
     };

    try
    {
      ...

      // Retrieve the encrypted content size.
      long encryptedContentLength = readUnsignedInt(inputStream);

      updateTaskStatus(new TaskStatus(TaskState.Starting, "Consuming content", true));

      CustomProtectedInputStream.create(userPolicy, inputStream,
                                     encryptedContentLength,
                                     customProtectedInputStreamCreationCallback);
    }
    catch (com.microsoft.rightsmanagement.exceptions.InvalidParameterException e)
    {
      ...
    }
    catch (IOException e)
    {
      ...
    }
    ```

- **Step 3**: Read content from the [CustomProtectedInputStream](https://msdn.microsoft.com/library/dn758271.aspx) into *mDecryptedContent* then close.

    **Source**: *MsipcTaskFragment.java*

    ``` java
    @Override
    public void onSuccess(CustomProtectedInputStream customProtectedInputStream)
    {
      mUserPolicy = customProtectedInputStream.getUserPolicy();
      ByteArrayOutputStream buffer = new ByteArrayOutputStream();

      int nRead;                      
      byte[] dataChunk = new byte[16384];

      try
      {
        while ((nRead = customProtectedInputStream.read(dataChunk, 0,
                                                            dataChunk.length)) != -1)
        {
           buffer.write(dataChunk, 0, nRead);
        }

        buffer.flush();
        mDecryptedContent = new String(buffer.toByteArray(), Charset.forName("UTF-8"));

        buffer.close();
        customProtectedInputStream.close();
      }
      catch (IOException e)
      {
        ...
      }
    }
    ```

### Scenario: Create a custom protected file using a custom policy

- **Step 1**: With an email address provided by the user, create a policy descriptor.

    **Source**: *MsipcTaskFragment.java*

    **Description**: In practice, the following objects would be created by using user inputs from the device interface; [UserRights](https://msdn.microsoft.com/library/dn790911.aspx) and [PolicyDescriptor](https://msdn.microsoft.com/library/dn790843.aspx).

    ``` java
      // create userRights list
      UserRights userRights = new UserRights(Arrays.asList("consumer@domain.com"),
        Arrays.asList( CommonRights.View, EditableDocumentRights.Print));
      ArrayList<UserRights> usersRigthsList = new ArrayList<UserRights>();
      usersRigthsList.add(userRights);

      // Create PolicyDescriptor using userRights list
      PolicyDescriptor policyDescriptor = PolicyDescriptor.createPolicyDescriptorFromUserRights(
                                                             usersRigthsList);
      policyDescriptor.setOfflineCacheLifetimeInDays(10);
      policyDescriptor.setContentValidUntil(new Date());
    ```


- **Step 2**: Create a custom [UserPolicy](https://msdn.microsoft.com/library/dn790887.aspx) from the policy descriptor, *selectedDescriptor*.

    **Source**: *MsipcTaskFragment.java*

    ``` java
       mIAsyncControl = UserPolicy.create((PolicyDescriptor)selectedDescriptor,
         mEmailId, mRmsAuthCallback, UserPolicyCreationFlags.NONE, userPolicyCreationCallback);
    ```


- **Step 3**: Create and write content to the [CustomProtectedOutputStream](https://msdn.microsoft.com/library/dn758274.aspx) and then close.

    **Source**: *MsipcTaskFragment.java*

    ``` java
    File file = new File(filePath);
        final OutputStream outputStream = new FileOutputStream(file);
        CreationCallback<CustomProtectedOutputStream> customProtectedOutputStreamCreationCallback = new CreationCallback<CustomProtectedOutputStream>()
        {
            @Override
            public Context getContext()
            {
              …
            }

            @Override
            public void onCancel()
            {
              …
            }

            @Override
            public void onFailure(ProtectionException e)
            {
              …
            }

            @Override
            public void onSuccess(CustomProtectedOutputStream protectedOutputStream)
            {
                try
                {
                    // write serializedContentPolicy
                    byte[] serializedContentPolicy = mUserPolicy.getSerializedContentPolicy();
                    writeLongAsUnsignedIntToStream(outputStream, serializedContentPolicy.length);
                    outputStream.write(serializedContentPolicy);
                    // write encrypted content
                    if (contentToProtect != null)
                    {
                        writeLongAsUnsignedIntToStream(outputStream,
                                CustomProtectedOutputStream.getEncryptedContentLength(contentToProtect.length,
                                        protectedOutputStream.getUserPolicy()));
                        protectedOutputStream.write(contentToProtect);
                        protectedOutputStream.flush();
                        protectedOutputStream.close();
                    }
                    else
                    {
                        outputStream.flush();
                        outputStream.close();
                    }
                    …
                }
                catch (IOException e)
                {
                  …
                }
            }
        };
        try
        {
            mIAsyncControl = CustomProtectedOutputStream.create(outputStream, mUserPolicy,
                    customProtectedOutputStreamCreationCallback);
        }
        catch (InvalidParameterException e)
        {
          …
        }
    ```
