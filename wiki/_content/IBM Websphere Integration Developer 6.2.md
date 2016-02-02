# IBM Websphere Integration Developer 6.2

Launching IBM WID in modern Arch environment is not a trivial task, here is a detailed guide on how to do it.

## Installation

To intsall IBM WID 6.2 on Arch Linux you need:

*   Delete IBM Installation Manager if you have it installed
*   Comment out the following line in installer_dir/IM_linux/install.xml
*   Launch silent installation

```
# ./userinst --launcher.ini ./silent-install.ini

```

## Usage

To make IBM WID 6.2 run successfully you will need to install [swt](https://www.archlinux.org/packages/?name=swt), [lib32-gtk2](https://www.archlinux.org/packages/?name=lib32-gtk2), [lib32-libstdc++5](https://www.archlinux.org/packages/?name=lib32-libstdc%2B%2B5) and [lib32-libxtst](https://www.archlinux.org/packages/?name=lib32-libxtst). You can run WID with the following command

```
$ /opt/IBM/WID62/eclipse -product com.ibm.wbit.feature.ide -showlocation

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=IBM_Websphere_Integration_Developer_6.2&oldid=381763](https://wiki.archlinux.org/index.php?title=IBM_Websphere_Integration_Developer_6.2&oldid=381763)"