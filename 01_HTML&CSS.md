---
- html 标签, css 样式
- 前端三老铁: html 结构代码, css 样式属性, js 交互
- 盒子模型
- 标准, 浮动 ,定位
---

# HTML

## **一、路径**

- 相对路径

   同级 文件名
   下一级 文件夹/文件名
   上一级 ../文件名 

- 绝对路径

​    完整的域名

> img图片标签: 
>
> - src: 图片路径 
>
> - alt: 图片显示失败出现的文本
> - title: 鼠标悬停时图片显示的文本
>
> a链接标签: 
>
> - herf 路径
>
> - target 链接打开方式
>
>   - _self 覆盖当前窗口打开(默认值)
>
>   - _blank 在新窗口打开

---

## **二、表格**
 ### 1. table 样式属性

   - rowspan 跨行合并, colspan跨列合并, 注意要清除被合并的单元格
   - table: 表格的所有内容都要在table里 
   - border: 表格的边框		
   - cellspacing: 边框之间的空白间隙,默认为2px		
   - cellpadding: 文字与边框的间隙,默认为1px		
   - align: 水平对齐方式	

### 2. table 基本结构

- caption: 表格的标题
- thead: 存放表头
- tr, th: 表头,会自行加粗和居中	
- tbody: 存放表格内容		
- tr, td: 行和单元格	
- tfoot: 一般不用 

---

## **三、表单**

### 1. form: 表单域

- 按钮效果实现需要在表单域内
- 提交表单时有附带文件时必须有 enctype="multipart/form-data" 属性;

### 2. disable: 禁用

- 禁用表单标签

### 3. 表单常用标签

#### a) input: 控件

- type 属性:
  - text: 文本框
  - password: 暗文密码框
  - radio: 单选框, 单选互斥需要 name属性分组关联
  - button: 普通按钮
  - submit: 提交按
  - reset: 重置按钮
  - image: 图片按钮
  - file: 文件域 行内multiple 多选
- value: 默认值, 一般用于记住密码的操作
- palaceholder: 占位符, 未输入之前的提示信息
- maxlength: 可输入的最大字符数量
- size: 输入框的宽度,一般很少用到
- checked: 默认选中

#### b) textarea: 文本域

- 禁用文本域拉动 resize: none

#### c) select: 下拉框

   - option: 下拉框选项
   - selected: 下拉框默认选中
   - `multiple`: 展示所有下拉选项

#### d) label: 绑定标签

   - for="id名"

   - 被绑定标签设置 id="id名"

   - label标签内嵌套标签也可实现绑定

     ---
# CSS

## **一、引入CSS样式**

1. 行内式(内联样式)

   是通过标签的style属性来设置元素的样式，其基本语法格式如下：

   ` <标签名 style="属性1: 属性值1; 属性2: 属性值2; 属性3: 属性值3;"> 内容 </标签名>`

2. 内部样式表(内嵌式)

   在style 标签内部书写

3. 外部样式表(外链式)

   通过link 标签的href 链接css文件, 如下:

   ``` html
   <head>
     <link href="CSS文件的路径" type="text/CSS" rel="stylesheet" />
   </head>
   ```

## **二、选择器**

### 1. 基本选择器

- 标签选择器

- 类选择器

- ID选择器

- 通配符选择器

- 属性选择器

  | **选择器              | **示例 | **含义                              |
  | --------------------- | ------ | ----------------------------------- |
  | **E[attr]\******      |        | 存在attr属性即可                    |
  | **E[attr=val]\******  |        | 属性值完全等于val                   |
  | **E[attr\*=val]****** |        | 属性值里包含val字符并且在“任意”位置 |
  | **E[attr^=val]\****** |        | 属性值里包含val字符并且在“开始”位置 |
  | **E[attr$=val]\****** |        | 属性值里包含val字符并且在“结束”位置 |

### 2. 复合选择器

- 后代选择器
- 子代选择器
- 并集选择器
- 交集选择器

### 3. 伪类选择器

- a链接伪类选择器

  ***love hate***

  ```css
  - :link      /* 未访问的链接 */
  - :visited   /* 已访问的链接 */
  - :hover     /* 鼠标移动到链接上 */
  - :active    /* 选定的链接 */
  ```

- 结构(位置)伪类选择器

- 伪元素选择器

## **三、CSS盒子模型**

### 1. main

- border + padding + content 盒子真实宽高
- padding, margin属性, 对于行内元素无效
- margin: 0 auto; 盒子必须是有宽度的块级元素
- `border-color的 transparent属性实现小三角效果`

### 2. margin's bug

- 垂直塌陷

- 包含塌陷: 子盒子设置margin会带跑父盒子

  解决方式: 1.设置1px的外边框或内边距(一般不用)
  ​         2.overflow:hidden

### 3. 盒子模型转换

- `box-sizing`:
  - contnet-box 盒子改变时, 会保证content大小不变
  - border-box 改变content的大小以保证盒子真实宽高不变

## **四、浮动**

### 1. 特点

- 浮动的本质是为了解决文字环绕图片, 所以图片浮动不会遮盖文字

- display: inline-block

