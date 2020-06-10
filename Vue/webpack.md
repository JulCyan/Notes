# webpack 3.0

全局安装 webpack npm install webpack -g

4.0 以上版本需要 额外配置 npm install webpack-cli -g



##**webpack**

手动打包

​	命令行: webpack 目标文件相对路径 --output 打包结果路径(3.0版本不用 --output)





##**webpack.config.js**

根据配置文件自动打包

```js
module.exports = {
    entry: path 	// 此处path为绝对路径
    output: {
    	path: path,
    	name: "" 	// 打包文件名
	},
    devServer: {}, // 配置 webpack-dev-server
    plugins: [],
    module: {}
}
```

命令行: webpack





##**`webpack-dev-server`**

根据配置文件并监听打包文件变化

​	本地安装 npm install webpack-dev-server -D

​	依赖于本地 webpack, so  npm install webpack -D

​	写好 webpack.config.js 配置文件

​	在 package.json  script 项内添加脚本命令: 

```json
 "dev": "webpack-dev-server --open --port 3000 --contentBase src --hot --mode development"
 	键: 定义快捷启用指令名
 	param1: 需要使用的命令
 	param2: --open 自动打开url
 	parma3: --port xxxx 指定端口号 (默认8080)
 	parma4: --contentBase xxx 指定打开的目录 (默认是根目录)
 	param5: --hot 实现补丁打包以及页面无刷新重载 => 热更新

	※※: 
	param6: --mode 选择模式, 自动相应模式的配置
		development(开发模式) 针对速度进行了优化，仅仅提供了一种不压缩的 bundle
		production(生产模式) 可以开箱即用地进行各种优化, 包括压缩，作用域提升，tree-shaking 等
```

​	运行: npm run dev

由 webpack-dev-server 打包的文件, 并没有存在本地, 而是存在内存中

如需访问则直接在 localhost 根目录下 /文件名进行访问

​	



##**html-webpack-plugin**

cnpm install html-webpack-plugin -D

1: 将本地物理磁盘中指定的文件生成在内存中

2: 自动引用打包好的文件

```js
const htmlWebpackplugin = require("html-webpack-plugin");

modul.exports = {
	plugins: [
        new htmlWebpackplugin({
            path: '', // 需要转换的文件路径
            filename: '' // 转换后的文件名
        })
	]
}
```





##**loader**

加载器

webpack 默认只能打包 js 文件, 如果要打包其他后缀的文件需要使用第三方加载器

以 .css 为例

首先安装 npm install style-loader css-loader -D 两个第三方加载器

然后在 webpack.config.js 配置文件中

```js
module.exports = {
    // 在导出配置文件 module 配置节点的 rules 属性上配置打包规则
    module: {
        rules: [
            { test: /\.css$/, use: ['style-loader', 'css-loader']};
            // test: 匹配规则
            // use: 匹配成功后使用的加载器
            // 加载器的调用顺序是从后向前
        ]
    }
}
```



.less(css) => less-loader, 还需要下载 less到本地开发依赖, 但无需在 config 里配置



.scss/.sass(css) => sass-loader 还需要下载 node-sass



.jpg/.png/.gif/.bmp/.jpeg(image) => url-loader 追加?键值对配置, 与url无异

limit: byte, 大于或等于配置值的图片不会被转为base64格式

name: String, 指定转换的文件名 [hash:8]-[name].[ext] => hash值-文件原名-原后缀名



.ttf/.eot/.svg/.woff/.woff2(iconfont) => url-loader





### babel-loader@8+

ES6高级/ES7 => babel-loader

cnpm install babel-loader @babel/core @babel/plugin-transform-runtime @babel/preset-env -D

```js
rules: [
    { test: /\.js$/, use: "babel-loader", exclude: /node_modules/ }
    // exclude: 排除项
    // why? 编译多余已打包好的js文件浪费性能且 转换后也是不可用的
]
```

项目根目录下新建 .babelrc 文件, 格式为JSON(JSON文件不能有注释)

```json
{
  "presets": ["@babel/preset-env"], // 配置编译语法, 高级语法与低级语法的对应关系
  "plugins": ["@babel/plugin-transform-runtime"] // 配置编译使用的插件
}
```



### vue-loader

.vue => cnpm i vue-loader vue-template-compiler -D

```js
// webpack.config.js
module: {
    rules: [
        { test: /\.vue$/, use: "vue-loader" }
    ]
}
```

```js
// 在 webpack.config.js 中
const VueLoaderPlugin = require('vue-loader/lib/plugin');
module.exports = {
    pulgins: [
        new VueLoaderPlugin();
    ]
}
```

### url-loader

1. 文件 byte 小于limit 参数，url-loader将会把文件转为 DataURL

2. 文件 byte 大于limit 参数，url-loader会调用file-loader进行处理，参数也会直接传给 file-loader

   context: 基本目录，一个**绝对路径**，用于从配置中解析入口点和加载器, 默认当前目录

   在 webpack.config.js 进行配置

```js
rules: [
    { test: "\.(png|jpg|gif)$/", use: [
        {
            loader: "url-loader",
            options: {
                limit: 7621,
                name: "[path][name].[ext]",
                // or
                name (file) {
                    // 如果是开发模式返回相对于 context 路径的原文件名
                    if (env === 'development') {
                        return '[path][name].[ext]'
                    }
      				return '[hash].[ext]'
                },
                // 不写 publicPath 情况下默认用输出路径, 写了两者要保持一致或与资源原名原路径相同
                publicPath: "文件引用路径", // 相对 contentPath
                outputPath: "文件输出目录",// 路径最后要加 /
                // outputPath: "/" 原资源引用
                useRelativePath: "生成相对context 的url, bool;default: false",
            }
          }
    ]}
]
```

\[hash\]: `[<hashType>:hash:<digestType>:<length>]`

hashType:   {String}	md5	sha1, md5, sha256, sha512;

digestType: {String}	base64  hex, base62, base64...

length:     {Number}	9999    字符串的长度











# webpack 4.0

***`零配置工具`***

npm i webpack webpack-cli -D

packag.json 内 script 配置 webpack or webpack-dev-server

```json
"script": {
    "build": "webpack"
}
```

无需配置 webpack.config.js

why? => 使用零配置工具可以加快速度

零配置只包括 mode, entry, output

自动查找 `./src/index.js` 作为默认入口点。 而且，它会在 `./dist/main.js` 中输出模块包

关于 webpack-dev-server 配置见上, 其中 --mode 配置项 是 webpack 4.0 中新增的

### 将 CSS 提取到一个文件中

1. npm i mini-css-extract-plugin css-loader -D

2. webpack.config.js

```js
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

plugins: [
    new MiniCssExtractPlugin({
      filename: "[name].css",
      chunkFilename: "[id].css"
    })
  ]
```





### HTML webpack 插件

1. npm i html-webpack-plugin html-loader -D

```js
const HtmlWebPackPlugin = require("html-webpack-plugin");

rules: [{
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      }]
plugins: [
    new HtmlWebPackPlugin({
      template: "./src/index.html",
      filename: "./index.html"
    })
  ]
```








### 移除webpack打包bundle.js使用严格模式

npm install babel-plugin-transform-remove-strict-mode -D

```json
{
  "plugins": ["transform-remove-strict-mode"]
}
```





