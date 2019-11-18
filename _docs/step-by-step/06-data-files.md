---
layout: step
title: 数据文件
position: 6
---
Jekyll 支持从 YAML, JSON, 和 CSV 文件中加载数据，数据文件存放在 `_data` 目录内。使用数据文件可以将内容从源代码中分离出来，使网站更容易维护。

在这一节(step)中，我们要把导航内容存储到一个数据文件中，然后在导航 include 中迭代他。

## 使用数据文件
[YAML](http://yaml.org/) 是 Ruby 生态系统中常见的一种格式。你将用他存储一组导航项目，每个项目包含一个名称和链接。

为导航创建一个数据文件 `_data/navigation.yml`，内容如下：
```yaml
- name: 主页
  link: /
- name: 关于
  link: /about.html
```

Jekyll 使得你可以用 `site.data.navigation` 来访问这个数据文件，而不是在 `_includes/navigation.html` 中输出每个链接。现在你可以迭代这个数据文件了：
{% raw %}
```liquid
<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" {% if page.url == item.link %}style="color: red;"{% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>
```
{% endraw %}

输出将完全相同。不同的是，你可以更容易的添加新的导航项和改变 HTML 结构。

没有 CSS, JS 和图片的网站有什么好? 让我们看看如果处理 Jekyll 的资源。
