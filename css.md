### CSS

#### 1.介绍一下标准的CSS的盒子模型？低版本IE的盒子模型有什么不同？

> 答：CSS3的盒子模型由margin，border，padding，content四部分组成。其中W3C标准盒子模型和低版本IE盒子模型的区别在于width和height所包含的内容不同，css3标准盒模型的width和height只包含了content，而低版本的IE盒子模型width和height包含有border,padding,content。标准盒子模型的box-sizing:content-box，在实际开发中，若要将标准盒子模型转换成IE怪异模型使用box-sizing:border-box即可。

#### 2. CSS选择器有哪些？

```html
<div id="container" class="wrapper-box">
	<span>行内元素</span>
	<p>这是一行段落</p>
	<p>这是一行段落</p>
	<input type="text">
</div>
```

> 答：（1）id选择器  #container
>
> 		（2）类名选择器 .wrraper-box
> 																																							
> 		（3）标签选择器 div / p
> 																																							
> 		（4）子选择器 div > p
> 																																							
> 		（5）后代选择器 div p / #container p / .wrraper-box p	
> 																																							
> 		（6）通配符选择器 * 
> 																																							
> 		（7）伪类选择器  p:nth-child(1) / p:nth-child(2)
> 																																							
> 		（8）伪元素选择器 div::before p::after
> 																																							
> 		（9）兄弟选择器 span~p
> 																																							
> 		（10）相邻选择器 span+p
> 																																							
> 		（11）属性选择器 input[type]
>
> **注意：** 兄弟选择器：找到指定的元素后面的所有满足条件的兄弟元素
>
> 		    相邻选择器：选择紧接在某个元素后的元素，并且二者具有相同的父级元素

#### 3.::before和:after中双冒号和单冒号的区别？解释一下这2个元素的作用。

>答：在css3中使用::双冒号代表伪元素,:单冒号代表伪类，但是在部分浏览器中也可以使用:单冒号来表示伪元素，::before代表将元素内容生成在使用标签之前。`伪类一般匹配的是元素的特殊状态，如hover,visited,link等；伪元素一般匹配的是元素的特殊位置, 如::after, ::before等`。
>
>- ::before就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于dom之中，只存在在页面之中。
>- :before 和 :after 这两个伪元素，是在CSS2.1里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着Web的进化，在CSS3的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after

#### 4.CSS中哪些元素是可以继承的？

> 字体系列属性：font-size，font-family，font-weight，font-style，font
>
> 文本属性：text-indent，text-align，text-shadow，line-height，word-spacing，letter-spacing，color
>
> 光标属性：cursor
>
> 列表属性：list-style，list-style-image，list-style-type，list-style-position
>
> 元素可见性：visibility
>
> border只有border-collapse才能继承

#### 5.CSS选择器优先级？

> !important > 内联选择器 > ID选择器 > 类名选择器/属性选择器/伪类选择器 > 标签选择器/伪元素选择器 > *

#### 6.CSS优先级算法如何计算？

> 答：内联选择器 1，0，0，0
>
> 		ID选择器 0，1，0，0
> 																																							
> 		类名选择器/属性选择器/伪类选择器 0，0，1，0
> 																																							
> 		标签选择器/伪元素选择器 0，0，0，1
>
> 其中！important!important（权重），它没有特殊性值，但它的优先级是最高的，为了方便记忆，可以认为它的特殊性值为1,0,0,0,0。

```css
#container .wrapper-box div {} 则是0，1，1，1
#container #box .wrapper-box div {} 则是0，2，1，1
```

#### 7.关于伪类LVHA的解释？

>答：a标签有四种状态：链接访问前，链接访问后，鼠标滑过，激活，分别对应四种伪类：:link :visited :hover :active
>
>（1）当鼠标滑过a链接时，满足:link和:hover两种状态，要改变a标签的颜色，就必须将:hover伪类在:link伪类后面声明；
>（2）当鼠标点击激活a链接时，同时满足:link、:hover、:active三种状态，要显示a标签激活时的样式（:active），必须将:active声明放到:link和:hover之后。因此得出LVHA这个顺序。

#### 8.CSS3新增伪类有哪些？

