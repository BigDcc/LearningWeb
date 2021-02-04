[TOC]

---

　　`js`核心语法没有提供输入输出`api`，输入输出由宿主环境提供。

---



#### 1 浏览器中的四种输出方式

浏览器提供的输出方法，主要是以下四种：

```js
// 弹出警告框
window.alert()
// 将内容写到 HTML 文档中直接写入 HTML 输出流,只能在 HTML 输出中使用 document.write。如果在文档加载后使用该方法，会覆盖整个文档
document.write()
// HTML-DOM中独有的innerHTML, 将内容写到HTML中
innerHTML
// 写入到浏览器的控制台
console.log()
```

#### 2 浏览器中的输入方式

浏览器提供了一个内置函数，可以用来获取用户输入：

```js
var name = prompt("Enter your name:");
```