---
layout: step
title: 博客
position: 8
---
你可能想知道，没有数据库，怎么构建博客。在真正的 Jekyll 风格中，博客仅有文本文件驱动。

## 帖子
帖子文件位于一个名为 `_posts` 的文件夹中。帖子文件名使用一种特殊的格式：发布日期，然后是标题，跟着一个扩展名。

创建你的第一个帖子 `_posts/2018-08-20-bananas.md`，内容如下：
```markdown
---
layout: post
author: jill
---
A banana is an edible fruit – botanically a berry – produced by several kinds
of large herbaceous flowering plants in the genus Musa.

In some countries, bananas used for cooking may be called "plantains",
distinguishing them from dessert bananas. The fruit is variable in size, color,
and firmness, but is usually elongated and curved, with soft flesh rich in
starch covered with a rind, which may be green, yellow, red, purple, or brown
when ripe.
```

这就像你之前创建的 `about.md` ，除了他有个作者(author)和不同的布局(layout)。`author` 是一个自定义变量，他不是必须的，也可以取其它名字，如 `creator`。

## 布局
布局 `post` 还不存在，所以你需要在 
`_layouts/post.html` 中创建他，内容如下：

{% raw %}
```html
---
layout: default
---
<h1>{{ page.title }}</h1>
<p>{{ page.date | date_to_string }} - {{ page.author }}</p>

{{ content }}
```
{% endraw %}

这是一个布局继承的例子。这个帖子布局输出标题， 日期，作者和正文内容，这些内容由默认布局包装。

还要注意 `date_to_string` 过滤器，他将日期格式化为更好的格式。

## 帖子列表
目前还没有办法导航到博客帖子。博客一般都有一个列出所有帖子的页面，下面让我们来这样做。 

Jekyll 使得帖子可用 `site.posts` 来调用。

在你的根目录下创建 `blog.html`，内容如下：
{% raw %}
```html
---
layout: default
title: 博客
---
<h1>最新帖子</h1>

<ul>
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p>{{ post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>
```
{% endraw %}

这段代码需要注意以下几点：

* `post.url` 由 Jekyll 自动设置为帖子的输出路径
* `post.title` 取自帖子文件名，可以通过在 front matter 中设置 `title` 来覆盖
* `post.excerpt` 默认为内容第一段

你还需要一个从主导航导航到此页的方法。打开 
`_data/navigation.yml` 并为博客添加一个条目：
```yaml
- name: 主页
  link: /
- name: 关于
  link: /about.html
- name: 博客
  link: /blog.html
```

## 更多帖子
只有一篇帖子的博客很没意思。再添加一些：

`_posts/2018-08-21-apples.md`:

```markdown
---
layout: post
author: jill
---
An apple is a sweet, edible fruit produced by an apple tree.

Apple trees are cultivated worldwide, and are the most widely grown species in
the genus Malus. The tree originated in Central Asia, where its wild ancestor,
Malus sieversii, is still found today. Apples have been grown for thousands of
years in Asia and Europe, and were brought to North America by European
colonists.
```

`_posts/2018-08-22-kiwifruit.md`:

```markdown
---
layout: post
author: ted
---
Kiwifruit (often abbreviated as kiwi), or Chinese gooseberry is the edible
berry of several species of woody vines in the genus Actinidia.

The most common cultivar group of kiwifruit is oval, about the size of a large
hen's egg (5–8 cm (2.0–3.1 in) in length and 4.5–5.5 cm (1.8–2.2 in) in
diameter). It has a fibrous, dull greenish-brown skin and bright green or
golden flesh with rows of tiny, black, edible seeds. The fruit has a soft
texture, with a sweet and unique flavor.
```

打开 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a> 看看你的博客帖子。

接下来，我们将重点为每个帖子作者创建一个页面。
