### TypeScript面试常见题

#### 1.什么是TypeScript，为什么使用它？

> TypeScript是一种静态类型的面向对象的编程语言，它是JavaScript框架之一，它添加了可选的静态类型和其他功能。
>
> TypeScript可以让代码更容易维护和扩展，并提供更好的工具和编辑器支持。

#### 2.ts中的any和unknown有什么区别？

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

#### 3.ts与js的区别？

> - TypeScript是JavaScript的超集，扩展了JavaScript的语法
> - TypeScript是面向对象变成语言，JavaScript是脚本语言
> - TypeScript是强类型编程语言，Javascript是弱类型编程语言

#### 4.TypeScript中never和void的区别？

> - void表示没有任何数据类型（可以赋值为null或undefined）
> - never表示一个不包含值的类型，即永远不存在返回值
> - 拥有void返回值类型的函数能正常运行。拥有 never 返回值类型的函数无法正常返回，无法终止，或会抛出异常。

#### 5.type和interface的区别？

> type是类型的别名，可以用于基本类或基本类型的联合类型，也可以定义对象类型
>
> 接口interface只能用于定义对象类型