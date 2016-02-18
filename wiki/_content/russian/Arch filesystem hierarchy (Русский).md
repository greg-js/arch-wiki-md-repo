Arch Linux принадлежит к тем дистрибутивам, которые следуют стандарту иерархии файловой системы. Помимо описания каждой директории и ее назначения статья также раскрывает специфичные для Arch особенности.

## Contents

*   [1 Стандарт иерархии файловой системы](#.D0.A1.D1.82.D0.B0.D0.BD.D0.B4.D0.B0.D1.80.D1.82_.D0.B8.D0.B5.D1.80.D0.B0.D1.80.D1.85.D0.B8.D0.B8_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [1.1 Общедоступные и приватные файлы](#.D0.9E.D0.B1.D1.89.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D1.8B.D0.B5_.D0.B8_.D0.BF.D1.80.D0.B8.D0.B2.D0.B0.D1.82.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B)
*   [2 Директории](#.D0.94.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B8)
    *   [2.1 Корень файловой системы](#.D0.9A.D0.BE.D1.80.D0.B5.D0.BD.D1.8C_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
    *   [2.2 /bin: бинарные файлы основных команд](#.2Fbin:_.D0.B1.D0.B8.D0.BD.D0.B0.D1.80.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D1.85_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4)
    *   [2.3 /boot: Static bootloader files](#.2Fboot:_Static_bootloader_files)
    *   [2.4 /dev: Device files](#.2Fdev:_Device_files)
    *   [2.5 /etc: Host-specific configuration](#.2Fetc:_Host-specific_configuration)
        *   [2.5.1 /etc/X11](#.2Fetc.2FX11)
            *   [2.5.1.1 /etc/X11/xinit](#.2Fetc.2FX11.2Fxinit)
            *   [2.5.1.2 /etc/X11/xinit/xinitrc](#.2Fetc.2FX11.2Fxinit.2Fxinitrc)
    *   [2.6 /home: Каталоги пользователей](#.2Fhome:_.D0.9A.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.B8_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9)
    *   [2.7 /lost+found: Filesystem-specific recoverable data](#.2Flost.2Bfound:_Filesystem-specific_recoverable_data)
    *   [2.8 /mnt: Temporary mount points](#.2Fmnt:_Temporary_mount_points)
    *   [2.9 /opt: Problematic packages](#.2Fopt:_Problematic_packages)
    *   [2.10 /proc: Process information](#.2Fproc:_Process_information)
    *   [2.11 /root: Administrator directory](#.2Froot:_Administrator_directory)
    *   [2.12 /run: Ephemeral runtime data](#.2Frun:_Ephemeral_runtime_data)
    *   [2.13 /sbin: System binaries](#.2Fsbin:_System_binaries)
    *   [2.14 /srv: Service data](#.2Fsrv:_Service_data)
    *   [2.15 /tmp: Temporary files](#.2Ftmp:_Temporary_files)
    *   [2.16 /usr: Shareable, read-only data](#.2Fusr:_Shareable.2C_read-only_data)
        *   [2.16.1 /usr/bin: Binaries](#.2Fusr.2Fbin:_Binaries)
        *   [2.16.2 /usr/include: Header files](#.2Fusr.2Finclude:_Header_files)
        *   [2.16.3 /usr/lib: Libraries](#.2Fusr.2Flib:_Libraries)
        *   [2.16.4 /usr/sbin: System binaries](#.2Fusr.2Fsbin:_System_binaries)
        *   [2.16.5 /usr/share: Architecture independent data](#.2Fusr.2Fshare:_Architecture_independent_data)
        *   [2.16.6 /usr/src: Source code](#.2Fusr.2Fsrc:_Source_code)
        *   [2.16.7 /usr/local: Local hierarchy](#.2Fusr.2Flocal:_Local_hierarchy)
    *   [2.17 /var: Variable files](#.2Fvar:_Variable_files)
        *   [2.17.1 /var/abs](#.2Fvar.2Fabs)
        *   [2.17.2 /var/cache/pacman/pkg](#.2Fvar.2Fcache.2Fpacman.2Fpkg)
        *   [2.17.3 /var/lib: State information](#.2Fvar.2Flib:_State_information)
        *   [2.17.4 /var/log: Файлы логов](#.2Fvar.2Flog:_.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2)
        *   [2.17.5 /var/mail: User mail](#.2Fvar.2Fmail:_User_mail)
        *   [2.17.6 /var/spool: Queues](#.2Fvar.2Fspool:_Queues)
            *   [2.17.6.1 /var/spool/mail](#.2Fvar.2Fspool.2Fmail)
        *   [2.17.7 /var/tmp: Сохраненные временные файлы](#.2Fvar.2Ftmp:_.D0.A1.D0.BE.D1.85.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B)
*   [3 See also](#See_also)

## Стандарт иерархии файловой системы

С [домашней страницы Filesystem Hierarchy Standard (FHS)](http://www.pathname.com/fhs):

	"*Стандарт файловой системы был разработан, чтобы его использовали разработчики дистрибутивов Unix, пакетов программ и системные разработчики. Он в первую очередь является рекомендацией, а не руководством по управлению файловой системой Unix или иерархией каталогов.*"

### Общедоступные и приватные файлы

**Общедоступные** файлы подразумевают под собой такие права (биты) доступа, чтобы пользоваться и изменять их могли и другие пользователи. **Приватные** файлы считаются не общедоступными, то есть защищённые от доступа и редактирование другими. К примеру, общедоступные файлами считаются те, что хранятся в домашних директориях пользователей (предполагается, что права доступа (биты) не были изменены пользователем)

**Статичные** файлы включают в себя бинарные файлы, библиотеки, файлы документации и другие файлы, которые не могут быть изменены без вмешательства системного администратора. Также существуют **переменные** файлы, которые не являются статичными.

## Директории

### Корень файловой системы

Корневой каталог файловой системы, обозначаемый косой чертой (**/**), это первичный каталог, с которого берут начало все остальные; вершина иерархии. Все файлы и каталоги находятся под корневым каталогом "/", даже если они находятся на другом физическом устройстве. Содержимого корневого каталога должно быть достаточно, чтобы загружать, восстанавливать, исправлять систему.

### /bin: бинарные файлы основных команд

Traditionally the place for binaries that must be available in single user mode and accessible by all users (e.g., cat, ls, cp). /bin/ provides programs that must be available even if only the partition containing / is mounted. In practice, this is not the case on Arch as all the necessary libraries are in /usr/lib. In the future the Arch devs intend to merge /bin into /usr/bin. Unlike /sbin, the /bin directory is meant to contain commands that are of use to both the root user as well as non-root users.

### /boot: Static bootloader files

Unsharable, static directory containing the kernel and ramdisk images as well as the bootloader configuration file, and bootloader stages. /boot also stores data that is used before the kernel begins executing userspace programs. This may include saved master boot sectors and sector map files.

### /dev: Device files

Essential device nodes created by udev during the boot process and as machine hardware is discovered by events. This directory highlights one important aspect of the UNIX filesystem - everything is a file or a directory. Exploring this directory will reveal many files, each representing a hardware component of the system. The majority of devices are either block or character devices; however other types of devices exist and can be created. In general, 'block devices' are devices that store or hold data, whereas 'character devices' can be thought of as devices that transmit or transfer data. For example, hard disk drives and optical drives are categorized as block devices while serial ports, mice and USB ports are all character devices.

### /etc: Host-specific configuration

Host-specific, unsharable configuration files shall be placed in the /etc directory. If more than one configuration file is required for an application, it is customary to use a subdirectory in order to keep the /etc/ area as clean as possible. It is considered good practice to make frequent backups of this directory as it contains all system related configuration files.

#### /etc/X11

Конфигурационные файлы X Window System

##### /etc/X11/xinit

Конфигурационные файлы xinit. 'xinit' это метод конфигурации запуска X сессии, который разработан для использования как части скрипта.

##### /etc/X11/xinit/xinitrc

Глобальный файл xinitrc, используемый всеми X сессиями, запущенными с помощью xinit (или startx). При запуске X настройки этого файла будут перезаписаны файлом .xinitrc домашней директории пользователя.

### /home: Каталоги пользователей

UNIX - это многопользовательская среда. Поэтому каждому пользователю предназначена отдельная директория, доступ к окторой есть только у него и у пользователя root.

Каталог пользователя $USER находится в `/home/$USER`. Еще одно обозначение домашнего каталога - `~/`. В своем каталоге пользователь может устанавливать программы, а также производить любые действия с файлами: создавать, изменять, удалять.

Домашние каталоги пользователей содержат их личные данные и настройки, так называемые dot files (их имена начинаются с точки), и они являются скрытыми. Чтобы увидеть скрытые файлы, выполните: `ls -a` 
**Обратите внимание:** Чтобы увидеть скрытые файлы в [Thunar](/index.php/Thunar "Thunar") или [GNOME Files](/index.php/GNOME_Files "GNOME Files") воспользуйтесь сочетанием клавиш Ctrl + h

Пользовательские настройки обладают большим приоритетом, чем глобальные. Например, пользователь может настроить свои собственные файлы `.xinitrc` и `.bashrc` для конфигурации [xinit](/index.php/Xinit "Xinit") и [Bash](/index.php/Bash "Bash") соответственно. Это позволит пользователю изменить оконный менеджер на свой любимый, изменить aliases, установить особые команды и переменные среды. При создании нового пользователя файлы настройек берутся из каталога `/etc/skel`.

Дирекория `/home` может иметь значительный объем, так как она обычно используется для хранения загрузок, компиляции, установки и запуска программ, почты, медиа файлов.

### /lost+found: Filesystem-specific recoverable data

UNIX-like operating systems must execute a proper shutdown sequence. At times, a system might crash or a power failure might take the machine down. Either way, at the next boot, a filesystem check using the *fsck* program shall be performed. *Fsck* will go through the system and try to recover any corrupt files that it finds. The result of this recovery operation will be placed in this directory. The files recovered are not likely to be complete or make much sense but there always is a chance that something worthwhile is recovered.

### /mnt: Temporary mount points

This is a generic mount point for temporary filesystems or devices. Mounting is the process of making a filesystem available to the system. After mounting, files will be accessible under the mount-point. Additional mount-points (subdirectories) may be created under /mnt/. There is no limitation to creating a mount-point anywhere on the system, but by convention and for practicality, littering a file system with mount-points should be avoided.

### /opt: Problematic packages

Packages and large static files that do not fit cleanly into the above GNU filesystem layout can be placed in /opt. A package placing files in the /opt/ directory creates a directory bearing the same name as the package. This directory in turn holds files that otherwise would be scattered throughout the file system. For example, the acrobat package has Browser, Reader, and Resource directories sitting at the same level as the bin directory. This doesn't fit into a normal GNU filesystem layout, so Arch places all the files in a subdirectory of /opt.

### /proc: Process information

Directory /proc is very special in that it is also a virtual filesystem. It is sometimes referred to as the *process information pseudo-file system*. It doesn't contain 'real' files, but rather, runtime system information (e.g. system memory, devices mounted, hardware configuration, etc). For this reason it can be regarded as a control and information center for the kernel. In fact, quite a lot of system utilities are simply calls to files in this directory. For example, 'lsmod' is the same as 'cat /proc/modules' while 'lspci' is a synonym for 'cat /proc/pci'. By altering files located in this directory, kernel parameters may be read/changed (sysctl) while the system is running.

The most distinctive facet about files in this directory is the fact that all of them have a file size of 0, with the exception of **kcore, mounts** and **self**.

### /root: Administrator directory

Home directory of the System Administrator, 'root'. This may be somewhat confusing, ('/root under root') but historically, '/' was root's home directory (hence the name of the Administrator account). To keep things tidier, 'root' eventually got his own home directory. Why not in '/home'? Because '/home' is often located on a different partition or even on another system and would thus be inaccessible to 'root' when - for some reason - only '/' is mounted.

### /run: Ephemeral runtime data

The /run mountpoint is supposed to be a tmpfs mounted during early boot, available and writable to for all tools at any time during bootup. [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)"), [udev](/index.php/Udev "Udev") or mdadm that are required early in the boot process require this directory, because /var can be implemented as a separate file system to be mounted at a later stage in the start-up process. It replaces /var/run/, which becomes a symlink of /run.

### /sbin: System binaries

Traditionally UNIX discriminates between 'normal' executables and those used for system maintenance and/or administrative tasks. The latter were supposed to reside either here or - the less important ones - in /usr/sbin. Programs executed after /usr is known to be mounted (when there are no problems) are generally placed into /usr/sbin. This directory contains binaries that are essential to the working of the system. These include system administration as well as maintenance and hardware configuration programs. [GRUB](/index.php/GRUB "GRUB") (the command), fdisk, init, route, ifconfig, etc., all reside here. In practice, programs in /sbin require /usr to be mounted as all the necessary libraries are in /usr/lib. In the future the Arch devs intend to merge /sbin into /usr/bin.

### /srv: Service data

Site-specific data which is served by the system. The main purpose of specifying this is so that users may find the location of the data files for a particular service, and so that services which require a single tree for read-only data, writable data and scripts (such as CGI scripts) can be reasonably placed. Data of interest to a specific user shall be placed in that user's home directory.

### /tmp: Temporary files

This directory contains files that are required temporarily. Many programs use this to create lock files and for temporary storage of data. Do not remove files from this directory unless you know exactly what you are doing! Many of these files are important for currently running programs and deleting them may result in a system crash. On most systems, old files in this directory are cleared out at boot or at daily intervals.

### /usr: Shareable, read-only data

While root is the primary filesystem, /usr is the secondary hierarchy, for user data, containing the majority of (multi-)user utilities and applications. /usr is shareable, read-only data. This means that /usr shall be shareable between various hosts and must not be written to, except by the package manager (installation, update, upgrade). Any information that is host-specific or varies with time is stored elsewhere.

Aside from /home/, /usr/ usually contains by far the largest share of data on a system. Hence, this is one of the most important directories in the system as it contains all the user binaries, their documentation, libraries, header files, etc. X and its supporting libraries can be found here. User programs like telnet, ftp, etc., are also placed here. In the original UNIX implementations, /usr/ (for *user*), was where the home directories of the system's users were placed (that is to say, /usr/*someone* was then the directory now known as /home/*someone*). Over time, /usr/ has become where userspace programs and data (as opposed to 'kernelspace' programs and data) reside. The name has not changed, but its meaning has narrowed and lengthened from *everything user related* to *user usable programs and data*. As such, the backronym '**U**ser **S**ystem **R**esources' was created.

#### /usr/bin: Binaries

Command binaries. This directory contains the vast majority of binaries (applications) on your system. Executables in this directory vary widely. For instance vi, gcc, and gnome-session reside here. Traditionally, this contained only binaries that did not require root privileges and that were not necessary in single-user mode. However, this is no longer enforced and the Arch devs plan to move all binaries here.

#### /usr/include: Header files

Header files needed for compiling userspace source code..

#### /usr/lib: Libraries

**Обратите внимание:** The `/lib` directory becomes a symlink to `/usr/lib`. [Here](https://www.archlinux.org/news/the-lib-directory-becomes-a-symlink/) is the news. If you encounter error during this update. Please see [DeveloperWiki:usrlib](/index.php/DeveloperWiki:usrlib "DeveloperWiki:usrlib") for solution.

Contains application private data (kernel modules, systemd services, udev rules, etc) and shared library images (the C programming code library). Libraries are collections of frequently used program routines and are readily identifiable through their filename extension of *.so. They are essential for basic system functionality. Kernel modules (drivers) are in the subdirectory /lib/modules/<kernel-version>.

#### /usr/sbin: System binaries

Non-essential system binaries of use to the system administrator. This is where the network daemons for the system reside, along with other binaries that (generally) only the system administrator has access to, but which are not required for system maintenance and repair. The Arch devs plan to move all the binaries from /usr/sbin to /usr/bin.

#### /usr/share: Architecture independent data

This directory contains 'shareable', architecture-independent files (docs, icons, fonts etc). Note, however, that '/usr/share' is generally not intended to be shared by different operating systems or by different releases of the same operating system. Any program or package which contains or requires data that do not need to be modified should store these data in '/usr/share/' (or '/usr/local/share/', if manually installed - see below). It is recommended that a subdirectory be used in /usr/share for this purpose.

#### /usr/src: Source code

The 'linux' sub-directory holds the Linux kernel sources, and header-files.

#### /usr/local: Local hierarchy

Optional tertiary hierarchy for local data. The original idea behind '/usr/local' was to have a separate ('local') '/usr/' directory on every machine besides '/usr/', which might be mounted read-only from somewhere else. It copies the structure of '/usr/'. These days, '/usr/local/' is widely regarded as a good place in which to keep self-compiled or third-party programs. This directory is empty by default in Arch Linux. It may be used for manually compiled software installations if desired. [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") installs to /usr/, therefore, manually compiled/installed software installed to /usr/local/ may peacefully co-exist with pacman-tracked system software.

### /var: Variable files

Variable files, such as logs, spool files, and temporary e-mail files. On Arch, the [ABS](/index.php/ABS "ABS") tree and pacman cache also reside here. Why not put the variable and transient data into /usr/? Because there might be circumstances when /usr/ is mounted as read-only, e.g. if it is on a CD or on another computer. '/var/' contains variable data, i.e. files and directories the system must be able to write to during operation, whereas /usr/ shall only contain static data. Some directories can be put onto separate partitions or systems, e.g. for easier backups, due to network topology or security concerns. Other directories have to be on the root partition, because they are vital for the boot process. 'Mountable' directories are: '/home', '/mnt', '/tmp', '/usr' and '/var'. Essential for booting are: '/bin', '/boot', '/dev', '/etc', '/lib', '/proc' and '/sbin'.

#### /var/abs

The [ABS](/index.php/ABS "ABS") tree. A ports-like package build system hierarchy containing build scripts within subdirectories corresponding to all installable Arch software.

#### /var/cache/pacman/pkg

Кэш пакетов pacman.

#### /var/lib: State information

Persistent data modified by programs as they run (e.g. databases, packaging system metadata etc.).

#### /var/log: Файлы логов

Файлы логов.

#### /var/mail: User mail

Shareable directory for users' mailboxes.

#### /var/spool: Queues

Spool for tasks waiting to be processed (e.g. print queues and unread mail).

##### /var/spool/mail

Устаревшее расположение почтовых ящиков пользователя.

#### /var/tmp: Сохраненные временные файлы

Временные файлы, которые остаются сохраненными между перезагрузками.

## See also

*   [wikipedia:Filesystem Hierarchy Standard](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard "wikipedia:Filesystem Hierarchy Standard")