> 答：（1）elem:nth-child(n)选中父元素下的第n个子元素，并且这个子元素的标签名为elem，n可以接受具体的数值，也可以接受函数。
>
> （2）elem:nth-last-child(n)作用同上，不过是从后开始查找。
>
> （3）elem:last-child选中最后一个子元素。
>
> （4）elem:only-child如果elem是父元素下唯一的子元素，则选中之。
>
> （5）elem:nth-of-type(n)选中父元素下第n个elem类型元素，n可以接受具体的数值，也可以接受函数。
>
> （6）elem:first-of-type选中父元素下第一个elem类型元素。
>
> （7）elem:last-of-type选中父元素下最后一个elem类型元素。
>
> （8）elem:only-of-type如果父元素下的子元素只有一个elem类型元素，则选中该元素。
>
> （9）elem:empty选中不包含子元素和内容的elem类型元素。
>
> （10）elem:target选择当前活动的elem元素。
>
> （11）:not(elem)选择非elem元素的每个元素。
>
> （12）:enabled 控制表单控件的禁用状态。
>
> （13）:disabled	控制表单控件的禁用状态。
>
> （14）:checked单选框或复选框被选中。

#### 9.如何实现div居中？

> 答：（1）使用margin: 0 auto；实现水平居中。
>
> ​	（2）利用绝对定位，设置四个方向的值都为0，并将margin设置为auto，由于宽高固定，因此对应方向实现平分，可以实现水平和垂直方向上的居中。
> 				
> ​	（3）使用绝对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后再通过margin负值来调整元素的中心点到页面的中心。
> 				
> ​	（4）使用相对定位，先将元素的左上角通过top:50%和left:50%定位到页面的中心，然后通过使用transform：translate(-50%, -50%)，可以实现水平和垂直方向上的居中。
> 				
> ​	（5）使用flex布局，将justify-content：center  align-item：center设置容器的垂直和水平方向上为居中对齐，然后它的子元素也可以实现垂直和水平的居中。
>
> 注意：对于宽高不定的元素，上面的后面两种方法，可以实现元素的垂直和水平的居中。

#### 10.display有哪些值？说明他们的作用。

> block：块类型。默认宽度为父元素的宽度，可设置宽高，换行显示。
>
> inline：行内元素类型。默认宽度为内容宽度，不可设置宽高，同行显示。
>
> inline-block：默认宽度为内容宽度，可以设置宽高，同行显示。
>
> none：元素不显示，并从文档流中移除。
>
> list-item：像块类型元素一样显示，并添加样式列表标记。
>
> table：此元素会作为块级表格来显示。
>
> inherit：	规定应该从父元素继承display属性的值。

#### 11.position 有哪些属性？

>static：静态定位，默认值，元素出现在正常的文档流中。
>
>fixed：固定定位，相对了浏览器窗口进行定位，脱离文档流。
>
>relative：相对对位，是相对于元素本身所在文档流中的位置进行定位的。
>
>absolute：绝对定位，脱离文档流，是相对于它的第一个position值不为static的祖先元素的padding box来进行定位的。
>我们可以这样来理解，我们首先需要找到绝对定位元素的一个position的值不为static的祖先元素，然后相对于这个祖先元素的padding box来定位，也就是说在计算定位距离的时候，padding的值也要算进去。
>
>**注意：**将元素的position设置为relative后，位移量移动的区域还占据着

#### 12.什么是重排？什么是重绘？怎样引起对应的产生？

> **重排（重构/回流/reflow）**：当渲染树中的一部分(或全部)因为元素的规模尺寸，布局，隐藏等改变而需要重新构建, 这就称为回流(**reflow**)。
>
> **重绘（repaint/redraw）**：重绘是指一个元素外观的改变所触发的浏览器行为，浏览器会根据元素的新属性重新绘制，使元素呈现新的外观。
>
> 引起重排
>
> - 页面初始渲染，这是开销最大的一次重排
> - 添加/删除可见的DOM元素
> - 改变元素位置
> - 改变元素尺寸，比如边距（margin）、填充（padding）、边框（border）、宽度和高度等
> - 改变元素内容，比如文字数量，图片大小等
> - 改变元素字体大小
> - 改变浏览器窗口尺寸，比如resize事件发生时
> - 激活CSS伪类（例如：:hover）
> - 通过display：none隐藏一个DOM节点
> - 给页面中的DOM节点添加动画
>
> 引起重绘
>
> - 改变颜色`color`、`background`相关属性
> - 通过`visibility：hidden`隐藏元素
> - 改变`border-style`
> - `border-radius`、`box-shadow`
> - `outline`相关属性

