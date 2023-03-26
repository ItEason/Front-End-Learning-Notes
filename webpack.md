#### 1.说一下webpack是什么?

> 模块打包工具

#### 2.webpack的核心概念？

> entry：入口，Webpack 执行构建的第一步将从 Entry 开始，可抽象成输入。告诉webpack要使用哪个模块作为构建项目的起点，默认为./src/index.js
>
> ouput：出口，告诉webpack在哪里输出它打包好的代码以及如何命名，默认为./dist
>
> Module：模块，在 Webpack 里一切皆模块，一个模块对应着一个文件
>
> plugins：扩展插件
>
> Chunk：代码块，一个 Chunk 由多个模块组合而成，用于代码合并与分割
> Loader：模块转换器，用于把模块原内容按照需求转换成新内容