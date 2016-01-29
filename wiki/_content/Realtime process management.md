# Realtime process management

This article provides information on prioritizing process threads in real time, as opposed to at startup only. It shows how you can control CPU, memory, and other resource utilization of individual processes, or all processes run by a particular group.

While many recent processors are powerful enough to play a dozen video or audio streams simultaneously, it is still possible that another thread hijacks the processor for half a second to complete another task. This results in short interrupts in audio or video streams. It is also possible that video/audio streams get out of sync. While this is annoying for a casual music listener; for a content producer, composer or video editor this issue is much more serious as it interrupts their workflow.

The simple solution is to give the audio and video processes a **higher priority**. However, while normal users can set a higher _nice_ value to a process, which means that its priority is lower, only root can set lower values and start processes at a lower _nice_ value than 0\. This protects the normal user from underpowering processes which are essential to the system. This can be especially important on multi-user machines.

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 pam](#pam)
    *   [1.2 Configuring PAM](#Configuring_PAM)
*   [2 Hard and soft realtime](#Hard_and_soft_realtime)
*   [3 Power is nothing without control](#Power_is_nothing_without_control)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 PAM-enabled login](#PAM-enabled_login)
    *   [4.2 Console/autologin](#Console.2Fautologin)
*   [5 Reference](#Reference)
    *   [5.1 RLIMIT Definitions](#RLIMIT_Definitions)
    *   [5.2 Scheduling policies](#Scheduling_policies)
    *   [5.3 Scheduling classes](#Scheduling_classes)
*   [6 See also](#See_also)

## Configuration

By default, real-time prioritizing is enabled on Arch, however its configuration is simplistic and open to editing by the user. For example, in order to allow users to set nice priorities below 0, we need to tweak the default hard limit provided by PAM.

### pam

The [pam](https://www.archlinux.org/packages/?name=pam) package from the official repositories provides the _pluggable authentication modules_ for the linux kernel.

**Note:** If you are running a custom kernel, ensure you have enabled "preemptible kernel" settings. The stock Arch kernel needs no modifications.

### Configuring PAM

The `/etc/security/limits.conf` file provides configuration for the `pam_limits` PAM module, which sets limits on system resources. It lets you do things like define the default nice level for all processes, individual groups, the maximum locked-in memory address space, and more.

**Note:** Processes initiated by Systemd service ignore limits.conf. You need to set in the .service files, for more info, man systemd.exec.

There are two types of resource limits that `pam_limits` provides: **hard limits** and **soft limits**. Hard limits are set by `root` and enforced by the kernel, while soft limits may be configured by the user within the range allowed by the hard limits. By default, Arch uses the `-` limit, which refers to both hard and soft limits.

The default Arch Linux settings set the maximum real-time priority allowed for non-priveleged processes to 0, the maximum nice priority allowed to raise to 0, and some custom settings for the `audio` group. Finally, the `memlock` item sets the maximum locked-in memory address space to 40,000 KiB. These defaults are shown below:

```
*               -       rtprio          0
*               -       nice            0
@audio          -       rtprio          65
@audio          -       nice           -10
@audio          -       memlock         40000

```

An example for why one might want to alter these settings is to get high-performance audio working. The defaults are permissive enough to get `jack-server` running with `hydrogen` or `ardour`. However, for higher performance audio applications it might be necessary to redefine the values for `rt_prio` from 65 to 80 or even higher! The following settings work well with `ardour`:

```
@audio          -       rtprio          70
@audio          -       memlock         250000

```

See [Pro Audio](/index.php/Pro_Audio#JACK "Pro Audio") for more on professional audio configuration of an Arch system.

There are an infinite variety of possible PAM limits configurations. While an overview is provided here, it is highly advisable to read the `man 5 limits.conf` page in order to better understand these functions.

## Hard and soft realtime

Realtime is a synonym for a process which has the capability to run in time without being interrupted by any other process. However, cycles can occasionally be dropped despite this. Low power supply or a process with higher priority could be a potential cause. To solve this problem, there is a scaling of realtime quality. This article deals with **soft** realtime. Hard realtime is usually not so much desired as it is _needed_. An example could be made for car's ABS (anti-lock braking system). This can not be "rendered" and there is no second chance.

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

NaN

### Scheduling policies

CFS implements three scheduling policies:

NaN

### Scheduling classes

NaN

## See also

*   [IO Benchmarking: How, why and with what](http://www.cuddletech.com/blog/pivot/entry.php?id=820)
*   [CGROUPS Kernel documentation](http://www.kernel.org/doc/Documentation/cgroups/cgroups.txt)
*   [Optimizing servers and processes for speed with ionice, nice, ulimit](http://www.askapache.com/linux-unix/optimize-nice-ionice.html)
*   [SYSSTAT utilities home page](http://sebastien.godard.pagesperso-orange.fr/)
*   [Multitasking from the Linux command line and process prioritization](http://gaarai.com/2009/03/06/multitasking-from-the-linux-command-line-plus-process-prioritization/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Realtime_process_management&oldid=414017](https://wiki.archlinux.org/index.php?title=Realtime_process_management&oldid=414017)"