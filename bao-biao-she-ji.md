# 设计理念 #
报表设计核心理念：报表只是一种模式，而不是一种页面。

任何大小的页面都是报表，报表也不是一个尺寸的概念，海报也可以是报表。

目前模式一共有三种：*实时模式、报表模式、历史回放模式。*

om-lab目前支持两种页面：dashboard页面和工作站设备页面，
目前需要dashboard页面可选支持报表模式、历史回放模式；
工作站设备页面仅支持历史回放模式。

# om-lab里报表配置的流程 #

dashboard页面都有一个选项：“是否支持报表模式”，当选中后，用户就可以在omview里生成和下载这个页面的报表。

dashboard页面的属性中应增加选项：“页面大小”， 可选：“标准横向单页”， “标准纵向单页”，“自定义”

om-lab中需要支持对页的增删改（用户可以在不编辑完第一页时，直接去增加2，3页，并修改第三页）


## 标准横向单页 ##
  使用这个页面大小时，横向铺满，纵向以1920*1080的除去导航栏后的那个屏幕像素作为“一页单位”，用户在布局时会有页的概念。

  页与页之间展示在view上时有微小的纵向间距分割。

## 标准纵向单页 ##
  使用这个页面大小时，横向只占1400左右（预估算）的宽度，居中。纵向上的高度是横向宽度的1.41倍（1.41是A4纸的高宽比，严格按该比例定义页）

## 自定义大小 ##
  用户可以输入自定义大小的页面，主要输入两个参数：宽占比（50-100%，这是宽度占屏幕的比例），高宽比（50-200%，这是高度比宽度）

# 已有卡片的升级要求 #
  由于需要支持报表模式后，就意味着所有卡片（dashboard页面里的每种控件）的时间都必须支持页面的两种模式：实时模式、给定起终点模式（起点终点由页面报表模式定义的时间段决定）。

  举例：
  
##  实时值指标卡片 ##
  实时值指标卡片目前是请求实时值，升级支持报表模式后，应支持页面传入的起点和终点时间，报表模式下实时值指标卡片显示的是“页面起点时刻”到“页面终点时刻”的平均值
  
  所有实时类卡片显示的原则都如此，报表模式下显示时间范围内均值，时间范围由页面传入。

## 实时曲线卡片 ##
  实时模式：按自己定义的时间段（比如过去1小时，过去一天来）
  
  报表模式下：按报表传入的时间段来。

# 需新增加的卡片 #


 ## 标题卡片 ##
 
 ## 文字卡片 ##

 ## 表格卡片 ##
 
  这块建议完全使用Markdown的做法。比如表格卡片的编辑，就用markdown的文本定义法，加快开发速度。

 ## 饼图卡片 ##

 ##　曲线图卡片 ##



# om-view里报表查看流程 #
用户进入每个dashboard页面后，如果该页面在omlab中被配置了“支持报表模式”，那么omview里这个页面的右上角出现一个“报表图标”

用户选中“报表图标”后，弹出选项让用户选择报表的时间段，类似omsite中选择历史回放的时间段一样，可快速支持今日、昨日、本周、上周、本月、上月等。

选择好时间段，用户点击生成报表后，将提示Loading，并开始生成该页面的报表。

生成结束后，右上角报表图标处于“选中状态”，同时图标左侧出现一个下载图标，用户点击下载图标可以弹出选项让用户选下载格式（需支持word，pdf），确定后下载到chrome默认目录。




# 用户常见的A4纸报表的最简验证测试流程 #

 1. omlab新建页面，大小定义为纵向单页，属性中勾选“支持报表模式”。
 
 2. 用户新建第二页，第三页，在1-3页中分别拖动一个仪表盘卡片，绑点为室外温度（OutdoorTdbin）。

 3. 保存页面。

 4. 进入omview中，刷新该页面，点击右上角的报表模式，选择时间段为今日后，下载word文件，文件分为三页，每页上呈现一个仪表盘，都显示的是今日平均室外温度。