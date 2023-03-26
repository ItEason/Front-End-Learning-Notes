#### let变量

1.变量名不能重复  

```javascript
let name = 'zs'; 
let name = 'ls'; 
// 控制台打印：Uncaught SyntaxError: Identifier 'name' has already been declared
```

2.块级作用域 

```javascript
{
	let name = 'zs'
}
console.log(name) // 控制台不打印任何数据
```

3.不存在变量提升 

```javascript
console.log(name)
let name = 'zs'
// 控制台打印：Uncaught ReferenceError: Cannot access 'name' before initialization
```

4.不影响作用域链

```javascript
{
    let name = 'zs';
    function fn() {
        console.log(name);
        // 控制台输出'zs'
    }
}
```

案例使用：

```html
	<div class="container">
        <h2 class="page-header">点击切换颜色</h2>
        <div class="item"></div>
        <div class="item"></div>
        <div class="item"></div>
    </div>
    <script>
        let items = document.querySelectorAll('.item')
        for (var i = 0; i < items.length; i++) {
            items[i].onclick = function () {
                // 修改当前元素背景颜色
                items[i].style.background = 'pink';
            }
        }
        console.log(window.i); // 控制台打印3
    </script>
```

![](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230218154246284.png)

> 因为var变量具有提升变量的特点，直接提升到了window中，使用let即可解决该问题。

#### const变量

1. 不能重复定义且一定要赋初始值

   ```javascript
   const name;
   // 控制台打印：Uncaught SyntaxError: Missing initializer in const declaration 
   ```

   

2. 常量的值不能修改

   ```javascript
   const name = 'zs'
   name = 'ls';
   // 控制台打印：let和const.html:47 Uncaught TypeError: Assignment to constant variable.
   ```

   

3. 块级作用域

   ```javascript
   {
       const name = 'zs';
   }
   console.log(name); // 控制台不打印任何数据
   ```

4. 不存在变量提升

   > 注意：let变量是允许声明变量名不不赋值的，const变量是不允许的，必须声明且初始化变量。

#### 变量解构赋值

##### 数组的解构

```javascript
const fruits = ['苹果', '香蕉', '橙子'];
const [apple, banana, orange] = fruits;

```

![image-20230218155957026](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230218155957026.png)

##### 对象的解构

```javascript
const person = {
    name: 'zs',
    age: '21',
    say() {
        console.log('hello!');
    }
}

const {name, age, say} = person;
```

![image-20230218160225404](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230218160225404.png)

#### 模板字符串``

```javascript
// 变量拼接
const name = 'zs', age = 21, address = '广东';
console.log(`我叫${name}，今年${age}岁，住在${address}`)

// 内容直接出现换行符
const str = `<ul>
				<li>1</li>
				<li>2</li>
				<li>3</li>
				<li>4</li>
			</ul>`
```

![image-20230218161200957](D:\desktop\image-20230218161200957.png)

#### 箭头函数

1. this是静态的，this通过继承外部函数环境中的变量获取，不能通过apply、bind、call方法修改指向

```javascript
		function getName1() {
            console.log(this.name);
        }

        let getName2 = () => {
            console.log(this.name);
        }

        window.name = 'global';
        
        getName1(); // global
        getName2(); // global
		// 使用call改变函数的this指向
		getName1.call({name: 'eason'}); // eason
		getName2.call({name: 'eason'}); //global
```

2.不能使用new命令，没有constructor方法，不能够用作构造函数

```javascript
		let person = (name, age) => {
            this.name = name;
            this.age = age;
        }
        let m = new person('eason', 21);
        console.log(m); // Uncaught TypeError: person is not a constructor
```

3.不能使用arguments变量，可以使用...rest进行参数接收

```javascript
		function getInfo(name, age, sex) {
            console.log(arguments);
        }

        let fn = (name, age, sex) => {
            console.log(arguments);
        }

        getInfo('eason', 21, 'male'); // 输出arguments对象
        fn('eason', 21, 'male'); // arguments is not defined
		// 注意：rest参数一定要放在最后
		 let fn = (...rest) => {
            console.log(rest);
        }
        fn('eason', 21, 'male'); // ['eason', 21, 'male']
```

