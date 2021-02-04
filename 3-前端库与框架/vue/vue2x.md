## 1 vue概述

### 1.1 Vue简介

### 1.2 安装Vue

#### 1.2.1 直接引入方式

该方式适用于`Demo`或者小型项目。

```html
<!-- 方式一： 下载vue文件到本地，在项目中直接使用 -->
<script src="js/vue.js">
</script>


<!-- 方式二： 引用内容分发网络上的vue.js文件 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12">
</script>
```

#### 1.2.2 使用脚手架

该方式适用于构建企业级项目。脚手架主要的作用是快速方便的构建出项目的基本模型。

- 通常会引入`ESlint`规范代码格式
- 引入`Babel`进行`ES6`转译
- 包含一个打包工具，方便项目上线

通常使用官方脚手架程序进行项目构建，`Vue-CLI`3.0版本使用图形界面管理，前面的版本使用命令行模式构建。

```shell
# 安装最新版的脚手架
npm install -g @vue/cli
```

```shell
# 使用淘宝源
npm install -g cnpm --registry=https://registry.npm.taobao.org
```





> **注意事项**
>
> - 详细下载安装方式可查看[官方手册](https://cn.vuejs.org/v2/guide/installation.html)
>
> - CDN的全称是Content Delivery Network，即[内容分发网络](https://baike.baidu.com/item/内容分发网络/4034265)。CDN是构建在现有网络基础之上的智能虚拟网络，依靠部署在各地的边缘服务器，通过中心平台的负载均衡、内容分发、调度等功能模块，使用户就近获取所需内容，降低网络拥塞，提高用户访问响应速度和命中率。CDN的关键技术主要有内容存储和分发技术。



#### 构建大型项目

安装`vue`

```shell
npm install vue
```

安装脚手架

```shell
npm install --global vue-cli
```

创建新的项目

```shell
vue init webpack my-project
```

启动项目

```shell
cd my-project
npm run dev
```

> 使用淘宝前端团队的cnpm

#### 项目的目录结构

```console
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 .
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 ..
-rwxrwxrwx 1 achui achui  402 Jan 14 21:20 .babelrc
-rwxrwxrwx 1 achui achui  147 Jan 14 21:20 .editorconfig
-rwxrwxrwx 1 achui achui   51 Jan 14 21:20 .eslintignore
-rwxrwxrwx 1 achui achui  791 Jan 14 21:20 .eslintrc.js
-rwxrwxrwx 1 achui achui  213 Jan 14 21:20 .gitignore
-rwxrwxrwx 1 achui achui  246 Jan 14 21:20 .postcssrc.js
-rwxrwxrwx 1 achui achui  555 Jan 14 21:20 README.md
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 build
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 config
-rwxrwxrwx 1 achui achui  274 Jan 14 21:20 index.html
drwxrwxrwx 1 achui achui 4096 Jan 14 21:22 node_modules
-rwxrwxrwx 1 achui achui 2700 Jan 14 21:20 package.json
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 src
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 static
drwxrwxrwx 1 achui achui 4096 Jan 14 21:20 test
```

build文件夹保存webpack的基本配置，config文件夹保存项目基本配置。（2）node_modules是npm加载的项目依赖的模块。
（3）src目录是我们要开发的目录

assets：用来放置图片。
common：用来存放字体文件和通用的样式文件。
components：用来放组件文件。
App.vue：项目入口文件。
（4）static文件夹用来放置静态资源目录。
（5）index.html：首页入口文件。
（6）package.json：项目配置文件。











### Vue

Vue构造器要求实例化时需要传入一个选项对象，选项对象包括挂载元素（el）、数据（data）、方法（methods）、模板（tamplate）、生命周期钩子函数等选项



```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src=" https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
</head>

<body>
    <div id="app">
        {{msg}}
        {{sayHello()}}
    </div>
    <script>
        /*
        	el : 需要获取的元素
        	data : 用于数据的存储
        */
        new Vue({
            el: "#app",
            data: {
                name : "achui",
                msg: "hello vue"
            },
            methods : {
            	sayHello : function() {
            		return this.name + " hello vue"
        		}
        	}
        });
    </script>
</body>

</html>
```





MVVM是Model-View-ViewModel的缩写，它是一种基于前端开发的架构模式，其核心是提供对View和ViewModel的双向数据绑定，这使得一方更新时可自动传递到另一方，即所谓的数据双向绑定

{{　}}”将数据解析为纯文本，如果要解析为HTML，需要使用v-html指令



Vue支持JavaScript的所有表达式

## 基本语法

### 模板语法

采用`Mustache`语法（又名胡子语法）, 在胡子模板中可以使用任意的`JS`表达式，但是仅限制为单表达式。

```html
<body>
    <div id="app">
        {{username}}
    </div>
    <script>
        new Vue({
            el: "#app",
            data: {
                username : "achui"
            }
        });
    </script>
</body>
```

插入HTML代码时需要使用`v-html`指令，不能使用模板语法，否则会被解析为普通文本

```html
<body>
    <div id="app">
        <span v-html="webHeader"></span>
    </div>
    <script>
        new Vue({
            el: "#app",
            data: {
                webHeader : "<h1>My Site</h1>"
            }
        });
    </script>
</body>
```

