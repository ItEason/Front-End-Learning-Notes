# Node.js

## 前言

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;❤这是我第三次对node.js进行学习，第一次是在校的大二下学期，因为自己能力的局限性，在B站看完全部教学视频自己也有使用node.js写api接口，所掌握的知识点十分有限。第二次是大二的暑假对node.js进行了二刷，对知识的理解也比第一次更深刻。这次是笔者大三下学期，此时的我已经在公司里实习了，因为项目中的服务器端使用的就是node.js，导师也分配了一些设计api接口的任务。因此借五一假期进行三刷，同时写下本编文章，记录自己的学习路程。最后，祝自己能找到一份理想工作。❤




&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;随着时代的发展，前端程序员必备的开发知识也不仅局限于HTML、CSS、Javascript、前端框架等了。node.js也成为了一项必备的技能之一，相信接触过招聘网站的同学都知道，十个前端岗位要求中，超过一半是需要具备服务器端开发语言的，其中node.js就属于其中，其必要性可想而知。

## Node是什么？

​		以下是对node.js官网的一句原话。翻译过来的意思就是：Node.js是一个开源的，跨平台的JavaScript运行环境。通俗点来说：Node.js就是一款应用程序，是一款软件，它可以运行JavaScript。

> Node.js@ is an open-source, cross-platform JavaScript runtime enviroment.

![image-20230429174035417](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230429174035417.png)

## Node的应用？

- 开发服务器应用
  - 静态页面访问
- 开发工具类应用
  - Vite
  - Webpack
  - Babel
- 开发桌面端应用
  - vsCode
  - postman
  - Figma

![image-20230429174801730](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230429174801730.png)

`注意:`在node.js中是不能操作DOM和BOM的，因为node.js中的JavaScript组成部分是由ECMAScript组成和Node API组成，JavaScript则是由ECAMScript、Web API组成，要注意区分二者的区别。

小结

1. Node.js中不能使用BOM和DOM的API，可以使用console和定时器API
2. Nod.js中的顶级对象为global，也可以使用globalThis访问顶级对象

## Buffer

> Buffer 中文译为[缓冲区]，是一个类似于 Array 的对象，用于表示固定长度的字节序列
>
> 换句话说，Buffer 就是一段固定长度的内存空间，用于处理二进制数据

![image-20230429191544977](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230429191544977.png)

创建

> buffer的创建有三种方式，分别为alloc、allocUnsafe、from

```js
// 1. alloc
let buf = Buffer.alloc(10);
console.log(buf); // <Buffer 00 00 00 00 00 00 00 00 00 00>

// 2.allocUnsafe 可能会包含旧的内存数据，速度相比alloc较快些
let buf2 = Buffer.allocUnsafe(10);
console.log(buf); // <Buffer 00 00 00 00 00 00 00 00 00 00>

// 3. from 该方法会将参数转化为对应的Unicode(ASCII)
let buf3 = Buffer.from("hello");
console.log(buf3) // <Buffer 68 65 6c 6c 6f>
```

 转换

> Buffer的可阅读性没有那么强，我们可以使用toString()方法的调用来将数据Buffer流转换为字符串，提高可阅读性。

```js
let buf = Buffer.from("hello");

let str = buf.toString(); // hello
```

 修改

> 在buffer中可以使用访问数据元素的方式进行buffer对应下标的数据访问，如buffer[0]、buffer[1]、buffer[2]...，也可以使用赋值的方式进行修改buffer[0] = 98(Unicode)

```js
let buffer = Buffer.from('hello')
console.log(buffer) // <Buffer 68 65 6c 6c 6f>

// 修改buffer[0]
buffer[0] = 95;
console.log(buffer) // <Buffer 5f 65 6c 6c 6f>
```

 溢出

> 计算机中8个字位的二进制存储只能存储十进制的255，即最大十进制数据就是255，超过后就会溢出。在buffer中，当二进制溢出时会舍弃最高位的数字。举个例子：buffer[0] = 361 361转换位二进制为：0001 0110 1001，因为只能存储八位因此存储的结果为0110 1001。

中文

> 在buffer中，一个中文占3个字节

