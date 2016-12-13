ArchLinux is not officially supported by Tizen SDK, but it is possible to use it by previously installing the required dependencies.

## Installation

Install [webkitgtk](https://www.archlinux.org/packages/?name=webkitgtk), [cpio](https://www.archlinux.org/packages/?name=cpio) and [rpmextract](https://www.archlinux.org/packages/?name=rpmextract). If you also want to use the emulator, install [libpng12](https://www.archlinux.org/packages/?name=libpng12), [sdl](https://www.archlinux.org/packages/?name=sdl), [glib2](https://www.archlinux.org/packages/?name=glib2), [acl](https://www.archlinux.org/packages/?name=acl), [zlib](https://www.archlinux.org/packages/?name=zlib), [pixman](https://www.archlinux.org/packages/?name=pixman), [bridge-utils](https://www.archlinux.org/packages/?name=bridge-utils), [openvpn](https://www.archlinux.org/packages/?name=openvpn) and [libcurl-gnutls](https://www.archlinux.org/packages/?name=libcurl-gnutls). You will also need Oracle JDK, so install [jdk](https://aur.archlinux.org/packages/jdk/) from the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository"). If you have other java versions installed, you must set the default point to Oracle implementation:

```
# archlinux-java set java-8-jdk

```

Then you can download the installer from the official web (latest 64 bit Ubuntu version with IDE recommended) [[1]](https://developer.tizen.org/development/tools/download). Once the download has finished, grant exec permission to the installer and run it. Note you must **not** run the installer as root:

```
$ chmod +x tizen-web-ide_TizenSDK_2.4.0_Rev8_ubuntu-64.bin
$ ./tizen-web-ide_TizenSDK_2.4.0_Rev8_ubuntu-64.bin

```

You must accept the license agreement and then the installation button will be enabled. It is recommended to install the SDK at the default location, since installing it elsewhere can cause the IDE to be unable to find some tools (like edje_cc). Once installed, you should be able to build projects and launch the emulator.