#### 13.display:none 和 visibility：hidden的区别？

>相同点：都可控制元素的显示和隐藏
>
>不同点：display：none脱离文档流，DOM树中消失，会引起重排（回流）和重绘，visibility：hidden占文档流，依旧占据了空间，不会引起重排（回流），会引起重绘。

#### 14.说一下对BFC的了解？

> BFC:块级格式化上下文（block formatting context），一个元素开启了BFC后其内部的元素布局不会影响外部元素的布局，同时外部元素布局也不会影响BFC内部。
>
> 产生BFC的条件：
>
> - overflow属性不为visible
> - position属性不为static和relative
> - display属性为table-cell，inline-block，table-caption
> - float属性不为none
> - 弹性元素（display为flex...）
>
> BFC解决了什么问题？
>
> 1. float引起的父元素高度塌陷
> 2. 清除元素内部浮动
> 3. 解决盒子margin折叠问题

#### 15. 如何清除float浮动？

> 1. 给父元素添加一个高度（注意：高度必须大于等于子元素的最大高度）
> 2. 使用伪元素::after，::before
> 3. 使用BFC特性
> 4. 使用clear:both属性，子元素空白标签使用该属性即可

#### 16.请解释一下CSS3的Flex box（弹性布局）

>flex布局是CSS3新增的一种布局方式，我们可以通过将一个元素的display属性值设置为flex从而使它成为一个flex容器，它的所有子元素都会成为它的弹性元素。设置为flex布局后，其子属性的float，clea和vertical-align无效。
>
>一个容器默认有两条轴，一个是水平的主轴，一个是与主轴垂直的辅轴。我们可以使用flex-direction来指定主轴的方向。我们可以使用justify-content来指定元素在主轴上的排列方式，使用align-items来指定元素在辅轴上的排列方式。还可以使用flex-wrap来规定当一行排列不下时的换行方式。
>
>同时使用align-self属性可以指定该元素的特定排序位置。

#### 17.用纯 CSS 创建一个三角形的原理是什么？

>   采用的是相邻边框连接处的均分原理。
>   将元素的宽高设为0，只设置
>   border，把任意三条边隐藏掉（颜色设为
>   transparent），剩下的就是一个三角形。
>   #demo {
>   width: 0;
>   height: 0;
>   border-width: 20px;
>   border-style: solid;
>   border-color: transparent transparent red transparent;
>   border-top: none;   // 加上这一行可以让三角形顶格， 不加三角形会下移20px
>
>   注意：
>
>   - 取消一条边的时候，与这条边相邻的两条边的接触部分会变成直的
>   - 当仅有邻边时， 两个边会变成对分的三角
>   - 当保留边没有其他接触时，极限情况所有东西都会消失

#### 18.如何实现文本溢出的省略样式？

> 1.单行文本溢出
>
> ```css
> {
>  	white-space: nowrap; // 文字强制不换行
> 	text-overflow: ellipsis; // 文字溢出换省略号
> 	overflow: hidden; // 溢出文字隐藏
> }
> ```
>
> 2.多行文本溢出
>
> ```css
> {
>  word-break: break-all; // 当文本内容为纯数字时需要加上这句属性
>  overflow: hidden;  // 溢出文字隐藏
>  text-overflow: ellipsis; // 文本溢出换省略符号
>  display: -webkit-box;
>  -webkit-line-clamp: 2;
>  -webkit-box-orient: vertical;
> }
> ```

#### 19.CSS3新增特性

> - box-sizing:css3 盒子模型
> - border-radius:圆角边框
> - box-shadow:盒子阴影
> - background-size:背景图片大小
> - transition:过渡
> - transform:转换(位移 旋转 缩放)
> - animation:动画
> - linear-gradient:线性渐变
> - flex布局 
> - 媒体查询多栏布局
> - 字体图标iconfont

#### 20.margin 和 padding 分别适合什么场景使用？

