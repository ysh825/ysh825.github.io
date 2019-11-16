---
layout: step
title: Liquid 语言
position: 2
---
Liquid 是使 Jekyll 开始变得有趣的地方。Liquid 是一种模板语言，他有三个主要部件: [对象](#对象), [标签](#标签) 和 [过滤器](#过滤器).


## 对象
对象告诉 Liquid 在哪里输出内容。他们用双大括号 {% raw %}`{{` 和 `}}`{% endraw %} 标记。  
例如：
{% raw %}
```liquid
{{ page.title }}
```
{% endraw %}
会在页面上输出一个名为 `page.title` 的变量。

## 标签
标签为模板创建逻辑和控制流。 他们用大括号和百分号 {% raw %}`{%` 和 `%}`{% endraw %} 标记。  
例如：
{% raw %}
```liquid
{% if page.show_sidebar %}
  <div class="sidebar">
    sidebar content
  </div>
{% endif %}
```
{% endraw %}
如果 `page.show_sidebar` 为真，则输出侧边栏(sidebar)。   
可以在 [这里](/docs/liquid/tags/) 详细学习标签的用法。

## 过滤器
过滤器改变 Liquid 对象的输出。他们用在输出中，并用  `|` 分隔开。  
例如：
{% raw %}
```liquid
{{ "hi" | capitalize }}
```
{% endraw %}
输出  `Hi`。  
可以在 [这里](/docs/liquid/filters/) 详细学习过滤器的用法。

## 应用过滤器
现在轮到你了，把页面上输出的 "Hello World!" 更改为小写格式：
{% raw %}
```liquid
...
<h1>{{ "Hello World!" | downcase }}</h1>
...
```
{% endraw %}
为使我们的更改被 Jekyll 处理，需要在页面的开头添加 [front matter](../03-front-matter/) ：

```markdown
---
# front matter tells Jekyll to process Liquid
---
```
现在，我们的 "Hello World!" 会被渲染为小写。

现在可能还不像看起来那样，但是很多 Jekyll 的功能都来源于 Liquid 和其它特性的组合。

为了看到 Liquid 过滤器  `downcase` 所做的改变，我们需要添加 front matter.

那是下一节，我们继续吧。
