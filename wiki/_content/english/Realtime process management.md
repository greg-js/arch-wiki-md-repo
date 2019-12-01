Related articles

*   [cgroups](/index.php/Cgroups "Cgroups")
*   [Performance](/index.php/Performance "Performance")

This article provides information on prioritizing process threads in real time, as opposed to at startup only. It shows how you can control CPU, memory, and other resource utilization of individual processes, or all processes run by a particular group.

While many recent processors are powerful enough to play a dozen video or audio streams simultaneously, it is still possible that another thread hijacks the processor for half a second to complete another task. This results in short interrupts in audio or video streams. It is also possible that video/audio streams get out of sync. While this is annoying for a casual music listener; for a content producer, composer or video editor this issue is much more serious as it interrupts their workflow.

The simple solution is to give the audio and video processes a **higher priority**. However, while normal users can set a higher *nice* value to a process, which means that its priority is lower, only root can set lower values and start processes at a lower *nice* value than 0\. This protects the normal user from underpowering processes which are essential to the system. This can be especially important on multi-user machines.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Configuration](#Configuration)
    *   [1.1 Configuring PAM](#Configuring_PAM)
    *   [1.2 Configuring systemd services](#Configuring_systemd_services)
*   [2 Hard and soft realtime](#Hard_and_soft_realtime)
*   [3 Power is nothing without control](#Power_is_nothing_without_control)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 PAM-enabled login](#PAM-enabled_login)
    *   [4.2 Console/autologin](#Console/autologin)
*   [5 Reference](#Reference)
    *   [5.1 RLIMIT Definitions](#RLIMIT_Definitions)
    *   [5.2 Scheduling policies](#Scheduling_policies)
    *   [5.3 Scheduling classes](#Scheduling_classes)
*   [6 See also](#See_also)

## Configuration

By default, real-time prioritizing is enabled on Arch. System, group and user wide configuration can be achieved using [PAM](/index.php/PAM "PAM") and [systemd](/index.php/Systemd "Systemd").

The [realtime](https://www.archlinux.org/groups/x86_64/realtime/) package group provides additional tools to modify the realtime scheduling policies of [IRQs](https://en.wikipedia.org/wiki/Interrupt_request_(PC_architecture) and processes.

**Note:** When running a custom kernel, ensure it is `PREEMPT` enabled to make use of the methods mentioned above.

### Configuring PAM

The `/etc/security/limits.conf` file provides configuration for the `pam_limits` PAM module, which sets limits on system resources (see [limits.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/limits.conf.5)).

**Tip:** It is advised to externalize the configuration of `pam_limits` to separate files below `/etc/security/limits.d` as those take precedence over the main configuration file.

There are two types of resource limits that `pam_limits` provides: **hard limits** and **soft limits**. Hard limits are set by `root` and enforced by the kernel, while soft limits may be configured by the user within the range allowed by the hard limits.

Installing the package [realtime-privileges](https://www.archlinux.org/packages/?name=realtime-privileges) and adding the user to the `realtime` group, provides reasonable default values (e.g. relevant for [Professional audio](/index.php/Professional_audio "Professional audio")).

### Configuring systemd services

Processes spawned by systemd system services need to specifically setup equivalents to `limits.conf`. Further information can be found in the sections `CREDENTIALS` and `PROCESS PROPERTIES` in [systemd.exec(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.exec.5).

## Hard and soft realtime

Realtime is a synonym for a process which has the capability to run in time without being interrupted by any other process. However, cycles can occasionally be dropped despite this. Low power supply or a process with higher priority could be a potential cause. To solve this problem, there is a scaling of realtime quality. This article deals with **soft** realtime. Hard realtime is usually not so much desired as it is *needed*. An example could be made for car's ABS (anti-lock braking system). This can not be "rendered" and there is no second chance.

## Power is nothing without control

The realtime-lsm module granted the right to get higher capabilities to users belonging to a certain UID. The rlimit way works similar, but it can be controlled graduated finer. There is a new functionality in PAM which can be used to control the capabilities on a per user or a per group level. In the current version (0.80-2) these values are not set correctly out of the box and still create problems. With PAM you can grant realtime priority to a certain user or to a certain user group. PAM's concept makes it imaginable that there will be ways in the future to grant rights on a per application level; however, this is not yet possible.

## Tips and tricks

### PAM-enabled login

See [Start X at login](/index.php/Start_X_at_login "Start X at login").

For your system to use PAM limits settings you have to use a `pam`-enabled login method/manager. Nearly all graphical login managers are pam-enabled, and it now appears that the default Arch login is `pam`-enabled as well. You can confirm this by searching `/etc/pam.d`:

```
$ grep pam_limits.so /etc/pam.d/*

```

If you get nothing, you are whacked. But you will, as long as you have a login manager (and now [PolicyKit](/index.php/PolicyKit "PolicyKit")). We want an output like this one:

```
/etc/pam.d/crond:session   required    pam_limits.so
/etc/pam.d/login:session		required	pam_limits.so
/etc/pam.d/polkit-1:session         required        pam_limits.so
/etc/pam.d/system-auth:session   required  pam_limits.so
/etc/pam.d/system-services:session   required    pam_limits.so

```

So we see that `login`, PolicyKit, and the others all require the pam_limits.so module. This is a good thing, and means PAM limits will be enforced.

### Console/autologin

See: [Automatically login some user to a virtual console on startup](/index.php/Automatically_login_some_user_to_a_virtual_console_on_startup "Automatically login some user to a virtual console on startup")

If you prefer to not have a graphical login, you still have a way. You need to edit the `pam` stuff for `su` (from [coreutils](https://www.archlinux.org/packages/?name=coreutils)):

 `/etc/pam.d/su` 
```
 ...
 session              required        pam_limits.so

```

Source [[1]](https://bbs.archlinux.org/viewtopic.php?pid=387214).

## Reference

### RLIMIT Definitions

	RLIMIT_AS

	The maximum size of the process’s virtual memory (address space) in bytes. This limit affects calls to brk(2), mmap(2) and mremap(2), which fail with the error ENOMEM upon exceeding this limit. Also automatic stack expansion will fail (and generate a SIGSEGV that kills the process if no alternate stack has been made available via sigaltstack(2)). Since the value is a long, on machines with a 32-bit long either this limit is at most 2 GiB, or this resource is unlimited.

	RLIMIT_CORE

	Maximum size of core file. When 0 no core dump files are created. When non-zero, larger dumps are truncated to this size.

	RLIMIT_CPU

	CPU time limit in seconds. When the process reaches the soft limit, it is sent a SIGXCPU signal. The default action for this signal is to terminate the process. However, the signal can be caught, and the handler can return control to the main program. If the process continues to consume CPU time, it will be sent SIGXCPU once per second until the hard limit is reached, at which time it is sent SIGKILL. (This latter point describes Linux 2.2 through 2.6 behavior. Implementations vary in how they treat processes which continue to consume CPU time after reaching the soft limit. Portable applications that need to catch this signal should perform an orderly termination upon first receipt of SIGXCPU.)

	RLIMIT_DATA

	The maximum size of the process’s data segment (initialized data, uninitialized data, and heap). This limit affects calls to brk(2) and sbrk(2), which fail with the error ENOMEM upon encountering the soft limit of this resource.

	RLIMIT_FSIZE

	The maximum size of files that the process may create. Attempts to extend a file beyond this limit result in delivery of a SIGXFSZ signal. By default, this signal terminates a process, but a process can catch this signal instead, in which case the relevant system call (e.g., write(2), truncate(2)) fails with the error EFBIG.

	RLIMIT_LOCKS

	(Early Linux 2.4 only) A limit on the combined number of flock(2) locks and fcntl(2) leases that this process may establish.

	RLIMIT_MEMLOCK

	The maximum number of bytes of memory that may be locked into RAM. In effect this limit is rounded down to the nearest multiple of the system page size. This limit affects mlock(2) and mlockall(2) and the mmap(2) MAP_LOCKED operation. Since Linux 2.6.9 it also affects the shmctl(2) SHM_LOCK operation, where it sets a maximum on the total bytes in shared memory segments (see shmget(2)) that may be locked by the real user ID of the calling process. The shmctl(2) SHM_LOCK locks are accounted for separately from the per-process memory locks established by mlock(2), mlockall(2), and mmap(2) MAP_LOCKED; a process can lock bytes up to this limit in each of these two categories. In Linux kernels before 2.6.9, this limit controlled the amount of memory that could be locked by a privileged process. Since Linux 2.6.9, no limits are placed on the amount of memory that a privileged process may lock, and this limit instead governs the amount of memory that an unprivileged process may lock.

	RLIMIT_MSGQUEUE

	(Since Linux 2.6.8) Specifies the limit on the number of bytes that can be allocated for POSIX message queues for the real user ID of the calling process. This limit is enforced for mq_open(3). Each message queue that the user creates counts (until it is removed) against this limit according to the formula: bytes = attr.mq_maxmsg * sizeof(struct msg_msg *) + attr.mq_maxmsg * attr.mq_msgsize where attr is the mq_attr structure specified as the fourth argument to mq_open(3). The first addend in the formula, which includes sizeof(struct msg_msg *) (4 bytes on Linux/i386), ensures that the user cannot create an unlimited number of zero-length messages (such messages nevertheless each consume some system memory for bookkeeping overhead).

	RLIMIT_NICE

	(since Linux 2.6.12, but see BUGS below) Specifies a ceiling to which the process’s nice value can be raised using setpriority(2) or nice(2). The actual ceiling for the nice value is calculated as 20 – rlim_cur. (This strangeness occurs because negative numbers cannot be specified as resource limit values, since they typically have special meanings. For example, RLIM_INFINITY typically is the same as -1.)

	RLIMIT_NOFILE

	Specifies a value one greater than the maximum file descriptor number that can be opened by this process. Attempts (open(2), pipe(2), dup(2), etc.) to exceed this limit yield the error EMFILE. (Historically, this limit was named RLIMIT_OFILE on BSD.)

	RLIMIT_NPROC

	The maximum number of processes (or, more precisely on Linux, threads) that can be created for the real user ID of the calling process. Upon encountering this limit, fork(2) fails with the error EAGAIN.

	RLIMIT_RSS

	Specifies the limit (in pages) of the process’s resident set (the number of virtual pages resident in RAM). This limit only has effect in Linux 2.4.x, x < 30, and there only affects calls to madvise(2) specifying MADV_WILLNEED.

	RLIMIT_RTPRIO

	(Since Linux 2.6.12, but see BUGS) Specifies a ceiling on the real-time priority that may be set for this process using sched_setscheduler(2) and sched_setparam(2).

	RLIMIT_RTTIME

	(Since Linux 2.6.25) Specifies a limit on the amount of CPU time that a process scheduled under a real-time scheduling policy may consume without making a blocking system call. For the purpose of this limit, each time a process makes a blocking system call, the count of its consumed CPU time is reset to zero. The CPU time count is not reset if the process continues trying to use the CPU but is preempted, its time slice expires, or it calls sched_yield(2). Upon reaching the soft limit, the process is sent a SIGXCPU signal. If the process catches or ignores this signal and continues consuming CPU time, then SIGXCPU will be generated once each second until the hard limit is reached, at which point the process is sent a SIGKILL signal. The intended use of this limit is to stop a runaway real-time process from locking up the system.

	RLIMIT_SIGPENDING

	(Since Linux 2.6.8) Specifies the limit on the number of signals that may be queued for the real user ID of the calling process. Both standard and real-time signals are counted for the purpose of checking this limit. However, the limit is only enforced for sigqueue(2); it is always possible to use kill(2) to queue one instance of any of the signals that are not already queued to the process.

	RLIMIT_STACK

	The maximum size of the process stack, in bytes. Upon reaching this limit, a SIGSEGV signal is generated. To handle this signal, a process must employ an alternate signal stack (sigaltstack(2)).

### Scheduling policies

CFS implements three scheduling policies:

	SCHED_NORMAL (traditionally called SCHED_OTHER)

	The scheduling policy that is used for regular tasks.

	SCHED_BATCH

	Does not preempt nearly as often as regular tasks would, thereby allowing tasks to run longer and make better use of caches but at the cost of interactivity. This is well suited for batch jobs.

	SCHED_IDLE

	This is even weaker than nice 19, but its not a true idle timer scheduler in order to avoid to get into priority inversion problems which would deadlock the machine.

### Scheduling classes

	IOPRIO_CLASS_RT

	This is the realtime io class. The RT scheduling class is given first access to the disk, regardless of what else is going on in the system. Thus the RT class needs to be used with some care, as it can starve other processes. As with the best effort class, 8 priority levels are defined denoting how big a time slice a given process will receive on each scheduling window. This scheduling class is given higher priority than any other in the system, processes from this class are given first access to the disk every time. Thus it needs to be used with some care, one io RT process can starve the entire system. Within the RT class, there are 8 levels of class data that determine exactly how much time this process needs the disk for on each service. In the future this might change to be more directly mappable to performance, by passing in a wanted data rate instead.

	IOPRIO_CLASS_BE

	This is the best-effort scheduling class, which is the default for any process that hasn’t set a specific io priority. This is the default scheduling class for any process that hasn’t asked for a specific io priority. Programs inherit the CPU nice setting for io priorities. This class takes a priority argument from 0-7, with lower number being higher priority. Programs running at the same best effort priority are served in a round-robin fashion. The class data determines how much io bandwidth the process will get, it’s directly mappable to the cpu nice levels just more coarsely implemented. 0 is the highest BE prio level, 7 is the lowest. The mapping between cpu nice level and io nice level is determined as: io_nice = (cpu_nice + 20) / 5.

	IOPRIO_CLASS_IDLE

	This is the idle scheduling class, processes running at this level only get io time when no one else needs the disk. A program running with idle io priority will only get disk time when no other program has asked for disk io for a defined grace period. The impact of idle io processes on normal system activity should be zero. This scheduling class does not take a priority argument. The idle class has no class data, since it doesn’t really apply here.

## See also

*   [IO Benchmarking: How, why and with what](http://cuddletech.com/?p=330)
*   [SYSSTAT utilities home page](http://sebastien.godard.pagesperso-orange.fr/)
*   [Multitasking from the Linux command line and process prioritization](http://gaarai.com/2009/03/06/multitasking-from-the-linux-command-line-plus-process-prioritization/)