```js
let buf = Buffer.from('你好');

console.log(buf); // <Buffer e4 bd a0 e5 a5 bd>
```

## fs模块

> file system：fs模块可以实现与硬盘的交互，例如：文件的创建、删除、重命名、移动，还有文件内容的写入、读取，以及文件夹的相关操作。
>
> 在node.js中，我们可以使用require的方式将`fs`模块导入。

 写入

| 方法              | 说明     |
| ----------------- | -------- |
| writeFile         | 异步写入 |
| writeFileSync     | 同步写入 |
| createWriteStream | 流式写入 |

> 在`fs`模块中有一个writeFile（异步）/ writeFileSync（同步）方法，可以创建文件并写入内容。

```tsx
/*
* fs.writeFile(File, data[, option],callback)
* @param: file 文件名（必选）
* @param: data 待写入的内容（必须）
* @param: option 选项配置（可选），表示以什么格式方式写入文件，默认值是utf8
* @param：callback 回调函数（必选）
*/
const fs = require('fs')

fs.writeFile('../files/write.txt', '写入内容', (err, data) => {
    if (err) {
        console.log('写入文件失败' + err.message);
        return;
    }
    console.log(data);
    return;
})
```

> 文件的写入还有第二种方式就是使用<font color=red>createWriteStream</font>流式写入，<font color=orange>`程序打开一个文件是需要消耗资源的`</font>,流式写入可以减少打开关闭文件的次数。流式写入方式适用于<font color=orange>大文件写入或者频繁写入</font>的场景，而<font color=red>writeFile</font>适合于<font color=orange>写入频繁较低的场景</font>

```js
const fs = require('fs');

const ws = fs.createWriteStream('../files/观书有感.txt');

ws.write('半亩方塘一鉴开\r\n');
ws.write('天光云影共徘徊\r\n');
ws.write('问渠那得清如许\r\n');
ws.write('为有源头活水来\r\n');

ws.close();
```

文件写入的场景：

- 下载文件
- 安装软件
- 保存程序日志，如Git
- 编辑器保存文件
- 视频录制

> 当<font color=orange>需要持久化保存数据</font>的时候，应该想到<font color=orange>文件写入</font>。

 追加

> 在`fs`模块中有一个appendFile（异步） / appendFileSync（同步）方法，可以创建文件并追加内容

```tsx
/*
* fs.appendFile(path, data[, option],callback)
* @param: path 文件路径（必选）
* @param: data 待写入的内容（必须）
* @param: option 选项配置（可选），表示以什么格式方式写入文件，默认值是utf8
* @param：callback 回调函数（必选）
* return: undefined
*/
const fs = require('fs');

fs.appendFile('../files/write.txt', "\r\n我是追加的内容", (err, res) => {
    if (err) {
        return console.log('错误', err.message)
    }
    console.log(res);
    return;
})
```

 读取

| 方法             | 说明     |
| ---------------- | -------- |
| readFile         | 异步读取 |
| readFileSync     | 同步读取 |
| createReadStream | 流式读取 |

> 在`fs`模块中有一个readFile（异步）/ readFileSync（同步）方法，可以读取文件内容。

```js
/* 	readFile(path[, option], callback)
*  @param: path（必选） 文件路径
*  @param：option（可选） 读取文件的编码格式
*  @param：callback（必选）回调函数
*  return: undefined
*/
const fs = require('fs')

// 异步读取
fs.readFile('../结项总结.txt', 'utf8', (err, data) => {
    if (err) {
        console.log('读取文件失败!' + err.message);
        return
    }
    console.log('读取文件成功！' + data);
    return
})

// 同步读取
let data = fs.readFileSync('../结项总结.txt');
console.log(data.toString());

// 创建流式读取对象
const rs = fs.createReadStream(path);

// 绑定data事件，chunk
rs.on('data', chunk => {
    console.log(chunk);
})

// end 可选事件，当数据读取结束后自动执行
rs.on('end', ()=> {
    console.log('读取完成');
})

```

文件读取的场景：

- 电脑开机
- 程序运行
- 编辑器打开文件
- 查看图片
- 播放视频...

 移动

