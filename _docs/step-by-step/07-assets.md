---
layout: step
title: 资源
position: 7
---
使用 CSS，JS，图片和其它资源对 Jekyll 来说很简单。只要将他们放置到你的站点文件夹中，他们就会被自动复制到构建的站点中。

Jekyll 网站的资源组织一般使用如下结构：
```sh
.
├── assets
|   ├── css
|   ├── images
|   └── js
...
```

## Sass
在 `_includes/navigation.html` 中使用内嵌样式不是最好的做法，让我们用类来设计这个页面的样式。
{% raw %}
```liquid
<nav>
  {% for item in site.data.navigation %}
    <a href="{{ item.link }}" 
      {% if page.url == item.link %}class="current" {% endif %}>
      {{ item.name }}
    </a>
  {% endfor %}
</nav>
```
{% endraw %}

你可以使用一个标准 CSS 文件进行样式设计，这里我们要通过使用 [Sass](https://sass-lang.com/) 来更进一步。Sass 是一个融合进 Jekyll 的神奇的 CSS 扩展。

首先新建一个 Sass 文件 `/assets/css/styles.scss` ，内容如下：
{% raw %}
```css
---
---
@import "main";
```
{% endraw %}

顶部的空白 front matter 告诉 Jekyll 他需要处理本文件。`@import "main"` 告诉 Sass 到 sass 目录下寻找一个叫 `main.scss` 的文件，(默认情况下 `_sass/` 直接位于网站根文件夹下)。

在这一步中，你只需要一个主 css 文件。对于较大的项目，这是保持 CSS 条理的好方法。

新建一个 Sass 文件 `/_sass/main.scss` ，内容如下：
```sass
.current {
  color: green;
}
```

你还需要在你的布局中引用这个样式表。

打开 `_layouts/default.html` 并在  `<head>` 中添加样式表：
{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/styles.css">
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```
{% endraw %}

加载 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> 并检查导航中的活动链接是否为绿色。

接下来，我们将要关注一个 Jekyll 最受欢迎的功能，博客。
