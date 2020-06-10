---
适合初学者简便的NodeJS笔记
NodeJS初级 所学模块的常用API
特殊字符: 3rdP => third-party module 第三方模块
用control+F 搜索关键字阅读								-- 个人笔记
---

# **NodeJS**

what's it?

- 一个开发平台: 有对应的编程语言、 有语言运行时(运行环境)、有能实现特定功能的API 
- 特点: 
  1. 事件驱动(当事件被触发时, 执行传递过去的callback(回调函数))
  2. 非阻塞 I/O模型 (当执行input/output操作时, 不会阻塞线程)
  3. 单线程(JS就是单线程语言)
  4. 拥有世界上最大的开源库生态系统 => npm

## REPL

全称: Read-Eval-Print-Loop(交互解释器)

类似于Chrome console控制台

```

Read: 读取 -- 读取输入js数据结构并储存在内存中
Eval: 执行 -- 运行js数据结构
Print: 打印 -- 输出结构
Loop: 循环 --循环上述步骤

```

退出REPL: .exit or control + C{2} 



## **命令行**

**cmd**

```

dir                       	 查看当前文件夹下所有文件/文件夹
cls 	           		    清屏
cd 文件名             		  进入该目录
cd.. 	           		    返回上级目录
cd/                      	返回顶级目录
cd 盘符名 回车 盘符名		 切换盘符目录
盘符名						切换盘符

```

---


**node**

```

node			        		    开启REPL
node  js文件                          运行js代码
nodemon  js文件                       监控源代码更改并重新运行
node -version/v       		         查看node版本
node --inspect js文件                 node调试
node --inspect-brk js文件	            运行时启动断点调试
node --inspect=9229 js文件            非web服务断点调试
node --inspect-brk=9229 js文件        非web服务启动时开启断点调试

```

---


**npm**

```

npm -version/v              查看npm版本
npm install/i 包名          本地安装

npm install/i 包名 -save    
自动修改package.json文件
下次使用本地安装时会自动将package.json中生产及开发依赖模块安装到node_module目录下

npm install/i 包名 -g       全局安装(可以使用包命令)
npm uninstall 包名		  卸载本地安装
npm uninstall 包名 -g		  卸载全局安装
npm install/i 包名@版本号    下载对应版本的包
npm install/i 包名@latest   下载最新版本的包
npm install/i npm@latest    下载最新版本的npm
npm init                    手动新建一个package.josn&-loca.josn文件
npm init -yes/y             自动新建一个package.josn&-loca.josn文件

```

---

## 知识点

- 路由:

  根据用户请求路径做出相应响应

- NodeJS的开发环境和生产环境:

  在package.json的依赖分别是dependencies(生产依赖)和devDependencies(开发依赖)，

  开发环境一般而言会在代码中部署诸多测试用的代码、警告甚至是库.

  而生产环境追求的是快速化、最小化，这些东西是没必要放到生产环境中的.

  总体来说:  dependencies放运行时需要的依赖  故用npm install 包 -save

  ​	  devDependencies放像打包工具这些 故用npm install 包 -save-dev

- package.json:                                                                                   

  开发项目时首先用package.json描述, 故在项目根目录下用npm init -y                           

  安装第三方包时用package-loca.json文件描述, 故用npm install 包 -save

- POST请求

  post提交数据请求与提交文件请求的区别在于请求报文的请求头的不一样

  ```js
  // 普通post请求报文头 
  Content-Type: application/x-www-form-urlencoded
  // 有文件上传的post请求报文头 
  Content-Type: multipart/form-data; boundary=…--------------165552698916225
  ```

  故处理方式也不一样

  ---

## **Module**

- NodeJS内置模块使用

  直接引入: `Example: const http = require('http') `

- 第三方模块使用

  通过查看第三方模块的使用说明

  ```js
  normal
  npm install packageName
  // js
  const mime = require('mime');
  ```

