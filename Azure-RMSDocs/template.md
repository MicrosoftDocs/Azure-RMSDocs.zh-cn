---
# required metadata

title: [文章标题 | 服务名称]
description:
keywords:
author: [GITHUB USERNAME]
manager: [ALIAS]
ms.date: 04/28/2016
ms.topic: article
ms.prod:
ms.service:
ms.technology:
ms.assetid: [GET ONE FROM guidgenerator.com]

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
#ms.reviewer: [ALIAS]
#ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 元数据和标记模板

此 docs.ms 模板包含标记语法示例以及有关设置元数据的指南。 它在每个 EM 试验存储库的根目录下可用（例如，~/Azure-RMSDocs-pr
/template.md），并应读取为标记文件，你还可以参考[已发布的版本](https://stage.docs.microsoft.com/en-us/rights-management/template)，查看示例标记的呈现方式。

创建标记文件时，应将模板复制到新的文件，按下面所指定的那样填写元数据，将上方的 H1 标题设置为该文章的标题并删除内容。 


## 元数据 

上方是完整的元数据块，分为必填字段和可选字段；有关更多详细信息，请参阅 [OPS 元数据速查表](https://ppe.msdn.microsoft.com/en-us/ce-csi-docs/ops/ops-onboarding/managing-content/content-meta-data)。 一些关键说明：

- 冒号（：）和元数据元素的值之间**必须**有一个空格。
- 如果可选的元数据元素没有值，用 # 注释该元素（不要留空或使用 "na"）；如果你要向注释的元素添加值，请务必删除 #。
- 值（例如标题）中的冒号将元数据分析器隔断。 在它们的位置上，使用 HTML 编码 & #58;（例如，“标题：Azure Rights Management & #58;基础知识 |Azure RMS”）
- **标题**：该标题将显示在搜索引擎结果中。 标题应以竖线 (|) 结尾，后跟服务名称（见以上示例）。 标题无需（且很可能不应）与 H1 标题中的标题相同。 大约应为 65 个字符（包含内容 | 服务名称）
- **作者**，**管理员**，**审阅者**：作者字段应包含作者的 **Github 用户名**，而不是其别名。  而“管理者”和“审阅者”字段则应包含别名。 ms.reviewer 指定与文章或服务关联的 PM 的名称。
- **ms.assetid**：这是来自 CAPS 的文章的 GUID。 创建新的标记文件时，从 [https://www.guidgenerator.com](https://www.guidgenerator.com) 获取 GUID。 
- **ms.prod**、**ms.service**、**ms.technology**、**ms.devlang**、**ms.topic**、**ms.tgt_pltfrm**：可在[此处](https://microsoft.sharepoint.com/teams/STBCSI/Insights/_layouts/15/WopiFrame.aspx?sourcedoc=%7b7A321BF1-0611-4184-84DA-A0E964C435FA%7d&file=WEDCS_MasterList_CSIValues.xlsx&action=default)找到这些元素的可能值。

## 基本标记和 GFM

支持所有基本和 Github 风格的标记。 有关详细信息，请参阅：

- [基线标记语法](https://daringfireball.net/projects/markdown/syntax)
- [GitHub 风格的标记 (GFM) 文档](https://guides.github.com/features/mastering-markdown)

## 标题

一级和二级标题的示例如上所示。 

你的主题中**必须**仅存在一级标题，它将显示为页面上标题。  

二级标题将生成页面上 TOC，后者将显示在页面上标题下方的“本文内容”部分中。

### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题

## 文本样式

*斜体* 

**粗体** 

~~删除线~~



## Links

若要链接到同一个存储库中的标记文件，请使用[相对链接](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2)。 

- 示例：[Azure Rights Management 是什么](./understand-explore/what-is-azure-rms.md)

若要链接到同一标记文件中的标题，请查看已发布文章的源，查找标头的 ID（例如 `id="blockquote"`，以及使用 # + ID 的链接（例如 `#blockquote`））。

- 示例：[块引用](#blockquote)

若要链接到同一个存储库中的标记文件中的标题，请使用相对链接 + 哈希标记链接。

- 示例：[注册过程中的技术概述](./understand-explore/rms-for-individuals-user-sign-up.md#technical-overview-of-the-sign-up-process)

若要链接到外部文件，请使用完整的 URL 作为链接。

- 示例：[Github](http://www.github.com)

如果 URL 出现在标记文件中，将转换为可单击的链接。

- 示例：http://www.github.com

## 列表

### 经过排序的列表

1. 如果 
1. 是
1. 在此视图中，
1. 经过排序的
1. 列表  


#### 带有嵌入式列表、经过排序的列表

1. 签名
1. 来自
1. 一个
1. 嵌入
    1. Scarlett 小姐
    1. Plum 教授
1. 经过排序的
1. 列表


### 未经排序的列表

- 如果
- 是
- a
- 项目符号
- 列表


##### 带有嵌入式列表、未经排序的列表

- 如果 
- 项目符号 
- 列表
    - Peacock 太太
    - Green 先生
- 包含  
- other
    1. Mustard 上校
    1. White 太太
- 列表


## 水平标尺

---

## 表

| 表        | 是           | 很好  |
| ------------- |:-------------:| -----:|
| 第 3 列是      | 右对齐 | $1600 |
| 第 2 列是      | 居中      |   $12 |
| 第 1 列为默认。 | 左对齐     |    $1 |


## 代码

### 代码块

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }

### 内联代码

这是 `in-line code` 的一个示例。

## 块引用

> 干旱已经持续了一千万年，可怕的蜥蜴的统治早已结束。 在位于赤道的这片将来有一天会被称为非洲的大陆上，生存的斗争已经达到凶残的至高点，而胜利似乎遥遥无期。 在这片贫瘠干涸的土地上，只有小巧、敏捷或凶猛的生物才可能繁衍生息，甚至才可能抱有生存下去的期望。

## 映像

### 静态映像

![这是替换文字](./media/AzRMS_elements.png)

### 链接映像

[![a链接映像的文本](./media/AzRMS_elements.png)](https://azure.microsoft.com) 

### 动画 GIF

![动画 GIF](./media/hololens.gif)

## 警报

### 备注

> [!NOTE]
> 这是说明

### 警告

> [!WARNING]
> 这是警告

### 提示

> [!TIP]
> 这是提示

### 重要

> [!IMPORTANT]
> 这是重要事项

## 视频

### 第 9 频道

<iframe src="http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-Express-Settings/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>


### YouTube

<iframe width="420" height="315" src="https://www.youtube.com/embed/R6_eWWfNB54" frameborder="0" allowfullscreen></iframe>

## docs.ms 扩展

### 按钮

> [!div class="button"]
[按钮链接](/rights-management)

### 选择器

> [!div class="op_single_selector"]
- [foo](/rights-management/template.md)
- [栏](/rights-management/scratch.md)

### 分步

>[!div class="step-by-step"]
[“上一步”](https://www.example.com)
[“下一步”](https://www.example.com)

<!--HONumber=Apr16_HO3-->


