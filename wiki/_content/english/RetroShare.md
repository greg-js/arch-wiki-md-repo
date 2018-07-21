**RetroShare** – open source, cross-platform [Friend-to-Friend](https://en.wikipedia.org/wiki/Friend-to-friend "wikipedia:Friend-to-friend") application that offers secure chat and file sharing features.

## Contents

*   [1 Installation from unofficial repository](#Installation_from_unofficial_repository)
*   [2 Installation from AUR](#Installation_from_AUR)
*   [3 Usage](#Usage)
*   [4 External Links](#External_Links)

## Installation from unofficial repository

1\. Add this repo:

```
/etc/pacman.conf
------------------------------

[home_Arch_Community_standard]
SigLevel = Never
Server = [http://download.opensuse.org/repositories/home:/AsamK:/RetroShare/Arch_Community_standard/x86_64](http://download.opensuse.org/repositories/home:/AsamK:/RetroShare/Arch_Community_standard/x86_64)

```

2\. Install RetroShare:

```
# pacman -Syu
# pacman -S home_Arch_Community_standard/retroshare06

```

## Installation from AUR

RetroShare is available in the [retroshare-git](https://aur.archlinux.org/packages/retroshare-git/) package providing compilation from source.

Note: this is unstable package! This package may not work!

## Usage

First, you have to create new profile. Then you need to explicitly add friends to be able to connect to them. In order to connect to your friends you need to exchange your certificates.

## External Links

*   [RetroShare Homepage](http://retroshare.net//)
*   [RetroShare Wikipedia entry](https://en.wikipedia.org/wiki/RetroShare "wikipedia:RetroShare")