- 能用require引入的是模块, 用package.json 描述的是包,并且包名内不能含有大写字母

---


### ***http***

用于http服务器与客户端

```js
const server = http.createServer();         		// 创建http服务器; return 实例化的http服务器
server.on("request",(request, response)=>{});  		// 注册请求响应事件
server.listen('8888', '127.0.0.1', (err)=>{})		// 注册监听端口事件
```

#### `request`

服务器解析http请求报文到request对象

- request对象

```js
server.on("request",(request, response)=>{
	request.method				  // 请求方式
	request.httpVersion			  // 客户端http协议版本
	request.headers				 // 请求报文头 =>一个对象
	request.rawHeaders			 // 原生请求报文头 =>一个String数组
	request.url					 // 请求报文行里的请求路径(不包含host)
	request.on("data", ()=>{}) 	  // 请求传递数据事件(会有多次传递)
	request.on("end", ()=>{})	 // 请求结束传递数据事件
});
```
---

#### `response`

服务器通过response对象向客户端发出响应

- response对象

```js
server.on("request",(request, response)=>{
	response.statusCode		// 设置http 响应状态码
	response.statusMessage	// 设置http 响应状态码对应的message
	response.setHeader()	// 设置http 响应报文头(default-不写也有; 复写报错)
	response.writeHead()	// 直接写入http 状态码以及响应报文头
	response.write()		// 设置http 响应正文
	response.end()			// 必写,结束http响应, 可以写入响应正文
}); 

// 设置响应报文跳转页面
response.statusCode = 302;
response.statusMessage = 'FOUND';
response.setHeader('Location', url); // url是要跳转
response.end(); // 响应正文不能是js数据
```

---


### **fs**

`Flie System` 文件系统, 用于操作文件/文件夹

- fs常用 

文件夹

```javascript
const fs = require('fs');

fs.madir(url, callback)				// 新建文件夹
fs.mkdirSync(url)					// 同步新建文件夹

fs.rename(url, newName, callback)	// 重命名文件夹
// 需要有临时路径实现跨磁盘访问 => const form = new multiparty.From({uploadDir: upUrl})
fs.renameSync						// 同步重命名文件夹

fs.rmdir(url, callback)				// 删除文件夹
fs.rmdirSync						// 同步删除文件夹
```

文件

```js
fs.readFile(url, [encoding,default-null], callback)  
// 读, 参数2: encoding,根据字符编码读为string, 不传读为buffer二进制编码

fs.writeFile(url, content[,encoding;default-'utf-8'] ,callback)  // 覆盖写入
fs.appendFile(url, content[,encoding;default-'utf-8'] ,callback) // 追加写入

fs.unlink(url, callback)		// 删除文件 return boolean
```

---


### **path**

用于处理文件与目录的路径

```js
path.join(url, 文件夹/文件名+)	// return 拼接完成路径
path.dirname(url)				// return 当前文件的上级文件夹路径
__filename 						// 当前文件完整绝对路径
__dirname 						// 当前文件的上级文件夹完整绝对路径
```

\__filename及 __dirname不是NodeJS的全局变量, 当运行node程序时nodeJS会将其放入
一个自执行函数(沙盒), f和d被作为函数的参数传入

---


### **url**

用于 URL 处理与解析

```js
const url = require('url');

const urlObj = url.parse(request.url[,parseQueryString[,slashesDenoteHost]])
/* 将请求路径包含信息转为JS对象
 * param2:default-false; true将query部分通过querystring模块的parse()方法解析为JS对象
 * param3:default-false; true将解析hostname, example:{host:127.0.0.1,path:.....}
 * return 一个包含请求数据的JS对象
*/

// 以下路径都不包含host信息 (主机地址,http协议号,端口号)
urlObj.pathname		 // 路径名(不包含get提交数据)
urlObj.path			// 完整路径名(包含get提交数据)
urlObj.query	    // get请求提交数据
```

---

### querystring

用于解析请求路径数据

