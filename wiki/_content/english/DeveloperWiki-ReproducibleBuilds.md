## Reproducible Builds

A list of reproducible build meetings and work in progress documentation.

[Reproducible build results](https://tests.reproducible-builds.org/archlinux/archlinux.html)

### To-Do List

*   Arch Linux Archive cleanup script

    	A script to remove only packages from the Archive which are not required to create a reproducible build of the current repository

*   Arch Linux Reproducible script

*   A script to locally reproduce an installed package

*   Resolve reproducible build issues
*   Documentation about reproducing a build

### Agenda Meeting 10-01-2018

*   UTF-8 failures with Python.

    	There are a lot of reproducible build issues due to the lack of LANG=$lang-UTF-8\. Do we need to explicitly set the LANG in the PKGBUILD

    	See for example [https://tests.reproducible-builds.org/archlinux/community/python-cssselect2/build1.log](https://tests.reproducible-builds.org/archlinux/community/python-cssselect2/build1.log)

*   Package disorderfs

    	Not high important right now, I've added it on my todolist. This could be used later in combination with the reproducible build script

*   Pacman release

    	How do we convince the Pacman team to create a new release, are there any known blockers they waiting on?

*   Reproducible build script progress

    	Discuss what the script exactly should do, create an RFC? To describe it's functionality.

    	FIXME: add issues I encountered.

*   Arch Linux Archive: don't remove packages mentioned in BUILDINFO file

    	There should be a script which checks if packages can be removed from the Archive, since currently it removes packages older then 6 Months?

    	Sangy was working on this if I recall correctly, what is the status?

    	Write documentation what this script should do. (Specification)

*   Killed builds

    	Someone should investigate this, how do we reproduce this locally? Hints?

*   SSL verification issues

    	How do we circumvent SSL issues from reproducing a package locally which was build earlier, when the SSL certificate was valid

*   Create a public to-do list

    	We should get more people in to work on reproducible builds, how can we guide them and where do we keep track of the progress made and issues which require attention.