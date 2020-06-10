## Vue CLI 3

替换 loader

```js
module.exports = {
  // 使用webpack-chain 进行链式操作
  chainWebpack: config => { // config 就是原配置对象
    const svgRule = config.module.rule('svg')

    // 清除已有的所有 loader。
    // 如果你不这样做，接下来的 loader 会附加在该规则现有的 loader 之后
    svgRule.uses.clear()

    // 添加要替换的 loader
    svgRule
      .use('vue-svg-loader')
        .loader('vue-svg-loader')
  }
}
```