```js
const querystring = require('querystring');
querystring.parse(urlObj.query); 					// return 将get请求提交数据转换后的JS对象
querystring.unescape(request.url);					// return 解析后的请求路径pathname
```

---

### multiparty-3rdP

用于处理post提交文件请求

```js
const form = new multiparty.From({uploadDir: url}); 
// 传递给form对象的uploadDir一个值, 作为临时路径保证可以跨磁盘访问
from.parse(request, (err, fields, files)={})	// 解析客户端表单提交数据
// 参数2: 表单提交的字段 取值  fields[keys][0] 对应的键是一个数组
// 参数3: 表单提交的文件 取值同 fields
```

---

### **multer**

用于处理form data

---

###mime-3rdP

用于检测文件类型 npm install mime -g 

```js
const mime = require('mime');
mime.getType(文件url) 		// 得到文件的Content-Type
```
---


### ***`express`-3rdP***

基于 NodeJS 平台，快速、开放、极简的 Web 开发框架

#### ***`实例化的app`***

```js

app.use(bodyParser.urlencoded({ extended: false }))	
// http接收post请求时利用bodyParser模块的urlencoded将请求体解析为JS对象

app.use(url, express.static(url))	// 设置请求静态资源时转接的根目录

app.use(url, oneRouter)
// 设置路由中间件; 当请求路径为param1时转接到oneRouter下
// param1: 请求路径
// param2: 转接路由模块

app.use(url, ()=>{})		// 不区分请求方式 且请求路径开头  符合即可
app.all(url, ()=>{})		// 不区别请求方式 但请求路径  必须完全符合

app.get(url, ()=>{})		// 设置接收get请求时的响应
app.post(url, ()=>{})		// 设置接收post请求时的响应

// 用以检测所有包含关键字的请求, 以是否设置 req.session.xxx 检测拦截
app.all("*", (req, res, next) => {	
    // 只要是请求后台就要先检测有没有登录
    if (req.url.includes("studentmanager")) {
        if (req.session.loginedName) {
            next();	// 请求继续
        } else {
            res.send("<script>alert(\"请先登录\");location.href = 					'http://127.0.0.1:8000/account/login'</script>>")
        }
    } else {
        next();
    }
});

app.listen(8888, '127.0.0.1', ()=>{})	// 设置监听端口


// 定义模板引擎
npm install jade -save	// example
app.set('views', url);  // 指定模板文件存放位置

// 设置默认的模板引擎
app.set('view engine', 'jade')  

// 若是需要更改文件后缀名
app.engine('.html', require('jade').__express)
app.set('view engine', 'html')

在指定的模板引擎文件夹下创建 index.jade
使用res.render(index, {}}) 自动替换完成后渲染给浏览器

```

---

####req与res

```js

const express = require('express');
const app = express();
app.post('/index',(request, response)=>{
	request.query 		// 一个包含get请求提交数据的JS对象
	request.body  		// 一个包含post请求提交数据的JS对象
		// 需要使用 app.use(bodyParser.urlencoded({ extended: false }))
    
	response.status() 	// 设置响应报文状态码; return response对象
	response.json()		// 设置响应正文, 转为JSON 参数是arr,或obj, 这时它与response.send()方法一致
	response.send()		// 设置响应正文
	// param: Buffer, arr, obj, str, 根据传递数据的不同自动设置不同的响应头
	response.end()		// 设置响应正文, 只能自动设置Buffer和html 的响应头
    
	response.set()		// 设置响应头
	response.redirect(url)	// 设置跳转, 自动设置状态码302及状态码对应信息FOUND
	response.sendFile(url)		// 读取文件并自动渲染给浏览器
	response.location(url)		// 跳转页面
    
   	// 必须给express设置模板引擎才能使用
	response.render(view [,locals] [,callback]) 
    // param1: 读取文件的路径
    // param2: 读取文件进行模板替换的数据
    // param3: 回调函数有err, content两个参数
});

app.get('index/:year/:mouth/:day', (req, res)=>{
    req.params		//	获取以 /index/2018/11/15形式传参的参数对象
})
```

