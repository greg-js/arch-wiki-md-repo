**翻译状态：** 本文是英文页面 [Ruby](/index.php/Ruby "Ruby") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-01-05，点击[这里](https://wiki.archlinux.org/index.php?title=Ruby&diff=0&oldid=499910)可以查看翻译后英文页面的改动。

Ruby 是一门专注于简洁和生产力的动态解释型开源编程语言。

## Contents

*   [1 安装 Ruby](#.E5.AE.89.E8.A3.85_Ruby)
    *   [1.1 多版本](#.E5.A4.9A.E7.89.88.E6.9C.AC)
    *   [1.2 文档](#.E6.96.87.E6.A1.A3)
*   [2 RubyGems](#RubyGems)
    *   [2.1 建立](#.E5.BB.BA.E7.AB.8B)
    *   [2.2 用法](#.E7.94.A8.E6.B3.95)
    *   [2.3 安装每个用户或全系统的 gems](#.E5.AE.89.E8.A3.85.E6.AF.8F.E4.B8.AA.E7.94.A8.E6.88.B7.E6.88.96.E5.85.A8.E7.B3.BB.E7.BB.9F.E7.9A.84_gems)
    *   [2.4 Bundler](#Bundler)
    *   [2.5 Managing RubyGems using pacman](#Managing_RubyGems_using_pacman)
        *   [2.5.1 Quarry](#Quarry)
*   [3 See also](#See_also)

## 安装 Ruby

对于最新版本的ruby，[安装](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85.E8.BD.AF.E4.BB.B6.E5.8C.85 "Help:Reading (简体中文)") [ruby](https://www.archlinux.org/packages/?name=ruby) 包。它包括 [ruby​​gems](#RubyGems)。

### 多版本

如果你要在同一个系统安装多个版本 (比如 2.0.0-p0 和 1.9.3-p392)，最简单的办法时安装 [RVM](/index.php/RVM "RVM")，[chruby](https://aur.archlinux.org/packages/chruby/) 或者 [rbenv](/index.php/Rbenv "Rbenv")。

### 文档

为了通过 `ri` 命令行工具使文档可用，安装 [ruby-docs](https://www.archlinux.org/packages/?name=ruby-docs)。 你可以查询文档通过：`ri Array`，`ri Array.pop` 等等。（就像 man 页面）

## RubyGems

RubyGems 是 Ruby 模块(叫做 *gems*) 的包管理器，在某种程度上与 [pacman](/index.php/Pacman "Pacman") 相对于 Arch Linux 的角色相当。它包含在 [ruby](https://www.archlinux.org/packages/?name=ruby) 中。

### 建立

[添加](/index.php/Help:Reading_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E6.B7.BB.E5.8A.A0.E3.80.81.E5.88.9B.E5.BB.BA.E3.80.81.E7.BC.96.E8.BE.91.E6.96.87.E4.BB.B6 "Help:Reading (简体中文)") `$(ruby -e 'print Gem.user_dir')/bin` 到 `PATH` [环境变量](/index.php/Environment_variables_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Environment variables (简体中文)") 来允许 RubyGems 被执行：

 `~/.profile`  `PATH="$(ruby -e 'print Gem.user_dir')/bin:$PATH"` 

这样而不是输入完整的路径对可执行的 gems 是必需的，尽管库工作并不需要修改你的路径。

为了允许当前 [用户](/index.php/Users_and_groups_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Users and groups (简体中文)") 安装 RubyGems，例如 *你的用户帐号不允许安装到系统 RubyGems。*，你可以设置 `GEM_HOME` 为本地路径：

```
$ export GEM_HOME=$HOME/.gem

```

你可能想把这个变量追加到 `.profile` 中：

 `~/.profile` 
```
PATH="$(ruby -e 'print Gem.user_dir')/bin:$PATH"
export GEM_HOME=$HOME/.gem
```

使用 `gem env` 来查看当前的 RubyGems 环境：

```
$ gem env

```

### 用法

查看已安装有那些 gem:

```
$ gem list

```

获取某个 gem 的详细信息：

```
$ gem spec "gem_name"

```

默认情况下，`gem list` 和 `gem spec` 开启了 `--local` 选项，导致 *gem* 只会在本地系统里进行搜索。这可以用 `--remote` 参数来覆盖。这样来搜索一个 mysql gem：

```
$ gem list --remote mysql

```

安装一个 gem：

```
$ gem install mysql

```

安装过程可以加快一点，如果你不需要本地的文档的话：

```
$ gem install mysql --no-document

```

**注意:** 这可以通过配置以下 `~/.gemrc` 文件成为默认选项： `~/.gemrc` 
```
gem: --no-document

```

更新所有已安装的 gem：

```
$ gem update

```

### 安装每个用户或全系统的 gems

在 Arch Linux 下运行 `gem` 时，gems 默认是为用户安装的（安装到 `~/.gem/ruby​​/`），而不是系统范围内（安装到 `/usr/lib/ruby/gems/`）。这被认为是 Arch 上管理 gems 的最好方式，因为否则它们可能会干扰 pacman 安装的宝石。

可以通过以 root 身份运行 `gem` 命令并附加 `--no-user-install` 标志以在系统范围内安装 gems。这可以被设置为默认通过在 `/etc/gemrc`（系统范围）或在 `~/.gemrc`（用户，覆盖系统范围） 中用 `--no-user-install` 替换 `--user-install`。

[Bundler](#Bundler) 通过将宝石打包到您的应用程序中来解决这些问题。请参阅下面关于使用 bundler 的部分。

### Bundler

[Bundler](http://bundler.io) 帮助你指定你的项目需要使用哪些 gem，还有可选地指定哪个版本被需要。当声明恰当时，Bundler 会安装所有依赖的 gem (包括整个依赖树)，后期检查之后还会打印出 log。Bundler 默认是安装 gem 到一个共享的路径，不过也可以指定直接安装到你的应用。当你项目运行的时候，Bundler 就提供每个 gem 正确的版本，即便安装的 gem 其实有多个版本。这需要有一点工作：应用需要以 `bundle exec` 命令运行，还有几行的 boilerplate 代码要被写在你的应用的可执行文件里。

安装 Bundler：

```
$ gem install bundler

```

Bundler 默认把 gem 安装在系统全局，这跟 Arch 上处理 *gem* 的方案正好相反。要解决这个问题，添加下面的配置到你的 `~/.bashrc`:

```
export GEM_HOME=$(ruby -e 'print Gem.user_dir')

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
# your Gemfile available to Ruby." [http://bundler.io/rationale.html](http://bundler.io/rationale.html)
require 'bundler/setup'

...

```

最后运行你的程序:

```
bundle exec *main_executable_name.rb*

```

### Managing RubyGems using pacman

Instead of managing gems with `gem`, you can use [pacman](/index.php/Pacman "Pacman"), or an [AUR](/index.php/AUR "AUR") helper. Ruby packages follow the naming convention ruby-*gemname*.

This option provides the following advantages:

*   Gems are updated along with the rest of your system.
*   Installed gems are available system-wide, instead of being available only to the user who installed them.

**Note:** There are also tools integrating *gem* with *pacman* by automatically generating PKGBUILDs for specified gems: see [Creating packages#PKGBUILD generators](/index.php/Creating_packages#PKGBUILD_generators "Creating packages").

#### Quarry

Quarry is an opensource tool (GPL3 license) that allows to maintain [rubygems](http://rubygems.org) binary repository for Arch Linux, as an easier alternative to building packages manually from the AUR. The source is hosted at [github](https://github.com/anatol/quarry).

The repository is maintained by Arch developer anatolik at [http://pkgbuild.com/~anatolik/quarry/](http://pkgbuild.com/~anatolik/quarry/), and is currently for the x86_64 architecture only. It contains many popular gems and new gems can be added upon request.

See [Unofficial user repositories#quarry](/index.php/Unofficial_user_repositories#quarry "Unofficial user repositories") to enable it.

Then install required gem `# pacman -S ruby-$gemname`.

If you have general questions - send it at the project announcement [https://bbs.archlinux.org/viewtopic.php?id=182729](https://bbs.archlinux.org/viewtopic.php?id=182729)
If you have bugreports or code improvements - file at github [https://github.com/anatol/quarry](https://github.com/anatol/quarry)

## See also

*   [Ruby on Rails](/index.php/Ruby_on_Rails "Ruby on Rails")
*   Ruby - [http://ruby-lang.org/](http://ruby-lang.org/)
*   Bundler - [http://bundler.io/](http://bundler.io/)
*   [why's (poignant) Guide to Ruby](https://en.wikipedia.org/wiki/Why%27s_(poignant)_Guide_to_Ruby "wikipedia:Why's (poignant) Guide to Ruby")
*   [Learn Ruby The Hard Way](http://ruby.learncodethehardway.org/)
*   [Comparison of Bundler and RVM workflows](http://blog.hyfather.com/blog/2011/10/18/bundler/)