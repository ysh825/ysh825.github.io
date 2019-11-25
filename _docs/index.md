---
title: 快速入门
permalink: /docs/
redirect_from:
  - /docs/home/
  - /docs/quickstart/
  - /docs/extras/
---
Jekyll 是一个简单，可扩展的静态站点生成器。你只需用你喜欢的标记语言书写文本，他会根据布局帮你创建一个静态网站。 这个过程中，你可以调整你想要的网址样式，在布局中显示的数据等等。

## 操作说明

1. 安装一个完整的 [Ruby开发环境](/docs/installation/)
2. 用 [gems](/docs/ruby-101/#gems) 安装 Jekyll 和 [bundler](/docs/ruby-101/#bundler) 
```
gem install jekyll bundler
```
3. 新建一个 Jekyll 站点，目录为 `./myblog` 
```
jekyll new myblog
```
4. 转到你的新目录
```
cd myblog
```
5. 构建站点并启动一个本地服务器
```
bundle exec jekyll serve
```
6. 现在在浏览器中打开 [http://localhost:4000](http://localhost:4000){:target="_blank"}

如果在上述过程中遇到任何意外错误，请参阅 
[故障排除](/docs/troubleshooting/#configuration-problems) 页 或 前面提到的 [先决条件](/docs/installation/#requirements) 页，你可能缺少开发头文件或其它先决条件。