> 在Node.js中，我们可以使用<font color=orange>rename</font>或者<font color=orange>renameSync</font>来移动或者重命名<font color=orange>文件或者文件夹</font>
>
> 语法：
>
> <font color=orange>fs.rename(oldPath, newPath, callback)</font>
>
> <font color=orange>fs.renameSync(oldPath, newPath)</font>
>
> 参数说明：
>
> - oldPath：文件当前的额路径
> - newPath：文件新的路径
> - callback：操作后的回调函数

```js
const fs = require('fs');

// rename方法
fs.rename('../files/观书有感.txt', './观书有感.txt', err => {
    if (err) return console.log(err.message);
    console.log("重命名成功!");
})

// renameSync方法
fs.renameSync('./观书有感.txt', '../files/观书有感.txt');
```

 删除

> 在Node.js中，我们可以使用<font color=orange>unlink</font>或者<font color=orange>unlinkSync</font>来删除文件
>
> 语法：
>
> <font color=orange>fs.unlink(path, callback)</font>
>
> <font color=orange>fs.unlinkSync(path)</font>
>
> 参数说明：
>
> - path：文件路径
> - callback：操作后的回调

```js
const fs = require('fs');

// unlink
fs.unlink('../files/test.txt', err => {
    if (err) return console.log(err.message);

    console.log("文件删除成功...");
})

// unlinkSync
fs.unlink('../files/test.txt');
```

 操作文件夹

> 在node.js中，我们以对文件夹进行以下的操作

| 方法                  | 说明       |
| --------------------- | ---------- |
| mkdir / mkdirSync     | 创建文件夹 |
| readdir / readdirSync | 读取文件夹 |
| rmdir / rmdirSync     | 删除文件夹 |

<font color=orange>创建</font>

> 在Node.js中，我们可以使用<font color=orange>mkdir</font>或者<font color=orange>mkdirSync</font>来创建文件夹
>
> 语法：
>
> <font color=orange>fs.mkdir(path[, option], callback)</font>
>
> <font color=orange>fs.mkdirSync(path[, option])</font>
>
> 参数说明：
>
> - path：文件夹路径
> - option：选项配置（可选）
> - callback：操作后的回调

其中：当我们需要将`path`进行递归生成子目录时，可以在`option`中添加`{recursive：true}`

<font color=orange>读取</font>

在Node.js中，我们可以使用<font color=orange>mkdir</font>或者<font color=orange>mkdirSync</font>来创建文件夹

语法：

<font color=orange>fs.readdir(path[, option], callback)</font>

<font color=orange>fs.readdirSync(path[, option])</font>

参数说明：

- path：文件夹路径
- option：选项配置（可选）
- callback：操作后的回调

<font color=orange>删除</font>

在Node.js中，我们可以使用<font color=orange>mkdir</font>或者<font color=orange>mkdirSync</font>来创建文件夹

语法：

<font color=orange>fs.rmdir(path[, option], callback)</font>

<font color=orange>fs.rmdirSync(path[, option])</font>

参数说明：

- path：文件夹路径
- option：选项配置（可选）
- callback：操作后的回调

其中：当我们需要将`path`进行递归删除子目录时，可以在`option`中添加`{recursive：true}`，但是node环境会提示使用<font color=orange>fs.rm()</font>。

## path模块

> path模块提供了<font color=orange>操作路径</font>的功能，我们将介绍如下几个较为常用的几个API：

| API           | 说明                     |
| ------------- | ------------------------ |
| path.resolve  | 拼接规范的绝对路径       |
| path.sep      | 获取操作系统的路径分隔符 |
| path.parse    | 解析路径并返回对象       |
| path.basename | 获取路径的基础名称       |
| path.dirname  | 获取路径的目录名         |
| path.extname  | 获取路径的扩展名         |

## HTTP协议

> http协议的默认端口是8。

![image-20230430150053838](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230430150053838.png)

### 请求报文

> 请求报文由三部分组成，分别是<font color=orange>请求行、</font><font color=orange>请求头、</font><font color=orange>请求体</font>。其中请求头和请求体间有`空行`隔开。

![image-20230430151542279](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230430151542279.png)

请求行

