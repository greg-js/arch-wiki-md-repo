This page documents progress on fixing/implementing non-CVE security-related bugs and features.

## Contents

*   [1 Service Isolation](#Service_Isolation)
    *   [1.1 User/Group](#User.2FGroup)
    *   [1.2 PrivateDevices](#PrivateDevices)
    *   [1.3 PrivateNetwork](#PrivateNetwork)
    *   [1.4 PrivateTmp](#PrivateTmp)
    *   [1.5 ReadOnly/ReadWrite](#ReadOnly.2FReadWrite)
    *   [1.6 NetworkManager / wpa_supplicant](#NetworkManager_.2F_wpa_supplicant)
*   [2 World-readable/writeable directories](#World-readable.2Fwriteable_directories)
*   [3 Replacing setuid with capabilities](#Replacing_setuid_with_capabilities)
*   [4 kernel hardening](#kernel_hardening)
*   [5 Compiler / linker hardening](#Compiler_.2F_linker_hardening)
    *   [5.1 Packages not respecting flags](#Packages_not_respecting_flags)
        *   [5.1.1 Tangible attack surface](#Tangible_attack_surface)
        *   [5.1.2 Seemingly no tangible attack surface](#Seemingly_no_tangible_attack_surface)
    *   [5.2 Full RELRO](#Full_RELRO)
    *   [5.3 PIE](#PIE)
        *   [5.3.1 Example](#Example)
    *   [5.4 hardening-wrapper](#hardening-wrapper)
*   [6 non-root X](#non-root_X)
*   [7 grsecurity](#grsecurity)
    *   [7.1 kernel](#kernel)
        *   [7.1.1 use upstream features when possible](#use_upstream_features_when_possible)
        *   [7.1.2 Enable *privileged* user namespaces](#Enable_privileged_user_namespaces)
        *   [7.1.3 Enable KASLR and hide symbols](#Enable_KASLR_and_hide_symbols)
        *   [7.1.4 CONFIG_GRKERNSEC_PROC=n](#CONFIG_GRKERNSEC_PROC.3Dn)
        *   [7.1.5 CONFIG_GRKERNSEC_SYSCTL_ON=n](#CONFIG_GRKERNSEC_SYSCTL_ON.3Dn)
        *   [7.1.6 disable Yama](#disable_Yama)
    *   [7.2 PaX](#PaX)
*   [8 See also](#See_also)

## Service Isolation

Green cells indicate a security feature is implemented, and red cells indicate the lack of a feature. If it's not possible to implement a feature without losing functionality (even if off-by-default), a reason is given instead. This also applies to features that are simply not useful, such as PrivateTmp for services without any usage of `/tmp` as these can be handled with InaccessibleDirectories.

A red cell without a link to an issue report indicates that research/testing is required in order to either mark it as not possible or report an issue.

| Package | Service | User | Group | PrivateDevices | PrivateNetwork | PrivateTmp |
| [chrony](https://www.archlinux.org/packages/?name=chrony) | `chrony.service` | chrony | chrony | can use `/dev/rtc` | n/a | No |
| [cronie](https://www.archlinux.org/packages/?name=cronie) | `cronie.service` | root (jobs) | root (jobs) | jobs | jobs | jobs |
| [lighttpd](https://www.archlinux.org/packages/?name=lighttpd) | `lighttpd.service` | http | http | No | n/a | Yes |
| [paxd](https://www.archlinux.org/packages/?name=paxd) | `paxd.service` | root (xattrs) | root (xattrs) | No | No | not used |
| [pdnsd](https://www.archlinux.org/packages/?name=pdnsd) | `pdnsd.service` | pdnsd | pdnsd | can use `/dev/isdninfo` | n/a | not used |
| [polipo](https://www.archlinux.org/packages/?name=polipo) | `polipo.service` | polipo | polipo | Yes | n/a | No |
| [polkit](https://www.archlinux.org/packages/?name=polkit) | `polkit.service` | polkitd | polkitd | rules | rules | rules |
| [privoxy](https://www.archlinux.org/packages/?name=privoxy) | `privoxy.service` | privoxy | privoxy | Yes | n/a | No |
| [networkmanager](https://www.archlinux.org/packages/?name=networkmanager) | `NetworkManager.service` | root | root | No | n/a | No |
| [nginx](https://www.archlinux.org/packages/?name=nginx) | `nginx.service` | http | http | Yes | n/a | No |
| [ntp](https://www.archlinux.org/packages/?name=ntp) | `ntpdate.service` | ntp | ntp | No | n/a | Yes |
| `ntpd.service` | ntp | ntp | No | n/a | Yes |
| [tor](https://www.archlinux.org/packages/?name=tor) | `tor.service` | tor | tor | Yes | n/a | not used |
| [tinyproxy](https://www.archlinux.org/packages/?name=tinyproxy) | `tinyproxy.service` | tinyproxy | tinyproxy | Yes | n/a | No |
| [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) | `transmission.service` | transmission | transmission | No | n/a | No |
| [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) | `wpa_supplicant.service` | root | root | No | No | No |
| [znc](https://www.archlinux.org/packages/?name=znc) | `znc.service` | znc | znc | No | n/a | No |

### User/Group

In nearly every case, services should use an unprivileged user rather than running as root. Some cases may require the use of capabilities like CAP_NET_ADMIN or CAP_NET_BIND_SERVICE. Some exceptions are cron daemons, since they need to run scripts as root and anything needing CAP_SYS_ADMIN or a similar capability essentially equivalent to root access.

It is **not** appropriate to run services as `nobody`. If this user is shared among more than one service, then they are vulnerable to each other. For example, consider a caching dns server (pdnsd) running as nobody alongside ntpd running as nobody. If ntpd is compromised via a vulnerability, all the attacker should be able to do is mess with the time. However, thanks to the use of `nobody` they will be able to intercept/modify all dns requests and alter the persistent cache.

### PrivateDevices

If there is absolutely no usage of `/dev/`, then `InaccessibleDirectories` combined with `DevicePolicy=strict` is a valid alternative.

[https://fedoraproject.org/wiki/Changes/PrivateDevicesAndPrivateNetwork](https://fedoraproject.org/wiki/Changes/PrivateDevicesAndPrivateNetwork)

### PrivateNetwork

This can be used for any service without a need for network communication beyond sockets provided through socket activation.

[https://fedoraproject.org/wiki/Changes/PrivateDevicesAndPrivateNetwork](https://fedoraproject.org/wiki/Changes/PrivateDevicesAndPrivateNetwork)

### PrivateTmp

This should only be used if a service needs to make use of `/tmp`. Bash makes extensive use of `/tmp` for stuff like here documents, so any shell usage is enough to make it worthwhile.

[https://fedoraproject.org/wiki/Features/ServicesPrivateTmp](https://fedoraproject.org/wiki/Features/ServicesPrivateTmp)

### ReadOnly/ReadWrite

systemd has some basic MAC capabilities (InaccessibleDirectories, ReadWriteDirectories, ReadOnlyDirectories), but is limited to directories since it's based on bind mounts in a mount namespace. These features do not currently have the ability to recurse into submounts, causing the increase in security to be misleading. It doesn't appear that a whitelist model will work yet either, so it's far from providing true isolation at this point.

### NetworkManager / wpa_supplicant

It might be possible to drop nearly all capabilities other than CAP_NET_ADMIN. Of course, if these need CAP_SYS_ADMIN for something there's no point.

## World-readable/writeable directories

Many packages have unnecessarily world-readable directories, and some even have unnecessarily world-writeable ones. These permissions should be tightened up.

*   [FS#39808](https://bugs.archlinux.org/task/39808) - [lighttpd] /var/{cache,log}/lighttpd should not be world-readable

## Replacing setuid with capabilities

This is a scratch space tracking which packages still include setuid binaries and replacing these with capabilities where possible. Reducing setuid to CAP_SYS_ADMIN or any capabilities allowing escalation to root access is not very useful (at least without MAC/RBAC backing it up), so it will not be covered (yet?).

*   ~~[FS#39686](https://bugs.archlinux.org/task/39686) - [inetutils] rsh, rcp and rlogin should use cap_net_bind_service, not setuid~~
*   [sudo](https://www.archlinux.org/packages/?name=sudo) - requires setuid

## kernel hardening

*   CONFIG_SECURITY_DMESG_RESTRICT ([FS#39685](https://bugs.archlinux.org/task/39685) - closed, not implemented)
*   kptr_restrict=1 ([FS#34323](https://bugs.archlinux.org/task/34323) - closed, not implemented)
*   CONFIG_RANDOMIZE_BASE ([FS#41463](https://bugs.archlinux.org/task/41463) - closed, not implemented)
*   higher CONFIG_DEFAULT_MMAP_MIN_ADDR ([FS#41260](https://bugs.archlinux.org/task/41260) - implemented)
*   RO/NX protections for loadable kernel modules ([FS#41347](https://bugs.archlinux.org/task/41347) - implemented)

## Compiler / linker hardening

The current globally enabled hardening flags:

*   CPPFLAGS: -D_FORTIFY_SOURCE=2
*   CFLAGS/CXXFLAGS: -fstack-protector-strong --param=ssp-buffer-size=4
*   LDFLAGS: -z relro

### Packages not respecting flags

#### Tangible attack surface

*   [john](https://www.archlinux.org/packages/?name=john) - [FS#43232](https://bugs.archlinux.org/task/43232)
*   ~~[gpsd](https://www.archlinux.org/packages/?name=gpsd) - [FS#43233](https://bugs.archlinux.org/task/43233)~~
*   [bzip2](https://www.archlinux.org/packages/?name=bzip2) - [FS#43231](https://bugs.archlinux.org/task/43231)
*   [festival](https://www.archlinux.org/packages/?name=festival) - [FS#43229](https://bugs.archlinux.org/task/43229)
*   ~~[zita-alsa-pcmi](https://www.archlinux.org/packages/?name=zita-alsa-pcmi) - [FS#43230](https://bugs.archlinux.org/task/43230)~~ - rebuild
*   ~~[zita-resampler](https://www.archlinux.org/packages/?name=zita-resampler)~~ - rebuild
*   ~~[mpv](https://www.archlinux.org/packages/?name=mpv) - [FS#43235](https://bugs.archlinux.org/task/43235)~~ - hardening-wrapper
*   ~~[ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)~~ - hardening-wrapper
*   [ghostscript](https://www.archlinux.org/packages/?name=ghostscript) - [FS#43234](https://bugs.archlinux.org/task/43234)
*   [zip](https://www.archlinux.org/packages/?name=zip) - [FS#43236](https://bugs.archlinux.org/task/43236)
*   ~~[unrar](https://www.archlinux.org/packages/?name=unrar) - [FS#43237](https://bugs.archlinux.org/task/43237)~~ - hardening-wrapper
*   [python](https://www.archlinux.org/packages/?name=python), [python2](https://www.archlinux.org/packages/?name=python2) - [FS#43246](https://bugs.archlinux.org/task/43246)
*   [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) - missing SSP even with hardening-wrapper, needs to be investigated
*   [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick) - missing SSP even with hardening-wrapper, needs to be investigated

#### Seemingly no tangible attack surface

**Note:** It would be nice if these were fixed but it doesn't seem worth filing bugs for them.

*   [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)
*   [boost](https://www.archlinux.org/packages/?name=boost)
*   [gcc](https://www.archlinux.org/packages/?name=gcc)
*   [libcap](https://www.archlinux.org/packages/?name=libcap)
*   [glew](https://www.archlinux.org/packages/?name=glew)
*   [dmenu](https://www.archlinux.org/packages/?name=dmenu)
*   [gsl](https://www.archlinux.org/packages/?name=gsl)
*   [hdparm](https://www.archlinux.org/packages/?name=hdparm)
*   [lm_sensors](https://www.archlinux.org/packages/?name=lm_sensors)
*   [lsof](https://www.archlinux.org/packages/?name=lsof)
*   [procinfo-ng](https://www.archlinux.org/packages/?name=procinfo-ng)
*   [nethogs](https://www.archlinux.org/packages/?name=nethogs)
*   [qtchooser](https://aur.archlinux.org/packages/qtchooser/)
*   [rust](https://www.archlinux.org/packages/?name=rust)

### Full RELRO

Arch passes `-z relro` to the linker in the default `LDFLAGS`, causing many internal ELF data sections to be marked read-only. However, passing `-z now` to disable lazy relocations is required to make all of these sections read-only and prevent gaining control of the process solely via modifications of the existing data. This will cause a loss in initial start-up performance, but it is negligible for most binaries.

Packages with this enabled by default via upstream build flags:

*   [chromium](https://www.archlinux.org/packages/?name=chromium)
*   [colord](https://www.archlinux.org/packages/?name=colord)
*   [playpen](https://www.archlinux.org/packages/?name=playpen)
*   [openssh](https://www.archlinux.org/packages/?name=openssh)
*   [qemu](https://www.archlinux.org/packages/?name=qemu)
*   [systemd](https://www.archlinux.org/packages/?name=systemd)
*   [upower](https://www.archlinux.org/packages/?name=upower)
*   [tor](https://www.archlinux.org/packages/?name=tor)

### PIE

[ASLR](https://en.wikipedia.org/wiki/ASLR "wikipedia:ASLR") is enabled by default, and a stronger implementation is available in [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec). Data and code addresses in dynamic libraries are always randomized because these are always [position independent code](https://en.wikipedia.org/wiki/Position_independent_code "wikipedia:Position independent code"). However, executables are not position independent by default and cannot take advantage of ASLR. This also applies to important ELF data like the GOT/PLT where many library functions will be referenced, so ASLR is essentially useless without PIE. Passing `-fPIE` (or `-fPIC`) while compiling and `-pie` while linking will enable PIE, but these cannot simply be default flags because it will break libraries.

Packages with this enabled by default via upstream build flags:

*   [colord](https://www.archlinux.org/packages/?name=colord)
*   [chromium](https://www.archlinux.org/packages/?name=chromium)
*   [cups](https://www.archlinux.org/packages/?name=cups)
*   [playpen](https://www.archlinux.org/packages/?name=playpen)
*   [openssh](https://www.archlinux.org/packages/?name=openssh)
*   [qemu](https://www.archlinux.org/packages/?name=qemu)
*   [sudo](https://www.archlinux.org/packages/?name=sudo)
*   [systemd](https://www.archlinux.org/packages/?name=systemd)
*   [upower](https://www.archlinux.org/packages/?name=upower)
*   [tor](https://www.archlinux.org/packages/?name=tor)

#### Example

 `aslr.c` 
```
#include <stdio.h>

static void foo() {}
static int bar = 5;

int main(void) {
    int baz = 5;
    printf("function: %p, library function: %p, data: %p, stack: %p
", foo, &printf, &bar, &baz);
    return 0;
}
```
 `$ gcc -o aslr aslr.c; for i in $(seq 1 10); do ./aslr; done` 
```
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fff909cac1c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fffee85453c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fff0d05a1ec
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fff6e250bbc
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fff4889ec7c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fff0eb22b5c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fffdce51a0c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fff8c42db5c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fffce276c2c
function: 0x400506, library function: 0x4003e0, data: 0x600998, stack: 0x7fffedbb9ffc

```
 `$ gcc -fPIE -o aslr aslr.c; for i in $(seq 1 10); do ./aslr; done` 
```
function: 0x400516, library function: 0x7f1e55a3e150, data: 0x6009c0, stack: 0x7fff7ce9317c
function: 0x400516, library function: 0x7ffae3294150, data: 0x6009c0, stack: 0x7fff428a8e1c
function: 0x400516, library function: 0x7f39c4ed6150, data: 0x6009c0, stack: 0x7fffdb57db5c
function: 0x400516, library function: 0x7f8e4fccd150, data: 0x6009c0, stack: 0x7ffffd46bd3c
function: 0x400516, library function: 0x7f885508b150, data: 0x6009c0, stack: 0x7fffe7bf69cc
function: 0x400516, library function: 0x7ffa9a05f150, data: 0x6009c0, stack: 0x7ffff89fdfac
function: 0x400516, library function: 0x7ffe6114d150, data: 0x6009c0, stack: 0x7fff888accdc
function: 0x400516, library function: 0x7f30f1893150, data: 0x6009c0, stack: 0x7fff2cfcb6bc
function: 0x400516, library function: 0x7fd9e91dc150, data: 0x6009c0, stack: 0x7fff91c0062c
function: 0x400516, library function: 0x7fdf4c136150, data: 0x6009c0, stack: 0x7fff7f96928c

```
 `$ gcc -fPIE -pie -o aslr aslr.c; for i in $(seq 1 10); do ./aslr; done` 
```
function: 0x7f35659b4770, library function: 0x7f3565433150, data: 0x7f3565bb4c38, stack: 0x7ffff3de9a4c
function: 0x7f173ab2b770, library function: 0x7f173a5aa150, data: 0x7f173ad2bc38, stack: 0x7fffa0e7b12c
function: 0x7ff59b960770, library function: 0x7ff59b3df150, data: 0x7ff59bb60c38, stack: 0x7fffaca2f8cc
function: 0x7f557c39e770, library function: 0x7f557be1d150, data: 0x7f557c59ec38, stack: 0x7fff9127b98c
function: 0x7f1bc8f53770, library function: 0x7f1bc89d2150, data: 0x7f1bc9153c38, stack: 0x7fff75d767ac
function: 0x7f8af81e8770, library function: 0x7f8af7c67150, data: 0x7f8af83e8c38, stack: 0x7fff4bb7856c
function: 0x7f8be8334770, library function: 0x7f8be7db3150, data: 0x7f8be8534c38, stack: 0x7fffcf8b33cc
function: 0x7f3c246a5770, library function: 0x7f3c24124150, data: 0x7f3c248a5c38, stack: 0x7fffb25d8ccc
function: 0x7fa457c39770, library function: 0x7fa4576b8150, data: 0x7fa457e39c38, stack: 0x7fffc92d85fc
function: 0x7f1dffbb8770, library function: 0x7f1dff637150, data: 0x7f1dffdb8c38, stack: 0x7fffd2bfff2c
```

### hardening-wrapper

The [hardening-wrapper](https://www.archlinux.org/packages/?name=hardening-wrapper) package wraps C and C++ compilers in order to enable the chosen hardening flags by default for all builds. A wrapper (or patched toolchain) is a hard requirement for enabling PIE for all packages, because different flags need to be passed depending on whether an executable or library is being compiled. Enabling PIE by default on x86_64 should be pursued, and this is likely the best way to do it.

## non-root X

The [xorg-server](https://www.archlinux.org/packages/?name=xorg-server) package now ships with `/usr/bin/Xorg` as a wrapper script, calling the `/usr/bin/Xorg.wrap` setuid binary and dropping privileges if possible (video driver with [KMS](/index.php/KMS "KMS")). To decrease the attack surface, the setuid should be split into a separate package and added as a dependency to drivers without rootless X support. The script is already set up to fall back to `/usr/bin/Xorg.bin` if the wrapper is unavailable.

[FS#41257](https://bugs.archlinux.org/task/41257)

## grsecurity

See [grsecurity](/index.php/Grsecurity "Grsecurity") for most of the documentation. This section only covers ongoing packaging issues and the rationale behind certain choices.

### kernel

The kernel configuration will follow the [linux](https://www.archlinux.org/packages/?name=linux) package's kernel configuration to the extent possible. The grsecurity patch set occasionally lags a bit behind the standard kernel so there may be minor differences due to the version.

The default sysctl.d configuration file will not touch any flags outside of the kernel.grsecurity/kernel.pax namespaces. There should be no configuration changes creating an impact on the system when booting into a kernel without grsecurity/pax support.

*   [i686 configuration](https://projects.archlinux.org/svntogit/community.git/tree/trunk/config?h=packages/linux-grsec)
*   [x86_64 configuration](https://projects.archlinux.org/svntogit/community.git/tree/trunk/config.x86_64?h=packages/linux-grsec)

#### use upstream features when possible

Some grsecurity features have made their way upstream in one form or another. These can be preferred over the grsecurity-specific versions since backwards compatibility isn't a concern.

*   kernel.grsecurity.dmesg (CONFIG_GRKERNSEC_DMESG=y) -> kernel.dmesg_restrict (CONFIG_SECURITY_DMESG_RESTRICT=y)
*   kernel.grsecurity.linking_restrictions (CONFIG_GRKERNSEC_LINK=y) -> fs.protected_hardlinks, fs.protected_symlinks (set by /usr/lib/sysctl.d/50-default.conf from [systemd](https://www.archlinux.org/packages/?name=systemd))

#### Enable *privileged* user namespaces

The `CONFIG_USER_NS` configuration option is set, but grsecurity disallows unprivileged user namespaces so it doesn't introduce a security hole.

#### Enable KASLR and hide symbols

The vanilla kernel doesn't enable KASLR (yet), but there's no disadvantage to enabling it for [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec). It only randomizes the base address to one of 256 locations, so building a custom kernel for unique symbol addresses is still required for `CONFIG_GRKERNSEC_HIDESYM` to be a truly valuable exploit mitigation.

#### CONFIG_GRKERNSEC_PROC=n

The protection for /proc cannot be toggled dynamically and breaks too much out-of-the-box. It also doesn't mix well with containers because it's global rather than a setting for each process namespace. The upstream `hidepid` and `gid` mount options for /proc provide the core functionality with per-namespace granularity, but lack some of the auxiliary information hiding.

#### CONFIG_GRKERNSEC_SYSCTL_ON=n

This causes the flags to be disabled by default, as they will be enabled in a standard sysctl configuration instead. Otherwise, there is unavoidable audit spam in early boot (timechange, mount).

#### disable Yama

An equivalent to ptrace_scope is built-in to grsecurity, so there is no need for this.

### PaX

The kernel will only be compiled with supported for the extended attribute PaX flags. The ELF flags are not always a working solution, and it's much simpler if there is only one place to look for these. With only [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) installed, `kernel.pax.softmode = 1` is set to disable the userspace mitigations. Installing [paxd](https://www.archlinux.org/packages/?name=paxd) sets `kernel.pax.softmode = 0` and it automatically applies the common set of PaX exceptions whenever a Pacman transaction occurs.

## See also

*   [CVE-2014](/index.php/CVE-2014 "CVE-2014")