### javaScript

#### 1.说一下javaScript数据类型？基本数据类型和引用数据类型的区别是什么？

> javascript数据类型分为基本数据类型和引用数据类型，基本数据类型有7种，分别是Number、String、Undefined、Null、Boolean、Symbol、BigInt；引用数据类型有Object、Array、Date、Functiond，Rexp等。
>
> 基本数据类型和引用数据类型的区别是：存储方式的不同，基本数据类型的存储在栈内存中，而引用数据类型的存储在堆内存中，栈内存存储的是堆内存指针起始地址。

#### 2.说一下javascript有几种判断数据类型的方法？

> 1. typeof：判断基本数据类型，引用数据类型只能判断function，其余全部返回object；
> 2. instanceof：主要用于引用数据类型的判断，是根据原型链进行判断的，输出的是true or false；
> 3. constructor：不能判断undefined和null，输出的是true or false；
> 4. Object.prototype.toString.call()：可以判断任何数据类型，输出的形式是[object '数据类型']

```js
console.log(typeof null); // object
console.log((9).constructor === Number); // true
console.log(obj instanceof Object); // true
console.log(Object.prototype.toString.call(obj)); // [object Object]
```

#### 3.说一下cookie、localStorage、sessionStorage的区别？

> 相同点：都是存储在浏览器本地的
>
> 不同点：
>
> 1. 存储位置：cookie由服务端写入，而localStorage、sessionStorage由前端写入
> 2. 声明周期：cookie在服务器端写入后的时候就设置好了，localStorage写入就一直存在，除非手动清除，sessionStorage在页面关闭时就自动清除
> 3. 存储大小：cookie的存储空间大概4KB，localStorage、sessionStorage的存储空间比较大，大概在5M
> 4. 数据共享：Cookie、sessionStorage、 localStorage数据共享都遵循同源原则，sessionStorage还限制必须是同一个页面。在前端给后端发送请求的时候会自动携带Cookie中的数据，但是sessionStorage、 localStorage不会
> 5. 应用场景：cookie用于存储验证信息SessionID或者token，localStorage常用于存储不易变动的数据，减轻服务器的压力，sessionStorage可以用来检测用户是否是刷新进入页面，如音乐播放器恢复播放进度条的功能。
>
> **注意**：cookie只用在https协议中才会传输，在http协议是不会传输的。

#### 4.说一下闭包？

> 闭包就是：能够读取其他函数内部变量的函数
>
> 好处：
>
> 1. 可以读取其他函数的内部变量
> 2. 将变量始终保存在内存中
> 3. 可以封装对象的私有属性和方法
>
> 坏处：消耗内存、使用不当会造成内存溢出问题

```js
function outer() {
    let a = 10;
    function fn() {
        return a;
    }

    return fn();
}

outer(); // 返回结果为10；
```



#### 5.说一下promise是什么与使用方法？

> 1.概念：promise是异步编程的一种解决方案，解决了回调地狱问题。promise由三种状态：pending（进行中）fulfilled（成功）rejected（失败）
>
> 2.使用方法：promise参数接收一个函数，函数接收两个回调函数，分别是resolve,reject,函数体内可以使用多个resolve和reject，但是只执行第一个。我们可以调用.then()方法进行回调函数的执行，then方法接收两个函数参数，第一个函数查看resolve内容，第二个函数查看reject内容，同时也可使用。catch()方法进行reject内容的查看。

#### 6.说一下事件循环Event loop、宏任务、微任务？

> js是单线程机制，主线程在执行时会不断循环往复的从同步队列中读取任务，执行任务，当同步任务队列执行完毕后，再从异步队列任务中依次执行。宏任务和微任务都是异步任务，且微任务的执行优先级比宏任务高，因此每次都是执行完微任务再执行宏任务。宏任务有：定时器、DOM事件、Ajax事件。微任务有：promise回调、process.nextTick、async/await 等。

#### 7.说一下跨域是什么？如何解决跨域？

> 跨域：受浏览器同源策略影响（协议，域名，端口号）中的一个不同时，不能执行其他网站的脚本。
>
> 解决方法：
>
> - jsonp，只能解决GET请求
> - node.js中间件
> - 前端配置proxy代理
> - 服务器端进行cors配置，原理是设置请求头setHeader(Access-Control-Allow-Origin, '对应的域名')
> - nginx反向代理

#### 8.说一下map和forEach的区别？

> 相同点：都可以进行数组的的遍历，接收的参数相同，第一个是当前遍历对象item，第二个是当前遍历数组下标，第三个是遍历数组。
>
> 不同点：
>
> 1. 返回结果不同：forEach返回的结果是undefined，map会返回一个新数组，因此需要return出去
> 2. map的执行效率比forEach的高

#### 9.说一说创建ajax的过程？

> 1. 创建`XMLHttpRequest`对象，创建一个异步调用对象；
> 2. 创建一个新的`Http`请求，并设置对应的请求方法、请求地址、验证信息；
> 3. 发送`Http`请求；
> 4. 创建响应`HTTP`请求状态变化的函数，其中200<=state<=299，readyState === 4 就代表响应成功；

#### 10.说一下ES6箭头函数？

