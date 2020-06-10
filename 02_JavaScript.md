---
- JavaScript基础, WebAPI, JS高级, JQuery
- JaveScript由 ECMAScript, DOM, BOM组成
- 五种基本数据类型(值类型), 一种复杂数据类型(引用类型)
- 面向对象编程
- 函数
- 原型, 原型链
- 正则表达式
- jQuery基本使用
---

[阮一峰Javascript基础](https://wangdoc.com/javascript/index.html)

[阮一峰ES6入门](http://es6.ruanyifeng.com/)

# ECMAScript

## **基础知识**

- JavaScript的核心, 定义了JS语言规范

- 描述JavaScript的基本语法和数据类型

- 凡是能用JS实现的功能, 最终都会用JS来实现

- javascript三种书写方式
 ```
  - 行内样式: 在html标签内部写入事件
  - 内嵌样式: 在script标签写
  - 外链样式: 用script 的src 属性链接js文件
 ```

- JS报错有两种
  - 数据类型错误
  - 语法错误
- **window是JS中的顶级对象, 所有的全局变量都是其属性**

## **数据类型**

直接量: 可以直接拿来用的数据, 符合数据类型的数据就是直接量

1. 基本数据类型

   基本数据类型也称值类型, 共五种
   ```javascript
    - Number: 数字类型
      /* NaN是一个Number里一个特殊的数值, 语义为not a number
         NaN与任何数据都不等, 包括其自身
         NaN与任何数据相加都是NaN
         检测数据是否为NaN用isNaN(数据) 
        */
   
    - String: 字符串类型
      /* 字符串具有恒定性 */
         
    - Boolean: 只有两个值, true and false
   
    - undefined: 空值, 变量声明未赋值
   
    - null: 空值, 只能手动设置
   ```

2. 复杂数据类型

   复杂数据类型也称引用类型

   `Array: 数组`

   `Object: 对象`

3. 基本包装类

   what's it? 为了使基本的数据类型也可以调用方法, JavaScript在内部将

   Number

   String

   Boolean

   三种基本数据类型进行了包装, 这就是基本包装类

   - 转Number 
     ```javascript
     var str = "233.3";
     - parseInt(str); // 解析为整数
     - parseFloat(str); // 解析为浮点数
     - Number(true); // 将布尔类型数据解析为number类型
     ```

   - 转String

     ```javascript
     var num = 100;
     - num.toString(); // undefined和 null转换时会报错, 后者不会
     - Strinng(num);
     ```

    - 转Boolean

      ```javascript
      var num = -99;
      - Boolean(num);
      - // 除开0, -0, undefined, null, false, ''(空字符), NaN, document.all()八种外
      - // 任何数据转Boolean都为true
      ```

4. 数据类型的检测

   ```
   1. typeof (数据) 只能检测基本数据类型(除null外), 还可以检测function
   
   2. 检测数组
   	instanceof (不严谨)      (检测后者[构造函数]的原型是否在前者的原型链上)
   	数组 instanceof Array (true)
   	数组 instanceof Object (true)
   	Array.isArray(数据)
   		
   3. 万能的数据类型检测
   	Object.prototype.toString.call(数据)
   ```

## **关键字**

- this

  谁调用指向谁

- new

  1. 创建一个空对象
  2. 将this指向这个空对象
  3. 执行函数内代码
  4. 返回这个对象

- var

  在栈中开辟一块空间

- delete

  可以删除未用var 声明的变量及 对象的成员

- return

  结束函数, 返回return之后内容

- in

  检测对象中是否有key 键

##**常用API**

###String

```javascript
const str = "localhost";
str.toLowerCase(); // 将str转为小写; return str
str.toUpperCause(); // 将str转为大写; ruturn str
str.startWith("A"); // 判断str是否以param开头; return boolean值
```
---
###Array

```js
// 伪数组转数组
Array.from(arrayLike[, mapFn[, thisArg]])
// 参数1: 伪数组对象或可枚举对象
// 参数2: 可选, 数组中每个元素执行该函数
// 参数3: 可选, 更改函数this指向
```



---


# **DOM**

what's it?

文档对象模型, JS中一套操作文档流元素的API

***DOM的根本对象是document, 但document同时也是window的一个属性, 而window既是BOM的核心对象, 为JS提供访问浏览器的接口同时又是JS中的顶级对象, 所有的全局变量都是其属性***

##**about Element**

1. **直接获取元素**
   - document.getElementsByClassName('类名'); IE8不支持, 避免使用
   - 除ID选择器外, 可以使用 父元素.getElementsbyTagName();
   - document.querySelector( "选择器名"); 获取符合条件的第一个元素
   - document.querySelectorsAll( "选择器名"); 获取符合条件的所有元素

2. **about Node**
  ![](F:\Data for Web\Printscreen\Node.png)

3. **间接获取元素**

   ***IE8获取节点不包含空文本且不支持获取元素节点的API***

   - 获取子元素               .children  **IE8会额外获取注释节点**
   - 获取子节点               .childNodes子节点 
   - 获取下/上一个元素         .next/ previousElementSibling
   - 获取下/上一个节点         .next/ previousSibling
   - 获取第一个最后一个元素     .first/ lastElementChild
   - 获取第一个最后一个元素     .first/ lastChild
   - 获取元素的父元素节点       .parentNode
   - 获取元素的属性节点         .attributes

4. **增删查改**

   - 父元素.appendChild(子)      添加
   - 父元素.removeChild(子)      移除
   - .cloneNode(true)           (深)克隆
   - .replaceChild()            替换
   - .insertBefore()            添加到指定元素前

5. **获取元素属性的三种方式**

   ```
   .style 只能获取行内属性,String类型, 可以设置
   
   .setAttribute(属性名, 属性值)
   .getAttribute(属性名)
   
   window.getComputedStyle(element, null)  可以获取元素的所有属性, 但不能设置
   第二个参数一般是null, 也可以是该元素的伪元素, 那获取就是改元素的伪元素
   ```

##**三大家族**

   ***只可获取有关属性, 获取的属性都是Number类型且不可修改***

   1. offset

     ```offsetWidth/Height 获取元素的真实宽高(content+ padding+ border)
     offsetParent 获取元素最近的定位父元素
     offsetTop/Left 获取元素距离其offsetParent的Top/Left值
     ```
   2. scroll
     ```
     scrollWidth/Height 获取元素内容的真实宽高
     scrollTop/Left 获取元素内容滚动出去的距离
     window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop ||0;
     获取页面滚动出去的距离
     ```
   3. client
     ```
     clientWidth/Height 获取元素可视区域的大小
     clientTop/Left 获取元素上/左边框的大小
     window.innerWidth|| document.documentElement.clientWidth|| document.body.clientWidth||0;
     获取页面可视区域的大小
     ```
##**事件**

what's it?

*JS中用户与网页进行交互的一种机制*

1. 事件对象 event || window.event;

   事件触发时, 记录有关事件信息的变量, 这个变量是一个对象, 故称事件对象

   ```
   e.target 事件触发时的位置 => 事件源
   this === e.currentTarget 事件处理对象
   
   e.type 事件类型
   
   e.PageX/Y  IE8: e.PageX = window.pageXOffset+ e.clientX 事件触发点距页面
   e.screenX/Y 事件触发点距屏幕
   e.clientX/Y 事件触发点距页面可视区域
   
   e.stopPropagation() 阻止事件冒泡及捕获(IE8及之前没有捕获)
   .cancelBubble = true IE8
   ```

2. 事件注册与移除

   .on+ 事件名 

   ​	缺点: 不能注册多个同名事件

   ​	移除: .on+ 事件名 = null;

   .addEventListener(事件名, 事件处理函数, boolean值(false冒泡, true捕获));

   ​	可以注册多个同名事件, 会根据注册的先后依次触发

   ​	移除: .removeEventListener(type, fn, false) 移除

3. 事件种类

   ```
   鼠标按下 onmousedown
   鼠标弹起 onmouseup
   单击 onclick
   双击 ondblclick
   移入 onmouseover
   移出 onmouseout
   鼠标移动 onmousemove
   获得焦点 onfocus
   失去焦点 onblur
   滚动 onscroll
   大小变化 onresize
   键盘按下 onkeydown
   键盘按下 onkeypress
   键盘弹起 onkeyup
   值变化   onchange
   滚轮事件 mousewheel event.wheelDelta值为120的倍数上滚, -120倍数 下滚
   ```

4. 事件阶段

   第一阶段: 冒泡阶段, 如果一个元素的事件被触发，那么他的所有父级元素的同名事件也会被依次触发

   第二阶段: 目标阶段, 元素自身

   第三阶段: 捕获阶段, 从最顶级的父元素一级一级往下找子元素触发同名事件，直到触发事件的元素为止
#**BOM**

- **window**

  **BOM的核心对象window, 为JS提供操作浏览器窗口的API**

  ```
  // - window.name  无论怎样修改都是一个字符串
  
  // - window.top   一个只读属性, 不能修改
  
  // - window.onload 页面加载完毕(document, images, video, audio...)触发, 原生JS入口函数
  ```

- **location**
  包含当前页面的url信息 url：全球统一资源定位符
  *url = 协议名（http） + ip地址（域名） + 端口号 + 资源路径*

```javascript
  // - location.assign("url") 打开新的页面
  // (window.open('url', _self)Chrome默认拦截弹窗)
  
  // - location.replace("url") 打开页面替换当前(不可回退)
  
  // - location.reload() 刷新当前页面(F5)
```

- **history**

  记录浏览器历史
  ```
  - history.forward 前进( 要有已打开的下一个页面)
  - history.back 返回
  ```

- **navigator**

  包含当前浏览器的信息

  navigator.userAgent 获取浏览器平台

- **screen**

  screen.width& screen.height 获取屏幕分辨率

