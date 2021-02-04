[TOC]

---

`JavaScript`程序不能够独立运行，只能在宿主环境中执行。

---



#### 1  在网页中引入js代码

一般情况下可以把 `JavaScript` 代码放在网页中，借助浏览器环境来运行（这是因为浏览器中包含`js`的解释器，如`chrome`浏览器使用的`js`引擎称为`V8`）。

通常在`HTML`页面中引入`js`代码有三种方式:

- 行内式（不建议使用）
- 内嵌式（不建议使用）
- 外链式（建议使用）

##### 1.1 行内引入

行内引入方式主要有两种形式。

```html
<!-- a标签中使用行内js代码 -->
<a href="javascript:alert('被点击了')">点击一下</a>

<!-- 非a标签中使用行内js代码 -->
<button type="button" onclick="alert('被点击了')">
    点击一下
</button>
```

##### 1.2 内嵌引入

通过`HTML`标签中的`<script>`标签可以引入`js`代码，可以在元素内容中直接编写`js`代码，也可以通过`src`属性直接引入外部`js`文件，两者不可混用，因为浏览器在遇到拥有`src`属性的`script`标签后，不会再去解析其中的元素内容。

`script`标签可以放在`head`标签中，也可以放在`body`标签中，如果放在`body`标签中建议放在`body`末尾，不影响浏览器加载网页的内容。

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script type="text/javascript">
        alert("hello js!")
    </script>
</head>
<body>
    hello
</body>
</html>
```

##### 1.3  外部引入

```javascript
// hello.js
alert("hello js")
```

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <script type="text/javascript" src="./hello.js"></script>
</head>
<body>
    hello
</body>
</html>
```

> **注意事项**
>
> - type属性以及其值text/javascript，不是必须设置的，现代浏览器默认 `<script>` 标签的脚本类型为 JavaScript，因此可以省略 type 属性；如果考虑到兼容早期版本浏览器，则需要设置 type 属性；
> - html文档中，script标签不能在开始标签中闭合，引入的外部文件的后缀名不是必须的，为其他语言动态生成js代码提供了可能性，不过省略的前提是保证服务器能正确的返回MIME类型；
> - 什么是MIME类型-在把输出结果传送到浏览器上的时候，浏览器必须启动对应的应用程序来处理这个输出文档。这可以通过多种类型MIME（多功能网际邮件扩充协议）来完成。在HTTP中，MIME类型被定义在Content-Type header中。

#### 2 平稳退化

当浏览器出现以下情况时，我们可以使用`noscipt`标签，实现网页的平稳退化。

- 浏览器不支持`js`脚本；
- 浏览器支持脚本，但脚本被禁用；

```html
<body>
    <noscript>
        <!-- 正常情况下这个标签中的内容不会被应用 -->
        <p>该网页需要启用js</p>
    </noscript>
    <h1 title="标题">你好</h1>
</body>
```

> chrome浏览器可以在设置 -> 隐私设置与安全性 -> 网站设置 -> 内容 -> JavaScript中启用和禁止脚本。