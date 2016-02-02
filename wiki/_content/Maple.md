# Maple

From the [official website](http://www.maplesoft.com/products/maple/):

	_Maple is a high-level language and interactive environment for numerical computation, visualization, and programming. Using Maple, you can analyze data, develop algorithms, and create models and applications. The language, tools, and built-in math functions enable you to explore multiple approaches and reach a solution faster than with spreadsheets or traditional programming languages, such as C/C++ or Java._

## Contents

*   [1 Overview](#Overview)
*   [2 Installation](#Installation)
*   [3 Issues](#Issues)
    *   [3.1 "Failed to determine Host ID of license server"](#.22Failed_to_determine_Host_ID_of_license_server.22)

## Overview

Maple is proprietary software produced by Maplesoft and requires a license to obtain, install, and activate. Arch is not officially supported, but the installer provided by Maplesoft may work in some cases.

## Installation

Maplesoft provides an installer script that may work on some Arch Linux installations. Make sure that you have a working [Java](/index.php/Java "Java") installation before beginning.

After purchasing your license, [download](http://www.maplesoft.com/support/downloads/) the appropriate Maple release package and unpack it in a location of your choosing. Open a terminal, change to the directory in which you unpacked the files, and run the installer script as a normal user. Installing the program's files inside of a user's home directory is the default option, and allows for easy removal of all components at a later time.

Once the package is installed, you will need to provide a license activation code. This should have been included in your installation archive.

## Issues

### "Failed to determine Host ID of license server"

In order to get Maple to accept your activation code, you may need to install the [ld-lsb](https://aur.archlinux.org/packages/ld-lsb/) package from the AUR. This will fake a standard Linux standard base runtime and convince the authentication server to accept your valid activation code. The [lsb-release](https://www.archlinux.org/packages/community/any/lsb-release/) package does not solve this issue, as the [MapleSoft installation support site](http://www.maplesoft.com/support/Faqs/detail.aspx?sid=32610) might lead one to believe.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Maple&oldid=409953](https://wiki.archlinux.org/index.php?title=Maple&oldid=409953)"