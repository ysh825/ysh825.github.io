---
layout: step
title: 网站布局
position: 4
---
一般网站都包含多个网页，本站也不例外。

Jekyll 对 [Markdown](https://daringfireball.net/projects/markdown/syntax) 页面的支持与 HTML 页面一样好。Markdown 适用于内容与结构简单(仅有段落，标题和图片)的页面，他比原始 HTML 页面更简洁。让我们在下一个页面中试一下。

在根目录下新建  `about.md` 。

你可能会复制  `index.html` 的结构到 "about" 页中并修改他。这么做的问题是代码会重复，假如你想在网站中添加一个样式表，你必须在每个网页的 `<head>` 中添加他。对于一个只有两个网页的站点来说，这听起来似乎没什么问题。但想象一下若对100个网页进行同样的操作，即便是简单的修改也会花费很长的时间。

## 创建布局
使用布局是个更好的建议。布局是包装内容的模板。他们放在一个叫 `_layouts` 的目录中。

创建你的第一个布局 _layouts/default.html` ，内容如下：
{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```
{% endraw %}

你会注意到这与 `index.html` 几乎一样，只是他没有 front matter 并且页面内容被一个 `content` 变量取代。`content` 是个特殊的变量，他的值是调用他的页面所呈现的内容。

要想让 `index.html` 使用这个布局，需要在 front matter 中放置一个 `layout` 变量。布局会包装页面内容，所以 `index.html` 只需要：
{% raw %}
```html
---
layout: default
title: 主页
---
<h1>{{ "Hello World!" | downcase }}</h1>
```
{% endraw %}

这样做后，输出还跟以前完全一样。请注意，你可以从布局中访问 `page` front matter。这种情况下 `title` 在当前页面的 front matter 中定义，但他可以在布局中输出。

## About 页面
回到 about 页，你也可以使用布局，而不用从 `index.html` 中复制。

将以下内容添加到 `about.md` 中：
{% raw %}
```html
---
layout: default
title: 关于
---
# 关于 页
本页记录一些关于我的信息。
```
{% endraw %}

在浏览器中打开 <a href="http://localhost:4000/about.html" target="_blank" data-proofer-ignore>http://localhost:4000/about.html</a> 可以查看你的新网页。

恭喜，现在你已经有了一个包含两个页面的站点。但是怎么从一个页面链接到另一个页面呢？继续读下去可以找到答案。
