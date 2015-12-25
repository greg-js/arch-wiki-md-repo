# Ros

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** Non-standard layout (Discuss in [Talk:Ros#](https://wiki.archlinux.org/index.php/Talk:Ros))

[ROS](http://www.ros.org) is an open-source, meta-operating system for your robot. It provides the services you would expect from an operating system, including hardware abstraction, low-level device control, implementation of commonly-used functionality, message-passing between processes, and package management.

## Contents

*   [1 Setup Notes - Jade](#Setup_Notes_-_Jade)
*   [2 Setup Notes - Indigo](#Setup_Notes_-_Indigo)
*   [3 Setup Notes - Hydro](#Setup_Notes_-_Hydro)
*   [4 Setup Notes - Groovy](#Setup_Notes_-_Groovy)
*   [5 Usage Notes - Groovy](#Usage_Notes_-_Groovy)
*   [6 Rebuild when boost is updated](#Rebuild_when_boost_is_updated)

## Setup Notes - Jade

For ROS Jade, see [Installation Instructions for jade in Arch Linux](http://wiki.ros.org/jade/Installation/Arch).

## Setup Notes - Indigo

For ROS Indigo, see [Installation Instructions for Indigo in Arch Linux](http://wiki.ros.org/indigo/Installation/Arch).

## Setup Notes - Hydro

For ROS Hydro, see [Installation Instructions for Hydro in Arch Linux](http://wiki.ros.org/hydro/Installation/Arch).

**Ogre 1.8**

You may want to use ogre 1.8 ([aur package](https://aur.archlinux.org/packages/ogre-1.8/)) if you want to use gazebo. In order to compile some hydro packages that requires ogre (like rviz) you can add this export to the pkgbuild:

```
export PKG_CONFIG_PATH=/opt/OGRE-1.8/lib/pkgconfig/:$PKG_CONFIG_PATH

```

## Setup Notes - Groovy

ROS Groovy core, comm, and robot variants have meta-packages that should install all the necessary packages: [ros-groovy-ros](https://aur.archlinux.org/packages/ros-groovy-ros/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ros-groovy-ros)]</sup>, [ros-groovy-ros-comm](https://aur.archlinux.org/packages/ros-groovy-ros-comm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ros-groovy-ros-comm)]</sup>, (TODO: robot metapackage). In addition, [ros-groovy-rviz](https://aur.archlinux.org/packages/ros-groovy-rviz/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ros-groovy-rviz)]</sup> (along with its dependencies) has a package.

The packages are all available in the maintainer's github: [arch-ros-stacks](https://github.com/zootboy/arch-ros-stacks). Not all packages there are in a working state, so use with caution. Please, report any issues with the packages on their respective AUR pages.

## Usage Notes - Groovy

Due to the fact that Ubuntu and Arch handle the python2/3 binary split differently, catkin_make[_isolated] will not work on its own. To use these commands, create the following aliases in your ~/.bashrc (or equivalent):

```
alias catkin_make='catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so'
alias catkin_make_isolated='catkin_make_isolated -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so'

```

Without these lines, cmake will default to python 3, which you do not want. It is also possible to simply add the defines into any call of catkin_make[_isolated] (which you have to do if you want to call those commands within a script).

For further information on how to use ROS, see the [ROS Tutorials](http://www.ros.org/wiki/ROS/Tutorials).

## Rebuild when boost is updated

When you update a library that ROS depends on, e.g. boost, then you need to rebuild all the packages that link to it. You can search for the packages, with a command similar to the one below. You can use the output from that to rebuild the AUR packages with your favorite AUR helper/wrapper.

```
export LANG=C;grep -r "libboost" /opt/ros/indigo |  awk '{ print $3 }' | grep opt |  pacman -Qo - | awk '{ print $5 }' | tr '\n' ' '

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Ros&oldid=413254](https://wiki.archlinux.org/index.php?title=Ros&oldid=413254)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mathematics and science](/index.php/Category:Mathematics_and_science "Category:Mathematics and science")