4. 不能使用 yield 命令，没有prototype原型

   箭头函数的应用

   ```javascript
   // 需求 从数组中返回偶数的元素
   const arr = [1,6,9,10,100,25];
   // 一句代码直接搞定
   const result = arr.filter(item => item % 2 === 0);
   ```
#### 参数默认值

   形参初始值具有默认值的参数，，一般位置要靠后(潜规则)

   ```javascript
   function add(a,b,c=10) {
       return a + b + c;
   }
   // 当不传递对应的参数时，就会使用函数方法中的默认参数值
   add(1,2)
   ```

#### 扩展运算符

```javascript
// 应用一：数组的克隆
const fruits = ['苹果','香蕉','菠萝','橙子'];
const result = [...fruits] // 结果输出：(4) ['苹果', '香蕉', '菠萝', '橙子']

// 应用二：数组的合并
const starts = ['rose', 'james','kobe'];
const res = [...fruits, ...starts];
// 结果输出：['苹果', '香蕉', '菠萝', '橙子', 'rose', 'james', 'kobe']
```

#### Symbol数据类型

> ES6引入了一种新的原始数据类型 Symbol，表示独一无二的值。它是JavaScript语言的第七种数据类型，是一种类似于字符串的数据类型。
>
> Symbol特点：
>
> - Symbol的值是唯一的，用来解决命名冲突的问题
> - Symbol值不能与其他数据进行运算
> - Symbol定义的对象属性不能使用for…in循环遍历，但是可以使Reflect.ownKeys来获取对象的所有键名

1. 创建
```js
let s1 = Symbol("eason");
let s2 = Symbol("eason");
console.log(s1 === s2) // 结果打印：false

let name1 = Symbol("eason");
let name2 = Symbol("eason");
console.log(name1 === name2) // 结果打印：true
```
2. 不能与其他数据类型进行运算

   ```js
   let res = s1 + 100; 
   let res = s1 > 100; 
   let res = s1 + s2;
   // 以上控制台都会打印： Cannot convert a Symbol value to a number
   ```

> javascript的7种基本数据类型：number string undefined null symbol boolean  bigInt

#### Iterator迭代器

> **iterator**接口，当某个类型实现了该接口后，遍历其数据时可以使用for...of进行遍历，for-of循环通过break、continue、return或throw提前退出。
>
> 实现了iterator接口的有:
>
> - Array
> - Set
> - Map
> - String
> - TypeArray
> - arguments
> - NodeList

#### Promise

> `Promise`有一个构造函数，接收一个函数作为参数，这个传入构造函数里的函数被称作`executor`。 `Promise`的构造函数会同步地调用`executor`，`executor`又接收`resolve`函数跟`reject`函数作为参数，然后我们就可以通过这两个函数俩决定当前`Promise`的状态（`resolve`进入`fulfilled`或者`reject`进入`rejected`）。
>
> 当promise对象创建成功后，可以调用`Promise.prototype.then()`方法进行实例对象的调用，用时`then()`方法接收两个回调函数，第一个为`resolve()`内容的显示，第二个为`reject()`内容的显示。当然，`then()`方法的第二个参数也可以省略，但是会报错，要想代码不报错且捕获reject()使用`catch()`方法即可。

```js
		// 创建一个promise实例对象
        const p = new Promise(function (resolve, reject) {
            let a = 2;
            // 异步任务
            setTimeout(function () {
                console.log('promise执行完成');
                if (a === 1) {
                    resolve('请求数据成功...');
                } else {
                    reject('请求数据失败...')
                }
            }, 1000)
        })
        // 内置api-then
        p.then(data => console.log(data), err => console.log(err))
```

![image-20230221170142242](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221170142242.png)

