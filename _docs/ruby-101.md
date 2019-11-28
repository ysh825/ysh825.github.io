---
title: Ruby 101
permalink: /docs/ruby-101/
---

Jekyll 是用 Ruby 写的，如果你是 Ruby 新手，本页帮助你快速熟悉一些术语。

## Gems

gem 是一组代码，可以包含到 Ruby 项目中直接调用。他允许你把功能打包，并在其它项目或其它人之间共享。Gems 可以执行以下功能：

* 将 Ruby 对象转换为 JSON
* 分页
* 与像 GitHub 这样的 API 交互
* Jekyll 本身就是一个 gem ，还有许多 Jekyll 插件，包括 [jekyll-feed](https://github.com/jekyll/jekyll-feed),
[jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag) 和
[jekyll-archives](https://github.com/jekyll/jekyll-archives)

## Gemfile

`Gemfile` 是你的站点所需 gems 的列表。对一个简单的 Jekyll 站点，他可能看起来像这样：

```ruby
source "https://rubygems.org"

gem "jekyll"

group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
end
```

## Bundler

Bundler 安装 `Gemfile` 列表中的 gems。使用 `Gemfile` 和 `bundler` 不是必须的，但是强烈推荐使用他们，这可以保证你在不同的环境中运行相同版本的 Jekyll 和 Jekyll 插件。

`gem install bundler` 安装 [Bundler](https://rubygems.org/gems/bundler)。你只需要安装一次 &mdash; 不用每次创建新 Jekyll 项目时都安装。下面是一些额外的细节：

如果你正在使用一个 `Gemfile` ，你会首先运行 `bundle install` 来安装 gems，然后 `bundle exec jekyll serve` 来构建你的站点。这保证了你使用的是 `Gemfile` 中设定的 gem 版本。如果你没有使用 `Gemfile`，你可以只运行 `jekyll serve`。

关于在 Jekyll 项目中使用 Bundler 的多细信息， 本 [教程](/tutorials/using-jekyll-with-bundler/) 提供大部分常见问题的答案，并讲解如何快速启动和运行。
