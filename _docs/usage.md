---
title:  命令行用法
permalink: /docs/usage/
---

Jekyll gem 让你可以在命令行终端中运行 `jekyll` 程序。

你可以通过多种方式执行这些命令：

* `jekyll new` - 新建一个 Jekyll 站点，使用基于 gem 的默认主题
* `jekyll new --blank` - 新建一个空白的 Jekyll 站点框架
* `jekyll build` 或 `jekyll b` - 执行一次站点构建，并将结果输出到默认文件夹 `./_site` 中
* `jekyll serve` 或 `jekyll s` - 启动本地服务器，并且每当源文件变更时，都实时构建站点
* `jekyll doctor` - 输出任何弃用功能或配置问题
* `jekyll clean` - 移除所有生成的文件：目标文件夹，元数据文件，Sass 和 Jekyll 缓存。
* `jekyll help` - 显示帮助信息，可针对给定的子命令，例如： `jekyll help build`
* `jekyll new-theme` - 新建一个 Jekyll 主题框架

通常，本地开发时使用 `jekyll serve` 命令；需要为生产环境生成站点时，使用 `jekyll build` 命令。

如需更改 Jekyll 的默认构建行为，请查看 [配置选项](/docs/configuration/).