> 箭头函数是ES6规范引入的，与普通function函数相比，箭头函数写法更简洁。箭头函数的特点是：
>
> - this指向是静态的，this是通过继承外部函数环境中的变量获取的，call、bind、apply都无法改变其this的指向
> - 没有Constructor方法，因此不能做构造函数，不能使用new命令，否则会报错
> - 不能使用arguments，可以使用..rest进行参数的接收
> - 没有prototype原型，不能使用yield关键字

#### 11.说一下JS变量提升？

> var声明的变量存在变量提升、let与const声明的变量不存在提升，但是存在暂时性死区的问题。 
>
> 变量提升：在js编译阶段将该被声明的变量提升至代码的最前面。同时声明优先级来说，函数提升优先级大于变量提升，变量提升会覆盖掉函数提升 暂时性死区：暂时性死区是在变量未定义之前，就访问该变量所造成的的问题

#### 12.说一下axios拦截器原理？

> axios拦截器分为请求拦截器和响应拦截器，请求拦截器：在发送请求前做一些必要的操作处理，例如：添加统一cookie，请求体加验证，设置请求头等，相当于每一个接口里相同操作的一个封装；响应拦截器的功能也是如此，只是在得到响应数据后进行操作处理，例如：数据统一处理，判断用户登录失效

#### 13.说一下undefined和null的区别，如何让一个属性变成null？

> 首先 Undefined 和 Null 都是基本数据类型，undefined是全局对象的一个属性，当变量被定义但没被赋值、一个函数没有返回值、读取对象不存在的属性或者函数定义了参数但是没有传实参时，这个时候都是undefined。
>
> null代表对象的值未设置，相当于一个对象没有设置指针地址就是null。
>
> 直接将属性显式赋值成null即可。

#### 14.说一下isNaN

>isNaN() 函数 检查参数是否为非数值
>
>若是字符串，对象...返回结果为true
>
>若是数值返回结果为false
>
>需要注意的是：
>
>数字形式的字符串。例如 "123"、"-3.1415"，虽然是字符串型，但被 isNaN() 判为数，返回 false。（"12,345,678"，"1.2.3" 这些返回 true）

#### 15.说一下js垃圾回收机制？

> 我们将有些已经被使用过的，后续可能不会再使用的数据称为垃圾数据，数据一直保存在内存中，占用的内存会越来越多，为了防止内存泄漏，程序会不定期的寻找不再使用的变量，并释放掉他们所占用的内存空间。垃圾回收机制主要通过“标记-清除”来进行变量回收，当变量进入环境时，会标记为“进入环境”。当变量离开环境时，会标记为“离开环境”，标记为“离开环境”的变量就会回收内存。
>
> 垃圾回收机制算法：
>
> - 引用技术法：
>   1. 跟踪记录被`引用的次数`
>   2. 如果被引用了一次，那么就记录次数1，多次引用会`累加++`
>   3. 如果减少一个引用就`减1--`
>   4. 如果引用次数是`0`，则释放内存

#### 16.说一下数组去重的方法？

> 1. filter + indexOf
> 2. 双重循环
> 3. includes
> 4. Set集合

#### 17.说一下==和===的区别？

> ==在允许强制转换的条件下检查值的等价性，===在不允许强制转换的条件下检查值的等价性。
>
> ==当两边的值相同时判断即为true，===当且仅当两边的类型和值相同时判断才为true
>
> 例如: 55 == '55' (true) 55 === '55' (false)

#### 18.{} 和 [] 的 valueOf 和 toString 的结果是什么？

```js
{}.valueOf(); // {}
{}.toString(); // "[object Object]"
[].valueOf(); // []
[].toString(); // ""
```

#### 19.说一下原型和原型链？

> 所有的函数都有prototype属性（原型），即原型是函数的一个属性
>
> 所有的对象身上都有__proto__属性
>
> 在javascript中，每一个函数都有一个原型属性prototype指向自身的原型，而这个函数创建的实例也会有一个__proto__对象指向自己的原型，函数的原型是一个对象，而函数的原型也会有__proto__属性指向自己的原型，这样逐层深入到Object对象的原型，这样就形成了原型链。

#### 20. 说一下回调函数?

> 概念：如果将函数A作为参数传递给函数B时，我们称函数A为回调函数。
>
> ```js
> fn() {
>  console.log('我是函数A');
> }
> 
> // fn传递给了setInterval因此fn就是一个回调函数
> SetInterval(fn, 1000);
> ```
>

#### 21.说一下作用域和作用域链？

> 局部作用域分为函数作用域和块作用域
>
> 函数和变量的可使用范围称为作用域。
>
> 作用域链的本质上是底层的变量查找机制，每一个函数都有作用域链，查找变量或者函数时，需要从局部作用域到全局作用域依次查找，这些作用域集合称作作用域链。

#### 22. 说一下typeof null是object的原因？

> 在javascript中，不同的对象是使用二进制存储的，当二进制前3位为0时，系统会判断为object对象，而null的二进制全为0，因此被判断为object。

#### 23.说一下宏任务和微任务，是怎样执行的？

> 宏任务和微任务都是异步任务，且微任务的执行优先级高于宏任务
>
> 微任务：promise.then、process.nextTick、async/await等
>
> 宏任务：定时器、DOM操作、script、ajax事件
>
> - 先执宏任务script
> - 进入script后，所有同步任务主线执行
> - 所有宏任务放入宏任务执行队列
> - 所有微任务放入微任务执行队列
> - 先清空微任务队列
> - 再取一个宏任务，执行，再清空微任务队列
> - 依次循环