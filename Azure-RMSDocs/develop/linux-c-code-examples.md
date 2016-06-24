---
# required metadata

title: Linux 代码示例 | Azure RMS
description: 本主题向你介绍 Linux 版 RMS SDK 的重要方案和代码元素。
keywords:
author: bruceperlerms
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: azure
ms.service: rights-management
ms.technology: techgroup-identity
ms.assetid: 0F7714CA-1D3E-4846-B187-739825B7DE26
# optional metadata

#ROBOTS:
audience: developer
#ms.devlang:
ms.reviewer: shubhamp
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Linux 代码示例

本主题向你介绍 Linux 版 RMS SDK 的重要方案和代码元素。

以下代码片段取自示例应用程序 *rms\_sample* 和 *rmsauth\_sample*。 相关详细信息，请参阅 GitHub 存储库中的[示例](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples)。

## 方案，通过受保护的文件访问保护策略信息

**打开并读取 RMS 保护的文件**
**源**：[rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：在从用户处获取文件名后，读取证书（参见 *MainWindow::addCertificates*），使用客户端 ID 和重定向 URL 设置身份验证回调，调用 *ConvertFromPFile*（参见以下代码示例），然后读取保护策略名称、说明和内容有效性日期。

**C++**：

    void MainWindow::ConvertFromPFILE(const string&amp; fileIn,
        const string&amp; clientId,
        const string&amp; redirectUrl,
        const string&amp; clientEmail) 
    {
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    string fileOut;
    
    // generate output filename
    auto pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
     fileOut = fileIn.substr(0, pos);
    }
    
     // create streams
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!outFile-&gt;is_open()) {
     AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
     return;
      }
    
    try
    {
    // create authentication context
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    auto pfs = PFileConverter::ConvertFromPFile(
      clientEmail,
      inFile,
      outFile,
      auth,
      this-&gt;consent);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e)
    {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }

