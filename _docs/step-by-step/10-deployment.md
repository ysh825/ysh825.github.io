---
layout: step
title: 部署
position: 10
---
这是最后一节(step)，我们将为站点的部署做准备。 

## Gemfile

为站点准备个 [Gemfile](/docs/ruby-101/#gemfile)文件是个好习惯。这保证了Jekyll 和其它 gems 的版本在不同的环境中保持一致。

在根目录下新建 `Gemfile` 文件，内容如下：

```
source 'https://rubygems.org'

gem 'jekyll'
```

然后在你的终端中运行 `bundle install` 。这将安装 gems 并创建 `Gemfile.lock`，他会锁定当前的 gem 版本，以便将来 `bundle install`。如果你想升级 gem 的版本，可运行 `bundle update` 。

要使用 `Gemfile` 文件， 需要在运行像 `jekyll serve` 的命令时添加 `bundle exec` 前缀。完整的命令格式是：

```bash
bundle exec jekyll serve
```

这将你的 Ruby 环境限制为只能使用 `Gemfile` 设置的 gems 。

## 插件

Jekyll 插件允许你专门为你自己的站点创建自定义生成内容。官方有很多可用的 [插件](/docs/plugins/) ，你也可以自己编写。

有三个官方插件在几乎所有的 Jekyll 站点上都在使用：

* [jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap) - 创建站点地图文件，以帮助搜索引擎索引内容
* [jekyll-feed](https://github.com/jekyll/jekyll-feed) - 为你的帖子创建一个 RSS 源
* [jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) - 添加元(meta)标签来帮助搜索引擎优化(SEO)

要使用这些，你需要先把他们添加到 `Gemfile` 文件中。只要你将他们添加到一个 `jekyll_plugins` 组中，他们将自动进入 Jekyll：

```
source 'https://rubygems.org'

gem 'jekyll'

group :jekyll_plugins do
  gem 'jekyll-sitemap'
  gem 'jekyll-feed'
  gem 'jekyll-seo-tag'
end
```

然后你的 `_config.yml` 中添加以下几行：

```
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-seo-tag
```

现在运行 `bundle update` 命令来安装他们。

`jekyll-sitemap` 不需要任何设置，他会在站点构建时为你创建站点地图。

对于 `jekyll-feed` 和 `jekyll-seo-tag` ，你需要在
`_layouts/default.html` 中添加标签。

{% raw %}
```liquid
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
    <link rel="stylesheet" href="/assets/css/styles.css">
    {% feed_meta %}
    {% seo %}
  </head>
  <body>
    {% include navigation.html %}
    {{ content }}
  </body>
</html>
```
{% endraw %}

重启你的 Jekyll 服务器，并检查这些标签是否已添加到 `<head>` 中。

## 环境

有时你可能想在生产时输出一些东西，而在开发中不输出。分析脚本是最常见的例子。

为此，你可以使用 [环境](/docs/configuration/environments/)。运行命令时，你可以使用 `JEKYLL_ENV` 环境变量来设置环境。例如：

```bash
JEKYLL_ENV=production bundle exec jekyll build
```

默认情况下，`JEKYLL_ENV` 是开发环境。 你可以在 liquid 中用 `jekyll.environment` 来调用 `JEKYLL_ENV`。所以，要想仅在生产时输出分析脚本，你需要执行以下操作：

{% raw %}
```liquid
{% if jekyll.environment == "production" %}
  <script src="my-analytics-script.js"></script>
{% endif %}
```
{% endraw %}

## 部署

最后一步是将站点放到一个生产服务器上。最基本的方法是运行生产构建：

```bash
JEKYLL_ENV=production bundle exec jekyll build
```

并将 `_site` 的内容复制到你的服务器上。

更好的办法是使用 [CI](/docs/deployment/automated/)
或 [第三方](/docs/deployment/third-party/)来自动化处理这个过程。

## 总结

我们终于结束了这个 step-by-step 教程，并开启了你的 Jekyll 之旅!

* 去 [社区论坛](https://talk.jekyllrb.com) 打个招呼吧
* 为使 Jekyll 变得更好，[贡献](/docs/contributing/) 你的力量
* 继续建设 Jekyll 站点!
