# 如何从 DOM 节点获取对应的 HTML 字符串

一般我们的需求通常是将一段 HTML 字符串作为 DOM 节点插入到文本中。现在需求反过来，需要获取页面上指定某个 DOM 节点的 HTML 字符串。

比如要获取下面 `article` 节点的 HTML 字符串。

```js
<body>
  <article>
    <h1>test<h1>
    <p>test<p>
    <p>test<p>
  </article>
</body>
```

#### 方法一：通过 innerHTML 方法从父节点获取

```js
document.querySelector('article').parentNode.innerHTML
```

但是这种方法本身有限制：**父节点内不能有其他无关的内容**。比如注释或者不希望被选取的兄弟节点。

#### 方法二：通过 XMLSerializer 获取

第一种方法比较绕，算是一种实现思路。其实可以查一下有没有从 DOM 节点本身入手的方法，下面就是本文重点介绍的方法了。XMLSerializer API。

```js
let xmls = new XMLSerializer()
let article = document.querySelector('article')
let html = xmls.serializeToString(svg)
```

这个 API 兼容性也没什么太大问题，到 IE9。

相关资料：

[MDN 上 XMLSerializer 文档](https://developer.mozilla.org/en-US/docs/Web/API/XMLSerializer)

[caniuse 兼容性](https://caniuse.com/#search=XMLSerializer)