> 请求行主要由三部分组成<font color=orange>请求方式、</font><font color=orange>请求地址（url）、</font><font color=orange>HTTP版本号。</font>

![image-20230430151949436](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230430151949436.png)

> 请求方法：

| 方法                             | 作用             |
| -------------------------------- | ---------------- |
| GET                              | 主要用于获取数据 |
| POST                             | 主要用于新增数据 |
| PUT / PATCH                      | 主要用于更新数据 |
| DELETE                           | 主要用于删除数据 |
| HEAD / OPTIONS / CONNECT / TRACE | 使用相对较少     |

> url（Uniform Resource Locator）：统一资源定位符，本身也是一个字符串。

![image-20230430152724162](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230430152724162.png)

> HTTP版本

| 版本号 | 发布时间 |
| ------ | -------- |
| 1.0    | 1996年   |
| 1.1    | 1999年   |
| 2      | 2015年   |
| 3      | 2018年   |

请求头

> 请求头都是以`键值对`的形式出现的，记录了浏览器的一些相关信息。

请求体

> 请求体的内容由开发者决定，多个请求内容由&连接。

### 响应报文

> 响应报文主要由三部分组成：<font color=orange>响应行、</font><font color=orange>响应头、</font><font color=orange>响应体。</font>我们可以观察到`请求报文`和`响应报文`的组成结构都是大同小异的。

![响应报文](E:\node图片\响应报文.png)

> 响应行：主要由<font color=orange>HTTP版本号、</font><font color=orange>响应状态码、</font><font color=orange>状态码含义</font>组成。

以下是比较常见的响应状态码和状态码含义：

![image-20230430163707926](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230430163707926.png)

![image-20230430163721761](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230430163721761.png)

### IP地址

> IP本质上是一个`32bit`的`二进制字`符串，将`每8bit`进行拆分，得到`IPV4`的形式的`十进制`字符串，同时使用`.`进行分割，这样就形成了日常我们所接触到的ip形式。

![image-20230501092708846](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230501092708846.png)

## HTTP模块

> 在Node.js中，可以使用引入http模块的方式来创建一个本地服务器。
>
> 注意：
>
> - 在使用http模块时，响应体需要返回中文，但没有设置对应的header时，浏览器收到的数据会乱码

<font color=black>创建</font>

```js
// 1.导入http模块
const http = require('http');
const path = require("path")

// 2.调用createServer，创建http实例
const server = http.createServer((request, response) => {
    // request：请求报文 、 response：响应报文
});

// 3.使用on方法为http实例绑定request事件
server.on('request', (req, res) => {
    res.setHeader('Content-Type', 'text/html;charset=utf-8')
    let url = req.url
    switch (url) {
        case '/api': res.end(JSON.stringify({
            method: req.method,
            msg: "请求成功",
            status: 200,
        }))
            break;

        default:
            res.end("404")  
            break;
    }
    // 3.1 设置响应头，解决中文乱码问题
    res.setHeader('Content-Type', 'text/html;charset=utf-8');
})

// 4.开启服务器
server.listen(8080, () => {
    console.log("serve running");
})
```

<font color=black>获取请求头</font>

> 想要获取请求的数据，需要通过<font color=orange>request</font>对象。

| 含义          | 语法                                                         | 重点掌握 |
| ------------- | ------------------------------------------------------------ | -------- |
| 请求方法      | request.method                                               | *        |
| 请求版本      | request.httpVersion                                          |          |
| 请求路径      | request.url                                                  | *        |
| URL路径       | require("url").parse(request.url).pathname                   | *        |
| URL查询字符串 | require("url").parse(request.url, true).query                | *        |
| 请求头        | request.headers                                              | *        |
| 请求体        | request.on("data", chunk => {})<br />request.on("end", ()=>{}) |          |

> 注意事项：
>
> 1. request.url只能获取路径以及查询字符串，无法获取URL中的域名以及协议的内容
> 2. request.headers将请求信息转化为一个对象，并将对象的属性名都转化为了[小写]
> 3. 关于路径：如果访问网站的时候，只填写了IP地址或者域名信息，此时请求的路径为[/]
> 4. 关于favicon.ico：这个请求是属于浏览器自动发送的请求