- 脱标, 不占据标准流位置
- 浮动元素顶部对齐, 上个元素如果是标准流元素则与其底部对齐
- 不会主动占据标准流元素的位置

### 2. 清除浮动影响

 **Why: 子盒子浮动会导致父盒子高度为0**

- 高度法

- 额外标签法

- overflow: hidden

- 单伪元素(常用)

  ```css
  .clearfix::after {
      content: ".";
      display: block;
      clear: both;
      height: 0;
      visibility: hidden;
  }
  // 兼容
  .clearfix {
      *zoom: 1;
  }
  ```

- 双伪元素

## **五、定位**

### 1. 分类

 position:

- static 静态定位(标准流)
- fixed 固定定位
- relative 相对定位(不脱标,占有标准流位置)
- absolute 绝对定位(子绝父相)

### 2. 特点

- display: inline-block

- 元素成为定位流元素(布局最高层级)
- 边偏移属性
- z-index 设置层级

### 3. 定位元素居中

- 水平 `left: 50%; transform: translateX(-50%);`
- 垂直同理

## **六、元素的可见性**

### 1.display

 dispaly: none 不显示且清除元素位置

 dispaly: block 显示

 display: flex 弹性布局

### 2.visibility

 visibility: hidden 不显示保留位置

 visibility: visible 显示

## **七、overflow 超出处理**

- `overflow:hidden`

  - 解决包含塌陷

  - 清除浮动影响

  - 超出部分隐藏

- others

  - `overflow: auto` 自适应添加滚动条 (常用)

  - overflow: scroll 滚动条
  - overflow: visible 不隐藏超出部分也不添加滚动条

## **八、CSS高级技巧**

### 1. cursor 鼠标样式

- default 小白 
- pointer 小手
- move 移动 
- text 文本
- wait 等待
- help 帮助
- not-allowed 禁止

### 2. 文本换行

```css
.English {
    width: 200px;
    border: solid 1px red;
    /* 不打乱单词 在半角空格或链接符号 - 处换行 */
    /* word-all 可以打断单词换行 */
    word-break: keep-all;
}
// 超出文本用...显示        
.Chinese {
    width: 200px;
    border: solid 1px red;
    /* 强制文本一行显示(不换行)  默认值为normal*/
    white-space: nowrap;
    /* 隐藏内容用 ... 代替 */
    text-overflow: ellipsis;
    /* text-overflow 必须配合overflow: hidden 使用 */
    overflow: hidden;
}
```

### 3. iconfont 字体图标

- fontclass

  1. link 引入字体图标css文件

     `<link rel="stylesheet" type="text/css" href="./iconfont.css">`

  2. 给需要使用字体图标的标签加上iconfont 以及对应字体图标的类名

     ```css
     <i class="iconfont icon-xxx"></i>
     或者
     <i class="iconfont">&#x33;</i>
     ```

  3. 字体库链接
  - [阿里iconfont字库](http://www.iconfont.cn/)
  - [外网icomoon字库](http://www.iconfont.cn/)
  - [Icons8](https://icons8.com/)提供png下载


- unicode
  引入CSS代码,给需要使用字体图标的标签加上  iconfont

### 4. transform 变形

#### a) translate 平移

#### b) scale 缩放

#### c) rotate(deg) 旋转

```css
rotate3d(0,1,1,ndeg)
// 统一控制方向轴的旋转, 旋转度数一致, 需要旋转写1, 不旋转写0
```

#### d) skew(deg, deg) 倾斜

#### e) transform-origin

```css
-// 设置旋转中心点
- tranform-origin: left bottom;
- transform-origin: 50% 75%;
```

#### f) perspective 透视
```css
透视可以将一个2D平面，在转换的过程当中，呈现3D效果;
perspective一般作为一个属性，设置给父元素，作用于所有3D转换的子元素
transform-style: preserve-3d; // 此盒子呈现3D效果
```

#### g) others

```css
1. backface-visibility: hidden
属性定义当元素不面向屏幕时是否可见, 不是正面对象屏幕，就隐藏

2. @keyframes 动画名称 {
  from{ 开始位置 } (0%) (节点设置可用百分比);
  to{ 结束 } (100%);  
}
 - animation:动画名称 动画时间 运动曲线 何时开始
			播放次数: 定次n/ 无限循环infinite 播放模式: 默认normal/ 往返播放alternate;
 - animation-fill-mode: forwards;// 动画完成时保持最后节点状态
```

## **九、CSS书写规范**

### a) 样式属性书写顺序

>布局定位属性--> 自身属性--> 文本属性--> 其他属性; 
>
>此条可根据自身习惯书写, 但尽量保证同类属性写在一起; 
>
>属性列举: 布局定位属性主要包括:
>margin、padding、float（包括clear、position（相应的top、right、bottom、left、display、visibility、overflow 等；
>
>自身属性主要包括: width& height& background& border; 
>
>文本属性主要包括：font、color、text-align、text-decoration、text-indent等；
>
>其他属性包括: list-style、vertical-align、cursor、z-index、zoom等;
>
>所列出的这些属性只是最常用到的, 并不代表全部;



​	




#### 	

