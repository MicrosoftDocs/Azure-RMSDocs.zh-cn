# <a name="class-mipcustomprotectedstream"></a>class mip::CustomProtectedStream 
包装一个流，以提供对读写的透明加密和解密。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public std::shared_future<int64_t> ReadAsync(uint8_t* pbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  以异步方式从流读取数据块。
public std::shared_future<int64_t> WriteAsync(const uint8_t* cpbBuffer, int64_t cbBuffer, int64_t cbOffset, std::launch launchType)  |  以异步方式将数据块写入流。
public std::future<bool> FlushAsync(std::launch launchType)  |  以异步方式刷新输出流缓冲区。
public int64_t Read(uint8_t* pbBuffer, int64_t cbBuffer)  |  以同步方式从流读取数据块。
public inline virtual std::vector<uint8_t> Read(uint64_t u64size)  |  以同步方式从流读取数据块。
public int64_t Write(const uint8_t* cpbBuffer, int64_t cbBuffer)  |  以同步方式将数据块写入流。
public bool Flush()  |  以同步方式刷新输出流缓冲区。
public SharedStream Clone()  |  克隆流。
public void Seek(uint64_t u64Position)  |  查找流中的位置。
public bool CanRead() const  |  获取流是否可读的指示。
public bool CanWrite() const  |  获取流是否可写入的指示。
public uint64_t Position()  |  获取流相对于开始位置的当前位置（以字节为单位）
public uint64_t Size()  |  获取流的大小（以字节为单位）
public void Size(uint64_t u64Value)  |  设置流的大小（以字节为单位）
  
## <a name="members"></a>成員
  
### <a name="readasync"></a>ReadAsync
以异步方式从流读取数据块。
  
#### <a name="parameters"></a>参数
* pbBuffer：应读入流的缓冲区 
* cbBuffer：缓冲区的大小 
* cbOffset：相对于输入流开始位置（即应开始读取的位置）的偏移量 
* launchType：异步启动类型
  
#### <a name="returns"></a>Returns
包含实际读取字节数的 Async future，确保缓冲区始终存在，直到从 std::future 中检索到结果
  
### <a name="writeasync"></a>WriteAsync
以异步方式将数据块写入流。
  
#### <a name="parameters"></a>参数
* cpbBuffer：写入数据的缓冲区 
* cbBuffer：缓冲区的大小 
* cbOffset：输出流开始位置与应在其中开始写入的位置之间的偏移量 
* launchType：异步启动类型
  
#### <a name="returns"></a>Returns
包含实际写入字节数的 Async future，确保缓冲区始终存在，直到从 std::future 中检索到结果
  
### <a name="flushasync"></a>FlushAsync
以异步方式刷新输出流缓冲区。
  
#### <a name="parameters"></a>参数
* launchType：异步启动类型
  
#### <a name="returns"></a>Returns
包含指示刷新是否成功的 Async future
  
### <a name="read"></a>读取
以同步方式从流读取数据块。
  
#### <a name="parameters"></a>参数
* pbBuffer：应读入流的缓冲区 
* cbBuffer：缓冲区的大小
  
#### <a name="returns"></a>Returns
读取的实际字节数
  
### <a name="read"></a>读取
以同步方式从流读取数据块。
  
#### <a name="parameters"></a>参数
* u64size：要读取的数据的大小（以字节为单位）
  
#### <a name="returns"></a>Returns
实际读取数据的矢量
  
### <a name="write"></a>写入
以同步方式将数据块写入流。
  
#### <a name="parameters"></a>参数
* cpbBuffer：写入数据的缓冲区 
* cbBuffer：缓冲区的大小
  
#### <a name="returns"></a>Returns
实际写入的字节数
  
### <a name="flush"></a>刷新
以同步方式刷新输出流缓冲区。
  
#### <a name="returns"></a>Returns
刷新是否成功
  
### <a name="sharedstream"></a>SharedStream
克隆流。
  
#### <a name="returns"></a>Returns
克隆的流
  
### <a name="seek"></a>Seek
查找流中的位置。
  
#### <a name="parameters"></a>参数
* u64Position：相对于流开始位置的字节偏移量
  
### <a name="canread"></a>CanRead
获取流是否可读的指示。
  
#### <a name="returns"></a>Returns
流是否可读
  
### <a name="canwrite"></a>CanWrite
获取流是否可写入的指示。
  
#### <a name="returns"></a>Returns
流是否可写入
  
### <a name="position"></a>位置
获取流相对于开始位置的当前位置（以字节为单位）
  
#### <a name="returns"></a>Returns
流相对于开始位置的当前位置（以字节为单位）
  
### <a name="size"></a>大小
获取流的大小（以字节为单位）
  
#### <a name="returns"></a>Returns
流的大小（以字节为单位）
  
### <a name="size"></a>大小
设置流的大小（以字节为单位）
  
#### <a name="parameters"></a>参数
* u64Value：流的大小（以字节为单位）