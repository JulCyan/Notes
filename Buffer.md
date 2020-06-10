

# Buffer 

思考：Buffer 类型产生的原因？主要用来解决什么问题？

看一下什么是 Buffer? 什么是 Stream?


一、类型介绍

1. JavaScript 语言没有读取或操作二进制数据流的机制。
2. Node.js 中引入了 Buffer 类型使我们可以操作 TCP流 或 文件流。
3. Buffer 类型的对象类似于整数数组，但 Buffer 的大小是固定的、且在 V8 堆外分配物理内存。 Buffer 的大小在被创建时确定，且无法调整。（ buf.length 是固定的，不允许修改 ）
4. Buffer 是全局的，所以使用的时候无需 require() 的方式来加载


二、如何创建一个 Buffer 对象


常见的 API 介绍

1. 创建一个 Buffer 对象

```javascript
// 1. 通过 Buffer.from() 创建一个 Buffer 对象

// 1.1 通过一个字节数组来创建一个 Buffer 对象
var array = [0x68, 0x65, 0x6c, 0x6c, 0x6f, 0x20, 0xe4, 0xb8, 0x96, 0xe7, 0x95, 0x8c];
var buf = Buffer.from(array);
console.log(buf.toString('utf8'));

// 1.2 通过字符串来创建一个 Buffer 对象
// Buffer.from(string[, encoding])
var buf = Buffer.from('你好世界！ Hello World!~');
console.log(buf);
console.log(buf.toString());

```


2. 拼接多个 Buffer 对象为一个对象

```javascript
// Buffer.concat(list[, totalLength])
var bufferList = [];
var buf = Buffer.concat(bufferList);
```


3. 获取字符串对应的字节个数

```javascript
// Buffer.byteLength(string[, encoding])

var len = Buffer.byteLength('你好世界Hello', 'utf8');
console.log(len);
```

4. 判断一个对象是否是 Buffer 类型对象

```javascript
// Buffer.isBuffer(obj)
// obj <Object>
// Returns: <boolean>
// Returns true if obj is a Buffer, false otherwise.

```


5. 获取 Buffer 中的某个字节

```javascript
// 根据索引获取 Buffer 中的某个字节（byte、octet）
// buf[index]

```


6、获取 Buffer 对象中的字节的个数

```javascript
// buf.length
// 注意：length 属性不可修改
```



7. 已过时的 API

```javascript
// 以下 API 已全部过时
new Buffer(array)
new Buffer(buffer)
new Buffer(arrayBuffer[, byteOffset [, length]])
new Buffer(size)
new Buffer(string[, encoding])

```




三、Buffer 对象与编码

Node.js 目前支持的编码如下：

1. ascii
2. utf8
3. utf16le
  - ucs2 是 utf16le 的别名 
4. base64
5. latin1
  - binary 是 latin1 的别名
6. hex
  - 用两位 16 进制来表示每个字节



示例代码：

```javascript

var buf = Buffer.from('你好世界，Hello World！', 'utf8');

console.log(buf.toString('hex'));
console.log(buf.toString('base64'));
console.log(buf.toString('utf8'));
```





四、思考：为什么会有 Buffer 类型？

1. Buffer 使用来临时存储一些数据（二进制数据）
2. 当我们要把一大块数据从一个地方传输到另外一个地方的时候可以通过 Buffer 对象进行传输
3. 通过 Buffer 每次可以传输小部分数据，直到所有数据都传输完毕。



五、补充

1. Stream

2. Writable Stream
  - 允许 node.js 写数据到流中

3. Readable Stream
  - 允许 node.js 从流中读取数据


