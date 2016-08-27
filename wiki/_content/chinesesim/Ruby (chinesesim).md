**翻译状态：** 本文是英文页面 [Ruby](/index.php/Ruby "Ruby") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2013-04-30，点击[这里](https://wiki.archlinux.org/index.php?title=Ruby&diff=0&oldid=255724)可以查看翻译后英文页面的改动。

Ruby 是一门专注于简洁和生产里的动态语言, 是解释型语言, 开源编程语言.

## Contents

*   [1 安装 Ruby](#.E5.AE.89.E8.A3.85_Ruby)
    *   [1.1 Ruby 2.0](#Ruby_2.0)
    *   [1.2 Ruby 1.9](#Ruby_1.9)
    *   [1.3 多版本](#.E5.A4.9A.E7.89.88.E6.9C.AC)
*   [2 RubyGems](#RubyGems)
    *   [2.1 用例](#.E7.94.A8.E4.BE.8B)
    *   [2.2 普通用户身份运行](#.E6.99.AE.E9.80.9A.E7.94.A8.E6.88.B7.E8.BA.AB.E4.BB.BD.E8.BF.90.E8.A1.8C)
    *   [2.3 以 root 身份运行](#.E4.BB.A5_root_.E8.BA.AB.E4.BB.BD.E8.BF.90.E8.A1.8C)
    *   [2.4 Bundler](#Bundler)
*   [3 用 pacman 管理 RubyGems](#.E7.94.A8_pacman_.E7.AE.A1.E7.90.86_RubyGems)
*   [4 又见](#.E5.8F.88.E8.A7.81)
*   [5 引用](#.E5.BC.95.E7.94.A8)

## 安装 Ruby

按照需要来选择安装 Ruby 的版本. 为了支持遗留下来的软件, 必要时请安装 Ruby 1.9 甚至 1.8\. 开展新项目建议 Ruby 2.0 .以下是一个概要, 关于当前有的版本和如何获取.

### Ruby 2.0

要安装 Ruby 2.0.0, 安装 [ruby](https://www.archlinux.org/packages/?name=ruby) 这个包. Ruby 2.0 包含了 [#RubyGems](#RubyGems).

### Ruby 1.9

要从 [AUR](/index.php/AUR "AUR") 安装 Ruby 1.9.3, 安装 [ruby1.9](https://aur.archlinux.org/packages/ruby1.9/). Ruby 1.9 包含了 RubyGems.

### 多版本

如果你要在同一个系统安装多个版本 (比如 2.0.0-p0 和 1.9.3-p392), 最简单的办法时安装 [RVM](/index.php/RVM "RVM") 或者 [rbenv](/index.php/Rbenv "Rbenv").

## RubyGems

*gem* 是 Ruby 模块 (叫做 Gems) 的包管理器, 某种程度上是 [pacman](/index.php/Pacman "Pacman") 相对于 Arch Linux 的角色. *gem* 命令你可以通过遵循上边的操作来得到.

### 用例

查看已安装有那些 gem:

```
$ gem list

```

获取某个 gem 的详细信息:

```
$ gem spec <gem_name>

```

默认情况下, `gem list` 和 `gem spec` 开启了 `--local` 选项, 导致 *gem* 只会在本地系统里进行搜索. 这可以用 `--remote` 参数来覆盖. 这样子以后, 来搜索一个 mysql gem:

```
$ gem list --remote mysql

```

安装一个 gem:

```
$ gem install mysql

```

安装过程可以加快一点, 如果你不需要本地的文档的话:

```
$ gem install mysql --no-rdoc --no-ri

```

更新所有已安装的 gem:

```
$ gem update

```

### 普通用户身份运行

作为普通用户安装 *gem* 的时候, gem 默认被安装在 `~/.gem` 而不是在系统全局. 这在 Arch 上被认为是做回的管理 gem 的方案. 不巧的是并非所有 gem 都乐意被安装在这, 甚至可能坚持要以 root 身份安装, 特别是模块含有本地扩展(从 C 编译的代码). 每个用户的方案被配置在 `/etc/gemrc` 文件里, 可以通过配置 `~/.gemrc` 文件来改变.

为了使用一些安装了可执行文件的 gem, 需要把 `$(ruby -e 'print Gem.user_dir')/bin` 添加到你的 `$PATH` 环境变量里.如果以上命令无法生效, 可以使用下面命令代替:

```
 #Setting the GEM_PATH and GEM_HOME variables may not be necessary, check 'gem env' output to verify whether both variables already exist 
 GEM_HOME=$(ls -t -U | ruby -e 'puts Gem.user_dir')
 GEM_PATH=$GEM_HOME
 export PATH=$PATH:$GEM_HOME/bin

```

### 以 root 身份运行

以 root 身份运行时 gem 会被安装在 `/root/.gems`, 而且**不会**被安装到 `/usr/lib/ruby/gems/`.

**注意:** 访问 bug #[33327](https://bugs.archlinux.org/task/33327) 查看更多信息.

[Bundler](/index.php/Ruby#Bundler "Ruby") 通过把模块打包到你的项目目录, 一定程度上解决了这些问题. 细节看下面关于使用 bundler.

### Bundler

[Bundler](http://github.com/carlhuda/bundler) 帮助你指定你的项目需要使用哪些 gem, 还有可选地指定哪个版本被需要. 当声明恰当时, Bundler 会安装所有依赖的 gem (包括整个依赖树), 后期检查之后还会打印出 log. Bundler 默认是安装 gem 到一个共享的路径, 不过也可以指定直接安装到你的应用. 当你项目运行的时候, Bundler 就提供每个 gem 正确的版本, 即便安装的 gem 其实有多个版本. 这需要有一点工作: 应用需要以 `bundle exec` 命令运行, 还有两行的 boilerplate 代码要被写在你的应用的可执行文件里.

安装 Bundler:

```
$ gem install 

```

Bundler 默认把 gem 安装在系统全局, 这跟 Arch 上处理 *gem* 的方案正好相反. 纠正的办法的话, 添加下面的配置到你的 `~/.bashrc`:

```
export GEM_HOME=~/.gem/ruby/2.0.0

```

新建一个 bundle:

```
$ bundle init

```

然后编辑当前目录 (gem init 执行的目录)下的 `Gemfile` 添加你需要的 gem:

 `Gemfile` 
```
gem "rails", "3.2.9"
gem "mysql"

```

运行下面的命令安装需要的 gem 到 `GEM_HOME`:

```
$ bundle install

```

或者作为可选方案, 运行下面的命令把 gem 安装到工作路径的 `.bundle`:

```
$ bundle install --path .bundle

```

别忘了要编辑你主要的执行文件:

```
#!/usr/bin/env ruby

# "This will automatically discover your Gemfile, and make all of the gems in
# your Gemfile available to Ruby." [http://gembundler.com/v1.3/rationale.html](http://gembundler.com/v1.3/rationale.html)
require 'rubygems'
require 'bundler/setup'

...

```

最后运行你的程序:

 `bundle exec <main_executable_name.rb>` 

## 用 pacman 管理 RubyGems

除了用 `gem` 命令管理 gem, 也可以用 `pacman`, 或者一些 [AUR](/index.php/AUR "AUR") 帮助工具. Ruby 模块遵循这样的命名惯例 ruby-[gemname]. 这个方案提供了以下的优点:

*   Gems 和你系统其他部分一样被升级. 这样你就不用去运行 `gem update`: 运行 `pacman -Syu` 足够了.
*   已安装的 gem 在全系统可用, 而不是只有安装了这些 gem 的用户.

如果 gem 在仓库里没有, 你可以用 [pacgem](https://aur.archlinux.org/packages/pacgem/) 自动创建一个, 这个模块接下来就能直接用 pacman 来安装.

## 又见

*   [Ruby on Rails](/index.php/Ruby_on_Rails "Ruby on Rails")

## 引用

*   Ruby - [http://ruby-lang.org/](http://ruby-lang.org/)
*   Rubyforge - [http://rubyforge.org](http://rubyforge.org)
*   Bundler - [http://github.com/carlhuda/bundler](http://github.com/carlhuda/bundler)