---

####***`Router路由模块`***

用于express处理请求的分类处理

```js
// 注意: 路由模块一定要用module.exports导出 否则会报错
const express = require('express');
let oneRouter = express.Router();		// 创建路由中间件(路由模块);
oneRouter.get();					 // 设置路由
module.exports = oneRouter; 		// 导出路由模块
module.exposts.fn = () => {}		// 给模块添加一个fn 方法并导出, 可以省略module JS内置
// 服务器入口文件
	const oneRouter = require(url);		// 引入路由中间件
	app.use('/man', manRouter);			// 使用路由中间件
// 使用服务器入口路由还是路由模块由书写顺序决定  (JS是单线程从上到下执行)



// 路由控制器Controller => 路由模块处理请求函数的集合 与express无关, JS内置方法

// 写法
exports.fn1 = (req, res) => {}	// 导出路由控制器模块方法
exports.fn2 = (req, res) => {}
// 用法
const routerControl = require(url);		// 引入
// 路由模块处理请求时
oneRouter.get(url, routerControl.fn1);	// 调用路由控制器方法进行处理
为什么这样做?		个人理解 => 模块化开发
```

---

####express-session-3rdP

```js
const session = require('express-session');
const express = require('express');
const app = express();
// 配置session
app.use(session({
    name: 'connect-sid',    // 返回给客户端session名
    secret: 'session-name', // 服务器生成session的签名
    resave : true,           // 一个请求在另一个请求结束时对session进行修改覆盖并保存，默认值为true
    cookie: {  // 配置cookie
        maxAge: 60*1000,    // cookie的寿命
        httpOnly: true      // 是否允许脚本修改cookie, true可以防止xss 攻击
    }
}));
// 当接受请求时
req.session.xxx = xxx
```

---

### body-parser-3rdP

一般用于express里解析post请求提交数据

```js
const express = require('express');
const bodyParser = require('body-parser');

const app = express(); 					// 利用express模块实例化http服务器
app.use(bodyParser.urlencoded({ extended: false }))
// http接收post请求时利用bodyParser模块的urlencoded将请求体编译为JS对象
request.body  							// 一个包含post请求提交数据的JS对象
```

---

###captchapng-3rdP

用于生成验证码图片

```js
// 使用
/**
 * Captcha PNG img generator
 * @Author: George Chan
 * @Email: gchan@21cn.com
 * @Version: 1.0
 * @Date: 2013-08-18
 * @license http://www.opensource.org/licenses/bsd-license.php BSD License
 */
 
const http = require('http');
const captchapng = require('captchapng');
 
http.createServer(function (request, response) {
    if(request.url == '/captcha.png') {
        var p = new captchapng(80, 30, parseInt(Math.random()*9000+1000)); 
        // 宽, 高, 验证码
        p.color(0, 0, 0, 0);  // 设置背景颜色及透明度 透明度0-255
        p.color(80, 80, 80, 255); // 设置文字颜色及透明度
        var img = p.getBase64();	
        var imgbase64 = new Buffer(img,'base64');
        response.writeHead(200, {
            'Content-Type': 'image/png'
        });
        response.end(imgbase64);
    } else response.end('');
}).listen(8181);
```

---

###*others 3rd Party Module*

```js
date-format

const dataFormat = require('data-format');      // 该实例对象是一个函数
dataFormat('yyyyMMddhhmmssSSS', new Date());    // return 本地时间的数字字符串


util

const util = require('util');
util.inspect(); 	// return 一个字符串形式的JS数据(并不是JSON对象)
```
---

## ***Global***

`全局变量在所有模块中均可使用`

```js
// 以下变量虽然看起来像全局变量，但实际上不是。 它们的作用域只在模块内 
	__dirname
	__filename
	exports
	module
	require()
```

