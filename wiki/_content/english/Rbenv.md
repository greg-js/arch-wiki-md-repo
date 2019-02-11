Related articles

*   [RVM](/index.php/RVM "RVM")
*   [Chruby](/index.php/Chruby "Chruby")
*   [Ruby](/index.php/Ruby "Ruby")

[rbenv](https://github.com/sstephenson/rbenv) (Simple Ruby Version Management) lets you easily switch between multiple versions of Ruby. It's simple, unobtrusive, and follows the UNIX tradition of single-purpose tools that do one thing well.

Another tool to be used for the same purpose is [RVM](/index.php/RVM "RVM").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Plugins](#Plugins)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Ruby 2.3.x](#Ruby_2.3.x)
    *   [3.2 Ruby 2.x.x](#Ruby_2.x.x)
    *   [3.3 Ruby 1.9.3](#Ruby_1.9.3)
*   [4 External links](#External_links)

## Installation

[Install](/index.php/Install "Install") the [rbenv](https://aur.archlinux.org/packages/rbenv/) package.

## Plugins

rbenv can be extended via a plugin system, and the rbenv wiki includes a [list of useful plugins](https://github.com/sstephenson/rbenv/wiki/Plugins). The ruby-build plugin is especially useful, as it allows you to install Ruby versions with the `rbenv install` command. You can install [ruby-build](https://aur.archlinux.org/packages/ruby-build/) from the AUR.

## Troubleshooting

### Ruby 2.3.x

Before compiling, make sure you have all the dependencies needed:

```
 pacman -S --needed base-devel libffi libyaml openssl zlib

```

Installation of Ruby 2.3.x may break down due to openssl version described here:

*   [https://stackoverflow.com/questions/44116005/openssl-error-installing-ruby-2-1-x-and-2-3-x-on-archlinux-with-ruby-install-rub](https://stackoverflow.com/questions/44116005/openssl-error-installing-ruby-2-1-x-and-2-3-x-on-archlinux-with-ruby-install-rub)

```
 ossl_ssl.c:465:38: error: ‘CRYPTO_LOCK_SSL_SESSION’ undeclared

```

Here's a way how you can make a ruby compile:

1\. [Install](/index.php/Install "Install") the [openssl-1.0](https://www.archlinux.org/packages/?name=openssl-1.0) package first.

2\. Then run:

```
 PKG_CONFIG_PATH=/usr/lib/openssl-1.0/pkgconfig \
 rbenv install 2.3.4

```

### Ruby 2.x.x

Installation of Ruby 2.0.0, 2.1.4, 2.1.6, 2.1.7, 2.2.2 and 2.2.3 may show this error

```
 ossl_ssl.c:141:27: error: ‘SSLv3_method’ undeclared here (not in a function)

```

This can be solved using the patch as described [here](https://github.com/rbenv/ruby-build/issues/834#issuecomment-160627207)

```
 curl -fsSL https://gist.github.com/mislav/055441129184a1512bb5.txt | PKG_CONFIG_PATH=/usr/lib/openssl-1.0/pkgconfig rbenv install --patch 2.2.3

```

### Ruby 1.9.3

Installation of Ruby 1.9.3 may show the same error:

```
 ossl_ssl.c:116:27: error: ‘SSLv3_method’ undeclared here (not in a function)

```

This can be solved by using the patch as described [here](https://www.reddit.com/r/archlinux/comments/49bw8j/rvm_fails_to_compile_ruby_with_openssl_102g3/)

```
 curl -fsSL https://gist.githubusercontent.com/anonymous/679228bc324d6fdd3074.txt | rbenv install --patch 1.9.3-p448

```

If above was not enough you can install openssl-1.0 and gcc6 and try:

```
 curl -fsSL https://gist.githubusercontent.com/anonymous/679228bc324d6fdd3074.txt | CC=/usr/bin/gcc-6 PKG_CONFIG_PATH=/usr/lib/openssl-1.0/pkgconfig rbenv install --patch 1.9.3-p551

```

## External links

*   [Official web site](http://rbenv.org/)