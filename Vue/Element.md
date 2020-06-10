# Element





## Quick Start

npm i element-ui -S



### 完整引入

import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'

Vue.use(ElementUI)



### 按需引入

npm install babel-plugin-component -D



.babelrc

```
  "plugins": [
    [
      "component",
      {
        "libraryName": "element-ui",
        "styleLibraryName": "theme-chalk"
      }
    ]
  ]
```

import { Button, Select } from 'element-ui'



Vue.component(Button.name, Button)
Vue.component(Select.name, Select)



or



Vue.use(Button)
Vue.use(Select)





### this.$createElement

创建HTML元素

```js
const h = this.$createElement					  // 引入构造函数
h('i', { style: 'color: teal'}, '这是HTML片段')		// 构建实例
/**
* @param1: 标签名
* @param2: 样式(对象)
* @param3: text 或数组, 数组内是 h 构建的实例
*/
```







## Basic

### Layout 布局

























































































































## Notice



### Alert 警告

http://element-cn.eleme.io/#/zh-CN/component/alert

import { Alert } from "element-ui"

Vue.use(Alert)

```html
<el-alert
    title="成功提示的文案"
    type="success" 						// 信息类型
    description="文字说明(自动换行)"
    center								// 居中显示
    :closable="false					// 是否可关闭, default: true
    show-icon							// 展示类型图标
    close-text="知道了"				  // 自定义关闭文字
    @close="hello"						// 关闭钩子函数
    >
  </el-alert>
```







### Message 消息提示

http://element-cn.eleme.io/#/zh-CN/component/message

import { Message } from "element-ui"

Vue.prototype.$message = Message

与 Notification 相似










### MessageBox 弹框

http://element-cn.eleme.io/#/zh-CN/component/message-box









### Loading 加载

http://element-cn.eleme.io/#/zh-CN/component/loading

import { Loading } from "element-ui"

Vue.use(Loading.directive)



v-loading = "boolean" 指令  `开关改变 boolean 值即可`

default: Loading 遮罩会插入到绑定元素的子节点



行内参数设置

```html
element-loading-text="拼命加载中"			// 设置遮罩层下方内容
element-loading-spinner="el-icon-loading" 	// 设置图标类名 
element-loading-background="rgba(0, 0, 0, 0.8)" // 设置背景色
```



全屏

v-loading.fullscreen.lock= "boolean"

指令修饰符 lock 锁定屏幕滚动



Vue.prototype.$loading = Loading.service

还可以通过钩子函数形式(`服务方式`)

```js
	openFullScreen() {
        const loading = this.$loading({
          lock: true,
          text: 'Loading',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)',
          customClass: '' 					// Loading 的自定义样式类名
        });
        setTimeout(() => {
          loading.close();
        }, 2000);
      }
```

当使用服务方式时，遮罩默认即为全屏，无需额外设置

另一种方式(引入但未给 Vue 原型注册的方法): Loading.service(options);







### Notification 通知

http://element-cn.eleme.io/#/zh-CN/component/notification

import { Notification } from 'element-ui'

Vue.prototype.$notify = Notification



```js
const h = this.$createElement

const notify1 = this.$notify.info({ 
    // .info 通过调用方法的方式来进行 type 的设置
	title: '标题名称',
	message: h('i', { style: 'color: teal'}, '这是提示文案'),
    
    duration: 0,				// 自动关闭时间, default: 4500ms, 为0时不会自动关闭
    type: 'success',			// 通知类型, default: 无, 共四种: warning, error
    position: 'bottom-right', 	 // 弹出位置, default: top-right
    offset: 100				    // 设置偏移值, 距离屏幕 px 值
    dangerouslyUseHTMLString: true, // 设置为true时, 会将 message 作为 HTML片段 处理
    showClose: false				// 隐藏关闭按钮, default: true
});

notify1.close() 		// 调用方法关闭
```