```js
		// 创建一个promise实例对象
        const p = new Promise(function (resolve, reject) {
            let a = 1;
            // 异步任务
            setTimeout(function () {
                console.log('promise执行完成');
                if (a === 1) {
                    resolve('请求数据成功...');
                } else {
                    reject('请求数据失败...')
                }
            }, 1000)
        })
        // 内置api-then
        p.then(data => console.log(data), err => console.log(err))
```

![image-20230221170240186](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221170240186.png)

那么，then()方法的返回值是什么呢？代码原封不动时，控制台打印结果如下：

![image-20230221170756425](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221170756425.png)

当我们给函数添加了对应的return值时，发现PromiseResult的内容居然跟被执行函数的返回值一致

```js
	p.then(data => {
            console.log(data);
            return 123;
        }, err => {
            console.log(err);
            return '123';
        });
```

![image-20230221170924301](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221170924301.png)

![image-20230221171206140](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221171206140.png)

PromiseResult会改变，那PromiseState会不会改变呢？当把定时器中的resolve()和reject()注释后

![image-20230221171419813](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221171419813.png)

```js
		p.then(data => {
            console.log(data);
            // 手动抛出一个错误对象
           	throw new Error('失败了!');
        }, err => {
            console.log(err);
            return '123';
        });
        console.log(res);
```

![image-20230221172439323](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230221172439323.png)

**`通过结果的验证得知：promise有三种状态：pending（等待），fulfilled（成功），rejected（失败）`**

then()也接收返回一个promise对象，以此解决回调地狱问题，让我们用**读取多个文件**实例加深理解。

```js
		//使用 promise 实现
		const p = new Promise((resolve, reject)=> {
    		fs.readFile("./resources/为学.md"，(err,data)=>{resolve(data);
   		});
  		
        // 使用then()链式编程
        p.then(success=> {
            return new Promise((resolve, reject)=> {
                fs.readFile("./resources/为学.md"，(err,data)=>{
                    resolve([success, data]
                });
            });
        }).then(success=> {
                return new Promise((resolve, reject)=> {
                fs.readFile("./resources/为学.md"，(err,data)=>{
                    sccuss.push(data)
                    resolve(sccuss);
                });
            });
        })
```

#### Set集合

**Set是一种叫做集合的数据结构，Map是一种叫做字典的数据结构。**

**集合、字典都可以存储不重复的值，方便用于去重**

**集合是以[值，值]的形式存储元素，字典是以[键，值]的形式存储。**

注意：当存储相同的值时，新值会将旧值覆盖。

```js
// 创建Set集合，同时接收对应的参数，参数可有可无
let s = new Set();
let arr = new Set([1, 2, 3, 4, 5, 6]);

// 1.add()方法：用于向Set集合中添加数据
s.add('a');
arr.add(7);

// 2.delete()方法，用于删除Set集合中的数据
s.delete('a');
arr.delete(7);

// 3.has()方法，用于检测数据是否存在Set集合中、
s.has('a'); // false
arr.has(1); // true

// 4.size，用于输出Set集合个数（可理解成长度）
arr.size 
// 打印输出：6
```

因为Set集合实现了iterator接口，使用for...of...可以遍历集合

```js
for(let key of arr) {
    console.log(key);
}
```

#### Map结构

> ​	ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合。但是“键”的范围不限于字符串，各种类型的值(包括对象)都可以当作键。Map 也实现了 iterator 接口，所以可以使用[扩展运算符]和 [for...of...] 进行遍历。Map的属性和方法:
>
> 1. size：返回Map的元素个数
> 2. set：增加一个新元素，返回当前 Map
> 3. get：返回键名对象的键值
> 4. has：检测 Map 中是否包含某个元素，返回 boolean 值
> 5. clear：清空集合，返回undefined
> 6. delete：删除键值对

```js
// 创建一个新的Map
let map = new Map();

// 1.添加元素
map.set('name', 'eason');

// 2.返回键名对象值
map.get('name');

// 3.检测Map中是否存在该键值
map.has('name') //true

// 4.返回个数
map.size // 1

// 5.清空map
map.clear();
```



遍历Map集合

```js
// [x,x]的形式是数组解构赋值
for(let [key, value] of map) {
    console.log(key + '->' + value);
}

// 直接输出键值对数据
for(let m of map) {
    ....
}
```