>margin是用来隔开元素与元素的间距；padding是用来隔开元素与内容的间隔。
>margin用于布局分开元素使元素与元素互不相干。
>padding用于元素与内容之间的间隔，让内容（文字）与（包裹）元素之间有一段距离。
>
>何时应当使用margin：
>
>- 需要在border外侧添加空白时。
>- 空白处不需要背景（色）时。
>- 上下相连的两个盒子之间的空白，需要相互抵消时。如15px+20px的margin，将得到20px的空白。
>
>何时应当时用padding：
>
>- 需要在border内测添加空白时。
>- 空白处需要背景（色）时。
>- 上下相连的两个盒子之间的空白，希望等于两者之和时。如15px+20px的padding，将得到35px的空白。

#### 21.px、em、rem、vh、vw分别是什么？

> - px：物理像素，绝对单位
> - em：相对与自身字体大小，如果自身没有设置字体大小会相对于父级字体大小，倘若父级也没有则继续向上寻找，直到找到html为止
> - rem：相对于html的font-size字体大小，相对单位
> - vw：相对于视窗宽度的大小，相对单位
> - vh：相对于视窗高度的大小，相对单位
>
> vw和vh也常用来做移动端适配。

#### 22.在谷歌浏览器中如何实现小于12px的文字？

> 我们知道在谷歌浏览器中，当css设置小于等于12px样式时，页面显示都是12px。解决的方法有：
>
> 1. 可以使用Webkit的内核的-webkit-text-size-adjust的私有CSS属性来解决，只要加了-webkit-text-size
>    -adjust:none;字体大小就不受限制了。但是chrome更新到27版本之后就不可以用了。所以高版chrome谷歌浏览器已经不再支持-webkit-text-size-adjust样式，所以要使用时候慎用。
> 2. 还可以使用css3的transform缩放属性-webkit-transform:scale(0.5);注意-webkit-transform:scale(0.
>    75);收缩的是整个元素的大小，这时候，如果是内联元素，必须要将内联元素转换成块元素，可以使用display：block/inline-block/...。
> 3. 使用图片：如果是内容固定不变情况下，使用将小于12px文字内容切出做图片，这样不影响兼容也不影响美观。

#### 23.你对line-height是如何理解的？

> - 行高是指一行文字的高度，具体说是两行文字间基线的距离。
> - `CSS`中起高度作用的是`height`和`line-height`，没有定义height属性，最终其表现作用一定是line-height。
> - 单行文本垂直居中：把`line-height`值设置为height一样大小的值可以实现单行文字的垂直居中，其实也可以把height删除。
> - 多行文本垂直居中：需要设置`display`属性为`inline-block。`

#### 24.设置一个两行固定中间内容自适应的布局？

```html
<div class="container">
    <div class="left"></div>
    <div class="center"></div>
    <div class="right"></div>
</div>

<style>
    .container {
        display: flex;
        width:100%;
        height:100px;
    }
    
    .left {
        width:100px;
        background:red;
    }
    
    .right {
        width: 200px;
        background: pink;
    }

    .center {
        background: skyblue;
        flex-grow: 1;
    }
</style>
```

#### 25.说一下隐藏元素的方法？

> - display：none （元素在页面消失）
> - opacity： 0 （设置元素透明度为0，元素不可见，存在在页面中）
> - visibility：hidden （元素还存在于页面）
> - position：absolute  z-index：999

#### 26.说一下link和@import的区别？

> 1. link是HTML标签，用于在HTML文档中引入外部CSS文件；而@import是CSS规则，用于在CSS文件中引入其他CSS文件。
> 2. link可以在HTML文档的head部分或body部分引入CSS文件，而@import只能在CSS文件中使用。
> 3. link可以同时引入多个CSS文件，而@import只能引入一个CSS文件。
> 4. link在页面加载时同时加载CSS文件，而@import在页面加载完毕后再加载CSS文件，可能会导致页面闪烁。
> 5. link可以通过rel属性指定CSS文件的关系，如stylesheet、alternate stylesheet等；而@import没有这个属性。

#### 27.说一下引入样式表CSS的方式有几种？分别是什么？优先级是什么？

> 在HTML中引入css样式通常有4种方式。
>
> - 内联样式（行内样式）
> - 嵌入式
> - 外部引入（link）
> - 导入样式@import
>
> 优先级：就近原则
>
> 内联样式（行内样式）>	嵌入式	>	外部样式	> 	导入样式