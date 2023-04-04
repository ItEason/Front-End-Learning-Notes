### HTML

#### 1.说一下HTML语义化的好处？

> -  提高代码的可阅读性
> -  有利于提高SEO-搜索引擎优化（Search Engine Optimization）
> -  利于页面内容结构化
>
> 常见的语义化标签：main、footer、header、aside、input...

#### 2.如何获取body和html对象？

> 获取body对象：document.body;
>
> 获取HTML对象：document.documentElement;

#### 3. 说一下innerHTML和innerText的区别？

> 相同点：都可以对元素的内容进行读写操作。
>
> element.innerText：从起始位置到最终位置的内容，但去除html标签、空格、换行
>
> element.innerHTML：从起始位置到最终位置的全部内容，包括html标签、空格、换行

#### 4.说一下H5自定义属性data-？

> 在html5中我们可以使用data-xxx设置元素的自定义属性，在javascript中使用dataset.xxx的形式获取元素的自定义属性即可。

#### 5.说一下回流和重绘？

> **回流（重排）：**
>
> 当渲染树中部分或全部元素的尺寸、结构、位置、属性发生变化时，浏览器会重新渲染部分或者全部文档的过程就称为回流。（重排）
>
> 下面这些操作会导致回流：
>
> - 页面的首次渲染
> - 浏览器的窗口大小发生变化
> -  元素的内容发生变化
> -  元素的尺寸或者位置发生变化
> -  元素的字体大小发生变化
> -  激活CSS伪类
> -  查询某些属性或者调用某些方法
> -  添加或者删除可见的DOM元素
>
> **重绘：**
>
> 当页面元素样式改变不影响元素在文档流中的位置时（background-color，border-color，visibility），浏览器只会将新样式赋予元素并进行重新绘制的过程成为重绘。
>
> -  color、background 相关属性：background-color、background-image 等
> -  outline 相关属性：outline-color、outline-width 、text-decoration
> - border-radius、visibility、box-shadow
> - visibility
>
> 注意： 当触发回流时，一定会触发重绘，但是重绘不一定会引发回流。

#### 6.说一下对响应式布局的理解，怎么实现？

> 理解：响应式网站是一种网络页面设计布局，页面的设计与开发应当根据用户行为以及设备环境(系统平台、屏幕尺寸、屏幕定向等)进行相应的响应和调整。

> 1. 百分比布局
> 2. rem布局
> 3. 媒体查询@media screen
> 4. flex布局
> 5. vh和vw布局

#### 7.说一下单页面和多页面的优缺点？

> 单页面：
>
> 优点：页面切换快
>
> 因为页面每次切换时，不需要做HTML文件的请求，减少了http请求
>
> 缺点：首屏加载时间慢，SEO（搜索引擎优化）差
>
> 因为首屏时需要请求`html`，同时还要发送`js`请求，两次请求回来了，首屏才会展示出来。相对于多页应用，首屏时间慢。
>
> SEO效果差，因为搜索引擎只认识`html`里的内容，不认识`js`的内容，而单页应用的内容都是靠`js`渲染生成出来的，搜索引擎不识别这部分内容
>
> 多页面就相反

#### 8.如何解决单页面首屏加载慢问题？

> 进行相应的性能优化操作，如：
>
> - 路由懒加载
> - 代码压缩
> - CDN加速
> - 网路传输压缩
> - SSR服务器渲染

#### 9.说一下H5新增？

> 新增语义化标签：header、section、aside、footer、nav、article
>
> 新增数据存储方法：sessionStorage、localStorage
>
> 新增音频标签audio、新增视频标签video
>
> 新增绘画canvas和svg元素；
>
> 新增input标签的type属性类型：date、time、month、email、url、search、range、color、number；
>
> 新增表单input元素验证：required、pattern；
>
> 新增获取用户地理位置定位API：Geolocation。


#### 10.说一下什么是事件？

> 事件是指用户在浏览器中的各种操作，如点击、鼠标启动、键盘输入等。JavaScript可以通过监听这些事件，响应用户的操作，从而实现交互式的网页效果。

#### 11.块元素和行内元素的区别？常见的块元素和行内元素有哪些？

> 块元素：独占一行，宽度自动填满父元素宽度。能够达到最大宽度且前后各有一个换行。可以包含行内元素和块元素。可以通过css改变宽高。
>
> 行内元素：不会独占一行，其宽度随元素的内容而变化，相邻的行内元素会排列到同一行，直到排列不下才换行，设置margin上下无效，左右有效，padding有效。
>
> 行内元素设置：width、height、padding-top、padding-bottom、margin-top、margin-bottom无效。
>
> 常见的块级元素：div、p、h、ul、li、form...等
>
> 常见的行内元素：a、img、span、li、em、strong...等

#### 12.说一下对web标准和w3c标准的理解？

> web标准主要分为结构、表现、行为3部分
>
> 结构：指我们平时在body里面写的标签，主要由HTML标签组成
>
> 表现：指更加丰富的HTML标签样式，主要由css组成
>
> 行为：指页面和用户的交互，主要由js部分组成
>
> w3c：对web标准提出了规范化的要求，即代码规范
>
> 对结构的要求 
>
> 1、标签字母要小写 
>
> 2、标签要闭合
>
>  3、标签不允许随意嵌套 
>
> 对表现和行为的要求 
>
> 1、建议使用外链CSS和js脚本，实现结构与表现分离、结构与行为分离， 能提高页面的渲染效率，更快地显示网页内容

#### 13.说一下HTML5的新增表单元素？

> HTML5拥有若干涉及表单的`元素`
>
> - detailist：元素规定输入域的选项列表
> - keygen：提供一种验证用户的可靠方法
> - output：output元素用于不同类型的输出
>
> 说明：
>
> - 若想要把`datalist`绑定到某个文本框，需要设置该文本框的`list`属性值等于`datalist`的id的值。
> - `output`元素是一个行内元素，比`span`元素更具有语义化。
>
> 表单type`属性`（验证型）
>
> | 属性值 |   说明   |
> | :----: | :------: |
> | email  | 邮件类型 |
> |  tel   | 电话号码 |
> |  url   | url类型  |
>
> 表单新增type'属性'（取值型）
>
> | 属性   | 说明                 |
> | ------ | -------------------- |
> | range  | 取数字(滑块方式)     |
> | number | 取数字(微调方式)     |
> | color  | 取颜色               |
> | date   | 取日期(如2018-11-11) |
> | month  | 取月份               |
> | week   | 取周数               |
> | time   | 取时间(如08:04)      |
>

#### 14.说一下readonly和disabled的区别？

> 相同点：都能使用户不能修改表单的内容
>
> 不同点：
>
> 1. readonly只对input、textarea有效，但是disabled对所有的表单元素都有效，包括radio、checkbox
> 2. readonly可以获取到焦点，只是不能修改。disabled设置的文本框无法获取焦点
> 3. 如果表单字段是disabled，则该字段不会发送（表单传值）和序列化

#### 15.页面字体在浏览器中应该使用偶数还是奇数？为什么？

> 使用偶数
>
> - 让页面更美观
> - 利于程序员对页面进行开发