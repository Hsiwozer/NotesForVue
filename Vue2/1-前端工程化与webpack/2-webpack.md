# webpack

1. #### 什么是webpack？

   概念：webpack 是前端项目工程化的具体解决方案。

   主要功能：它提供了友好的前端模块化开发支持，以及<font color="red">代码压缩混淆</font>、<font color="red">处理浏览器端Javascript 的兼容性</font>、<font color="red">性能优化</font>等强大的功能。

2. #### webpack 的基本使用

   - ##### <font color="red">初始化</font>

     - 新建项目空白目录，并运行`npm init -y` 命令，初始化包管理配置文件 package.json
     - 新建 src 源代码目录
     - 新建 src -> index.html 首页和 src -> index.js 脚本文件
     - 初始化首页基本的结构
     - 运行 `npm install jquery -S` 命令，安装 jQuery
     - 通过 ES6 模块化的方式导入 jQuery，实现列表隔行变色效果

   - ##### <font color="red">安装配置与使用 webpack</font>

     - 在项目中安装 webpack，使用命令 `npm install webpack webpack-cli -D`

     - 在项目根目录中，创建名为 webpack.config.js 的 webpack 配置文件，并初始化如下的基本配置：

       ```js
       // 使用 node.js 中的导出语法，向外导出一个 webpack 的配置对象
       module.exports = {
           // 代表 webpack 运行的模式，可选值有 development 和 production
           mode: 'development'
       }
       ```

       

     - 在 package.json 的 scripts 节点下，新增 dev 脚本如下：

       ```json
       "scripts": {
         "dev": "webpack"
       }
       ```

       

     - 在终端中运行 `npm run dev` 命令，启动 webpack 进行项目的打包构建

   - ##### webpack 中的默认约定

     在 webpack 4.x 和 5.x 中，有如下默认约定：

     - 默认的打包入口文件为 src -> index.js
     - 默认的输出文件路径为 dist -> main.js

     可以在 webpack.config.js 中修改打包的默认约定。

     <font color="red">通过 entry 节点指定打包的入口，通过 output 节点指定打包的出口。</font>

     ```js
     const path = require('path')
     
     module.exports = {
         entry: path.join(__dirname, './src/index.js'),
         output: {
             path: path.join(__dirname, 'dist'),
             filename: 'main.js'
         }
     }
     ```

     

3. #### <font color="red">webpack 中的插件</font>

   - ##### <font color="red">webpack-dev-server</font>

     - `npm install webpack-dev-server@3.11.2 -D`

     - 类似于 node.js 阶段用到的 nodamon 工具

     - 每当修改了源代码，webpack 会自动进行项目的打包和构建

     - <font color="blue">**配置 webpack-dev-server**</font>

       - 修改 package.json -> scripts 中的命令：

         ```json
         "scripts": {
           "dev": "webpack serve"
         }
         ```

         

       - 再次运行 `npm run dev` 命令，重新进行项目打包

       - 在浏览器中访问 http://localhost:8080 地址，查看自动打包效果

       注意：该插件会启动一个实时打包的 http 服务

   - ##### <font color="red">html-webpack-plugin</font>

     - `npm install html-webpack-plugin -D`

     - webpack 中的 HTML插件（类似于一个模板引擎插件）

     - 可以通过此插件自定制 index.html 页面的内容

     - <font color="blue">**配置 html-webpack-plugin**</font>

       ```js
       const HtmlPlugin = require('html-webpack-plugin')
       
       const htmlPlugin = new HtmlPlugin({
           template: './src/index.html',
           filename: './index.html'
       })
       
       module.exports = {
           mode: 'development',
           plugins: [htmlPlugin]
       }
       ```

   - ##### <font color="red">devServer 节点</font>

     在 webpack.config.js 配置文件中，可以通过 devServer 节点对 webpack-dev-server 插件进行更多的配置，示例代码如下：

     ```js
     devServer: {
         open: true,
         port: 80,
         host: "127.0.0.1",
     },
     ```

     **注意：**凡是修改了 webpack.config.js 配置文件，或修改了 package.json 配置文件，必须重启实时打包的服务器，否则最新的配置文件无法生效！

