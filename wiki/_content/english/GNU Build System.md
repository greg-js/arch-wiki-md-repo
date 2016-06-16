The [GNU Build System](https://en.wikipedia.org/wiki/GNU_Build_System) is a collection of applications and configuration files that assist with compiling software projects. It's the software that developers use to provide the following convenient installation method for end users and package maintainers:

```
 ./configure --prefix=/usr
 make
 make install

```

The GNU Build System is also known as "GNU Autotools".

## Contents

*   [1 Installation](#Installation)
*   [2 About](#About)
    *   [2.1 Configure.ac](#Configure.ac)
    *   [2.2 Makefile.am](#Makefile.am)
*   [3 Configuration](#Configuration)

## Installation

Everything needed to use Autotools is included in the "base-devel" package group.

## About

There are two types of files you need to create to use Autotools:

*   configure.ac
*   Makefile.am

### Configure.ac

The configure.ac file is used by the application autoconf. This file tells autoconf about what is needed to build your application - things like the name of the application and what compiler and libraries to use. Only one configure.ac file is needed, and it goes in the root directory of your source code tree.

### Makefile.am

The Makefile.am file is used by the application automake. The Makefile.am file tells automake how to build (or simply what to do with) the files that are in the directory. Each directory will have its own Makefile.am file, including the root directory.

In summary:

*   configure.ac -> autoconf
*   makefile.am -> automake

Did you notice that the file extension for the AutoConf file is AC and that the file extension for the AutoMake file is AM? Cute, right?

## Configuration

Now, what do you put in those files?

The Makefile.am file is relatively simple. Here is an example of a project directory structure:

```
 /
 /src
 /src/resources.c
 /src/resources.h
 /src/theapp.c
 /src/theapp.h

```

You would need two Makefile.am files:

 `/Makefile.am` 
```

SUBDIRS = src

```

and

 `/src/Makefile.am` 
```

bin_PROGRAMS = theapp
theapp_SOURCES = resources.c theapp.c

```

Good news! As for the configure.ac file, autotools can help you create it. In the root directory of your project run the program autoscan. The autoscan program will look at your files and create a simple file called configure.scan for you to start with.

*   autoscan -> configure.scan

Just rename configure.scan to configure.ac.

Edit the configure.ac file. There are some nice easy to understand placeholders for you to fill in, such as "FULL-PACKAGE-NAME" and "VERSION".

*   [TODO HOW TO FILL IN Makefile.am]

*   [TODO HOW TO FILL IN configure.ac]

Now that you've prepared the configuration files it's time to let autotools to do some automating. Run:

```
autoreconf --install 

```

to run the autotools scripts. The "--install" command will install any missing files for you, such as the NEWS and README files.