---


### **Class:Buffer**

缓冲用于处理二进制数据

Buffer 类的实例类似于整数数组，但Buffer 的大小是固定的、且在V8 堆外分配物理内存。Buffer 的大小在被创建时确定，且无法调整。

Static method

```js
Buffer.concat(chunkList);			// 拼接chunks(数据块); return 拼接完成的chunks
// chunks必须转为字符串(toString())才能被querystring.parse()解析
```

---

## ***`MongoDB`***

MongoDB是一个基于分布式文件存储的数据库

在JS中操作MongoDB数据库的MongoDB模块基本使用

```js
// 引入操作MongoDB 的模块
const MongoClient = require('mongodb').MongoClient;

// 用于解析数据传输后的_id 以匹配数据库集合中对应_id的数据
const ObjectId = require('mongodb').ObjectId;	// 用法: ObjectId(实例_id) return 集合中_id	

const assert = require('assert'); 	// 用以检测是否报错
// mongoDB的位置
const url = "mongodb://localhost:27017";
// 操作的数据库
const dbName = 'myFirstDB';
// 建立连接
MongoClient.connect(url,  {
    useNewUrlParser: true 	// 解决兼容
  }, (err, client) => {
    let isOK = assert.equal(null, err);		// 判断是否相等没有错误就是null
    let db = client.db(dbName); 		// 获取数据库
    let user = db.collection('user');	// 获取集合
    // 增加
    user.insertOne({name: "boss", age: 20, sex: '男'}, (err, result) => {
    });   	// 增加一项
    user.insertMany([{name: "yihao", age: 18}, {name: 'erhao', age: 17}], (err, result)=> {
	});		//增加多项
    
   	// 修改
    user.updateOne({name:"小弟"}, {$set : {age: 18}}, (err, result)=> {
    }); 	// 修改匹配到的第一个 
    user.updataMany(); 		//修改全部匹配项
    
    // 删除
    user.deleteOne({name: 'chenshuai'}, (err, result) => {
    });		//删除匹配到的第一个
    user.deleteMany();	// 修改全部匹配项
    
    // 查找
    user.find({name: "chenshuai"}).toArray((err, doc) => {
        // doc 以数组形式存储全部匹配项 
        // 查找所有 find({})
    });		// 查找全部匹配项
    user.findOne({name: "chenshuai"}, (err, result) => {
        // result 以对象形式存储一条匹配项
    });
    
    // 模糊查询
    user.find({name: /chen/}).toArray((err, doc) => {
    });
    // 使用正则表达式进行模糊查询
    user.find({name: {$regex: 'chen'}}).toArray((err, doc) => {
    });
    
    client.close(); // 关闭数据库连接
});
```



##***`xtpl`***

NodeJS中常用的模板引擎常用模板引擎

```html
npm install xtpl xtemplate -save
npm install express -save
// 模板语法
<!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
  </head>
  <body>
      <div class="main">
        <div class="header">
        </div>
        {{{ block('content') }}}  // 占位
      </div>
  </body>
  </html>

// 替换模板
{{extend('./views/index.html')}}	// 链入父级模板, 引入链接模板时会自动引入其他模板
  {{#block('content')}}
  	{{#each(students)}}
  		<div class="body teacher-profile">
      		{{this.name}}
  		</div>
  	{{/each}}
  {{/block}}
```

```js
const express = require('express');
const txpl = require('xtpl');
// 自动渲染
app.set('views', config.viewPath);
app.engine('.html', xtpl.__express);
app.set('view engine', 'html');

res.render('index.html', {});


// 手动渲染
const path = require('path');
xtpl.renderFile(path.join(__dirname, ./views/index.html), {}, (err, content) => {
    res.send(content);
})
```

##md5加密

```js
<script src="/js/jquery.min.js"></script>
<script type="text/javascript" src="/js/md5.js"></script>
var password = $.md5($("#passwordId").val() + "HM17NIUBI")
```