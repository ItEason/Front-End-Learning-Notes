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
> 当页面元素样式改变不影响元素在文档流中的位置时（background-color，border-color，visibility），浏览器只会将新样式赋予元素并进行重新绘制操作。
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
> 5. vh和vw

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

#### 10.说一下link和@import的区别？

> 1. link是HTML标签，用于在HTML文档中引入外部CSS文件；而@import是CSS规则，用于在CSS文件中引入其他CSS文件。
> 2. link可以在HTML文档的head部分或body部分引入CSS文件，而@import只能在CSS文件中使用。
> 3. link可以同时引入多个CSS文件，而@import只能引入一个CSS文件。
> 4. link在页面加载时同时加载CSS文件，而@import在页面加载完毕后再加载CSS文件，可能会导致页面闪烁。
> 5. link可以通过rel属性指定CSS文件的关系，如stylesheet、alternate stylesheet等；而@import没有这个属性。
>