# <a name="class-mipaddcontentfooteraction"></a>class mip::AddContentFooterAction 
指定向文档添加内容脚注的操作类。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::string & GetUIElementName | 用来标记内容脚注元素的 API。
public const std::string & GetText | 获取要进入内容脚注的文本。
public const std::string & GetFontName | 获取用于显示内容脚注的字体名称。
public int GetFontSize | 获取用于显示内容脚注的字体大小。
public const std::string & GetFontColor | 获取用于显示内容脚注的字体颜色。
public ContentMarkAlignment GetAlignment | 获取脚注的对齐方式。
public int GetMargin | 从底部获取脚注的边距。
public ActionType GetType
## <a name="members"></a>成員
### <a name="getuielementname"></a>GetUIElementName
用来标记内容脚注元素的 API。
#### <a name="returns"></a>Returns
应用于保存内容脚注的 UI 元素的名称。 如果需要删除内容脚注，将在 [RemoveContentFooterAction](#classmip_1_1_remove_content_footer_action) 中返回相同名称。
### <a name="gettext"></a>GetText
获取要进入内容脚注的文本。
#### <a name="returns"></a>Returns
内容脚注文本。
### <a name="getfontname"></a>GetFontName
获取用于显示内容脚注的字体名称。
#### <a name="returns"></a>Returns
字体名称，如果策略未设置，则为默认值 Calibri。
### <a name="getfontsize"></a>GetFontSize
获取用于显示内容脚注的字体大小。
#### <a name="returns"></a>Returns
整数形式的字体大小。
### <a name="getfontcolor"></a>GetFontColor
获取用于显示内容脚注的字体颜色。
#### <a name="returns"></a>Returns
字符串形式的字体颜色（例如“#000000”）。
### <a name="getalignment"></a>GetAlignment
获取脚注的对齐方式。
#### <a name="returns"></a>Returns
ContentMarkAlignment 枚举器，左对齐|右对齐|水平居中。 
另请参阅：ContentMarkAlignment
### <a name="getmargin"></a>GetMargin
从底部获取脚注的边距。
#### <a name="returns"></a>Returns
表示文档底部边距的整数（例如 10 毫米）。
### <a name="actiontype"></a>ActionType
获取[操作](#classmip_1_1_action)类型。
#### <a name="returns"></a>Returns
ActionType：此基类可以转换成的派生操作类型。