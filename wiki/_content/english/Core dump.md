A [core dump](https://en.wikipedia.org/wiki/Core_dump "wikipedia:Core dump") is a file containing a process's address space (memory) when the process terminates unexpectedly. Core dumps may be produced on-demand (such as by a [debugger](#Making_a_core_dump)), or automatically upon termination. Core dumps are triggered by the kernel in response to program crashes, and may be passed to a helper program (such as [systemd-coredump](http://www.freedesktop.org/software/systemd/man/systemd-coredump.html)) for further processing. A core dump is not typically used by an average user, but may be passed on to developers upon request where it can be invaluable as a post-mortem snapshot of the program's state at the time of the crash, especially if the fault is hard to reliably reproduce.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Disabling automatic core dumps](#Disabling_automatic_core_dumps)
    *   [1.1 Using sysctl](#Using_sysctl)
    *   [1.2 Using ulimit](#Using_ulimit)
    *   [1.3 Using systemd](#Using_systemd)
*   [2 Making a core dump](#Making_a_core_dump)
    *   [2.1 Where do they go?](#Where_do_they_go?)
*   [3 Examining a core dump](#Examining_a_core_dump)
*   [4 Cleanup of core dump files](#Cleanup_of_core_dump_files)
*   [5 See also](#See_also)

## Disabling automatic core dumps

Users may wish to disable automatic core dumps for a number of reasons:

*   Performance: generating core dumps for memory-heavy processes can waste system resources and delay the cleanup of memory.
*   Disk space: core dumps of memory-heavy processes may consume disk space equal to, if not greater, than the process's memory footprint if not compressed.
*   Security: core dumps, although typically readable only by root, may contain sensitive data (such as passwords or cryptographic keys), which are written to disk following a crash.

### Using sysctl

[sysctl](/index.php/Sysctl "Sysctl") can be used to set the `kernel.core_pattern` to nothing to disable core dump handling. Create this file[[1]](https://github.com/systemd/systemd/issues/659#issuecomment-328372788):

 `/etc/sysctl.d/50-coredump.conf`  `kernel.core_pattern=|/bin/false` 

To apply the setting immediately, use `sysctl`:

```
# sysctl -p /etc/sysctl.d/50-coredump.conf

```

### Using ulimit

The maximum core dump size for users logged in via [PAM](/index.php/PAM "PAM") is enforced by [limits.conf](/index.php/Limits.conf "Limits.conf"). Setting it to zero disables core dumps entirely. [[2]](http://www.cyberciti.biz/faq/linux-disable-core-dumps/)

 `/etc/security/limits.conf`  `* hard core 0` 

ulimit sometimes referred to as obsolete [ulimit(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ulimit.3). The shell usually also have a builtin `ulimit` command.

### Using systemd

[systemd](/index.php/Systemd "Systemd")'s default behavior is to generate core dumps for all processes in `/var/lib/systemd/coredump`. This behavior can be overridden by creating a configuration snippet in the `/etc/systemd/coredump.conf.d/` directory with the following content[[3]](http://www.freedesktop.org/software/systemd/man/coredump.conf.html#Description)[[4]](https://bbs.archlinux.org/viewtopic.php?id=214207):

 `/etc/systemd/coredump.conf.d/custom.conf` 
```
[Coredump]
Storage=none
```

**Note:** Don't forget to include the `[Coredump]` section name, otherwise this option will be ignored: `systemd-coredump[1728]: [/etc/systemd/coredump.conf.d/custom.conf:1] Assignment outside of section. Ignoring.`

Then reload systemd's configuration.

```
# systemctl daemon-reload

```

This method alone is usually sufficient to disable userspace core dumps, so long as no other programs enable automatic core dumps on the system, but the coredump is still generated in memory and systemd-coredump run.

## Making a core dump

To generate a core dump of an arbitrary process, first [install](/index.php/Install "Install") the [gdb](https://www.archlinux.org/packages/?name=gdb) package. Then find the PID of the running process, for example with *pgrep*:

 `$ pgrep -f *firefox*`  `2071 firefox` 

Attach to the process:

```
$ gdb -p 2071

```

Then at the `(gdb)` prompt:

```
(gdb) generate-core-file
Saved corefile core.2071
(gdb) quit

```

Now you have a coredump file called `core.2071`.

### Where do they go?

The `kernel.core_pattern` [sysctl](/index.php/Sysctl "Sysctl") decides where automatic core dumps go. By default, core dumps are sent to *systemd-coredump* which can be configured in `/etc/systemd/coredump.conf`. By default, all core dumps are stored in `/var/lib/systemd/coredump` (due to `Storage=external`) and they are compressed with `lz4` (due to `Compress=yes`). Additionally, various size limits for the storage can be configured.

**Note:** The default value for `kernel.core_pattern` is set in `/usr/lib/sysctl.d/50-coredump.conf`. This file may be masked or overridden to use a different setting following normal [sysctl.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysctl.d.5) rules.

To retrieve a core dump from the journal, see [coredumpctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/coredumpctl.1).

## Examining a core dump

Use *coredumpctl* to find the corresponding dump:

```
# coredumpctl list

```

You need to uniquely identify the relevant dump. This is possible by specifying a `PID`, name of the executable, path to the executable or a journalctl predicate (see [coredumpctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/coredumpctl.1) and [journalctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/journalctl.1) for details). To see details of the core dumps:

```
# coredumpctl info *match*

```

Pay attention to "Signal" row, that helps to identify crash cause. For deeper analysis you can examine the backtrace using *gdb*:

```
# coredumpctl gdb *match*

```

When *gdb* is started, use the `bt` command to print the backtrace:

```
(gdb) bt

```

See [Debug - Getting Traces](/index.php/Debug_-_Getting_Traces "Debug - Getting Traces") if debugging symbols are requested, but not found.

## Cleanup of core dump files

The core dump files stored in `/var/lib/systemd/coredump/` will be automatically cleaned by `systemd-tmpfiles --clean`, which is triggered daily with `systemd-tmpfiles-clean.timer`. Core dumps are configured to persist for at least 3 days, see `systemd-tmpfiles --cat-config`.

## See also

*   [american fuzzy lop](http://lcamtuf.coredump.cx/afl/) - A tool for automated tests of the kernel and programs
*   [Filesystem fuzzing](https://lwn.net/Articles/637151/) - LWN article about testing filesystems for bugs