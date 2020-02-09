The Arch Linux development team is considering to participate this year in [Google Summer of Code (GSoC)](https://summerofcode.withgoogle.com/), here is a draft on what areas we are needing improvements.

The main idea here is to help the development of these tools, improving it, making patches and fixing bugs for now.

### Project Ideas

*   Aurweb rewrite in Python
*   PKGBUILD Language server (implement a [Language Server Protocol](https://langserver.org/))
*   Signing enclave system -[https://github.com/archlinux/signstar](https://github.com/archlinux/signstar)
*   Package rebuilder list - [https://github.com/archlinux/rebuilder](https://github.com/archlinux/rebuilder)
*   Package version crawler - [https://github.com/archlinux/sandcrawler](https://github.com/archlinux/sandcrawler)
*   Dbscripts rewrite in Python (svn2git) - [https://github.com/archlinux/arch-repo-management](https://github.com/archlinux/arch-repo-management)
*   Arch Linux Installer (arch-installer) - [https://github.com/kgizdov/arch-installer](https://github.com/kgizdov/arch-installer)

#### Pacman-related Ideas

*   adding sync db write into libalpm, and use that to reimplement repo-add/repo-remove
*   --print-format should work for many, many more options
*   iterator interface for databases
*   getting pacman to compile in C++ and switching to some STL
*   parallel computations

### Potential Mentors

*   AUR - Lukas
*   Archweb - Jelle
*   Pacman - Allan
*   arch-installer - Konstantin