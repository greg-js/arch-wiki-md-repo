[ROS](http://www.ros.org) is an open-source, meta-operating system for your robot. It provides the services you would expect from an operating system, including hardware abstraction, low-level device control, implementation of commonly-used functionality, message-passing between processes, and package management.

## Contents

*   [1 Installation Instructions](#Installation_Instructions)
    *   [1.1 Lunar](#Lunar)
    *   [1.2 Kinetic](#Kinetic)
    *   [1.3 Configure the build tool](#Configure_the_build_tool)
*   [2 catkin_make](#catkin_make)
*   [3 catkin build](#catkin_build)
*   [4 Rebuild when shared libraries are updated](#Rebuild_when_shared_libraries_are_updated)

## Installation Instructions

### Lunar

ROS Lunar is available in AUR packages and seems to be working quite nicely although it lacks some simulators of the [ros-lunar-desktop-full](https://aur.archlinux.org/packages/ros-lunar-desktop-full/) package, the [ros-lunar-desktop](https://aur.archlinux.org/packages/ros-lunar-desktop/) is complete and seems to have everything functional.

### Kinetic

Kinetic packages on the AUR are a work in progress. There are [some issues regarding opencv3](https://github.com/bchretien/arch-ros-stacks/issues/57#issuecomment-228612399) that have not been fully resolved yet (installing [ros-kinetic-opencv3](https://aur.archlinux.org/packages/ros-kinetic-opencv3/) works, but is somewhat inefficient since it rebuilds opencv3). Currently, installing a metapackage such as [ros-kinetic-ros-core](https://aur.archlinux.org/packages/ros-kinetic-ros-core/) or [ros-kinetic-robot](https://aur.archlinux.org/packages/ros-kinetic-robot/) should bring in all required dependencies (see [[1]](https://paste.xinu.at/YXIz/) for the correct order, or use an [AUR helper](/index.php/AUR_helpers#Comparison_table "AUR helpers") that fully resolves dependency trees).

Packages are being added on an as-needed basis. Please send package requests to <aur AT seangreenslade DOT com>, and post any issues with the current packages in their respective AUR comments section.

### Configure the build tool

## catkin_make

Note that catkin uses python2, and therefore catkin_make may fail unless it is explicitly pointed to the python2 install. To do so, add the following alias to your .bashrc (or equivalent):

```
alias catkin_make="catkin_make -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so"

```

## catkin build

For configuring the systems using the `catkin build` environment, one have to configure the catkin workspace as usual and issue a

```
catkin config -DPYTHON_EXECUTABLE\=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so"

```

Afterwards, use `catkin build` as normal. Please remember to reconfigure your catkin whenever you delete the configuration files (i.e. the `catkin_ws` directory)

## Rebuild when shared libraries are updated

When you update a library that ROS depends on (e.g. Boost), all packages that link to it must be rebuilt. Most AUR helpers will not detect this situation. The following script will generate a list of all packages that are linked to missing so files:

[https://seangreenslade.com/h/snippets/ros-find-outofdate.py](https://seangreenslade.com/h/snippets/ros-find-outofdate.py)

(Note that the script requires [pyalpm](https://www.archlinux.org/packages/?name=pyalpm) to be installed.)