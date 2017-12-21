Artigos relacionados

*   [proot](/index.php/Proot "Proot")
*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")

[Chroot](https://en.wikipedia.org/wiki/pt:Chroot "wikipedia:pt:Chroot") é uma operação que altera o diretório raiz aparente para o processo atual de execução e seus filhos. Um programa que é executado em tal ambiente modificado não consegue acessar os arquivos e comandos fora dessa árvore de diretórios ambiental. Esse ambiente modificado é chamado de um *prisão chroot* (ou *chroot jail*).

## Contents

*   [1 Raciocínio](#Racioc.C3.ADnio)
*   [2 Requisitos](#Requisitos)
*   [3 Uso](#Uso)
    *   [3.1 Usando arch-chroot](#Usando_arch-chroot)
        *   [3.1.1 Entrar em um chroot](#Entrar_em_um_chroot)
        *   [3.1.2 Executar um único comando e sair](#Executar_um_.C3.BAnico_comando_e_sair)
    *   [3.2 Usando chroot](#Usando_chroot)
*   [4 Executar aplicativos gráficos a partir do chroot](#Executar_aplicativos_gr.C3.A1ficos_a_partir_do_chroot)
*   [5 Sem privilégios de root](#Sem_privil.C3.A9gios_de_root)
    *   [5.1 Proot](#Proot)
    *   [5.2 Fakechroot](#Fakechroot)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Raciocínio

Changing root is commonly done for performing system maintenance on systems where booting and/or logging in is no longer possible. Common examples are:

*   Reinstalling the [bootloader](/index.php/Bootloader "Bootloader").
*   Rebuilding the [initramfs image](/index.php/Mkinitcpio "Mkinitcpio").
*   Upgrading or [downgrading packages](/index.php/Downgrading_packages "Downgrading packages").
*   Resetting a [forgotten password](/index.php/Password_recovery "Password recovery").
*   Building packages in a clean chroot, see [DeveloperWiki:Building in a Clean Chroot](/index.php/DeveloperWiki:Building_in_a_Clean_Chroot "DeveloperWiki:Building in a Clean Chroot").

See also [Wikipedia:Chroot#Limitations](https://en.wikipedia.org/wiki/Chroot#Limitations "wikipedia:Chroot").

## Requisitos

*   Root privilege.

*   Another Linux environment, e.g. a LiveCD or USB flash media, or from another existing Linux distribution.

*   Matching architecture environments; i.e. the chroot from and chroot to. The architecture of the current environment can be discovered with: `uname -m` (e.g. i686 or x86_64).

*   Kernel modules loaded that are needed in the chroot environment.

*   Swap enabled if needed: `# swapon /dev/sd*xY*` 

*   Internet connection established if needed.

## Uso

**Note:**

*   Some [systemd](/index.php/Systemd "Systemd") tools such as *localectl* and *timedatectl* can not be used inside a chroot, as they require an active [dbus](/index.php/Dbus "Dbus") connection. [[1]](https://github.com/systemd/systemd/issues/798#issuecomment-126568596)
*   The file system that will serve as the new root (`/`) of your chroot must be accessible (i.e., decrypted, mounted).

There are two main options for using chroot, described below.

### Usando arch-chroot

The bash script `arch-chroot` is part of the [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) package. Before it runs `/usr/bin/chroot`, the script mounts api filesystems like `/proc` and makes `/etc/resolv.conf` available from the chroot.

#### Entrar em um chroot

Run arch-chroot with the new root directory as first argument:

```
# arch-chroot */location/of/new/root*

```

For example, in the [installation guide](/index.php/Installation_guide "Installation guide") this directory would be `/mnt`:

```
# arch-chroot /mnt

```

To exit the chroot simply use:

```
# exit

```

#### Executar um único comando e sair

To run a command from the chroot, and exit again append the command to the end of the line:

```
# arch-chroot */location/of/new/root* *mycommand*

```

For example, to run `mkinitcpio -p linux` for a chroot located at `/mnt/arch` do:

```
# arch-chroot /mnt/arch mkinitcpio -p linux

```

### Usando chroot

**Warning:** When using `--rbind`, some subdirectories of `dev/` and `sys/` will not be unmountable. Attempting to unmount with `umount -l` in this situation will break your session, requiring a reboot. If possible, use `-o bind` instead.

In the following example */location/of/new/root* is the directory where the new root resides.

First, mount the temporary api filesystems:

```
# cd */location/of/new/root*
# mount -t proc proc proc/
# mount --rbind /sys sys/
# mount --rbind /dev dev/

```

And optionally:

```
# mount --rbind /run run/

```

Next, in order to use an internet connection in the chroot environment copy over the DNS details:

```
# cp /etc/resolv.conf etc/resolv.conf

```

Finally, to change root into */location/of/new/root* using a bash shell:

```
# chroot */location/of/new/root* /bin/bash

```

**Note:** If you see the error:

*   `chroot: cannot run command '/usr/bin/bash': Exec format error`, it is likely that the architectures of the host environment and chroot environment do not match.
*   `chroot: '/usr/bin/bash': permission denied`, remount with the exec permission: `mount -o remount,exec /mnt/arch`.

After chrooting it may be necessary to load the local bash configuration:

```
# source /etc/profile
# source ~/.bashrc

```

**Tip:** Optionally, create a unique prompt to be able to differentiate your chroot environment: `# export PS1="(chroot) $PS1"` 

When finished with the chroot, you can exit it via:

```
# exit

```

Then unmount the temporary file systems:

```
# cd /
# umount --recursive */location/of/new/root*

```

**Note:** If there is an error mentioning something like: `umount: /path: device is busy` this usually means that either: a program (even a shell) was left running in the chroot or that a sub-mount still exists. Quit the program and use `mount` to find and `umount` sub-mounts). It may be tricky to `umount` some things and one can hopefully have `umount --force` work, as a last resort use `umount --lazy` which just releases them. In either case to be safe, `reboot` as soon as possible if these are unresolved to avoid possible future conflicts.

## Executar aplicativos gráficos a partir do chroot

If you have an [X server](/index.php/X_server "X server") running on your system, you can start graphical applications from the chroot environment.

To allow the chroot environment to connect to an X server, open a virtual terminal inside the X server (i.e. inside the desktop of the user that is currently logged in), then run the [xhost](/index.php/Xhost "Xhost") command, which gives permission to anyone to connect to the user's X server:

```
$ xhost +local:

```

Then, to direct the applications to the X server from chroot, set the DISPLAY environment variable inside the chroot to match the DISPLAY variable of the user that owns the X server. So for example, run

```
$ echo $DISPLAY

```

as the user that owns the X server to see the value of DISPLAY. If the value is ":0" (for example), then in the chroot environment run

```
# export DISPLAY=:0

```

## Sem privilégios de root

Chroot requires root privileges, which may not be desirable or possible for the user to obtain in certain situations. There are, however, various ways to simulate chroot-like behavior using alternative implementations.

### Proot

[Proot](/index.php/Proot "Proot") may be used to change the apparent root directory and use `mount --bind` without root privileges. This is useful for confining applications to a single directory or running programs built for a different CPU architecture, but it has limitations due to the fact that all files are owned by the user on the host system. Proot provides a `--root-id` argument that can be used as a workaround for some of these limitations in a similar (albeit more limited) manner to *fakeroot*.

### Fakechroot

[fakechroot](https://www.archlinux.org/packages/?name=fakechroot) is a library shim which intercepts the chroot call and fakes the results. It can be used in conjunction with [fakeroot](https://www.archlinux.org/packages/?name=fakeroot) to simulate a chroot as a regular user.

```
# fakechroot fakeroot chroot ~/my-chroot bash

```

## Veja também

*   [Basic Chroot](https://help.ubuntu.com/community/BasicChroot)