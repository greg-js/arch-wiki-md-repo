This page describes security packaging guidelines for Arch Linux packages. For C/C++ projects the compiler and linker can apply security hardening options. Arch Linux by default applies PIE, Fortify source, stack protector, nx and relro. Hardening protections can be reviewed by running [checksec](https://www.archlinux.org/packages/?name=checksec).

```
$ checksec --file=/usr/bin/cat

```

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 RELRO](#RELRO)
    *   [1.1 Haskell](#Haskell)
*   [2 Stack canary](#Stack_canary)
*   [3 NX](#NX)
    *   [3.1 C/C++](#C/C++)
*   [4 PIE](#PIE)
    *   [4.1 C/C++](#C/C++_2)
    *   [4.2 Golang](#Golang)
    *   [4.3 Haskell](#Haskell_2)
*   [5 RPATH/RUNPATH](#RPATH/RUNPATH)
*   [6 FORTIFY](#FORTIFY)
*   [7 Systemd services](#Systemd_services)
    *   [7.1 File access](#File_access)
    *   [7.2 User](#User)
    *   [7.3 Memory](#Memory)
    *   [7.4 System calls](#System_calls)
    *   [7.5 Network](#Network)
    *   [7.6 Various](#Various)

## RELRO

RELRO is a generic mitigation technique to harden the data sections of an ELF binary/process. When a program is loaded several ELF memory sections need to be written to by the linker. but can be turned read-only before turning control over to the program. This prevents attackers of overriding some ELF sections. There are two different RELRO modes:

*   Partial RELRO (`-Wl,-z,relro`) some sections are marked as read-only after program load except the GOT (.got.plt) is still writeable.

*   Full RELRO (`-Wl,-z,now`) during program load all dynamic symbols are resolved, allowing for the complete GOT to be marked read-only.

If an application reports partial relro, investigate if the build toolchain passes our LDFLAGS or allows overriding LDFLAGS. For Go packages investigate if the build method uses "build.go" as pure golang Makefile replacement which does not allow passing of LDFLAGS.

### Haskell

For Haskell it's not clear how to achieve Full RELRO at the moment.

## Stack canary

A [stack canary](https://en.wikipedia.org/wiki/Stack_canary "wikipedia:Stack canary") is added by the compiler between the buffer and control data on the stack. If this well known value is corrupted, a buffer overflow occurred and the running program segfaults to prevent possible arbitrary code execution.

The [gcc](https://www.archlinux.org/packages/?name=gcc) package has it enabled stack protection by default with the [--enable-default-ssp](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gcc#n120) compile option.

## NX

### C/C++

Executable-space protection marks memory regions as non-executable, such that an attempt to execute machine code in these regions will cause an exception. It makes use of hardware features such as the NX bit (no-execute bit), or in some cases software emulation of those features.

## PIE

### C/C++

The [gcc](https://www.archlinux.org/packages/?name=gcc) package has it enabled by default for C/C++ with [--enable-default-pie](https://git.archlinux.org/svntogit/packages.git/tree/trunk/PKGBUILD?h=packages/gcc#n119).

### Golang

For Go packages add a [makedepend](/index.php/PKGBUILD#makedepends "PKGBUILD") on [go-pie](https://www.archlinux.org/packages/?name=go-pie).

### Haskell

Pass the following flag to *runhaskell* Setup configure

```
--ghc-option='-pie'

```

## RPATH/RUNPATH

RUNPATH/RPATH provides further search paths for the object it is listed in (it can be used both for executable and for shared objects).

```
$ objdump -x /usr/bin/perl | egrep 'RPATH|RUNPATH'

```

If the RPATH value contains a path within an attackers control it can possibly execute code by installing a malicious library in that directory for example [CVE-2006-1566](https://nvd.nist.gov/vuln/detail/CVE-2006-1566) [CVE-2005-4280](https://www.cvedetails.com/cve/CVE-2005-4280/).

The RPATH entry is set by the linker by passing for example the following string to LDFLAGS `-Wl,-rpath -Wl,/usr/local/lib`. To make an RUNPATH entry append `--enable-new-dtags` to the linker flags.

## FORTIFY

Fortify source is a macro that adds buffer overflow protection in various functions that perform operations on memory and strings. It checks whether an attacker tries to copy more bytes to overflow a buffer and then stops the execution of the program. This protection is enabled with the default CPPFLAGS in `makepkg.conf`:

```
CPPFLAGS="-D_FORTIFY_SOURCE=2"

```

## Systemd services

If a systemd service file is shipped with the package due to upstream not providing any, look into applying the following systemd service hardening features. Systemd provides a way to analyse security features which are enabled for a service.

```
$ systemd-analyze security pacman.service

```

### File access

A service can be hardened by restricting file system access.

Set up a new file system namespace for the executed process and mounts private `/tmp` and var/tmp directories inside it that is not shared by processes outside the namespace. Useful for programs which write data to `/tmp`.

```
PrivateTmp=true

```

ProtectSystem has three different varieties of mounting directories as read-only for the executed process. The "full" option mounts `/usr`, `/boot` and `/etc` read only. ProtectHome makes `/home`, `/root` and `/run/user` inaccessible to the executed process.

```
ProtectSystem=strict
ProtectHome=true

```

Sets up a new `/dev` namespace for the executed process and only adds API pseudo devices such as `/dev/null`, `/dev/zero` or `/dev/random`, but not for physical devices or system memory, system ports and others. This is useful to secure the execute process from writing directly to physical devices, systemd also adds a system call filter for calls within the `@raw-io` set.

```
PrivateDevices=true

```

These options make the executed process unable to change kernel variables accessible through `/proc/sys`, `/sys`, etc. ProtectControlGroups makes the `/sys/fs/cgroup` hierarchy read-only.

```
ProtectKernelTunables=true
ProtectControlGroups=true

```

More detailed information can be found in [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5).

### User

Ensure that the executed process and it's children can never gain new privileges through `execve()`.

```
NoNewPrivileges=true

```

### Memory

Prohibit attempts to create memory mappings that are both writable and executable, to change mappings to be executable or to crate executable shared memory. This sandboxes a process against allowing an attacker to write in to memory which is also executed. Note that enabling this is not compatible with all applications which rely on a JIT.

```
MemoryDenyWriteExecute=true

```

### System calls

Locks down the [personality(2)](https://jlk.fjfi.cvut.cz/arch/manpages/man/personality.2) system call so that the kernel execution domain can not be changed.

```
LockPersonality=true

```

System calls can be restricted in a service as well, systemd can display syscalls to filter on:

```
$ systemd-analyze syscall-filter

```

Restricting swap syscall can be done as following:

```
SystemCallFilter=@swap

```

### Network

If the running process does not require any network access it can be fully disabled by setting up a new network namespace for the process and only configuration a loopback interface.

```
PrivateNetwork=true

```

If network is required, the type of address families used can be restricted for the [socket(2)](https://jlk.fjfi.cvut.cz/arch/manpages/man/socket.2) system call by for example only allowing UNIX sockets.

```
RestrictAddressFamilies=AF_UNIX

```

For when only network to localhost or specific IP ranges is required a process can be restricted by only allowing network access to localhost.

```
IPAddressAllow=localhost
IPAddressDeny=any

```

More information about network filtering can be found in [systemd.resource-control(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.resource-control.5).

### Various

Sets up a new UTS namespace for the execute process and disallows changing the hostname or domainname.

```
ProtectHostname=true

```