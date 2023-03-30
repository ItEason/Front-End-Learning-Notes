#### 1.如何创建一个http服务？

> 1. 首先下载express依赖
> 2. 创建一个js文件require一下express
> 3. 调用expres对象，创建一个http实例
> 4. 调用实例的listen方法，传入端口和回调函数
> 5. 最后控制台node执行该js文件即可

#### 2.说一下nodejs常用的中间件？

> cors中间件：解决跨域问题
>
> bodyParser中间件：解决post请求获取不到参数问题
>
> jsonwebtoken中间件：用于生成token字符串
>
> express-jwt中间件：用于解析token字符串
>
> ...

