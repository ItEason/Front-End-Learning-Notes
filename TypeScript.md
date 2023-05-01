### TypeScript

#### 基础数据类型
##### boolean
```ts
let flag1: boolean = true;let flag2: boolean = false;
```
##### number
```ts
let num1: number = 1;let num2: number = 2;
```
##### string
```ts
let str1: string = "1";let str2: string = "2";
```
##### any
>不清楚用什么类型，可以使用 `any` 类型。这些值可能来自于动态的内容，比如来自用户输入或第三方代码库
```ts
let notSure: any = 4;
notSure = "3";
notSure = true
```
>不建议使用 any，不然就丧失了 TS 的意义。注意：只是不建议，但是在某些开发场景上还是可以使用any的。
##### unknow
>`unknown` 类型代表任何类型，它的定义和 `any` 定义很像，但是它是一个安全类型，使用 `unknown` 做任何事情都是不合法的。/
```ts
function divide(param: unknow) {    
	return param / 2;
}
```
##### void
```ts
function sum(): void {    console.log(`void返回值`);}
```
##### never
>`never`类型表示的是那些永不存在的值的类型。有些情况下值会永不存在，比如，- 如果一个函数执行时抛出了异常，那么这个函数永远不存在返回值，因为抛出异常会直接中断程序运行。- 函数中执行无限循环的代码，使得程序永远无法运行到函数返回值那一步。
```ts
function fn(msg: string): never {    throw new Error(msg)}
```
##### 数组类型
```ts
// 数组类型
let arr: number[] = [1, 2, 3, 4, 5];
let arr1: string[] = ["1", "2", "3", "4"];
let arr2: boolean[] = [true, false, true, false]
```
#### type
```ts
// string
type custom = string
let str1: custom = "1";
let str2: custom = "2";
// number
type num = number;
let num1: num = 1;
let num2: num = 2;
```
#### 函数
##### 函数类型
```ts
function add(num1: number, num2: number): number {    
	return num1 + num2;
	}
```
##### 函数表达式
```ts
//  函数表达式
let add2 = (num1: number, num2: number): number => num1 + num2
```
##### 可选参数
```ts
// 可选参数
let add3 = (num1: number, num2: number, num3?: number): number => {    return num1 + num2}console.log(add3(1, 2)); 3console.log(add3(1, 2, 3)); 3
```
##### 默认参数
```ts
// 默认参数
function sum(num1: number, num2: number = 100): number {    return num1 + num2}
```
##### 函数赋值
```ts
let add2 = (x: number, y: number): number => {    return x + y} const add3:(x: number, y: number) => number = add2
```
#### interface
>`interface`(接口) 是 TS 设计出来用于定义对象类型的，可以对对象的形状进行描述。### 基本概念。
##### 基本用法

```ts
// interface
interface person {    
	name: string    
	age: number,    
	address: string
}
let me: person = {    
	name: 'eason',    
	age: 21,    
	address: '广东云浮'
}
console.log(me)
// { name: 'eason', age: 21, address: '广东云浮' }
```
##### 可选概念
> 在使用`interface`进行变量的类型定义时，可以使用在变量名后添加?，代表该变量是可选变量，即使对象中不存在该变量也不会报错。
```ts
interface person1 {
	name: string,
	age: number,
	address?:string
}

let me1: person1 = {    
	name: 'eason',    
	age: 21
}
// { name: 'eason', age: 21 }
```
#####  只读属性
```ts
interface person2  {
    readonly id:number,
    name:string,
    age:string,
    address:string
}
let m2: person2 = {
    id: 1,
    name: 'eason',
    age: 21,
    address: '广东'
}
console.log(me2.id);
me2.id = 2 // 无法为“id”赋值，因为它是只读属性。
console.log(me.2d);
```
##### interface 描述函数类型
```ts
interface ISum {    
	(x:number,y:number):number
} 
const add:ISum = (num1, num2) => {    
	return num1 + num2	
}
```
##### 可索引的类型
```ts
let arr: likeArray = ['hello', 'lin'];
console.log(arr[1]);
```

#### 类
##### 基本写法
```ts
class Person {    
	name: string    
	constructor(name: string) {        
		this.name = name;    
	}    
	speak() {        
		console.log(`${this.name} is speaking`);    
	}
}
const p1 = new Person('eason')；
console.log(p1.name);
p1.speak()；
```
##### 继承
```ts
// 继承
class employee extends Person {    
	address: string    
	constructor(name: string, address: string) {        
		super(name)        
		this.address = address    
	}    
	speak() {        
		console.log(`我叫${this.name}，在${this.address}工作`)    
	}
}
new employee("eason", "广州海珠").speak()
```
##### 修饰符
> 在TypeScript里，成员都默认为 `public`。

###### public
```ts
class Person {    
	public name: string    
	public constructor(name: string) {       
    	this.name = name;    
    }    
    
    public speak() {        
    	onsole.log(`${this.name} is speaking`);    
    }
}
```
###### private
> 当成员被标记成 `private`时，它就不能在声明它的类的外部访问。
```ts
 class employee extends Person {    
 	private address: string    
 	constructor(name: string, address: string) {        
 		super(name);        
 		this.address = address;    
 	}    
 	speak() {        
 		console.log(`我叫${this.name}，在${this.address}工作`)    
 	}
 }
 new employee("eason", "广州海珠").address  
 // 属性“address”为私有属性，只能在类“employee”中访问。
```

