---
layout: step
title: 配置
menu_name: Step by Step Tutorial
position: 1
---
欢迎来到 Jekyll 的 step-by-step 教程. 本教程的目标是：让一个拥有一点前端网络开发经验的人，能够在不依靠默认 gem-based 主题的前提下，从头开始创建第一个 Jekyll 网站 . 
让我们开始吧 !

## 安装

Jekyll 是一个 Ruby 程序，所以首先要在本地电脑上安装 Ruby. 转到 [安装指南](/docs/installation/) ，并依照你的操作系统的说明操作.

使用 Ruby 安装程序，你可以在终端中运行以下命令来安装 Jekyll:

```
gem install jekyll bundler
```

创建一个新的  `Gemfile` 来列出项目的依赖项，运行:

```
bundle init
```

编辑这个 `Gemfile` 并将 jekyll 添加为依赖项:

```
gem "jekyll"
```

最后运行 `bundle` 来为你的项目安装 jekyll.

现在，你可以在本教程列出的所有 jekyll 命令前面加上 `bundle exec` 前缀，以保证你使用的 jekyll 是 `Gemfile` 定义的版本 .

## 创建网站

是时候创建一个站点了! 为你的站点新建一个文件夹, 你可以随便命名. 本教程中，我们命名为 “root” .

If you're feeling adventurous, you can also initialize a Git repository here.
One of the great things about Jekyll is there's no database. All content and
site structure are files which a Git repository can version. Using a repository
is completely optional but it's a great habit to get into. You can learn more
about using Git by reading through the
[Git Handbook](https://guides.github.com/introduction/git-handbook/).

让我们来添加第一个文件. 在根目录下创建 `index.html` 文件，其内容如下:

```html
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>主页</title>
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```

## 构建

Jekyll 是一个静态网站生成器，所以我们需要 Jekyll 事先构建网站，然后才能浏览它。可以在站点根目录下运行以下两条命令来构建它:

* `jekyll build` - 构建站点并将静态站点输出到名为 `_site` 的文件夹中.
* `jekyll serve` - 除了与上一条做同样的事情外, 还在你做更改时实时重构，同时运行一个本地网站服务器，网址为：`http://localhost:4000`.

当你正在开发一个站点时，可以使用 `jekyll serve` 命令，因为他会实时更新你所做的任何更改.

运行 `jekyll serve` 并在浏览器中打开 <a href="http://localhost:4000" target="_blank" data-proofer-ignore>http://localhost:4000</a>. 你应该会看到 "Hello World!".

Well, 你可能在想这有什么意义? Jekyll 只是把一个 HTML 文件从一个地方复制到了另一个地方。 耐心点吧，年轻人, 这才刚刚开始!
