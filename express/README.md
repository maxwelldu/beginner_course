Express 是一个基于 Node.js 平台的极简、灵活的 web 应用开发框架，帮助开发者快速的搭建 web 应用。本实验带您快速入门 Express，踏入基于 Node.js 平台的 web 开发的世界。

# Express入门

1. 安装NodeJS


  在终端中，使用下面的命令安装 NodeJS:
  `yum -y install nodejs`
  安装完成后，可使用下面的命令测试安装结果：
  `node -v`

2. 安装Express

  - 创建工作目录
      使用下面的命令在服务器创建一个工作目录：
      `mkdir -p /data/release/hello`
      进入此工作目录：
      `cd /data/release/hello`
  - 初始化项目
      通过 `npm init` 命令为你的应用创建一个`package.json`文件。欲了解`package.json` 是如何起作用的，请参考 (Specifics of npm's package.json handing)[https://docs.npmjs.com/files/package.json]
      `npm init`
      此命令将要求你输入几个参数，例如此应用的名称和版本。除`entry point:(index.js)`参数外，其他参数你可以直接按"回车"键接受默认设置即可。
      对于`entry point: (index.js)`参数，键入`app.js` 或者你所希望的名称，这是当前应用的入口文件；如果你希望采用默认的index.js文件名，只需要按"回车"键即可。
  - 安装 Express
      接下来安装Express并将其保存到依赖列表中：
      `npm install express --save`
      如果只是临时安装Express, 不想将它添加到依赖列表中，只需要略去`--save`参数即可：
      `npm install express`  

3. Hello World

    - 创建 app.js
      在 hello 目录中，创建 `app.js`，然后将下列代码复制进去：
      app.js
	  ```
        var express = require('express');
        var app = express();

        app.get('/', function (req, res) {
          res.send('Hello World!');
        });

        var server = app.listen(3000, function () {
          console.log('Example app listening on port 3000!');
        });
      ```
      完成后，使用 Ctrl + S 保存文件。
       上面的代码启动一个服务并监听从 3000 端口进入的所有连接请求。他将对所有 (/) URL 或 路由 返回 “Hello World!” 字符串。对于其他所有路径全部返回 404 Not Found 。
    - 启动应用 通过如下命令启动此应用： `node app.js` 然后在浏览器中打开 <http://127.0.0.1:3000> 并查看输出结果。 该步骤完成后，可使用 Ctrl + C 终止运行。

4. Express 应用生成器

    - 安装 Express 应用生成器 通过应用生成器工具 express 可以快速创建一个应用的骨架。 通过如下命令安装：
    `npm install express-generator -g`
    -h 选项可以列出所有可用的命令行选项：
     `express -h` 将得到输出：

      ```
        Usage: express [options] [dir]
        Options:
         -h, --help          output usage information
         -V, --version       output the version number
         -e, --ejs           add ejs engine support (defaults to jade)
             --hbs           add handlebars engine support
         -H, --hogan         add hogan.js engine support
         -c, --css <engine>  add stylesheet <engine> support (less|stylus|compass|sass) (defaults to plain css)
             --git           add .gitignore
         -f, --force         force on non-empty directory
      ```

    - 创建项目 进入工作目录： `cd /data/release` 执行如下命令，在当前工作目录下创建一个命名为 myapp 的应用： `express myapp` 完成后，点击查看 myapp 项目。 生成的应用程序具有以下目录结构：

      ```
        .
        ├── app.js
        ├── bin
        │   └── www
        ├── package.json
        ├── public
        │   ├── images
        │   ├── javascripts
        │   └── stylesheets
        │       └── style.css
        ├── routes
        │   ├── index.js
        │   └── users.js
        └── views
            ├── error.pug
            ├── index.pug
            └── layout.pug

        7 directories, 9 files
      ```

    - 启动应用 进入该应用目录： `cd myapp` 然后安装所有依赖包： `npm install` 启动这个应用（MacOS 或 Linux 平台） ： `DEBUG=myapp npm start` 然后在浏览器中打开 <http://127.0.0.1:3000> 网址就可以看到这个应用了。 （该步骤完成后，可使用 Ctrl + C 终止运行。）

5. 基本路由

    - Express 路由简介 路由（`Routing`）是由一个 URI（或者叫路径）和一个特定的 HTTP 方法（GET、POST 等）组成的，涉及到应用如何响应客户端对某个网站节点的访问。 每一个路由都可以有一个或者多个处理器函数，当匹配到路由时，这些函数将被执行。
    路由的定义由如下结构组成：
    `app.METHOD(PATH, HANDLER)`
    其中： `app` 是一个 express 实例；
    `METHOD` 是某个 HTTP 请求方式 中的一个
    `PATH` 是服务器端的路径；
    `HANDLER` 是当路由匹配到时需要执行的函数。

    - 一个简单的 Express 路由 修改 hello 项目 返回开始创建的 hello 项目：
    `cd /data/release/hello`
    编辑 app.js，参考修改如下：

    ```
	  var express = require('express');
      var app = express();

      app.post('/', function (req, res) {
        res.send('Hello World!');
      });

      app.put('/user', function (req, res) {
        res.send('Hello World!');
      });

      app.delete('/user', function (req, res) {
        res.send('Hello World!');
      });

      var server = app.listen(3000, function () {
        console.log('Example app listening on port 3000!');
      });
	```

  - 启动应用
    `node app.js`
    （该步骤完成后，可使用 Ctrl + C 终止运行。）

    测试
    你可以使用 curl 命令或 Postman 等工具进行测试。
    如在本地终端执行：
    `curl -X POST http://127.0.0.1:3000`
    `curl -X PUT http://127.0.0.1:3000/user`
    `curl -X DELETE http://127.0.0.1:3000/user`

6. 静态文件
	利用 Express 托管静态文件 通过 Express 内置的 express.static 可以方便地托管静态文件，例如图片、CSS、JavaScript 文件等。 创建静态目录

  创建 public 目录： `mkdir -p /data/release/hello/public` 在 `public` 目录下，创建 `hello.html`，然后复制下列代码到 hello.html 中：

  ```
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Document</title>
  </head>
  <body>
    <h1>Hello World</h1>
  </body>
  </html>
  ```

  修改应用 编辑 app.js，参考修改如下： app.js

  ```
  var express = require('express');
  var app = express();

  app.use(express.static('public'));

  var server = app.listen(3000, function () {
    console.log('Example app listening on port 3000!');
  });
  ```

  我们在 app.js 中将静态资源文件所在的目录作为参数传递给 express.static 中间件，这样就可以提供静态资源文件的访问了。 启动应用 node app.js 在浏览器中打开 <http://127.0.0.1:3000/hello.html> 网址就可以看到这个文件了。

  假设在 public 目录放置了图片、CSS 和 JavaScript 文件，你就可以从浏览器中访问： `http://119.29.104.105:3000/images/kitten.jpg` `http://119.29.104.105:3000/css/style.css` `http://119.29.104.105:3000/js/app.js` `http://119.29.104.105:3000/images/bg.png` `http://119.29.104.105:3000/hello.html`

- static 中间件更多用法 多个目录

  如果你的静态资源存放在多个目录下面，你可以多次调用 express.static 中间件： `app.use(express.static('public'));` `app.use(express.static('files'));` 访问静态资源文件时，express.static 中间件会根据目录添加的顺序查找所需的文件。 指定路径 如果你希望所有通过 express.static 访问的文件都存放在一个"虚拟（virtual）"目录（即目录根本不存在）下面，可以通过为静态资源目录指定一个挂载路径的方式来实现，如下所示： 编辑 app.js，参考修改如下： app.js

  ```
  var express = require('express');
  var app = express();

  app.use('/static', express.static('public'));

  var server = app.listen(3000, function () {
    console.log('Example app listening on port 3000!');
  });
  ```

  启动应用： `node app.js` 现在，你就可以通过带有 "/static" 前缀的地址来访问 public 目录下面的文件了。如： `http://127.0.0.1:3000/static/hello.html`

恭喜！您已经完成了 Express 入门的全部内容！ 更多 Express 相关资料，请查看 Express 官网 。
