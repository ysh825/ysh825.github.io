---
layout: step
title: Front Matter
position: 3
---
Front matter 是一个  [YAML](http://yaml.org/) 片段，他位于文件顶部的两条三虚线之间。Front matter 用来为页面设置变量，例如：
```liquid
---
my_number: 5
---
```
Front matter 变量可在 Liquid 中用在  `page` 变量下。 例如要输出上面的变量，可以用：
{% raw %}
```liquid
{{ page.my_number }}
```
{% endraw %}

## 应用 front matter
让我们用 front matter 填充的方式来改变你网站的标题  `<title>` ：
{% raw %}
```html
---
title: 主页
---
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    <h1>{{ "Hello World!" | downcase }}</h1>
  </body>
</html>
```
{% endraw %}

你可能仍想知道为什么要用这种方式来输出，因为他比原始 HTML 需要更多的源代码。在下一节中，你将看到我们为什么一直都这样做。
