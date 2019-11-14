# Jekyll 文档网站

Ysh825 把 Jekyll V4.00 源文件的 docs 目录整个拷过来, 重现 Jekyll 网站. 以后会逐步翻译学习相关文档, 并以此为参考学习验证 Jekyll 功能.

本目录包含 Jekyll V4.00 文档网站的源代码, [jekyllrb.com](https://ysh825.github.io/).

## Contributing

关于 contributing 的信息, 参考 [Contributing page](https://jekyllrb.com/docs/contributing/).

## 本地运行

在执行上传请求前, 可以先在本地目录运行以下命令以预览你的修改:

1. `bundle install --without test test_legacy benchmark`
2. `bundle exec rake site:preview`

毕竟这只是一个 jekyll 网站ll! :wink:

## Updating Font Awesome

1. Go to <https://icomoon.io/app/>
2. Choose Import Icons and load `icomoon-selection.json`
3. Choose Generate Font → Download
4. Copy the font files and adapt the CSS to the paths we use in Jekyll