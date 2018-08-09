Slack is a cloud-based set of proprietary team collaboration tools and services. Slack strives to be a flexible communication and collaboration platform for work, hobbyists, and other groups.

## Installation

Slack is available here: [slack-desktop](https://aur.archlinux.org/packages/slack-desktop/). Install using your favorite AUR helper or with makepkg.

## Glibc Incompatibility

There is an incompatibility with glibc-2.28 and the latest version of Slack. The solution is as follows:

Depends: [patchelf](https://www.archlinux.org/packages/?name=patchelf)

```
 #wget [https://archive.archlinux.org/repos/2018/08/01/core/os/x86_64/glibc-2.27-3-x86_64.pkg.tar.xz](https://archive.archlinux.org/repos/2018/08/01/core/os/x86_64/glibc-2.27-3-x86_64.pkg.tar.xz) -P /var/cache/pacman/pkg
 #mdkir /opt/glibc-2.27
 #bsdtar xf /var/cache/pacman/pkg/glibc-2.27-3-x86_64.pkg.tar.xz --cd /opt/glibc-2.27
 #patchelf --set-interpreter /opt/glibc-2.27/usr/lib/ld-linux-x86-64.so.2 --set-rpath \$ORIGIN:\$ORIGIN/lib/:/opt/glibc-2.27/usr/lib/ /usr/bin/slack

```