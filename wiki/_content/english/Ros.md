[ROS](http://www.ros.org) is an open-source, meta-operating system for your robot. It provides the services you would expect from an operating system, including hardware abstraction, low-level device control, implementation of commonly-used functionality, message-passing between processes, and package management.

## Contents

*   [1 Installation Instructions](#Installation_Instructions)
    *   [1.1 Kinetic](#Kinetic)
    *   [1.2 Jade](#Jade)
    *   [1.3 Indigo](#Indigo)
*   [2 Rebuild when Boost is updated](#Rebuild_when_Boost_is_updated)

## Installation Instructions

### Kinetic

Kinetic packages on the AUR are a work in progress. There are [some issues regarding opencv3](https://github.com/bchretien/arch-ros-stacks/issues/57#issuecomment-228612399) that have not been fully resolved yet. That said, installing a metapackage such as [ros-kinetic-ros-core](https://aur.archlinux.org/packages/ros-kinetic-ros-core/) or [ros-kinetic-robot](https://aur.archlinux.org/packages/ros-kinetic-robot/) should bring in all required dependencies. Beware of AUR helpers, some cannot navigate the highly complex dependency trees that ROS generates.

Packages are being added on an as-needed basis. Please send package requests to <aur AT seangreenslade DOT com>, and post any issues with the current packages in their respective AUR comments section.

Note that catkin uses python2, and therefore catkin_make may fail unless it it explicitly pointed to the python2 install. To do so, add the following alias to your .bashrc (or equivalent):

```
alias catkin_make="catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so"

```

### Jade

For ROS Jade, see [Installation Instructions for jade in Arch Linux](http://wiki.ros.org/jade/Installation/Arch).

**Note:** If using gcc in version 6.x or above, log4cxx 0.10 (one of dependencies) will not build. Use SVN version ([log4cxx-svn](https://aur.archlinux.org/packages/log4cxx-svn/) in aur) until 0.11 is released.

### Indigo

For ROS Indigo, see [Installation Instructions for Indigo in Arch Linux](http://wiki.ros.org/indigo/Installation/Arch).

## Rebuild when Boost is updated

When you update a library that ROS depends on, e.g. Boost, then you need to rebuild all the packages that link to it. You can determine which ROS packages depend on Boost with a command similar to the one below.

```
export LANG=C;pacman -Qi boost | grep "Required By" | tr " " "
" | grep -e "^ros"

```