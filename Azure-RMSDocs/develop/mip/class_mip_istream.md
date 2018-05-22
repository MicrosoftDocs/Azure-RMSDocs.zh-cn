# <a name="class-mipistream"></a>class mip::IStream 
受保护的流的 Base 接口。
从 Windows::Storage::Streams::IRandomAccessStream::IRandomAccessStream 和 Windows::Storage::Streams::FileRandomAccessStream::FileRandomAccessStream 转网。 [https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx)[https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx](https://msdn.microsoft.com/en-us/library/windows/apps/windows.storage.streams.filerandomaccessstream.aspx)
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public std::shared_future<int64_t> ReadAsync(uint8_t* pbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  以异步方式从流读取数据块。
public std::shared_future<int64_t> WriteAsync(const uint8_t* cpbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  以异步方式将数据块写入流。
public std::future<bool> FlushAsync(std::launch launchType)  |  以异步方式刷新输出流缓冲区。
 public int64_t Read(uint8_t* pbBuffer, int64_t cbBuffer)  |  以同步方式从流读取数据块。
 public int64_t Write(const uint8_t* cpbBuffer, int64_t cbBuffer)  |  以同步方式将数据块写入流。
 public bool Flush()  |  以同步方式刷新输出流缓冲区。
 public SharedStream Clone()  |  克隆流。
 public void Seek(uint64_t u64Position)  |  查找流中的位置。
 public bool CanRead() const  |  获取流是否可读的指示。
 public bool CanWrite() const  |  获取流是否可写入的指示。
 public uint64_t Position()  |  获取流相对于开始位置的当前位置（以字节为单位）
 public uint64_t Size()  |  获取流的大小（以字节为单位）
 public void Size(uint64_t u64Value)  |  设置流的大小（以字节为单位）
public virtual std::vector<uint8_t> Read(uint64_t u64size)  |  以同步方式从流读取数据块。
  
## <a name="members"></a>成員
  
### <a name="readasync"></a>ReadAsync
以异步方式从流读取数据块。

参数：  
* **pbBuffer**：应读入流的缓冲区 


* **cbBuffer**：缓冲区的大小 


* **cbOffset**：相对于输入流开始位置（即应开始读取的位置）的偏移量 


* **launchType**：异步启动类型



  
**返回结果**：包含实际读取字节数的 Async future，确保缓冲区始终存在，直到从 std::future 中检索到结果
  
### <a name="writeasync"></a>WriteAsync
以异步方式将数据块写入流。

参数：  
* **cpbBuffer**：要写入的数据缓冲区 


* **cbBuffer**：缓冲区的大小 


* **cbOffset**：相对于输出流开始位置（即应开始写入的位置）的偏移量 


* **launchType**：异步启动类型



  
**返回结果**：包含实际写入字节数的 Async future，确保缓冲区始终存在，直到从 std::future 中检索到结果
  
### <a name="flushasync"></a>FlushAsync
以异步方式刷新输出流缓冲区。

参数：  
* **launchType**：异步启动类型



  
**返回结果**：包含刷新是否成功的指示的 Async future
  
### <a name="read"></a>读取
以同步方式从流读取数据块。

参数：  
* **pbBuffer**：应读入流的缓冲区 


* **cbBuffer**：缓冲区的大小



  
**返回结果**：读取的实际字节数
  
### <a name="write"></a>写入
以同步方式将数据块写入流。

参数：  
* **cpbBuffer**：要写入的数据缓冲区 


* **cbBuffer**：缓冲区的大小



  
**返回结果**：写入的实际字节数
  
### <a name="flush"></a>刷新
以同步方式刷新输出流缓冲区。

  
**返回结果**：刷新是否成功
  
### <a name="sharedstream"></a>SharedStream
克隆流。

  
**返回结果**：克隆的流
  
### <a name="seek"></a>Seek
查找流中的位置。

参数：  
* **u64Position**：相对于流开始位置的字节偏移量


  
### <a name="canread"></a>CanRead
获取流是否可读的指示。

  
**返回结果**：流是否可读
  
### <a name="canwrite"></a>CanWrite
获取流是否可写入的指示。

  
**返回结果**：流是否可写入
  
### <a name="position"></a>位置
获取流相对于开始位置的当前位置（以字节为单位）

  
**返回结果**：流相对于开始位置的当前位置（以字节为单位）
  
### <a name="size"></a>大小
获取流的大小（以字节为单位）

  
**返回结果**：流的大小（以字节为单位）
  
### <a name="size"></a>大小
设置流的大小（以字节为单位）

参数：  
* **u64Value**：流的大小（以字节为单位）


  
### <a name="read"></a>读取
以同步方式从流读取数据块。

参数：  
* **u64size**：要读取的数据大小（以字节为单位）



  
**返回结果**：实际读取数据的矢量