[Chef](http://chef.io/) is a configuration management tool written in Ruby and Erlang. It uses a pure-Ruby, domain-specific language (DSL) for writing system configuration "recipes". Chef is used to streamline the task of configuring and maintaining a company's servers, and can integrate with cloud-based platforms such as Rackspace, Internap, Amazon EC2, Google Cloud Platform, OpenStack, SoftLayer, and Microsoft Azure to automatically provision and configure new machines. Chef contains solutions for both small and large scale systems, with features and pricing for the respective ranges.

## Contents

*   [1 Chef Development Kit](#Chef_Development_Kit)
    *   [1.1 Installation](#Installation)
*   [2 Omnibus Chef Installer](#Omnibus_Chef_Installer)
    *   [2.1 Installation by Package](#Installation_by_Package)
    *   [2.2 Installing from Source](#Installing_from_Source)
    *   [2.3 Uninstallation](#Uninstallation)
*   [3 Other Installation Methods](#Other_Installation_Methods)
    *   [3.1 By Package](#By_Package)
    *   [3.2 By RubyGem](#By_RubyGem)

## Chef Development Kit

[Chef Development Kit](https://downloads.chef.io/chef-dk/) (ChefDK) is a streamlined development and deployment workflow for Chef platform. It includes:

*   Chef
*   Berkshelf
*   Test Kitchen
*   ChefSpec
*   Foodcritic

### Installation

Install the [chef-dk](https://aur.archlinux.org/packages/chef-dk/) package from AUR. This is the recommend installation method to get `chef-client`, `chef-solo`, `chef-zero`, `chef-apply` and `chef-shell` (typically for use on workstations).

## Omnibus Chef Installer

A monolithic package that provides Chef.

### Installation by Package

Install the [omnibus-chef](https://aur.archlinux.org/packages/omnibus-chef/) package from AUR. If not using an AUR helper, first install the needed dependency, [ruby-bundler](https://www.archlinux.org/packages/?name=ruby-bundler).

This package builds and installs an omnibus Makeself installer for Chef. If you choose not to run the installer upon installation of the package, you can run it any time:

```
# /usr/local/bin/chef-installer

```

### Installing from Source

```
 $ git clone https://github.com/opscode/omnibus-chef.git
 $ cd omnibus-chef

```

Wipe out any previous installations and the omnibus cache:

```
# rm -Rf /opt/chef/* /var/cache/omnibus/*

```

Set up the directories and change the ownership to yourself so building as root is not required:

```
# mkdir -p /opt/chef /var/cache/omnibus
# chown -R "$USER:users" /opt/chef
# chown -R "$USER:users" /var/cache/omnibus

```

Run the following to build:

```
$ bundle install --binstubs
$ bundle exec omnibus clean chef
$ bundle exec omnibus build chef

```

After that, you may like to change the ownership of directories back to the system:

```
# chown -R root:root /opt/chef
# chown -R root:root /var/cache/omnibus

```

A Makeself portable installer will be created, e.g. chef-11.8.2_0.arch.3.12.6-1-ARCH.sh. Run this executable to install chef.

### Uninstallation

Remove all installation files manually:

```
# rm -Rf /opt/chef

```

You can also ensure the omnibus cache is removed:

```
# rm -Rf /var/cache/omnibus

```

## Other Installation Methods

**Note:** Do not use these methods. It is recommended to install ChefDk or use the Omnibus installer method (see above). This section is included only for completeness-sake.

### By Package

Install the [ruby-chef](https://aur.archlinux.org/packages/ruby-chef/) package from AUR.

### By RubyGem

This is one of easiest ways to install Chef, but it is highly not recommended. If you already have gem versions of the dependencies installed to the system you could run into conflicts.

Ensure you first [install](/index.php/Install "Install") the [ruby](https://www.archlinux.org/packages/?name=ruby) package from the [official repositories](/index.php/Official_repositories "Official repositories"). This also provides RubyGems.

Next, install the Chef RubyGem:

```
 # gem install chef

```