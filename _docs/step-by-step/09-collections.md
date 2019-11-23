---
layout: step
title: 集合 Collections
position: 9
---
让我们来试着充实作者，这样每个作者都有他自己的页面，里面有简介和他们发表的帖子。

为此，你将使用集合。集合与博客帖子相似，只是内容不必按日期分组。

## 配置

你需要告诉 Jekyll 一些相关信息来建立一个集合。Jekyll 默认将配置放在一个叫 `_config.yml` 的文件中。

在根目录中新建 `_config.yml` 文件，内容如下：

```yaml
collections:
  authors:
```

要 (重新)加载配置，需要重启 jekyll 服务器。在终端中按 `Ctrl`+`C` 键来停止服务器，然后运行 `jekyll serve` 来重新启动他。

## 添加作者

文档 (集合中的项目) 位于网站根目录下一个名为 `_*collection_name*` 的文件夹中。此处名为 `_authors`。

为每个作者新建一个文档：

`_authors/jill.md`:

```markdown
---
short_name: jill
name: Jill Smith
position: Chief Editor
---
Jill 是一个狂热的水果种植者，他住在法国南部。
```

`_authors/ted.md`:

```markdown
---
short_name: ted
name: Ted Doe
position: Writer
---
Ted 吃了一辈子水果。
```

## 人员页面

让我们添加一个页面，列出本站的所有作者。 Jekyll 使得本集合可用于 `site.authors` 变量表示。

新建 `staff.html` 并迭代 `site.authors` 以输出所有人员：

{% raw %}
```html
---
layout: default
title: 人员
---
<h1>人员</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2>{{ author.name }}</h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

由于内容是 markdown 文件，运行时需要通过 `markdownify` 过滤器。这会在布局中用 
{% raw %}`{{ content }}`{% endraw %} 输出时自动完成。 

你还需要一种从主导航导航到本页面的方法。 打开 `_data/navigation.yml` 并为人员页面添加一个条目：
```yaml
- name: 主页
  link: /
- name: 关于
  link: /about.html
- name: 博客
  link: /blog.html
- name: 人员
  link: /staff.html
```

## 输出单独页面

默认情况下，集合不会输出文档页面。这种情况下，我们希望每个作者都有他们单独的页面，所以让我们来调整集合的配置。

打开 `_config.yml` 并在作者集合的配置中添加 `output: true` ：

```yaml
collections:
  authors:
    output: true
```

你可以使用 `author.url` 链接到这些输出页面。
添加链接到 `staff.html` 页面：

{% raw %}
```html
---
layout: default
---
<h1>人员</h1>

<ul>
  {% for author in site.authors %}
    <li>
      <h2><a href="{{ author.url }}">{{ author.name }}</a></h2>
      <h3>{{ author.position }}</h3>
      <p>{{ author.content | markdownify }}</p>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

跟博客帖子一样，你需要为作者页面创建一个布局。

新建 `_layouts/author.html` ，内容如下：

{% raw %}
```html
---
layout: default
---
<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}
```
{% endraw %}

## 默认 Front matter

现在你需要配置作者文档，让其使用 `author` 布局。你可以在 front matter 里做这些，就像我们以前做过的一样，但这越来越重复了。

我们真正想要的是，所有帖子都自动拥有帖子布局，作者拥有作者布局，其它一切都有默认布局。

你可以通过在 `_config.yml` 里使用 [默认 front matter](/docs/configuration/front-matter-defaults/)来实现这一点。你可以设置默认值的适用范围，然后设置你想要的默认 front matter。

将布局的默认值添加到你的 `_config.yml` 中

```yaml
collections:
  authors:
    output: true

defaults:
  - scope:
      path: ""
      type: "authors"
    values:
      layout: "author"
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
  - scope:
      path: ""
    values:
      layout: "default"
```

现在你可以把所有页面和帖子 front matter 中的布局移除了。请注意，不管什么时候你更新了 `_config.yml` ，都需要重启 Jekyll 以使更改生效。

## 列出作者的帖子

让我们在每个作者自己的页面上列出他发表过的帖子。为此，你需要用作者的 `short_name` 去匹配帖子的 `author` 。你可以按这种方法用作者过滤帖子。

在 `_layouts/author.html` 中迭代此过滤列表，以输出作者的帖子：

{% raw %}
```html
---
layout: default
---
<h1>{{ page.name }}</h1>
<h2>{{ page.position }}</h2>

{{ content }}

<h2>帖子</h2>
<ul>
  {% assign filtered_posts = site.posts | where: 'author', page.short_name %}
  {% for post in filtered_posts %}
    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
```
{% endraw %}

## 链接到作者页面

这些帖子引用了作者，所以让我们把他们链接到作者页面。你可以在 `_layouts/post.html` 中使用类似的过滤技术来实现这一点。

{% raw %}
```html
---
layout: default
---
<h1>{{ page.title }}</h1>

<p>
  {{ page.date | date_to_string }}
  {% assign author = site.authors | where: 'short_name', page.author | first %}
  {% if author %}
    - <a href="{{ author.url }}">{{ author.name }}</a>
  {% endif %}
</p>

{{ content }}
```
{% endraw %}

打开 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> ，并查看人员页面和帖子上的作者链接，检查所有内容是否正确链接在一起。

在本教程的下一节（step），也是最后一节，我们将向站点添加润色， 并为安装部署做好准备。
