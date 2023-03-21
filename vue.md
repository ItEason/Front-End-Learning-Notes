### Vue2x

#### 1.说一下v-if和v-show的区别

> 相同点：都是控制元素显示和隐藏的指令
>
> 不同点：v-show控制大元素不管是ture还是false，都会被渲染，通过display：none控制元素的显示和隐藏。v-if控制的元素只有在ture时才会进行渲染，为false时不会出现在DOM树中。其中v-if消耗的性能比v-show的要大，因此v-if一般用于不频繁操作的元素，v-show更倾向于频繁操作的使用。

#### 2.说一下vue钩子函数

> 1.三个阶段：挂载阶段：beforeCreate，created，beforeMount，mounted、更新阶段：beforeUpdate，updated、销毁阶段：beforeDestory，destroyed。2.每个阶段的特点：beforeCreate：创建实例之前 created：实例创建完成，执行new Vue(options)，可访问data、methods、computed、watch上的方法和数据，可进行数据请求，但是不能访问DOM结构，不能获取ref，若要操作DOM，使用nextTick函数 beforeMount：挂载之前调用，将template编译render函数 mounted：实例挂载到DOM元素上，此时可以通过DOM API获取到DOM节点，可进行数据请求 beforeUpdate：beforeupdate：响应式数据更新时调用，发生在虚拟DOM打补丁之前，适合在更新之前访问现有的DOM，比如手动移除已添加的事件监听器 🤔 updated：虚拟 DOM 重新渲染和打补丁之后调用，组件DOM已经更新 🤔 beforeDestroy：实例销毁之前调用，this仍能获取到实例，常用于销毁定时器、解绑全局事件、销毁插件对象等操作 🤔 destroyed: 实例销毁之后 3. 父子组件执行顺序 挂载：父created -> 子created -> 子mounted> 父mounted 更新：父beforeUpdate -> 子beforeUpdated -> 子updated -> 父亲updated 销毁：父beforeDestroy -> 子beforeDestroy -> 子destroyed -> 父destroyed


#### 3.说一下Vue中$nextTick()作用与原理？

> vue更新DOM时是异步执行的，修改数据后，视图不会立即更新，而是等同一事件循环中的数据完全更新完成后，再统一进行视图的更新。所以修改完数据，立即在方法中获取DOM，获取的仍然是未修改的DOM。作用：该方法中的代码会在当前渲染完成后执行，就解决了异步渲染获取不到更新DOM的问题了，原理：$nextTick()方法的实质是返回一个promise对象。

#### 4.说一下computed与watch的区别？

> computed是计算属性，依赖于其他属性值，具有缓存，只有所依赖的属性值发生变化才会进行重新计算；watch是数据监听，支持异步，每当监听的数据发生变化就会立即执行后续操作。

#### 5.说一下$router和$route的区别？

> $router是VueRouter的实例，在script标签中使用$router导航不同的url地址
>
> $route是router的跳转对象，可以通过$route获取当前路由的name、query、parmas、path等

#### 6.说一下组件通信？

> 1. 通过props属性通信
> 2. 通过$emit触发自定义事件
> 3. 使用ref
> 4. EventBus
> 5. provide和inject
> 6. Vuex
> 7. $parent 或$root 
> 8. attrs 与 listeners

#### 7.说一下为什么vue中data是一个函数？

> vue中data是一个函数且必须是一个函数，因为当vue组件每次更新时，计算机会给data开辟一个新的内存空间，实例化几次就分配几个内存地址，这样新旧数据就不会产生数据污染问题，保护各自的数据互不影响。

#### 8.说一下v-model实现的原理？

> 1. v-bind绑定一个value值
> 2. v-on指令给当前元素绑定input事件

#### 9.说一下scoped的作用和原理

> 作用：组件css作用域，防止子组件的css样式被父组件css样式覆盖
>
> - 默认情况下，如果子组件和父组件css选择器权重相同，优先加载父组件css样式
>
> 原理：给标签添加一个v-data-xxx的自定义属性，通过属性选择器来提高css权重

#### 10.说一下.vue组件的组成部分？各自的含义？

> template：需要渲染的区域
>
> script：存放引入资源和业务实现的数据和操作
>
> style：页面css样式区域

#### 11.说一下v-if和v-for的优先级？

> 在vue中，永远不要把v-if和v-for同时使用在一个元素上，会造成性能消耗
>
> 在vue2x中，v-for的优先级要高于v-if的优先级
>
> 在vue3中，v-if的优先级要高于v-for的优先级

#### 12.说一下vue中的常见修饰符？

> 事件修饰符
>
> - stop：阻止事件冒泡
> - prevent：阻止默认行为
> - self：只触发本身
> - once：只触发一次
> - capture：事件捕获，与事件冒泡的方向相反，事件捕获由外向内
>
> 表单修饰符
>
> - lazy：当光标离开标签后，才会赋值给value
> - trim：过滤value首位的空格
> - number：自动将value转化为数字类型
>
> 键盘修饰符
>
> - 普通键：enter、tab、delete、space、esc、up...
> - 系统修饰键:ctrl、alt、meta、shift

#### 13.说一下vue中父子组件的生命周期？

> - 父子组件的生命周期是一个嵌套的过程
>
> - 渲染过程
>
>   - 父`beforeCreate` -> 父`Created` -> 父`beforeMount` -> 子`beforeCreate` -> 子`Created` -> 子`beforeMount` -> 子`Mounted` ->父`Mounted`
>
> - 子组件更新过程
>   - 父`beforeUpdate` -> 子` beforeUpdate` -> 子`Updated `-> 父`updated`
>
> - 父组件更新过程
>   - 父`beforeUpdate` -> 父`Updated`
>
> - 销毁过程
>   - 父`beforeDestroy`->子`beforeDestroy`->子`destroyed`->父`destroyed`
>

#### 14.说一下diff算法？

> diff算法是指对新旧虚拟节点进行对比，并返回一个patch对象，用来存储两个节点不同的地方，最后利用patch记录的消息局部更新DOM。

#### 15.说一下:key的理解？

> :key是为 Vue 中 vnode 的唯一标记，因为vue是虚拟DOM，更新DOM时用diff算法对节点进行一一对比，当新节点和旧节点的：key值相同时会进行复用，没有设置key值时会对页面的节点进行全部的渲染，性能消耗较大，vue中key值相等于一个性能优化的处理。key值的设置不能是元素的index

#### 16.说一下虚拟DOM的优缺点？

> - 缺点
>   - 首次渲染大量DOM时，由于多了一层虚拟DOM的计算，会比innerHTML插入慢
> - 优点
>   - 减少了dom操作，减少了回流与重绘
>   - 保证性能的下限，虽说性能不是最佳，但是它具备局部更新的能力，所以大部分时候还是比正常的DOM性能高很多的