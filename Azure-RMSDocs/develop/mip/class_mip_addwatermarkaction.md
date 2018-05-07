# <a name="class-mipaddwatermarkaction"></a>class mip::AddWatermarkAction 
指定添加水印的操作类。
## <a name="summary"></a>“摘要”
 成員                        | 描述                                
--------------------------------|---------------------------------------------
public const std::string & GetUIElementName | 用于标记水印元素的 API。
public WatermarkLayout GetLayout | 用于获取水印布局的 API。
public const std::string & GetText | 获取表示要进入内容头的文本。
public const std::string & GetFontName | 获取用于显示内容头的字体名称。
public int GetFontSize | 获取用于显示内容头的字体大小。
public const std::string & GetFontColor | 获取用于显示内容头的字体颜色。
public ActionType GetType
## <a name="members"></a>成員
### <a name="getuielementname"></a>GetUIElementName
用于标记水印元素的 API。
#### <a name="returns"></a>Returns
应用于保存水印的 UI 元素的名称。 如果需要删除水印，将在 RemoveWatermarkingAction 中返回相同名称。
### <a name="getlayout"></a>GetLayout
用于获取水印布局的 API。
#### <a name="returns"></a>Returns
WatermarkLayout：采用枚举水平|对角线形式的水印布局。 、
### <a name="gettext"></a>GetText
获取表示要进入内容头的文本。
#### <a name="returns"></a>Returns
内容头文本。
### <a name="getfontname"></a>GetFontName
获取用于显示内容头的字体名称。
#### <a name="returns"></a>Returns
字体名称，如果策略未设置，则为默认值 Calibri。
### <a name="getfontsize"></a>GetFontSize
获取用于显示内容头的字体大小。
#### <a name="returns"></a>Returns
整数形式的字体大小。
### <a name="getfontcolor"></a>GetFontColor
获取用于显示内容头的字体颜色。
#### <a name="returns"></a>Returns
字符串形式的字体颜色（例如“#000000”）。
### <a name="actiontype"></a>ActionType
获取[操作](#classmip_1_1_action)类型。
#### <a name="returns"></a>Returns
ActionType：此基类可以转换成的派生操作类型。