#### Class

> - class (类)作为对象的模板被引入，可以通过 class 关键字定义类
> - class 的本质是 function，同样可以看成**一个块**
> - 可以看作一个语法糖，让**对象原型的写法更加清晰**
> - 更加标准的**面向对象编程**语法

`constructor`构造器，当调用new时就会立即执行。

```js
		class Person {
            constructor(name, age, sex) {
                this.name = name;
                this.age = age;
                this.sex = sex;
                console.log('我被执行了...')
            }

        }

        let person = new Person('eason', 21, 'male');
        console.log(person); 
```



`static`静态成员，当属性或方法被关键字static修饰后，new实例对象不能访问。

```js
		class Person {
            static name = 'eason'
            static age = 21
            sex = 'male'
        }

        let person = new Person();
        console.log(person.name); // undefined
        console.log(Person.name); // eason
		console.log(person.sex); // male
```

`class类的继承`:使`super`关键字可以调用父类中的`constructor`方法

```js
		class Person {
            constructor(name, age, sex) {
                this.name = name;
                this.age = age;
                this.sex = sex;
            }

        }

        class Me extends Person {
            constructor(name, age, sex, address) {
                super(name, age, sex);
                this.address = address
            }
        }

        console.log(new Me('eason', 21, 'male', '广东'));
```

![image-20230222103052024](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\image-20230222103052024.png)

`重写`:子类可以对父类中的方法进行重写，声明与父类同名方法即可实现。

```js
		class Person {
            constructor(name, age, sex) {
                this.name = name;
                this.age = age;
                this.sex = sex;
            }
			// 父类获取名字方法
            getName() {
                return this.name;
            }
			// 父类获取年龄方法
            getAge() {
                return this.age;
            }
        }

        class Me extends Person {
            constructor(name, age, sex, address) {
                super(name, age, sex);
                this.address = address
            }
			// 子类重写获取名字方法
            getName() {
                return '我的名字是：' + this.name;
            }
        }
        let m = new Me('eason', 21, 'male', '广东');
        console.log(m.getName()); // 我的名字是：eason
```

`Getter和Setter`

```js
		class Person {
            constructor(name, age, sex) {
                this.name = name;
                this.age = age;
                this.sex = sex;
            }
			get Name() {
                console.log('名字被读取了...');
                return  this.name;
            }
            // set必须有要对应的参数
            set Name(newName) {
                console.log('名字被修改了...')
            }
        }
```

#### import 和 export

```js
// 分别导出
export const name = 'eason';

export function say() {
    console.log('你好！');
}

// 全部导出
export {name, say}

// 默认导出，注意有且只有一个默认导出export default
export default {
    name: 'eason',
    say() {
        console.log('你好');
    }
}

export const school = 'ges';
```

```js
 // 全部导入 其中as是起别名
import * as m1 from './m1.js'
 console.log(m1.name);

// 按需导入
import { name } from './m1.js'
console.log(name);
```

#### async / await

> 被async关键字修饰的函数，最终都会成为一个promise对象。

```js
        // async
        async function fn() {
            // 返回的结果永远都是一个promise对象(不论你返回什么)
            return 'eason'
        }

        let result = fn()
        console.log(result); 
```

> await是用来读取promise对象中resolve()函数中的值，返回的结果就是resolve参数结果。注意：当promise返回的是reject函数参数时程序出停止执行，报错，使用try...catch方法进行捕获即可。

```js
		// async
        async function fn() {
            let res = await new Promise((resolve, reject) => {
                resolve('用户数据')
            })
            console.log(res); // 结果输出：用户数据
        }
        fn()
```

#### export和export default的区别？

> 相同点：都可以导出变量、函数、文件、模块等
>
> 不同点：
>
> - 在一个js文件中可以存在多个export，但是只能存在一个export default
> - 通过export方式导出，在导入时需要{}按需导入。而通过export default方式导出则不需要，可以起任意别名导入
> - export default与export不要同时使用

# 持续更新中...

