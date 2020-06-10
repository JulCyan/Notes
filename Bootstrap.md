# bootstrap

## 全局CSS样式

###1.栅格系统

1.1 基本栅格类

+ .col-xs-* 超小屏幕 <768px xs(自适应)
+ .col-sm-* 小屏幕 >=768px
+ .col-md-* 中屏幕 >=992px
+ .col-lg-* 大屏幕 >=1200px

1.2 偏移列

   ​	.col-xs-offset-* 左边增加*列, 实现偏移或居中

1.3 排序列

   + .col-xs-push-* 向后偏移\*列
   + .col-xs-pull-* 向前偏移*列



###2.排版

2.1 \<small\> 标签 ,使文本字号更小的颜色更浅(设置文本为父文本大小的 85%)

2.2 主体副本类 

   ​	.lead

2.2 强调文本类

   + .text-left 文本向左对齐
   + .text-center 文本居中对齐
   + .text-right 文本向右对齐
   + .text-muted 文本淡弱(斜体, 颜色浅)
   + .text-primary 文本蓝色斜体
   + .text-success 文本绿色斜体
   + .text-info 文本#d9edf7斜体
   + .text-warning 文本橙色斜体
   + .text-danger 文本红色斜体
   + .text-lowercase 文本小写
   + .text-uppercase 文本大写
   + .text-capitalize 单词首字母大写
   + .text-nowarp 超出不换行
   + .text-justify 文本对齐, 超出换行

   2.3 文本缩写

   ​	\<abbr\> 标签, title设置鼠标悬停文本, 标签内设置显示文本

   ​	.initialism 使其更小

   2.4 引用

   ​	\<blockquote\> 标签

   ​	.pull-right 向右对齐

   2.5 列表

   ​	.list-unstyled 未定义样式列表

   ​	.list-inline 内联列表

   ​	.dl-horizontal 水平列表



###3.代码

   3.1  \<code\> 标签将代码内联显示

   3.2  \<pre\> 标签将代码块单独显示



###4.表格

+ .table 基本表格样式(只有横向分割线)
+ .table-striped 在 \<body\> 内添加斑马线形式的条纹
+ .table-bordered 为所有表格的单元格添加边框
+ .table-hover 在 \<tbody\> 内的任一行启用鼠标悬停状态
+ .table-condensed 表格紧凑
+ .active 单元格悬停
+ .success 操作成功
+ .info 信息变化
+ .warning 警告操作
+ .danger 危险操作



###5.表单

5.1 基本布局要求

+ 向父 \<form\> 元素添加 *role="form"*

+ 把标签和控件放在一个带有 class *.form-group* 的 \<div\> 中。这是获取最佳间距所必需的
   + 向所有的文本元素 \<input\>、\<textarea\> 及 \<select\> 添加 class *.form-conrol*

5.2 内联表单

   + form 添加 class .form-inline
   + 默认控制 100% 宽度, so, 内联需要手动设置
   + 控制使用 class .sr-only 隐藏

5.3 控件

   + .checkbox-inline 
   + .radio-inline 单/复选框一行显示
   + 当您需要在一个水平表单内的表单标签后放置纯文本时，请在 \<p\> 上使用 class *.form-control-static*

   + .control-lg 
   + .control-sm 切换表单高度



### 6.按钮

+ .btn 基本按钮样式
+ .btn-defaultb 默认按钮
+ .btn-primary 原始样式
+ .btn-link 链接按钮
+ .btn-lg 大按钮
+ .btn-sm 小按钮
+ .btn-xs 超小按钮
+ .btn-block 块级按钮(width="100%")
+ .active 点击样式
+ .disabled 禁用



### 7.图片

7.1 

+ .img-rounded 添加 border-radius: 6px
+ .img-circle 添加 border-radius: 500px
+ .img-thumbnail 添加一些padding 和 灰色边框
+ .img-responsive 图片响应式



### 8.辅助类

8.1 文本移入

8.2 背景

8.3

+ .center-block 元素display:block并居中显示
+ .clearfix 清除浮动
+ .show 强制元素显示
+ .hidden 强制元素隐藏
+ .sr-only 隐藏
+ .sr-only-fucesable 获取焦点显示
+ .text-hide 元素文本作文背景
+ .close 显示关闭按钮
+ .caret 显示下拉功能

8.4

+ .visible-*-block 在\*屏幕display: block
+ .visible-*-inline
+ .visible-*-inline-block