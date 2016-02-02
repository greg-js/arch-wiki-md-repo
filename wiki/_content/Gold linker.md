# Gold linker

The Gold linker is a newer and reportedly faster linker than the standard GNU ld linker. It is included in the [binutils](https://www.archlinux.org/packages/?name=binutils) package.

To use the GOLD linker, simply

```
export LD=ld.gold

```

Alternatively, if your $PATH has /usr/local/bin before /usr/bin, you can do

```
ln -s /usr/bin/ld.gold /usr/local/bin/ld

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Gold_linker&oldid=342455](https://wiki.archlinux.org/index.php?title=Gold_linker&oldid=342455)"