[PaX](https://en.wikipedia.org/wiki/PaX "wikipedia:PaX") is developed as a subset of the [grsecurity](/index.php/Grsecurity "Grsecurity") patches, and is included in the [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package in the official repositories. It is also available in the standalone [linux-pax](https://aur.archlinux.org/packages/linux-pax/) package in the [AUR](/index.php/AUR "AUR").

PaX contains most of the [grsecurity](/index.php/Grsecurity "Grsecurity") mitigations against memory corruption exploits. It hardens the kernel and userspace processes in many ways, including improved [address space layout randomization](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization"), strengthening the separation between kernel and userspace code / data and wiping out various classes of information leaks. The kernel hardening features have no user-facing impact, but the MPROTECT / RANDMMAP mitigations require making exceptions for some applications.

Using PaX alone is not recommended as the synergies with other grsecurity features are important. For example, defeating even the improved PaX ASLR is trivial without the [GRKERNSEC_PROC_MEMMAP feature](https://en.wikibooks.org/wiki/Grsecurity/Appendix/Grsecurity_and_PaX_Configuration_Options#Harden_ASLR_against_information_leaks_and_entropy_reduction) if the attacker has filesystem access.

## Contents

*   [1 Installation](#Installation)
*   [2 Performance](#Performance)
    *   [2.1 Tunable parameters](#Tunable_parameters)
    *   [2.2 Custom kernel](#Custom_kernel)
*   [3 PaX exceptions](#PaX_exceptions)
    *   [3.1 Using the paxd daemon](#Using_the_paxd_daemon)
        *   [3.1.1 User exceptions](#User_exceptions)
    *   [3.2 Manually](#Manually)
    *   [3.3 Soft mode](#Soft_mode)
*   [4 Testing the userspace features](#Testing_the_userspace_features)
*   [5 See also](#See_also)

## Installation

The Pax subset is installed with the [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package; however, it is set to soft mode by default, meaning it is opt-in rather than opt-out.

The recommended way to switch to opt-in is to [install](/index.php/Install "Install") the [paxd](https://www.archlinux.org/packages/?name=paxd) package.

**Note:** After installing [paxd](https://www.archlinux.org/packages/?name=paxd) the system must be rebooted to apply the changes. Alternatively apply the [sysctl](/index.php/Sysctl "Sysctl") configuration to the running system using `sysctl -p usr/lib/sysctl.d/10-enable-pax.conf`

It is also possible to temporarily disable soft mode:

```
# kernel.pax.softmode=0

```

Note that this will only work until the next reboot.

## Performance

### Tunable parameters

The `pax_sanitize_slab=0` option can be set on the kernel line to disable slab object sanitization. This will increase the risk of information leaks from the kernel, while reducing the performance hit from `CONFIG_PAX_MEMORY_SANITIZE` (~3% for a kernel compile by default).

The `pax_nouderef` option can be set on the kernel line to disable UDEREF. It is cheap on i686 since it takes advantage of memory segmentation but can cause serious performance issues with some virtualization environments. On x86_64, there are 3 implementations of UDEREF:

*   slow / weak legacy implementation (~10% slower kernel compile)
*   strong implementation on Sandy Bridge and later (default when supported, use `nopcid` to use the legacy implementation)
*   fast / weak implementation on Sandy Bridge and later (pass `pax_weakuderef` to use it)

### Custom kernel

Building a custom kernel allows full control over the compromise between performance and security. The pre-built [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package prioritizes security over performance. On i686, disabling `CONFIG_PAX_MEMORY_SANITIZE` and `CONFIG_PAX_MEMORY_STACKLEAK` will make the performance hit negligible. On x86_64, disabling those options along with `CONFIG_PAX_MEMORY_UDEREF` will do the same, although `pax_nouderef` also exists at runtime as documented above.

## PaX exceptions

Some of the PaX exploit mitigations prevent certain applications from running and require the executables to be marked with exceptions. The MPROTECT feature is by far the most common source of issues, and [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) defaults to [logging violations](/index.php/Grsecurity#Auditing "Grsecurity") to the kernel log. It is more difficult to identify these issues with PaX installed on a vanilla kernel.

Extended attributes can be used to exclude executables from one or more of the features. This can be done in multiple ways.

### Using the paxd daemon

The [paxd](https://www.archlinux.org/packages/?name=paxd) package provided in the official repositories includes a daemon that automatically applies PaX exceptions from `/etc/paxd.conf` whenever an executable is updated or the configuration file is modified. This is the officially supported way of applying these exceptions for binaries provided by packages. To start / enable the daemon:

```
# systemctl start paxd
# systemctl enable paxd

```

#### User exceptions

[paxd](https://www.archlinux.org/packages/?name=paxd) also provides a user service so that individual users can apply exceptions, primarily to files in their home directory. It can be started / enabled with `systemctl --user` and will apply exceptions from `$XDG_CONFIG_HOME/paxd.conf` (falling back to `~/.config/paxd.conf`).

### Manually

The setfattr command can be used to manually set exclusions for a problematic binary. For example, to disable the MPROTECT and RANDMMAP features:

```
$ setfattr -n user.pax.flags -v "emr" /usr/bin/problematic_binary

```

**Note:** The [linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec) package *only* supports the extended attributes, and does not include support for the ELF exception markers. The extended attributes do not require special tooling and leave the binaries unaltered, making them a far better option.

The [pax-utils](https://www.archlinux.org/packages/?name=pax-utils) package includes some useful tools. For example, the `pspax` utility can display PaX permissions from the kernel's perspective along with capabilities. The `scanelf` tool can be used to query attributes of binaries.

One might also use getfattr to retrieve extended attributes set above (or set by paxd described above) if they choose not to run pax-utils or if they want to check the attributes of a process not running:

```
$ getfattr -n user.pax.flags /usr/bin/problematic_binary

```

### Soft mode

Setting `kernel.pax.softmode=1` with [sysctl](/index.php/Sysctl "Sysctl") will result in the mitigations being opt-in rather than opt-out. This could be used to apply the mitigations only to certain high-risk binaries such as web services on a server without causing any issues. However, opting out of the mitigations results in a significantly more secure system and [paxd](https://www.archlinux.org/packages/?name=paxd) takes care of nearly all the work automatically.

## Testing the userspace features

The [paxtest](https://www.archlinux.org/packages/?name=paxtest) tool can be used to test the userspace exploit mitigation features. Note that the UDEREF self-protection feature shrinks the address space on x86_64, reducing the entropy available for randomization. It's an extremely important feature and outweighs the minimal gain from the additional entropy.

 `Vanilla kernel (x86_64)` 
```
Executable anonymous mapping             : Killed
Executable bss                           : Killed
Executable data                          : Killed
Executable heap                          : Killed
Executable stack                         : Killed
Executable shared library bss            : Killed
Executable shared library data           : Killed
Executable anonymous mapping (mprotect)  : Vulnerable
Executable bss (mprotect)                : Vulnerable
Executable data (mprotect)               : Vulnerable
Executable heap (mprotect)               : Vulnerable
Executable stack (mprotect)              : Vulnerable
Executable shared library bss (mprotect) : Vulnerable
Executable shared library data (mprotect): Vulnerable
Writable text segments                   : Vulnerable
Anonymous mapping randomisation test     : 28 quality bits (guessed)
Heap randomisation test (ET_EXEC)        : 13 quality bits (guessed)
Heap randomisation test (PIE)            : 28 quality bits (guessed)
Main executable randomisation (ET_EXEC)  : 28 quality bits (guessed)
Main executable randomisation (PIE)      : 28 quality bits (guessed)
Shared library randomisation test        : 28 quality bits (guessed)
VDSO randomisation test                  : 20 quality bits (guessed)
Stack randomisation test (SEGMEXEC)      : 30 quality bits (guessed)
Stack randomisation test (PAGEEXEC)      : 30 quality bits (guessed)
Arg/env randomisation test (SEGMEXEC)    : 22 quality bits (guessed)
Arg/env randomisation test (PAGEEXEC)    : 22 quality bits (guessed)
Randomization under memory exhaustion @~0: 28 bits (guessed)
Randomization under memory exhaustion @0 : 28 bits (guessed)
Return to function (strcpy)              : paxtest: return address contains a NULL byte.
Return to function (memcpy)              : Killed
Return to function (strcpy, PIE)         : paxtest: return address contains a NULL byte.
Return to function (memcpy, PIE)         : Killed

```
 `PaX kernel (x86_64 without UDEREF)` 
```
Executable anonymous mapping             : Killed
Executable bss                           : Killed
Executable data                          : Killed
Executable heap                          : Killed
Executable stack                         : Killed
Executable shared library bss            : Killed
Executable shared library data           : Killed
Executable anonymous mapping (mprotect)  : Killed
Executable bss (mprotect)                : Killed
Executable data (mprotect)               : Killed
Executable heap (mprotect)               : Killed
Executable stack (mprotect)              : Killed
Executable shared library bss (mprotect) : Killed
Executable shared library data (mprotect): Killed
Writable text segments                   : Killed
Anonymous mapping randomisation test     : 33 quality bits (guessed)
Heap randomisation test (ET_EXEC)        : 22 quality bits (guessed)
Heap randomisation test (PIE)            : 40 quality bits (guessed)
Main executable randomisation (ET_EXEC)  : 33 quality bits (guessed)
Main executable randomisation (PIE)      : 33 quality bits (guessed)
Shared library randomisation test        : 33 quality bits (guessed)
VDSO randomisation test                  : 33 quality bits (guessed)
Stack randomisation test (SEGMEXEC)      : 40 quality bits (guessed)
Stack randomisation test (PAGEEXEC)      : 40 quality bits (guessed)
Arg/env randomisation test (SEGMEXEC)    : 44 quality bits (guessed)
Arg/env randomisation test (PAGEEXEC)    : 44 quality bits (guessed)
Randomization under memory exhaustion @~0: 33 bits (guessed)
Randomization under memory exhaustion @0 : 33 bits (guessed)
Return to function (strcpy)              : paxtest: return address contains a NULL byte.
Return to function (memcpy)              : Killed
Return to function (strcpy, PIE)         : paxtest: return address contains a NULL byte.
Return to function (memcpy, PIE)         : Killed

```
 `PaX kernel (x86_64 with UDEREF)` 
```
Executable anonymous mapping             : Killed
Executable bss                           : Killed
Executable data                          : Killed
Executable heap                          : Killed
Executable stack                         : Killed
Executable shared library bss            : Killed
Executable shared library data           : Killed
Executable anonymous mapping (mprotect)  : Killed
Executable bss (mprotect)                : Killed
Executable data (mprotect)               : Killed
Executable heap (mprotect)               : Killed
Executable stack (mprotect)              : Killed
Executable shared library bss (mprotect) : Killed
Executable shared library data (mprotect): Killed
Writable text segments                   : Killed
Anonymous mapping randomisation test     : 29 quality bits (guessed)
Heap randomisation test (ET_EXEC)        : 22 quality bits (guessed)
Heap randomisation test (PIE)            : 35 quality bits (guessed)
Main executable randomisation (ET_EXEC)  : 29 quality bits (guessed)
Main executable randomisation (PIE)      : 29 quality bits (guessed)
Shared library randomisation test        : 29 quality bits (guessed)
VDSO randomisation test                  : 29 quality bits (guessed)
Stack randomisation test (SEGMEXEC)      : 35 quality bits (guessed)
Stack randomisation test (PAGEEXEC)      : 35 quality bits (guessed)
Arg/env randomisation test (SEGMEXEC)    : 39 quality bits (guessed)
Arg/env randomisation test (PAGEEXEC)    : 39 quality bits (guessed)
Randomization under memory exhaustion @~0: 29 bits (guessed)
Randomization under memory exhaustion @0 : 29 bits (guessed)
Return to function (strcpy)              : paxtest: return address contains a NULL byte.
Return to function (memcpy)              : Killed
Return to function (strcpy, PIE)         : paxtest: return address contains a NULL byte.
Return to function (memcpy, PIE)         : Killed

```

## See also

*   [PaX documentation](https://pax.grsecurity.net/docs/)