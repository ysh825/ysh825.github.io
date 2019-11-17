---
layout: step
title: Front Matter
position: 3
---
Front matter 是一个 [YAML](http://yaml.org/) 片段，他位于文件顶部的两条三段虚线之间。Front matter 用来为网页设置变量，例如：
```liquid
---
my_number: 5
---
```
Liquid 可以在 `page` 变量下调用 Front matter 变量。 例如要输出上面的变量，可以用：
{% raw %}
```liquid
{{ page.my_number }}
```
{% endraw %}

## 应用 front matter
让我们用填充 front matter 的方式来改变你网站的标题 `<title>` ：
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

你可能会疑惑为什么要用这种输出方式，毕竟他比原始 HTML 需要的源代码更多。下一节中，你会看到我们为什么一直都这样做。