**创建受保护的文件流**
**源**[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：此方法通过 SDK 方法 *ProtectedFileStream::Aquire* 从传入的回溯流中创建受保护的文件流，该流随后返回到调用方。

**C++**：

    shared_ptr&lt;GetProtectedFileStreamResult&gt;PFileConverter::ConvertFromPFile(
    const string           &amp; userId,
    shared_ptr&lt;istream&gt;      inStream,
    shared_ptr&lt;iostream&gt;     outStream,
    IAuthenticationCallback&amp; auth,
    IConsentCallback       &amp; consent)
    {
    auto inIStream = rmscrypto::api::CreateStreamFromStdStream(inStream);
    
    auto fsResult = ProtectedFileStream::Acquire(
    inIStream,
    userId,
    auth,
    consent,
    POL_None,
    static_cast&lt;ResponseCacheFlags&gt;(RESPONSE_CACHE_INMEMORY
                                    | RESPONSE_CACHE_ONDISK));
    
    if ((fsResult.get() != nullptr) &amp;&amp; (fsResult-&gt;m_status == Success) &amp;&amp;
      (fsResult-&gt;m_stream != nullptr)) {
    auto pfs = fsResult-&gt;m_stream;
    
    // preparing
    readPosition  = 0;
    writePosition = 0;
    totalSize     = pfs-&gt;Size();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    }
      return fsResult;
    }

## 方案：使用模板创建新的受保护文件

**使用用户所选模板来保护文件**
**源**：[rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：在从用户处获取文件名，读取证书（参见 *MainWindow::addCertificates*）并使用客户端 ID 和重定向 URL 设置身份验证回调之后，所选文件将通过调用 *ConvertToPFileTemplates* 进行保护（参见下方代码示例）。

**C++**：

    void MainWindow::ConvertToPFILEUsingTemplates(const string&amp; fileIn,
                                              const string&amp; clientId,
                                              const string&amp; redirectUrl,
                                              const string&amp; clientEmail) 
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFileTemplates(
      clientEmail, inFile, fileExt, outFile, auth,
      this-&gt;consent, this-&gt;templates);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
   catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**使用从模板中创建的策略来保护文件**
**源**[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：提取与用户关联的模板列表，随后使用所选模板创建转而用于保护文件的策略。

**C++**：

    void PFileConverter::ConvertToPFileTemplates(const string           &amp; userId,
                                             shared_ptr&lt;istream&gt;      inStream,
                                             const string           &amp; fileExt,
                                             std::shared_ptr&lt;iostream&gt;outStream,
                                             IAuthenticationCallback&amp; auth,
                                             IConsentCallback&amp; /*consent*/,
                                             ITemplatesCallback     &amp; templ)
    {
    auto templates = TemplateDescriptor::GetTemplateList(userId, auth);
    
    rmscore::modernapi::AppDataHashMap signedData;
    
    size_t pos = templ.SelectTemplate(templates);
    
    if (pos &lt; templates.size()) {
    auto policy = UserPolicy::CreateFromTemplateDescriptor(
      templates[pos],
      userId,
      auth,
      USER_AllowAuditedExtraction,
      signedData);
   
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    }
    }

**在给定策略的情况下保护文件**
**源**[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：使用给定策略创建受保护的文件流，然后保护此文件。

**C++**：

    void PFileConverter::ConvertToPFileUsingPolicy(shared_ptr&lt;UserPolicy&gt;   policy,
                                               shared_ptr&lt;istream&gt;      inStream,
                                               const string           &amp; fileExt,
                                               std::shared_ptr&lt;iostream&gt;outStream)
    {
    if (policy.get() != nullptr) {
    auto outIStream = rmscrypto::api::CreateStreamFromStdStream(outStream);
    auto pStream    = ProtectedFileStream::Create(policy, outIStream, fileExt);
    
    // preparing
    readPosition  = 0;
    writePosition = pStream-&gt;Size();
    
    inStream-&gt;seekg(0, ios::end);
    totalSize = inStream-&gt;tellg();
    
    // start threads
    for (size_t i = 0; i &lt; THREADS_NUM; ++i) {
      threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(inStream),
                                  pStream,
                                  true));
    }
    
    for (thread&amp; t: threadPool) {
      if (t.joinable()) {
        t.join();
      }
    }
    
    pStream-&gt;Flush();
    }
    


## 方案：使用自定义保护来保护文件

**使用自定义保护来保护文件**
**源**：[rms\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：在从用户处获取文件名，读取证书（参见 *MainWindow::addCertificates*），从用户处收集权限信息，并使用客户端 ID 和重定向 URL 设置身份验证回调之后，所选文件将通过调用 *ConvertToPFilePredefinedRights* 进行保护（参见下方代码示例）。

**C++**：

    void MainWindow::ConvertToPFILEUsingRights(const string            &amp; fileIn,
                                           const vector&lt;UserRights&gt;&amp; userRights,
                                           const string            &amp; clientId,
                                           const string            &amp; redirectUrl,
                                           const string            &amp; clientEmail)
    {
    // generate output filename
    string fileOut = fileIn + &quot;.pfile&quot;;
    
    // add trusted certificates using HttpHelpers of RMS and Auth SDKs
    addCertificates();
    
    // create shared in/out streams
    auto inFile = make_shared&lt;ifstream&gt;(
    fileIn, ios_base::in | ios_base::binary);
    auto outFile = make_shared&lt;fstream&gt;(
    fileOut, ios_base::in | ios_base::out | ios_base::trunc | ios_base::binary);
    
    if (!inFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileIn.c_str());
    return;
    }
    
    if (!outFile-&gt;is_open()) {
    AddLog(&quot;ERROR: Failed to open &quot;, fileOut.c_str());
    return;
    }
    
    // find file extension
    string fileExt;
    auto   pos = fileIn.find_last_of(&#39;.&#39;);
    
    if (pos != string::npos) {
    fileExt = fileIn.substr(pos);
    }
    
    // is anything to add
    if (userRights.size() == 0) {
    AddLog(&quot;ERROR: &quot;, &quot;Please fill email and check rights&quot;);
    return;
    }
    
    
    try {
    // create authentication callback
    AuthCallback auth(clientId, redirectUrl);
    
    // process convertion
    PFileConverter::ConvertToPFilePredefinedRights(
      clientEmail,
      inFile,
      fileExt,
      outFile,
      auth,
      this-&gt;consent,
      userRights);
    
    AddLog(&quot;Successfully converted to &quot;, fileOut.c_str());
    }
    catch (const rmsauth::Exception&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.error().c_str());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    catch (const rmscore::exceptions::RMSException&amp; e) {
    AddLog(&quot;ERROR: &quot;, e.what());
    
    outFile-&gt;close();
    remove(fileOut.c_str());
    }
    inFile-&gt;close();
    outFile-&gt;close();
    }


**创建保护策略，授予用户所选权限**
**源**[rms\_sample/pfileconverter.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rms_sample)

**说明**：创建策略描述符并填充用户的权限信息，然后使用策略描述符来创建用户策略。 此策略可通过调用 *ConvertToPFileUsingPolicy* 来保护所选文件（参见本主题上一部分中的所述内容）。

**C++**：

    void PFileConverter::ConvertToPFilePredefinedRights(
    const string            &amp; userId,
    shared_ptr&lt;istream&gt;       inStream,
    const string            &amp; fileExt,
    shared_ptr&lt;iostream&gt;      outStream,
    IAuthenticationCallback &amp; auth,
    IConsentCallback&amp; /*consent*/,
    const vector&lt;UserRights&gt;&amp; userRights)
    {
    auto endValidation = chrono::system_clock::now() + chrono::hours(48);
    
    
    PolicyDescriptor desc(userRights);
    
    desc.Referrer(make_shared&lt;string&gt;(&quot;https://client.test.app&quot;));
    desc.ContentValidUntil(endValidation);
    desc.AllowOfflineAccess(false);
    desc.Name(&quot;Test Name&quot;);
    desc.Description(&quot;Test Description&quot;);
    
    auto policy = UserPolicy::Create(desc, userId, auth,
                                   USER_AllowAuditedExtraction);
    ConvertToPFileUsingPolicy(policy, inStream, fileExt, outStream);
    

## WorkerThread - 一种支持方法


*WorkerThread()* 方法由先前的两个示例方案（“创建受保护的文件流”和“在给定策略的情况下保护文件”）按以下方式进行调用：

**C++**：

    threadPool.push_back(thread(WorkerThread,
                                  static_pointer_cast&lt;iostream&gt;(outStream), pfs,
                                  false));


**支持方法 WorkerThread()**

**C++**：

    static mutex   threadLocker;
    static int64_t totalSize     = 0;
    static int64_t readPosition  = 0;
    static int64_t writePosition = 0;
    static vector&lt;thread&gt; threadPool;
    
    static void WorkerThread(shared_ptr&lt;iostream&gt;           stdStream,
                         shared_ptr&lt;ProtectedFileStream&gt;pStream,
                         bool                           modeWrite) {
    vector&lt;uint8_t&gt; buffer(4096);
    int64_t bufferSize = static_cast&lt;int64_t&gt;(buffer.size());
    
    while (totalSize - readPosition &gt; 0) {
    // lock
    threadLocker.lock();
    
    // check remain
    if (totalSize - readPosition &lt;= 0) {
      threadLocker.unlock();
      return;
    }
    
    // get read/write offset
    int64_t offsetRead  = readPosition;
    int64_t offsetWrite = writePosition;
    int64_t toProcess   = min(bufferSize, totalSize - readPosition);
    readPosition  += toProcess;
    writePosition += toProcess;
    
    // no need to lock more
    threadLocker.unlock();
    
    if (modeWrite) {
      // stdStream is not thread safe!!!
      try {
        threadLocker.lock();
    
        stdStream-&gt;seekg(offsetRead);
        stdStream-&gt;read(reinterpret_cast&lt;char *&gt;(&amp;buffer[0]), toProcess);
        threadLocker.unlock();
        auto written =
          pStream-&gt;WriteAsync(
            buffer.data(), toProcess, offsetWrite, std::launch::deferred).get();
    
        if (written != toProcess) {
          throw rmscore::exceptions::RMSStreamException(&quot;Error while writing data&quot;);
        }
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    } else {
      auto read =
        pStream-&gt;ReadAsync(&amp;buffer[0],
                           toProcess,
                           offsetRead,
                           std::launch::deferred).get();
    
      if (read == 0) {
        break;
      }
    
      try {
        // stdStream is not thread safe!!!
        threadLocker.lock();
    
        // seek to write
        stdStream-&gt;seekp(offsetWrite);
        stdStream-&gt;write(reinterpret_cast&lt;const char *&gt;(buffer.data()), read);
        threadLocker.unlock();
      }
      catch (exception&amp; e) {
        qDebug() &lt;&lt; &quot;Exception: &quot; &lt;&lt; e.what();
      }
    }
    }
    }


## 方案：RMS 身份验证

以下示例展示了两种不同的身份验证方法，即在使用 UI 和不使用 UI 的情况下获取 Azure 身份验证 oAuth2 令牌。
**通过 UI 获取 oAuth2 身份验证令牌**
**源**[rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**步骤 1**：创建 **rmsauth::FileCache** 对象的共享点。
说明：可设置缓存路径或使用默认路径。

**C++**：

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**步骤 2**：创建 **rmsauth::AuthenticationContext** 对象
说明：指定*机构 URI* 和 *FileCache* 对象。

**C++**：

    AuthenticationContext authContext(
                              std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                              AuthorityValidationType::False,
                              FileCachePtr);


**步骤 3**：调用 **authContext** 对象的 **aquireToken** 方法，并指定下述参数：
描述:

-   *请求资源* - 想要访问的受保护资源
-   *客户端唯一 ID* - 通常为 GUID
-   *重定向 URI* - 在提取身份验证令牌后重新寻址的 URI
-   *身份验证提示行为* - 若设置 **PromptBehavior::Auto**，则库将尝试使用缓存并在必要时刷新令牌
-   *用户 ID*：提示窗口中显示的用户名

**C++**：

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                std::string(“https://client.test.app”),
                PromptBehavior::Auto,
                std::string(“john.smith@msopentechtest01.onmicrosoft.com”));


**步骤 4**：从结果中获取访问令牌
说明：调用 **result-&gt; accessToken()** 方法

**注意** 任何身份验证库方法都可能引发 **rmsauth::Exception**

 
**在不使用 UI 的情况下获取 oAuth2 身份验证令牌**
**源**[rmsauth\_sample/mainwindow.cpp](https://github.com/AzureAD/rms-sdk-for-cpp/tree/master/samples/rmsauth_sample)

**步骤 1**：创建 **rmsauth::FileCache** 对象的共享点
说明：可设置缓存路径或使用默认路径

**C++**：

    auto FileCachePtr = std::make_shared&lt; rmsauth::FileCache&gt;();


**步骤 2**：创建 **UserCredential** 对象
说明：指定*用户登录名*和*密码*

**C++**：

    auto userCred = std::make_shared&lt;UserCredential&gt;(&quot;john.smith@msopentechtest01.onmicrosoft.com&quot;,
                                                 &quot;SomePass&quot;);


**步骤 3**：创建 **rmsauth::AuthenticationContext** 对象
说明：指定机构 *URI* 和 *FileCache* 对象

**C++**：

    AuthenticationContext authContext(
                        std::string(“https://sts.aadrm.com/_sts/oauth/authorize”),
                        AuthorityValidationType::False,
                        FileCachePtr);


**步骤 4**：调用 **authContext** 的 **aquireToken** 方法，并指定下述参数：
-   *请求资源* - 想要访问的受保护资源
-   *客户端唯一 ID* - 通常为 GUID
-   *用户凭据* - 传递所创建的对象

**C++**：

    auto result = authContext.acquireToken(
                std::string(“api.aadrm.com”),
                std::string(“4a63455a-cfa1-4ac6-bd2e-0d046cf1c3f7”),
                userCred);


**步骤 5**：从结果中获取访问令牌
说明：调用 **result-&gt; accessToken()** 方法

**注意** 任何身份验证库方法都可能引发 **rmsauth::Exception**



<!--HONumber=Apr16_HO4-->


