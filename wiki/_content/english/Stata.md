STATA is a general-purpose statistical software package for *nix, Windows and Mac. In the following you'll be presented with how to install STATA and the needed libraries.

## Contents

*   [1 Needed libraries](#Needed_libraries)
*   [2 Installing Stata](#Installing_Stata)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 Troubleshooting](#Troubleshooting)

## Needed libraries

Stata depends on [libpng12](https://www.archlinux.org/packages/?name=libpng12). Stata also uses the GTK+ framework.

If you are running STATA 14/15 and get a message about missing libncurses.so.5 [install](/index.php/Install "Install") [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/).

## Installing Stata

After you have installed these packages, you should extract the installation files to the folder, where you want to put Stata. Stata recommends putting it under `/usr/local/`. For example:

```
# mkdir /usr/local/stata15

```

Once you have created the directory, change into it:

```
$ cd /usr/local/stata15

```

Then from the directory, extract the installation file

```
# tar xvf /path/to/Stata15Linux64.tar.gz

```

And run the installation file:

```
# ./install

```

Follow the instructions and you will end up with Stata installed.

On a default installation of Arch Linux, icons will not show up if it starts. This is due to Stata being built against older versions of libraries. See the troubleshooting section for how to fix it.

## Tips and tricks

To add Stata to your path, add the following to the end of your path in your [bashrc](/index.php/Bashrc "Bashrc"):

 `~/.bashrc` 
```
PATH=$PATH:/usr/local/stata12/

```

## Troubleshooting

Stata 12 and 13 at least were built on older versions of libpng and zlib. Thus, icons will be missing when launching Xstata, the graphical interface. The workaround is **NOT** to downgrade your system's libraries, but rather to follow the advice given by StataCorp's technical department [here](http://www.statalist.org/forums/forum/general-stata-discussion/general/2199-linux-stata-bug-libpng-on-newer-opensuse-possibly-other-distributions). It involves compiling the older versions of libpng and zlib and putting them in a folder that your system will not interact with. Then a wrapper for Stata needs to be made to reference these libraries. These steps have been automated by a script on bitbucket, located [here](https://bitbucket.org/vilhuberl/stata-png-fix).