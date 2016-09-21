Ruby is a dynamic, interpreted, open source programming language with a focus on simplicity and productivity.

## Contents

*   [1 Installing Ruby](#Installing_Ruby)
    *   [1.1 Older versions](#Older_versions)
    *   [1.2 Multiple versions](#Multiple_versions)
    *   [1.3 Documentation](#Documentation)
*   [2 RubyGems](#RubyGems)
    *   [2.1 Setup](#Setup)
    *   [2.2 Usage](#Usage)
    *   [2.3 Installing gems per-user or system-wide](#Installing_gems_per-user_or_system-wide)
    *   [2.4 Bundler](#Bundler)
    *   [2.5 Managing RubyGems using pacman](#Managing_RubyGems_using_pacman)
        *   [2.5.1 Quarry](#Quarry)
*   [3 See also](#See_also)

## Installing Ruby

For the latest version of Ruby, [install](/index.php/Install "Install") the [ruby](https://www.archlinux.org/packages/?name=ruby) package. It includes [RubyGems](#RubyGems).

### Older versions

*   For Ruby 2.2, install the [ruby2.2](https://aur.archlinux.org/packages/ruby2.2/) package.
*   For Ruby 2.1, install the [ruby2.1](https://www.archlinux.org/packages/?name=ruby2.1) package.
*   For Ruby 2.0, install the [ruby2.0](https://aur.archlinux.org/packages/ruby2.0/) package.

### Multiple versions

If you want to run multiple versions on the same system (e.g. 2.0.0-p0 and 1.9.3-p392), the easiest way is to use [RVM](/index.php/RVM "RVM"), [chruby](https://aur.archlinux.org/packages/chruby/) or [rbenv](/index.php/Rbenv "Rbenv").

### Documentation

To make documentation available through the included `ri` command-line tool, install [ruby-docs](https://www.archlinux.org/packages/?name=ruby-docs). You can then query the docs with: `ri Array`, `ri Array.pop` etc. (much like man-pages)

## RubyGems

RubyGems is a package manager for Ruby modules (called *gems*), somewhat comparable to what [pacman](/index.php/Pacman "Pacman") is to Arch Linux. It is included in the [ruby](https://www.archlinux.org/packages/?name=ruby) package.

### Setup

Before you use RubyGems, you should add `$(ruby -e "print Gem.user_dir")/bin` to your `$PATH`. You can do this by adding the following line to `~/.bashrc`:

```
PATH="$(ruby -e 'print Gem.user_dir')/bin:$PATH"

```

This is required for executable gems to work without typing out the full location, although libraries will work without having to modify your path.

If the method above does not work, you can try adding these lines at the end of your shell configuration file instead:

```
 #Setting the GEM_PATH and GEM_HOME variables may not be necessary, check 'gem env' output to verify whether both variables already exist 
 GEM_HOME=$(ls -t -U | ruby -e 'puts Gem.user_dir')
 GEM_PATH=$GEM_HOME
 export PATH=$PATH:$GEM_HOME/bin

```

### Usage

To see what gems are installed:

```
$ gem list

```

To get information about a gem:

```
$ gem spec *gem_name*

```

By default, `gem list` and `gem spec` use the `--local` option, which forces *gem* to search only the local system. This can be overridden with the `--remote` flag. Thus, to search for the mysql gem:

```
$ gem list --remote mysql

```

To install a gem:

```
$ gem install mysql

```

The process can be sped up somewhat if you do not need local documentation:

```
$ gem install mysql --no-document

```

**Note:** This can be made the default option by configuring the following `~/.gemrc` file: `~/.gemrc` 
```
gem: --no-document

```

To update all installed gems:

```
$ gem update

```

### Installing gems per-user or system-wide

By default in Arch Linux, when running `gem`, gems are installed per-user (into `~/.gem/ruby/`), instead of system-wide (into `/usr/lib/ruby/gems/`). This is considered the best way to manage gems on Arch, because otherwise they might interfere with gems installed by Pacman.

Gems can be installed system wide by running the `gem` command as root, appended with the `--no-user-install` flag. This flag can be set as default by replacing `--user-install` by `--no-user-install` in `/etc/gemrc` (system-wide) or `~/.gemrc` (per-user, overrides system-wide).

[Bundler](#Bundler) solves these problems to some extent by packaging gems into your application. See the section below on using bundler.

### Bundler

[Bundler](http://bundler.io) allows you to specify which gems your application depends upon, and optionally which version those gems should be. Once this specification is in place, Bundler installs all required gems (including the full gem dependency tree) and logs the results for later inspection. By default, Bundler installs gems into a shared location, but they can also be installed directly into your application. When your application is run, Bundler provides the correct version of each gem, even if multiple versions of each gem have been installed. This requires a little bit of work: applications should be called with `bundle exec`, and two lines of boilerplate code must be placed in your application's main executable.

To install Bundler:

```
$ gem install bundler

```

By default, Bundler installs gems system-wide, which is contrary to the behaviour of *gem* itself on Arch. To correct this, add the following to your `~/.bashrc`:

```
export GEM_HOME=$(ruby -e 'print Gem.user_dir')

```

To start a new bundle:

```
$ bundle init

```

Then edit `Gemfile` in the current directory (created by bundle init) and list your required gems:

 `Gemfile` 
```
gem "rails", "3.2.9"
gem "mysql"

```

Run the following to install gems into `GEM_HOME`:

```
$ bundle install

```

Alternatively, run the following to install gems to `.bundle` in the working directory:

```
$ bundle install --path .bundle

```

Don't forget to edit your main executable:

```
#!/usr/bin/env ruby

# "This will automatically discover your Gemfile, and make all of the gems in
# your Gemfile available to Ruby." [http://bundler.io/rationale.html](http://bundler.io/rationale.html)
require 'bundler/setup'

...

```

Finally, run your program:

```
bundle exec *main_executable_name.rb*

```

### Managing RubyGems using pacman

Instead of managing gems with `gem`, you can use `pacman`, or some [AUR](/index.php/AUR "AUR") helper. Ruby packages follow the naming convention ruby-[gemname]. This option provides the following advantages:

*   Gems are updated along with the rest of your system. As a result, you never need to run `gem update`: `# pacman -Syu` suffices.
*   Installed gems are available system-wide, instead of being available only to the user who installed them.

If a gem is not available in AUR, you can use [gem2arch](https://aur.archlinux.org/packages/gem2arch/) or [pacgem](https://aur.archlinux.org/packages/pacgem/) to automatically create a package, which can then be installed by pacman.

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
*   [[http://ruby.learncodethehardway.org/](http://ruby.learncodethehardway.org/) Learn Ruby The H