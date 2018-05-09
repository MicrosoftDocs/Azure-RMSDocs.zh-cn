# <a name="class-mipstream"></a>class mip::Stream 
定义 mip sdk 和基于流的内容之间的接口的类。
  
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public int64_t Read(uint8_t* buffer, int64_t bufferLength)  |  从流读取到缓冲区。
public int64_t Write(const uint8_t* buffer, int64_t bufferLength)  |  从缓冲区写入流。
public bool Flush()  |  刷新流。
public void Seek(uint64_t position)  |  查找流中的特定位置。
public bool CanRead() const  |  检查流是否可读。
public bool CanWrite() const  |  检查流是否可写入。
public uint64_t Position()  |  获取流中的当前位置。
public uint64_t Size()  |  获取流中的内容的大小。
public void Size(uint64_t value)  |  设置流大小。
public std::shared_ptr<Stream> Clone()  |  克隆流。
  
## <a name="members"></a>成員
  
### <a name="read"></a>读取
从流读取到缓冲区。
  
#### <a name="parameters"></a>参数
* 指向缓冲区的缓冲区指针 
* bufferLength：缓冲区大小。 
  
#### <a name="returns"></a>Returns
实际读取的字节数。
  
### <a name="write"></a>写入
从缓冲区写入流。
  
#### <a name="parameters"></a>参数
* 指向缓冲区的缓冲区指针 
* bufferLength：缓冲区大小。 
  
#### <a name="returns"></a>Returns
实际读取的字节数。
  
### <a name="flush"></a>刷新
刷新流。
  
#### <a name="returns"></a>Returns
如果成功，则返回 true，否则返回 false。
  
### <a name="seek"></a>Seek
查找流中的特定位置。
  
#### <a name="parameters"></a>参数
* 在流中要查找的位置。
  
### <a name="canread"></a>CanRead
检查流是否可读。
  
#### <a name="returns"></a>Returns
如果可读，则返回 true，否则返回 false。
  
### <a name="canwrite"></a>CanWrite
检查流是否可写入。
  
#### <a name="returns"></a>Returns
如果可写入，则返回 true，否则返回 false。
  
### <a name="position"></a>位置
获取流中的当前位置。
  
#### <a name="returns"></a>Returns
流中的位置。
  
### <a name="size"></a>大小
获取流中的内容的大小。
  
#### <a name="returns"></a>Returns
流大小。
  
### <a name="size"></a>大小
设置流大小。
  
#### <a name="parameters"></a>参数
* 流大小。
  
### <a name="stream"></a>流
克隆流。
  
#### <a name="returns"></a>Returns
新流。