######  protected
 > `protected`修饰符与 `private`修饰符的行为很相似，但有一点不同， `protected`成员在派生类中仍然可以访问。继承它的子类可以访问，实例不能访问。
 ```ts
 // 基础写法
 class Person {    
 	protected name: string    
 	public constructor(name: string) {        
 		this.name = name;    
 	}    
 	public speak() {        
 		console.log(`${this.name} is speaking`);   
 	}
 }
 // 继承
 class employee extends Person {    
     public address: string    
     constructor(name: string, address: string) {        
         super(name)        
         this.address = address    
     }    
     speak() {        
         console.log(`我叫${this.name}，在${this.address}工作`)    
     }
 }
 new employee("eason", "广州海珠").name 
 // 错误
 ```
 ##### 多态
 > 子类对父类的方法进行了重写，子类和父类调同一个方法时会不一样。
 ```js
 class employee extends Person {    
 	public address: string    
 	constructor(name: string, address: string) {        
 		super(name)       
        this.address = address    
    }    
    speak() {       
    	console.log(`我叫${this.name}，在${this.address}工作`)    
    }
}
 ```
 ##### static
 > `static` 是静态属性，可以理解为是类上的一些常量，实例不能访问。
 ```js
 class circle {    
 	static pi: number = 3.14    
 	public radius: number    
 	public constructor(radius: number) {        
 		this.radius = radius    
 	}    
 	public calcLength() {        
 		return circle.pi * this.radius;    
 	}
 }
 console.log(new circle(10).calcLength());
 ```

##### abstract
 > 抽象类：是指**只能被继承，但不能被实例化的类**>> 特点：>> - 抽象类不允许被实例化> - 抽象类中的抽象方法必须被子类实现
 ```js
abstract class Animal {    
	constructor(name: string) {        
		this.name = name    
	}    
	public name: string    
	public abstract sayHi(): void
}
	
	class Dog extends Animal {    
		constructor(name: string) {        
			super(name)    
		}    	
 		// 没有该行代码会报错    
        public sayHi(): void {        
        	console.log("hi");    
        }
    }
 ```
##### implements
> implements 是实现的意思，class 实现 interface。
```ts
interface MusicInterface {    
	playMusic(): void
} 
class Cellphone implements MusicInterface {    
	playMusic() {}
}
```
#### 泛型
##### 基本使用
```tsx
function print<T>(arg: T): T {
    return arg;
}
```



##### 在函数中使用泛型
```js
function print<T>(arg: T): T {    
    console.log(Object.prototype.toString.call(arg));    
    return arg;
}
```
##### 在接口中使用泛型
```js
interface Search {    
    <T, Y>(name: T, age: Y): T
}
let fn: Search = function <T, Y>(name: T, id: Y): T {    
    console.log(name, id);    
    return name
}
fn('eason', 12)
```
##### 在类中使用泛型
```tsx
class person<T> {    
    public name: T    
    constructor(name: T) {        
        this.name = name    
    }    
	action<T>(say: T) {        
        console.log(say);    
    }
}
let me = new person("eason")me.action("eason")
```

#### 命名空间

> 在日常开发中，当我们想要在interface中继续添加export的ts规则时，我们可以使用namepace（命名空间）来修饰interface，同时在interface中定义需要export的规则即可。

```tsx
namespace Validation {
    export interface StringValidator {
        isAcceptable(s: string): boolean;
    }

    const lettersRegexp = /^[A-Za-z]+$/;
    const numberRegexp = /^[0-9]+$/;

    export class LettersOnlyValidator implements StringValidator {
        isAcceptable(s: string) {
            return lettersRegexp.test(s);
        }
    }

    export class ZipCodeValidator implements StringValidator {
        isAcceptable(s: string) {
            return s.length === 5 && numberRegexp.test(s);
        }
    }
}

```



### TypeScript面试常见题

#### 1.ts中的any和unknown有什么区别？

> unknown和any的主要区别是unknown类型会更加严格；在对unknown类型的的值执行大多数操作之前，我们必须进行某种形式的检查。而在对any类型的值执行操作之前，我们不必进行任何检查。`任何类型的数据都可以赋值给unknown和any。`

举例说明：

```tsx
let foo: any = 123;
console.log(foo.msg); // 符合TS的语法
let a_value1: unknown = foo; // OK
let a_value2: any = foo; // OK
let a_value3: string = foo; // OK

let bar: unknown = 222; // OK 
console.log(bar.msg); // Error
let k_value1: unknown = bar; // OK
let K_value2: any = bar; // OK
let K_value3: string = bar; // Error
```

**总结：**`any`和`unknown`都是顶级数据类型，但是unknown更加严格，不想any那样不做类型检查，反而因为未知性质，不允许访问属性，也不允许赋值给有其他明确数据类型的变量。

#### 2.ts与js的区别？

> - TypeScript是JavaScript的超集，扩展了JavaScript的语法
> - TypeScript是面向对象变成语言，JavaScript是脚本语言
> - TypeScript是强类型编程语言，Javascript是弱类型编程语言

#### 3.TypeScript中never和void的区别？

> - void表示没有任何数据类型（可以赋值为null或undefined）
> - never表示一个不包含值的类型，即永远不存在返回值
> - 拥有void返回值类型的函数能正常运行。拥有 never 返回值类型的函数无法正常返回，无法终止，或会抛出异常。

#### 4.type和interface的区别？

> type是类型的别名，可以用于基本类或基本类型的联合类型，也可以定义对象类型
>
> 接口interface只能用于定义对象类型
