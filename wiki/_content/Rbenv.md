# Rbenv

[rbenv](https://github.com/sstephenson/rbenv) (Simple Ruby Version Management) lets you easily switch between multiple versions of Ruby. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

Another tool to be used for the same purpose is [RVM](/index.php/RVM "RVM").

## Contents

*   [1 Comparison with RVM](#Comparison_with_RVM)
*   [2 Installation](#Installation)
*   [3 Plugins](#Plugins)
*   [4 External links](#External_links)

## Comparison with RVM

[From the wiki:](https://github.com/sstephenson/rbenv/wiki/Why-rbenv%3F)

rbenv does...

*   Let you change the global Ruby version on a per-user basis.
*   Provide support for per-project Ruby versions.
*   Allow you to override the Ruby version with an environment variable.

In contrast with rvm, rbenv does not...

*   Need to be loaded into your shell. Instead, rbenv's shim approach works by adding a directory to your $PATH.
*   Override shell commands like cd. That's dangerous and error-prone.
*   Have a configuration file. There's nothing to configure except which version of Ruby you want to use.
*   Install Ruby. You can build and install Ruby yourself, or use ruby-build to automate the process.
*   Manage gemsets. Bundler is a better way to manage application dependencies. If you have projects that are not yet using Bundler you can install the rbenv-gemset plugin.
*   Require changes to Ruby libraries for compatibility. The simplicity of rbenv means as long as it's in your $PATH, nothing else needs to know about it.
*   Prompt you with warnings when you switch to a project. Instead of executing arbitrary code, rbenv reads just the version name from each project. There's nothing to "trust."

## Installation

You can install [rbenv](https://aur.archlinux.org/packages/rbenv/) from the [AUR](/index.php/AUR "AUR").

## Plugins

rbenv can be extended via a plugin system, and the rbenv wiki includes a [list of useful plugins](https://github.com/sstephenson/rbenv/wiki/Plugins). The ruby-build plugin is especially useful, as it allows you to install Ruby versions with the `rbenv install` command. You can install [ruby-build](https://aur.archlinux.org/packages/ruby-build/) from the AUR.

## External links

*   [Official web site](http://rbenv.org/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Rbenv&oldid=410377](https://wiki.archlinux.org/index.php?title=Rbenv&oldid=410377)"