Related articles

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [VMware/Installing Arch as a guest](/index.php/VMware/Installing_Arch_as_a_guest "VMware/Installing Arch as a guest")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

This article is about installing VMware in Arch Linux; you may also be interested in [VMware/Installing Arch as a guest](/index.php/VMware/Installing_Arch_as_a_guest "VMware/Installing Arch as a guest").

**Note:**

*   This article is about the latest major VMware versions, meaning VMware Workstation Pro and Player 12.5 and 14\.
*   For older versions, use the [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) package.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 VMware bundle](#VMware_bundle)
    *   [1.2 Package build for x86_64](#Package_build_for_x86_64)
*   [2 Configuration](#Configuration)
    *   [2.1 Kernel modules](#Kernel_modules)
    *   [2.2 systemd services](#systemd_services)
        *   [2.2.1 Workstation Server service](#Workstation_Server_service)
*   [3 Launching the application](#Launching_the_application)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Entering the Workstation Pro license key](#Entering_the_Workstation_Pro_license_key)
        *   [4.1.1 From terminal](#From_terminal)
        *   [4.1.2 From GUI](#From_GUI)
    *   [4.2 Extracting the VMware BIOS](#Extracting_the_VMware_BIOS)
    *   [4.3 Extracting the installer](#Extracting_the_installer)
        *   [4.3.1 Using the modified BIOS](#Using_the_modified_BIOS)
    *   [4.4 Enable 3D graphics on Intel and Optimus](#Enable_3D_graphics_on_Intel_and_Optimus)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Kernel headers for version 4.x-xxxx were not found. If you installed them[...]](#Kernel_headers_for_version_4.x-xxxx_were_not_found._If_you_installed_them.5B....5D)
    *   [5.2 USB devices not recognized](#USB_devices_not_recognized)
    *   [5.3 Incorrect login/password when trying to access VMware remotely](#Incorrect_login.2Fpassword_when_trying_to_access_VMware_remotely)
    *   [5.4 Issues with ALSA output](#Issues_with_ALSA_output)
    *   [5.5 Kernel-based Virtual Machine (KVM) is running](#Kernel-based_Virtual_Machine_.28KVM.29_is_running)
    *   [5.6 Module Issues](#Module_Issues)
        *   [5.6.1 /dev/vmmon not found](#.2Fdev.2Fvmmon_not_found)
        *   [5.6.2 /dev/vmci not found](#.2Fdev.2Fvmci_not_found)
    *   [5.7 Installer Fails to Start](#Installer_Fails_to_Start)
        *   [5.7.1 User interface initialization failed](#User_interface_initialization_failed)
    *   [5.8 VMware Fails to Start](#VMware_Fails_to_Start)
        *   [5.8.1 Module CPUIDEarly power on failed](#Module_CPUIDEarly_power_on_failed)
        *   [5.8.2 Segmentation fault at startup due to old Intel microcode](#Segmentation_fault_at_startup_due_to_old_Intel_microcode)
        *   [5.8.3 vmplayer/vmware fails to start from version 12.5.4](#vmplayer.2Fvmware_fails_to_start_from_version_12.5.4)
        *   [5.8.4 vmplayer/vmware fails to start from version 12.5.3 to version 12.5.5](#vmplayer.2Fvmware_fails_to_start_from_version_12.5.3_to_version_12.5.5)
        *   [5.8.5 vmware 12 process terminates immediately after start, no GUI is launched](#vmware_12_process_terminates_immediately_after_start.2C_no_GUI_is_launched)
    *   [5.9 Guest Issues](#Guest_Issues)
        *   [5.9.1 Unable to download VMware Tools for Guests](#Unable_to_download_VMware_Tools_for_Guests)
        *   [5.9.2 Guests have incorrect system clocks or are unable to boot: "[...]timeTracker_user.c:234 bugNr=148722"](#Guests_have_incorrect_system_clocks_or_are_unable_to_boot:_.22.5B....5DtimeTracker_user.c:234_bugNr.3D148722.22)
        *   [5.9.3 Networking on Guests not available after system restart](#Networking_on_Guests_not_available_after_system_restart)
*   [6 Uninstallation](#Uninstallation)

## Installation

You can either install using VMware bundle or package [vmware-workstation](https://aur.archlinux.org/packages/vmware-workstation/). The latter is preferred if using *VMware Workstation* on x86_64.

**Warning:** VMware version 14 drops support for a number of CPUs including early core i7 cpus. Check the [Processor Requirements for Host Systems](https://docs.vmware.com/en/VMware-Workstation-Pro/14.0/com.vmware.ws.using.doc/GUID-BBD199AA-C346-4334-9F56-5A42F7328594.html). If version 14 does not support your cpu then you can use [vmware-workstation12](https://aur.archlinux.org/packages/vmware-workstation12/).

### VMware bundle

[Install](/index.php/Install "Install") the correct dependencies:

*   [fuse2](https://www.archlinux.org/packages/?name=fuse2) - for *vmware-vmblock-fuse*
*   [gtkmm](https://www.archlinux.org/packages/?name=gtkmm) - for the GUI
*   [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) - for module compilation
*   [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) - needed by the `--console` installer
*   [libcanberra](https://www.archlinux.org/packages/?name=libcanberra) - for event sounds
*   [pcsclite](https://www.archlinux.org/packages/?name=pcsclite)

Download the latest [VMware Workstation Pro](https://www.vmware.com/go/tryworkstation) or [Player](https://www.vmware.com/go/downloadplayer) (or a [beta](https://communities.vmware.com/community/vmtn/beta) version, if available).

Start the installation:

```
# sh VMware-*edition*-*version*.*release*.*architecture*.bundle

```

**Tip:** Some useful flags:

*   `--eulas-agreed` - Skip the EULAs
*   `--console` - Use the console UI.
*   `--custom` - Allows changing the install directory to e.g. `/usr/local` (make sure to update the `vmware-usbarbitrator.service` paths in [#systemd services](#systemd_services)).
*   `-I`, `--ignore-errors` - Ignore fatal errors.
*   `--set-setting=vmware-workstation serialNumber XXXXX-XXXXX-XXXXX-XXXXX-XXXXX` - Set the serial number during install (good for scripted installs).
*   `--required` - Only ask mandatory questions (results in silent install when combined with `--eulas-agreed` and `--console`).

For the `System service scripts directory`, use `/etc/init.d` (the default).

**Note:** During the installation you will get an error about `"No rc*.d style init script directories"` being given. This can be safely ignored, since Arch uses [systemd](/index.php/Systemd "Systemd").

**Tip:** To (re)build the modules from terminal later on, use:
```
# vmware-modconfig --console --install-all

```

### Package build for x86_64

Install [vmware-workstation](https://aur.archlinux.org/packages/vmware-workstation/), [vmware-workstation12](https://aur.archlinux.org/packages/vmware-workstation12/) or [vmware-workstation11](https://aur.archlinux.org/packages/vmware-workstation11/) for respectively versions 14, 12 and 11 of *VMware Workstation*. It is also necessary to install the appropriate headers package(s) for your installed kernel(s): for example [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) or [linux-lts-headers](https://www.archlinux.org/packages/?name=linux-lts-headers).

Then, as desired, enable some of the following services:

*   `vmware-networks.service` for guest network access
*   `vmware-usbarbitrator.service` for connecting USB devices to guest
*   `vmware-hostd.service` for sharing virtual machines

Lastly, load the VMware modules:

```
# modprobe -a vmw_vmci vmmon

```

## Configuration

### Kernel modules

VMware Workstation 12.5 supports kernels up to 4.8 out of the box.

For VMware bundle versions, a collection of patches needed for the VMware host modules to build against recent kernels can be found from the following GitHub repository, [vmware-host-modules](https://github.com/mkubecek/vmware-host-modules/). See the INSTALL document found on the repository for the most up-to-date module installation instructions for VMware versions from 12.5.5 and up.

Alternatively, the modules can be patched installing the [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) package and executing:

```
# vmware-patch -f

```

### systemd services

*(Optional)* Instead of using `/etc/init.d/vmware` (`start|stop|status|restart`) and `/usr/bin/vmware-usbarbitrator` directly to manage the services, you may also use `.service` files (also available in the [vmware-systemd-services](https://aur.archlinux.org/packages/vmware-systemd-services/) package, and also included in [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/) and [vmware-workstation](https://aur.archlinux.org/packages/vmware-workstation/) with a few differences):

 `/etc/systemd/system/vmware.service` 
```
[Unit]
Description=VMware daemon
Requires=vmware-usbarbitrator.service
Before=vmware-usbarbitrator.service
After=network.target

[Service]
ExecStart=/etc/init.d/vmware start
ExecStop=/etc/init.d/vmware stop
PIDFile=/var/lock/subsys/vmware
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```
 `/etc/systemd/system/vmware-usbarbitrator.service` 
```
[Unit]
Description=VMware USB Arbitrator
Requires=vmware.service
After=vmware.service

[Service]
ExecStart=/usr/bin/vmware-usbarbitrator
ExecStop=/usr/bin/vmware-usbarbitrator --kill
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Add this service as well, if you want to connect to your VMware Workstation installation from another Workstation Server Console:

 `/etc/systemd/system/vmware-workstation-server.service` 
```
[Unit]
Description=VMware Workstation Server
Requires=vmware.service
After=vmware.service

[Service]
ExecStart=/etc/init.d/vmware-workstation-server start
ExecStop=/etc/init.d/vmware-workstation-server stop
PIDFile=/var/lock/subsys/vmware-workstation-server
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

After which you can [enable](/index.php/Enable "Enable") them on boot.

#### Workstation Server service

The `vmware-workstation-server.service` calls `wssc-adminTool` in its command chain, despite having been renamed to `vmware-wssc-adminTool`.

To prevent the service startup, this can be fixed with a symlink:

```
# ln -s wssc-adminTool /usr/lib/vmware/bin/vmware-wssc-adminTool

```

## Launching the application

To open VMware Workstation Pro:

```
$ vmware

```

or Player:

```
$ vmplayer

```

## Tips and tricks

### Entering the Workstation Pro license key

#### From terminal

```
# /usr/lib/vmware/bin/vmware-vmx-debug --new-sn XXXXX-XXXXX-XXXXX-XXXXX-XXXXX

```

Where `XXXXX-XXXXX-XXXXX-XXXXX-XXXXX` is your license key.

**Note:** The `-debug` binary informs the user of an incorrect license.

#### From GUI

If the above does not work, you can try:

```
# /usr/lib/vmware/bin/vmware-enter-serial

```

### Extracting the VMware BIOS

```
$ objcopy /usr/lib/vmware/bin/vmware-vmx -O binary -j bios440 --set-section-flags bios440=a bios440.rom.Z
$ perl -e 'use Compress::Zlib; my $v; read STDIN, $v, '$(stat -c%s "./bios440.rom.Z")'; $v = uncompress($v); print $v;' < bios440.rom.Z > bios440.rom

```

### Extracting the installer

To view the contents of the installer `.bundle`:

```
$ sh VMware-*edition*-*version*.*release*.*architecture*.bundle --extract */tmp/vmware-bundle/*

```

#### Using the modified BIOS

If and when you decide to modify the extracted BIOS you can make your virtual machine use it by moving it to `~/vmware/*Virtual_machine_name*`:

```
$ mv bios440.rom ~/vmware/*Virtual_machine_name*/

```

then adding the name to the `*Virtual_machine_name*.vmx` file:

 `~/vmware/*Virtual_machine_name*/*Virtual_machine_name*.vmx`  `bios440.filename = "bios440.rom"` 

### Enable 3D graphics on Intel and Optimus

Some graphics drivers are blacklisted by default, due to poor and/or unstable 3D acceleration. After enabling *Accelerate 3D graphics*, the log may show something like:

```
Disabling 3D on this host due to presence of Mesa DRI driver.  Set mks.gl.allowBlacklistedDrivers = TRUE to override.

```

This means the append the following line to the file using your prefered editor:

 `~/.vmware/preferences`  `mks.gl.allowBlacklistedDrivers = TRUE` 

## Troubleshooting

### Kernel headers for version 4.x-xxxx were not found. If you installed them[...]

Install the headers ([linux-headers](https://www.archlinux.org/packages/?name=linux-headers)).

**Note:** Upgrading the kernel and the headers will require you to boot to the new kernel to match the version of the headers. This is a relatively common error.

### USB devices not recognized

**Tip:** Also handled by [vmware-patch](https://aur.archlinux.org/packages/vmware-patch/).

If not using the [systemd service](#systemd_services) to automatically handle the services, you need to manually start the `vmware-usbarbitrator` binary as root each time.

To start:

```
# vmware-usbarbitrator

```

To stop:

```
# vmware-usbarbitrator --kill

```

### Incorrect login/password when trying to access VMware remotely

VMware Workstation provides the possibility to remotely manage Shared VMs through the `vmware-workstation-server` service. However, this will fail with the error `"incorrect username/password"` due to incorrect [PAM](/index.php/PAM "PAM") configuration of the `vmware-authd` service. To fix it, edit `/etc/pam.d/vmware-authd` like this:

 `/etc/pam.d/vmware-authd` 
```
#%PAM-1.0
auth     *required       pam_unix.so*
account  *required       pam_unix.so*
password *required       pam_permit.so*
session  *required       pam_unix.so*

```

and restart the `vmware` [systemd](/index.php/Systemd "Systemd") service.

Now you can connect to the server with the credentials provided during the installation.

**Note:** [libxslt](https://www.archlinux.org/packages/?name=libxslt) may be required for starting virtual machines.

### Issues with ALSA output

[To fix](http://bankimbhavsar.blogspot.co.nz/2011/09/hd-audio-in-vmware-fusion-4-and-vmware.html) sound quality issues or enabling proper HD audio output, first run:

```
$ aplay -L

```

If interested in playing 5.1 *surround sound* from the guest, look for `surround51:CARD=*vendor_name*,DEV=*num*`, if experiencing quality issues, look for `front:CARD=*vendor_name*,DEV=*num*`. Finally put the name in the `.vmx`:

 `~/vmware/*Virtual_machine_name*/*Virtual_machine_name*.vmx` 
```
sound.fileName=*"surround51:CARD=Live,DEV=0"*
sound.autodetect=*"FALSE"*
```

[OSS emulation](/index.php/Advanced_Linux_Sound_Architecture#OSS_compatibility "Advanced Linux Sound Architecture") should also be disabled.

### Kernel-based Virtual Machine (KVM) is running

To disable `KVM` on boot, you can use something like:

 `/etc/modprobe.d/vmware.conf` 
```
blacklist kvm
blacklist kvm-amd   # For AMD CPUs
blacklist kvm-intel # For Intel CPUs

```

### Module Issues

#### /dev/vmmon not found

The full error is:

```
Could not open /dev/vmmon: No such file or directory.
Please make sure that the kernel module 'vmmon' is loaded.

```

This means that at least the `vmmon` module is not loaded. See the [#systemd services](#systemd_services) section for automatic loading.

#### /dev/vmci not found

The full error is:

```
Failed to open device "/dev/vmci": No such file or directory
Please make sure that the kernel module 'vmci' is loaded.

```

Try to recompile VMware kernel modules with:

```
# vmware-modconfig --console --install-all

```

### Installer Fails to Start

If you just get back to the prompt when opening the `.bundle`, then you probably have a deprecated or broken version of the VMware installer and it should removed (you may also refer to the [uninstallation](#Uninstallation) section of this article):

```
# rm -r /etc/vmware-installer/

```

#### User interface initialization failed

You may also see an error like this:

```
 Extracting VMware Installer...done.
 No protocol specified
 No protocol specified
 User interface initialization failed.  Exiting.  Check the log for details.

```

This can be fixed by either installing the [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/) dependency or temporarily allowing root access to X:

```
 $ xhost +
 $ sudo ./<vmware filename>.bundle
 $ xhost -

```

### VMware Fails to Start

#### Module CPUIDEarly power on failed

Version 14 has stricter cpu requirements than version 12\. If you have an affected cpu then, if you try to start a virtual machine, a dialog will appear with messages like "This host does not support virtualizing real mode." and "The Intel "VMX Unrestricted Guest" feature is necessary to run this virtual machine on an Intel processor."

The solution is to uninstall version 14 and install version 12 ([vmware-workstation12](https://aur.archlinux.org/packages/vmware-workstation12/)).

#### Segmentation fault at startup due to old Intel microcode

Old Intel microcode may result in the following kind of segmentation fault at startup:

```
/usr/bin/vmware: line 31: 4941 Segmentation fault "$BINDIR"/vmware-modconfig --appname="VMware Workstation" --icon="vmware-workstation"

```

See [Microcode](/index.php/Microcode "Microcode") for how to update the microcode.

#### vmplayer/vmware fails to start from version 12.5.4

As per [[1]](https://bbs.archlinux.org/viewtopic.php?id=224667) the temporary workaround is to downgrade the package `libpng` to version 1.6.28-1 and keep it in the `IgnorePkg` parameter in [/etc/pacman.conf](/index.php/Pacman#Skip_package_from_being_upgraded "Pacman").

An easier workaround is to make VMWare use the system's version of zlib instead of its own one:

```
# cd /usr/lib/vmware/lib/libz.so.1
# mv libz.so.1 libz.so.1.old
# ln -s /usr/lib/libz.so.1 .

```

#### vmplayer/vmware fails to start from version 12.5.3 to version 12.5.5

It seems to be a problem with the file `/usr/lib/vmware/lib/libstdc++.so.6/libstdc++.so.6`, missing `CXXABI_1.3.8`.

If the system have installed [gcc-libs](https://www.archlinux.org/packages/?name=gcc-libs), that library is already installed. Therefore, it's possible to remove that file and vmplayer will use the one provided by gcc-libs instead. As root do:

```
# mv /usr/lib/vmware/lib/libstdc++.so.6/libstdc++.so.6 /usr/lib/vmware/lib/libstdc++.so.6/libstdc++.so.6.bak

```

Also there is a workaround:

```
# export VMWARE_USE_SHIPPED_LIBS='yes'

```

#### vmware 12 process terminates immediately after start, no GUI is launched

Registered bug at [Mageia](https://bugs.mageia.org/show_bug.cgi?id=9739), but it seems that there are no error messages shown in terminal with arch. When inspecting the logs, which are in `/tmp/vmware-<id>`, there are `VMWARE_SHIPPED_LIBS_LIST is not set`, `VMWARE_SYSTEM_LIBS_LIST is not set`, `VMWARE_USE_SHIPPED_LIBS is not set`, `VMWARE_USE_SYSTEM_LIBS is not set` issues. Process simply terminates with `Unable to execute /usr/lib/vmware/bin/vmware-modconfig.` after vmware or vmplayer is executed. Solution is the same, as root do:

```
# mv /etc/vmware/icu/icudt44l.dat /etc/vmware/icu/icudt44l.dat.bak

```

Also there is a workaround:

```
# export VMWARE_USE_SHIPPED_LIBS='yes'

```

Despite setting the VMWARE_USE_SHIPPED_LIBS variable, VMWare may still fail to find certain libraries. An example is the libfontconfig.so.1 library. Check vmware logs in the tmp directory to see which libraries are still not found. Copy them to the appropriate path with libraries existing on the system:

```
# cp /usr/lib/libfontconfig.so.1 /usr/lib/vmware/lib/libfontconfig.so.1/

```

Instead of copying all these files manually, you may want to try exporting an additional setting:

```
# export VMWARE_USE_SYSTEM_LIBS='yes'

```

On systems with fontconfig version **2.13.0** and above, it may be needed to replace the shipped libfontconfig file with version **2.12.6** library file and force VMware to use that file instead of the newer system file. This applies for at least VMware version **12.5.9**. As root do:

```
# cd /usr/lib/vmware/lib/libfontconfig.so.1
# wget [https://archive.archlinux.org/packages/f/fontconfig/fontconfig-2.12.6-1-x86_64.pkg.tar.xz](https://archive.archlinux.org/packages/f/fontconfig/fontconfig-2.12.6-1-x86_64.pkg.tar.xz)
# tar -xvf fontconfig-2.12.6-1-x86_64.pkg.tar.xz usr/lib/libfontconfig.so.1.10.1
# mv libfontconfig.so.1 libfontconfig.so.1.old
# mv ./usr/lib/libfontconfig.so.1.10.1 ./libfontconfig.so.1
# rm -r ./usr ./fontconfig-2.12.6-1-x86_64.pkg.tar.xz
# export LD_LIBRARY_PATH=/usr/lib/vmware/lib/libfontconfig.so.1:$LD_LIBRARY_PATH

```

### Guest Issues

#### Unable to download VMware Tools for Guests

To download the tools manually, visit the [VMware repository](http://softwareupdate.vmware.com/cds/vmw-desktop/).

Navigate to: "*application name* / *version* / *build ID* / linux / packages/" and download the appropriate Tools.

Extract with:

```
$ tar -xvf vmware-tools-*name*-*version*-*buildID*.x86_64.component.tar

```

And install using the VMware installer:

```
# vmware-installer --install-component=*/path/*vmware-tools-*name*-*version*-*buildID*.x86_64.component

```

If the above does not work, try installing [ncurses5-compat-libs](https://aur.archlinux.org/packages/ncurses5-compat-libs/).

#### Guests have incorrect system clocks or are unable to boot: "[...]timeTracker_user.c:234 bugNr=148722"

This is due to [incomplete](http://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&externalId=1591) support of power management features ([Intel SpeedStep](https://en.wikipedia.org/wiki/Intel_speedstep "wikipedia:Intel speedstep") and [AMD PowerNow!](https://en.wikipedia.org/wiki/AMD_powernow "wikipedia:AMD powernow")/[Cool'n'Quiet](https://en.wikipedia.org/wiki/Cool%27n%27Quiet "wikipedia:Cool'n'Quiet")) in VMware Linux that vary the CPU frequency. In March 2012, with the release of [linux 3.3-1](https://projects.archlinux.org/svntogit/packages.git/commit/trunk/config.x86_64?h=packages/linux&id=9abe018d91a5d8c3af7523d30b8aa73f86b680be) the maximum frequency [Performance](/index.php/CPU_frequency_governors "CPU frequency governors") governor was replaced with the dynamic *Ondemand*. When the host CPU frequency changes, the Guest system clock runs too quickly or too slowly, but may also render the whole Guest unbootable.

To prevent this, the maximum host CPU frequency can be specified, and [Time Stamp Counter](https://en.wikipedia.org/wiki/Time_Stamp_Counter "wikipedia:Time Stamp Counter") (TSC) disabled, in the global configuration:

 `/etc/vmware/config` 
```
host.cpukHz = "X"  # The maximum speed in KHz, e.g. 3GHz is "3000000".
host.noTSC = "TRUE" # Keep the Guest system clock accurate even when
ptsc.noTSC = "TRUE" # the time stamp counter (TSC) is slow.
```

**Tip:** To periodically correct the time (once per minute), in the *Options* tab of VMware Tools, enable: *"Time synchronization between the virtual machine and the host operating system"*.

#### Networking on Guests not available after system restart

This is likely due to the `vmnet` module not being loaded [[2]](http://www.linuxquestions.org/questions/slackware-14/could-not-connect-ethernet0-to-virtual-network-dev-vmnet8-796095/). See also the [#systemd services](#systemd_services) section for automatic loading.

## Uninstallation

To uninstall VMware you need the product name (either `vmware-workstation` or `vmware-player`). To list all the installed products:

```
$ vmware-installer -l

```

and uninstall with (`--required` skips the confirmation):

```
# vmware-installer -u *product* --required

```

**Tip:** Use `--console` for the console UI.

Remember to also [disable](/index.php/Disable "Disable") and remove the services:

```
# rm /etc/systemd/system/vmware.service
# rm /etc/systemd/system/vmware-usbarbitrator.service

```

You may also want to have a look at the module directories in `/usr/lib/modules/*kernel_name*/misc/` for any leftovers, and remove `/etc/init.d/` if now empty.