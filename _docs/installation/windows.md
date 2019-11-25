---
title:  Windows 上的 Jekyll
permalink: /docs/installation/windows/
redirect_from:
  - /docs/windows/
---

While Windows is not an officially-supported platform, it can be used to run Jekyll with the proper tweaks. This page aims to
collect some of the general knowledge and lessons that have been unearthed by Windows users.


## 安装 Jekyll

### 通过 RubyInstaller 安装

The easiest way to run Jekyll is by using the [RubyInstaller](https://rubyinstaller.org/) for Windows.

RubyInstaller is a self-contained Windows-based installer that includes the Ruby language, an execution environment,
important documentation, and more.
We only cover RubyInstaller-2.4 and newer here, older versions need to
[install the Devkit](https://github.com/oneclick/rubyinstaller/wiki/Development-Kit) manually.

1. Download and Install a **Ruby+Devkit** version from [RubyInstaller Downloads](https://rubyinstaller.org/downloads/).
   Use default options for installation.
2. Run the `ridk install` step on the last stage of the installation wizard. This is needed for installing gems with native
   extensions. You can find additional information regarding this in the
   [RubyInstaller Documentation](https://github.com/oneclick/rubyinstaller2#using-the-installer-on-a-target-system)
3. Open a new command prompt window from the start menu, so that changes to the `PATH` environment variable becomes effective.
   Install Jekyll and Bundler via: `gem install jekyll bundler`
4. Check if Jekyll installed properly: `jekyll -v`

That's it, you're ready to use Jekyll!

### 在Windows 10 上通过 Bash 安装

如果你用的是1607版或更高版本的 Windows 10，另一个运行 Jekyll 的选项是 [安装](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide) Windows 的 Linux 子系统。

*注意：* 你必须已经使能了 [Windows 的  Linux 子系统](https://msdn.microsoft.com/en-us/commandline/wsl/about)

我们首先要确保所有的软件包/仓库 都是最新的。打开一个新的命令提示符实例，并键入以下命令：

```sh
bash
```
你的命令提示符实例现在应该是一个 Bash 实例。现在我们需要升级我们的软件包清单和软件包。

```sh
sudo apt-get update -y && sudo apt-get upgrade -y
```
现在我们可以安装 Ruby。为此，我们将使用一个叫 [BrightBox](https://www.brightbox.com/docs/ruby/ubuntu/)的存储仓库，他为 Ubuntu 托管最新版本的 Ruby。

```sh
sudo apt-add-repository ppa:brightbox/ruby-ng
sudo apt-get update
sudo apt-get install ruby2.5 ruby2.5-dev build-essential dh-autoreconf
```

下一步，让我们升级我们的 Ruby gems:

```sh
gem update
```

现在需要做的就是安装 Jekyll。

```sh
gem install jekyll bundler
```

(*注意: 此处没有 `sudo`*)

检查 Jekyll 是否安装正确，运行：

```sh
jekyll -v
```

**就这些了!**

你可以确保时间管理工作正常，检查你的 `_posts` 文件夹来，应该会看到一个以当前日期命名的 markdown 文件。

<div class="note info">
  <h5>非超级用户账户问题</h5>
  <p>如果 `jekyll new` 命令输出错误 "Your user account isn't allowed to install to the system RubyGems", 请参考 <a href="/docs/troubleshooting/#no-sudo">故障排除</a>中的 "以非超级用户运行 Jekyll " 说明。</p>
</div>

**注意：** Windows 的  Ubuntu 子系统上的 Bash 扔在开发中，所以你可能会遇到一些问题。

## 编码

If you use UTF-8 encoding, make sure that no `BOM` header characters exist in your files or very, very bad things will happen to
Jekyll. This is especially relevant when you're running Jekyll on Windows.

Additionally, you might need to change the code page of the console window to UTF-8 in case you get a
`Liquid Exception: Incompatible character encoding` error during the site generation process. It can be done with the following
command:

```sh
chcp 65001
```

## 时区管理

Since Windows doesn't have a native source of zoneinfo data, the Ruby Interpreter would not understand IANA Timezones and hence
using them had the `TZ` environment variable default to UTC/GMT 00:00.

Though Windows users could alternatively define their blog's timezone by setting the key to use POSIX format of defining
timezones, it wasn't as user-friendly when it came to having the clock altered to changing DST-rules.

Jekyll now uses a rubygem to internally configure Timezone based on established
[IANA Timezone Database](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).
While 'new' blogs created with Jekyll v3.4 and greater, will have the following added to their `Gemfile` by default, existing
sites *will* have to update their `Gemfile` (and installed) to enable development on Windows:

```ruby
# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
```

<div class="note warning">
  <h5>TZInfo 2.0 incompatibility</h5>
  <p>
    <code>v2.0</code> of the TZInfo library has introduced a change in how timezone offsets are calculated.
    This will result in incorrect date and time for your posts when the site is built with Jekyll 3.x on Windows.
  </p>
  <p>
    We therefore recommend that you lock the Timezone library to <code>v1.2</code> and above by listing
    <code>gem 'tzinfo', '~> 1.2'</code> in your <code>Gemfile</code>.
  </p>
</div>

## Auto Regeneration

Jekyll uses the `listen` gem to watch for changes when the `--watch` switch is specified during a build or serve.
While `listen` has built-in support for UNIX systems, it may require an extra gem for compatibility with Windows.

Add the following to the `Gemfile` for your site if you have issues with auto-regeneration on Windows alone:

```ruby
gem 'wdm', '~> 0.1.1', :install_if => Gem.win_platform?
```

You have to use a [Ruby+Devkit](https://rubyinstaller.org/downloads/) version of the RubyInstaller and install
the MSYS2 build tools to successfully install the `wdm` gem.