4. #### webpack 中的 loader

   在实际开发过程中，webpack 默认只能打包处理以 .js 后缀名结尾的模块。其他非 .js 后缀名结尾的模块，webpack 默认处理不了，需要调用loader 加载器才可以正常打包，否则会报错！

   loader 加载器的作用：<font color="red">协助 webpack 打包处理特定的文件模块</font>。比如：

   - css-loader 可以打包处理 .css 相关的文件

   - less-loader 可以打包处理 .less 相关的文件

   - babel-loader 可以打包处理 webpack 无法处理的高级 JS 语法

     

   ###### <font color="blue">ONE</font> 打包处理 css 文件

   1. 运行 `npm i style-loader@3.0.0 css-loader@5.2.6 -D` 命令，安装处理 css 文件的 loader

   2. 在 webpack.config.js 的 module -＞rules 数组中，添加 loader 规则如下：

      ```js
      module: {
          rules: [{ test: /\.css$/, use: ["style-loader", "css-loader"] }],
      },
      ```

      其中，test 表示匹配的文件类型，use 表示对应要调用的 loader

      注意：

      - use 数组中指定的 loader 顺序是固定的
      - 多个loader 的调用顺序是：从后往前调用

      

   ###### <font color="blue">TWO</font> 打包处理 less 文件

   1. 运行 `npm i less-loader@10.0.1 less@4.1.1 -D` 命令

   2. 在 webpack.config.js 的 module -＞rules 数组中，添加 loader 规则如下：

      ```js
      module: {
          rules: [{ test: /\.less$/, use: ["style-loader", "css-loader", "less-loader"] }],
      },
      ```

      

   ###### <font color="blue">THREE</font> 打包处理样式表中与 url 路径相关的文件

   1. 运行 `npm i url-loader@4.1.1 file-loader@6.2.0 -D` 命令

   2. 在 webpack.config.js 的 module -＞rules 数组中，添加 loader 规则如下：

      ```js
      module: {
          rules: [{ test: /\.jpg|png|gif$/, use: "url-loader?limit=22229" }],
      },
      ```

      其中 ？之后的是 loader 的参数项： 

      - limit 用来指定图片的大小，单位是字节 (byte）
      - 只有 <=limit 大小的图片，才会被转为 base64 格式的图片

   

   ###### <font color="blue">FOUR</font> 打包处理 JS 文件中的高级语法

   1. webpack 只能打包处理一部分高级的 JavaScript 语法。对于那些 webpack 无法处理的高级 js 语法，需要借助于 babel-loader 进行打包处理。例如 webpack 无法处理下面的 Javascript 代码：

      ```js
      function info(target) {
        target.info = 'Person info'
      }
      @info
      class Person {}
      console.log(Person.info)
      ```

   2. 安装 babel-loader 相关的包：

      `npm i babel-loader@8.2.2 @babel/core@7.14.6 @babel/plugin-proposal-decorators@7.14.5 -D`

      在 webpack.config.js 的 module -＞rules 数组中，添加 loader 规则如下：

      ```js
      module: {
          rules: [{ test: /\.js$/, use: "babel-loader", exclude: /node_modules/ }],
      },
      ```

   3. 在项目根目录下，创建名为 babel-config.js 的配置文件，定义 Babel 的配置项如下：

      ```js
      module.exports = {
      	plugins: [['@babel/plugin-proposal-decorators', { legacy: true }]]
      }
      ```

   

5. #### 打包发布

   - ##### 配置 webpack 的打包发布

     在 package.json 文件的 scripts 节点下，新增 build 命令如下：

     ```js
     "scripts": {
       "dev": "webpack serve",
         "build": "webpack --mode production"
     }
     ```

     --model 是一个参数项，用来指定 webpack 的运行模式。production 代表生产环境，会对打包生成的文件进行代码压缩和性能优化。

     **注意：**通过 --model 指定的参数项，会覆盖 webpack.config.js 中的 model 选项。

   - ##### 把 JavaScript 文件统一生成到 js 目录中

     在 webpack.config.js 配置文件的 output 节点中，进行如下配置：

     ```js
     output: {
     	path: path.join(__dirname, 'dist'),
     	filename: 'js/bundle.js'
     }
     ```

   - ##### 把图片文件统一生成到 image 目录中

     修改 webpack.config.js 中的 url-loader 配置项，新增 outputPath 选项即可指定图片文件的输出路径：

     ```js
     {
       test: /\.jpg|png|gif$/,
       use: {
         loader: 'url-loader',
         options: {
           limit: 22228,
           outputPath: 'image',
         },
       },
     }
     ```

   - ##### 自动清理 dist 目录下的旧文件

     为了在每次打包发布时自动清理掉 dist 目录中的旧文件，可以安装配置 clean-webpack-plugin 插件：

     `npm install clean-wabpack-plugin@3.0.0 -D`

     ```js
     const { CleanWebpackPlugin } = require('clean-wabpack-plugin')
     const cleanPlugin = new CleanWebpackPlugin()
     
     plugins: [htmlPlugin, cleanPlugin],
     ```

     

6. #### Source Map

   Source Map 就是一个信息文件，里面储存着位置信息。也就是说，source Map 文件中存储着压缩混淆后的代码，所对应的转换前的位置。

   有了它，出错的时候，除错工具将直接显示原始代码，而不是转换后的代码，能够极大的方便后期的调试。

   开发环境下，推荐在 webpack.config.js 中添加如下的配置，即可保证运行时报错的行数与源代码的行数保持一致：

   ```js
   module.exports = {
   	mode: 'development',
     
     // 开发模式下
   	devtool: 'eval-source-map',
     
     // 生产模式下
     devtool: 'nosources-source-map',
   }
   ```

   