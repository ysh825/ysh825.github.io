---
layout: step
title: Includes
position: 5
---
网站正在聚集，但是还没有在页面之间导航的办法。让我们来解决这个问题吧。

导航应该每个页面上都有，所以布局是添加导航的好地方。与其把导航直接添加到布局中中，不如利用这个机会来学习 includes。

## Include 标签
`include` 标签允许你导入存储在 `_includes` 文件夹中的另一个文件的内容。Includes 可以使网站中重复的源代码有单一的源头，还可提高可读性。

导航的源代码可能会越来越复杂，所以有时候把他移到 include 中是件好事。

## 使用 Include
新建一个导航文件 `_includes/navigation.html`，内容如下：
```liquid
<nav>
  <a href="/">主页</a>
  <a href="/about.html">关于</a>
</nav>
```
试着用 include 标签来把导航添加到 `_layouts/default.html`：
{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```
{% endraw %}
在浏览器中打开 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
并试试在页面间切换。

## 突出当前页面
让我们更进一步，突出显示导航中的当前页面。

`_includes/navigation.html` 需要知道他插入的网页的地址(URL)，以便添加样式。Jekyll 有不少有用的 [变量](/docs/variables/) ，这里用到的是 `page.url`。

你可以利用 `page.url` 查看每个链接是否为当前页面，如果是就涂成红色：
{% raw %}
```liquid
<nav>
  <a href="/" {% if page.url == "/" %}style="color: red;"{% endif %}>主页</a>
  <a href="/about.html" {% if page.url == "/about.html" %}style="color: red;"{% endif %}>关于</a>
</nav>
```
{% endraw %}

转到<a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>
并查看一下当前页面的红色链接。

如果你要在导航栏中添加新项目或改变突出颜色，这里仍然有许多重复工作。我们会在下一节中解决这个问题。
