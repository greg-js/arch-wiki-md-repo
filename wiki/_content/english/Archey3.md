Archey3 is a simple python script that prints basic system information and ASCII art of the Arch Linux logo.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting](#Starting)
*   [3 Configuration](#Configuration)
    *   [3.1 Colors](#Colors)
    *   [3.2 Editing the config file](#Editing_the_config_file)
*   [4 See also](#See_also)

## Installation

Install the [archey3](https://www.archlinux.org/packages/?name=archey3) package.

## Starting

Archey3 can be run by typing:

```
$ archey3

```

This should produce an output similar to below.

```
                               OS: Arch Linux x86_64
              #                Hostname: samsarchlinux
             ###               Kernel Release: 4.5.4-1-ARCH
            #####              Uptime: 1:48
            ######             WM: None
           ; #####;            DE: MATE
          +##.#####            Packages: 553
         +##########           RAM: 721 MB / 7850 MB
        #############;         Processor Type: Intel(R) Core(TM) i7-3520M CPU @ 2.90GHz
       ###############+        $EDITOR: None
      #######   #######        Root: 4.1G / 29G (14%) (ext3)
    .######;     ;###;`".      
   .#######;     ;#####.       
   #########.   .########`     
  ######'           '######    
 ;####                 ####;   
 ##'                     '##   
#'                         `#  

```

It can also be started automatically with each new [Bash](/index.php/Bash "Bash") session. To do this, append `archey3` to a new line in your `.bashrc` file, including any options.

## Configuration

Archey3's configuration file is stored at `~/.config/archey3.cfg` by default. However this can be adjusted using this command where CONFIG represents the file to use.

```
$ archey3 --config=CONFIG

```

### Colors

Archey3 can display colors other than the default blue. To change colors, append the `-c foo` flag, where "foo" represents the desired color. Supported colors are: black, red, green, yellow, blue, magenta, cyan, and white. For example, to display archey3 in red, type:

```
$ archey3 -c red

```

### Editing the config file

A sample config file, with comments showing all of the possible options for configuration, is available in the [Config reference](http://www.generictestdomain.net/archey3/config.html).

## See also

	[Project Homepage](http://www.generictestdomain.net/archey3/)

	[Archey3 Config Reference](http://www.generictestdomain.net/archey3/config.html)