Related articles

*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Docker](/index.php/Docker "Docker")
*   [limits.conf](/index.php/Limits.conf "Limits.conf")

**Control groups** (or **cgroups** as they are commonly known) are a feature provided by the Linux kernel to manage, restrict, and audit groups of processes. Compared to other approaches like the [nice(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nice.1) command or `/etc/security/limits.conf`, cgroups are more flexible as they can operate on (sub)sets of processes (possibly with different system users).

Control groups can be accessed with various tools:

*   using directives in [systemd](/index.php/Systemd "Systemd") unit files to specify limits for services and slices;
*   by accessing the `cgroup` filesystem directly;
*   via tools like `cgcreate`, `cgexec` and `cgclassify` (part of the [libcgroup](https://aur.archlinux.org/packages/libcgroup/) package);
*   using the "rules engine daemon" to automatically move certain users/groups/commands to groups (`/etc/cgrules.conf` and `/usr/lib/systemd/system/cgconfig.service`) (part of the [libcgroup](https://aur.archlinux.org/packages/libcgroup/) package); and
*   through other software such as [Linux Containers](/index.php/Linux_Containers "Linux Containers") (LXC) virtualization.

[cgmanager](https://www.archlinux.org/packages/?name=cgmanager) is [deprecated](https://github.com/lxc/cgmanager/issues/32) and unsupported as it does not work with systemd versions 232 and above.

For Arch Linux systemd is the perferred and easiest method of invoking and configuring cgroups as it is a part of default installation.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 With systemd](#With_systemd)
    *   [2.1 Hierarchy](#Hierarchy)
    *   [2.2 Find cgroup of a process](#Find_cgroup_of_a_process)
    *   [2.3 cgroup resource usage](#cgroup_resource_usage)
    *   [2.4 Custom cgroups](#Custom_cgroups)
    *   [2.5 As service](#As_service)
        *   [2.5.1 Service unit file](#Service_unit_file)
        *   [2.5.2 Grouping unit under a slice](#Grouping_unit_under_a_slice)
    *   [2.6 As root](#As_root)
    *   [2.7 As unprivileged user](#As_unprivileged_user)
        *   [2.7.1 Disabling v1 cgroups](#Disabling_v1_cgroups)
        *   [2.7.2 Controller types](#Controller_types)
        *   [2.7.3 User Delegation](#User_Delegation)
        *   [2.7.4 User-defined slices](#User-defined_slices)
    *   [2.8 Run-time adjustment](#Run-time_adjustment)
*   [3 With libcgroup](#With_libcgroup)
    *   [3.1 Ad-hoc groups](#Ad-hoc_groups)
    *   [3.2 Persistent group configuration](#Persistent_group_configuration)
*   [4 With the cgroup virtual filesystem](#With_the_cgroup_virtual_filesystem)
*   [5 Examples](#Examples)
    *   [5.1 Matlab](#Matlab)
        *   [5.1.1 With systemd](#With_systemd_2)
        *   [5.1.2 With libcgroup](#With_libcgroup_2)
*   [6 Documentation](#Documentation)
*   [7 See also](#See_also)

## Installing

Make sure you have one of these packages [installed](/index.php/Install "Install") for automated cgroup handling:

*   [systemd](https://www.archlinux.org/packages/?name=systemd) - for controlling resources of a systemd service.
*   [libcgroup](https://aur.archlinux.org/packages/libcgroup/) - set of standalone tools (`cgcreate`, `cgclassify`, persistence via `cgconfig.conf`).

## With systemd

### Hierarchy

Current cgroup hierarchy can be seen with `systemctl status` or `systemd-cgls` command.

 `systemctl status` 
```
● myarchlinux
    State: running
     Jobs: 0 queued
   Failed: 0 units
    Since: Wed 2019-12-04 22:16:28 UTC; 1 day 4h ago
   CGroup: /
           ├─user.slice 
           │ └─user-1000.slice 
           │   ├─user@1000.service 
           │   │ ├─gnome-shell-wayland.service 
           │   │ │ ├─ 1129 /usr/bin/gnome-shell
           │   │ ├─gnome-terminal-server.service 
           │   │ │ ├─33519 /usr/lib/gnome-terminal-server
           │   │ │ ├─37298 fish
           │   │ │ └─39239 systemctl status
           │   │ ├─init.scope 
           │   │ │ ├─1066 /usr/lib/systemd/systemd --user
           │   │ │ └─1067 (sd-pam)
           │   └─session-2.scope 
           │     ├─1053 gdm-session-worker [pam/gdm-password]
           │     ├─1078 /usr/bin/gnome-keyring-daemon --daemonize --login
           │     ├─1082 /usr/lib/gdm-wayland-session /usr/bin/gnome-session
           │     ├─1086 /usr/lib/gnome-session-binary
           │     └─3514 /usr/bin/ssh-agent -D -a /run/user/1000/keyring/.ssh
           ├─init.scope 
           │ └─1 /sbin/init
           └─system.slice 
             ├─systemd-udevd.service 
             │ └─285 /usr/lib/systemd/systemd-udevd
             ├─systemd-journald.service 
             │ └─272 /usr/lib/systemd/systemd-journald
             ├─NetworkManager.service 
             │ └─656 /usr/bin/NetworkManager --no-daemon
             ├─gdm.service 
             │ └─668 /usr/bin/gdm
             └─systemd-logind.service 
               └─654 /usr/lib/systemd/systemd-logind

```

### Find cgroup of a process

The cgroup name of a process can be found in `/proc/*PID*/cgroup`.

For example, the cgroup of the shell:

 `cat /proc/self/cgroup` 
```
0::/user.slice/user-1000.slice/session-3.scope

```

### cgroup resource usage

The `systemd-cgtop` command can be used to see the resource usage:

 `systemd-cgtop` 
```
Control Group                            Tasks   %CPU   Memory  Input/s Output/s
user.slice                                 540  152,8     3.3G        -        -
user.slice/user-1000.slice                 540  152,8     3.3G        -        -
user.slice/u…000.slice/session-1.scope     425  149,5     3.1G        -        -
system.slice                                37      -   215.6M        -        -

```

### Custom cgroups

[systemd.slice(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.slice.5) systemd unit files can be used to define a custom cgroup configuration.

The resource control options that can be assigned are documented in [systemd.resource-control(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.resource-control.5)

Example slice unit that only allows 30% of cpu used:

```
[Slice]
CPUQuota=30%
```

### As service

#### Service unit file

Resources can be directly specified in service definition or as a [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd")

```
[Service]
MemoryMax=1G # Limit service to 1 gigabyte
```

#### Grouping unit under a slice

Service can be specified what slice to run in:

```
[Service]
Slice=my.slice
```

### As root

`systemd-run` can be used to run a command in a specific slice.

```
$ systemd-run --slice=*my.slice* *command*

```

`--uid=*username*` option can be used to spawn the command as specific user.

```
$ systemd-run --uid=*username* --slice=*my.slice* *command*

```

The `--shell` option can be used to spawn a command shell inside the slice.

### As unprivileged user

Unprivileged users can divide the resources provided to them into new cgroups, if some conditions are met.

Version 1 cgroups must be disabled for a non-root user to be allowed to manage resources cgroups.

#### Disabling v1 cgroups

Arch Linux enables both v1 and v2 cgroups by default.

To disable v1 cgroups, the `systemd.unified_cgroup_hierarchy` [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") can be used.

Verify that v1 cgroups have been disabled:

 `$ ls /sys/fs/cgroup` 
```
cgroup.controllers      cgroup.subtree_control  init.scope/      system.slice/
cgroup.max.depth        cgroup.threads          io.cost.model    user.slice/
cgroup.max.descendants  cpu.pressure            io.cost.qos
cgroup.procs            cpuset.cpus.effective   io.pressure
cgroup.stat             cpuset.mems.effective   memory.pressure

```

If you see something like this, you still have v1 groups enabled:

 `$ ls /sys/fs/cgroup` 
```
blkio/    cpu,cpuacct/  freezer/  net_cls@           perf_event/  systemd/
cpu@      cpuset/       hugetlb/  net_cls,net_prio/  pids/        unified/
cpuacct@  devices/      memory/   net_prio@          rdma/

```

#### Controller types

Not all resources can be controlled by user.

| Controller | Can be controlled by user | Options |
| cpu | Requires delegation | CPUAccounting, CPUWeight, CPUQuota, AllowedCPUs, AllowedMemoryNodes |
| io | Requires delegation | IOWeight, IOReadBandwidthMax, IOWriteBandwidthMax, IODeviceLatencyTargetSec |
| memory | Yes | MemoryLow, MemoryHigh, MemoryMax, MemorySwapMax |
| pids | Yes | TasksMax |
| rdma | No | ? |
| eBPF | No | IPAddressDeny, DeviceAllow, DevicePolicy |

**Note:** eBPF is technically not a controller but those systemd options implemented using it and only root is allowed to set them.

#### User Delegation

For user to control cpu and io resources, the resources need to be delegated. This can be done by creating a unit overload.

For example if your user id is 1000:

 `systemctl edit user@1000.service` 
```
[Service]
Delegate=yes
```

Reboot and verify that the slice your user session is under has cpu and io controller:

 `$ cat /sys/fs/cgroup/user.slice/user-1000.slice/cgroup.controllers` 
```
**cpuset cpu io** memory pids

```

#### User-defined slices

The user slice files can be placed in `~/.config/systemd/user/`.

To run the command under certain slice:

```
$ systemd-run --user --slice=*my.slice* *command*

```

You can also run your login shell inside the slice:

```
$ systemd-run --user --slice=*my.slice* --shell

```

### Run-time adjustment

cgroups resources can be adjusted at run-time using `systemctl set-property` command. Option syntax is the same as in [systemd.resource-control(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.resource-control.5).

**Warning:** The adjustments will be made **permanent** unless `--runtime` option is passed. Adjustments are saved at `/etc/systemd/system.control/` for system wide options and `.config/systemd/user.control/` for user options.

**Note:** Not all resources changes immediately take effect. For example, changing TaskMax will only take effect on spawning new processes.

For example, cutting off internet access for all user sessions:

```
$ systemctl set-property user.slice IPAddressDeny=any

```

## With libcgroup

You can [enable](/index.php/Enable "Enable") the `cgconfig` service with systemd. This allows you to track any errors in `cgconfig.conf` more easily.

### Ad-hoc groups

One of the powers of cgroups is that you can create "ad-hoc" groups on the fly. You can even grant the privileges to create custom groups to regular users. `groupname` is the cgroup name:

```
# cgcreate -a *user* -t *user* -g memory,cpu:*groupname*

```

Now all the tunables in the group `groupname` are writable by your user:

```
$ ls -l /sys/fs/cgroup/memory/*groupname*
total 0
-rwxrwxr-x 1 user root 0 Sep 25 00:39 cgroup.event_control
-rwxrwxr-x 1 user root 0 Sep 25 00:39 cgroup.procs
-rwxrwxr-x 1 user root 0 Sep 25 00:39 cpu.rt_period_us
-rwxrwxr-x 1 user root 0 Sep 25 00:39 cpu.rt_runtime_us
-rwxrwxr-x 1 user root 0 Sep 25 00:39 cpu.shares
-rwxrwxr-x 1 user root 0 Sep 25 00:39 notify_on_release
-rwxrwxr-x 1 user root 0 Sep 25 00:39 tasks

```

Cgroups are hierarchical, so you can create as many subgroups as you like. If a normal user wants to run a `bash` shell under a new subgroup called `foo`:

```
$ cgcreate -g memory,cpu:**groupname/foo**
$ **cgexec**    -g memory,cpu:groupname/foo **bash**

```

To make sure (only meaningful for legacy (v1) cgroups):

```
$ cat /proc/self/cgroup
11:memory:/groupname/foo
6:cpu:/groupname/foo

```

A new subdirectory was created for this group. To limit the memory usage of all processes in this group to 10 MB, run the following:

```
$ echo 10000000 > /sys/fs/cgroup/memory/groupname/foo/memory.limit_in_bytes

```

Note that the memory limit applies to RAM use only -- once tasks hit this limit, they will begin to swap. But it won't affect the performance of other processes significantly.

Similarly you can change the CPU priority ("shares") of this group. By default all groups have 1024 shares. A group with 100 shares will get a ~10% portion of the CPU time:

```
$ echo 100 > /sys/fs/cgroup/cpu/groupname/foo/cpu.shares

```

You can find more tunables or statistics by listing the cgroup directory.

You can also change the cgroup of already running processes. To move all 'bash' commands to this group:

```
$ pidof bash
13244 13266
$ **cgclassify** -g memory,cpu:groupname/foo `pidof bash`
$ cat /proc/13244/cgroup
11:memory:/groupname/foo
6:cpu:/groupname/foo

```

### Persistent group configuration

**Note:** when using [Systemd](/index.php/Systemd "Systemd") > = 205 to manage cgroups, you can ignore this file entirely.

If you want your cgroups to be created at boot, you can define them in `/etc/cgconfig.conf` instead. For example, the "groupname" has a permission for `$USER` and *users* of group `$GROUP` to manage limits and add tasks. A *subgroup* "groupname/foo" group definitions would look like this:

 `/etc/cgconfig.conf ` 
```
group **groupname** {
  perm {
# who can manage limits
    admin {
      uid = **$USER**;
      gid = **$GROUP**;
    }
# who can add tasks to this group
    task {
      uid = **$USER**;
      gid = **$GROUP**;
    }
  }
# create this group in cpu and memory controllers
  cpu { }
  memory { }
}

group **groupname/foo** {
  cpu {
    **cpu.shares** = 100;
  }
  memory {
    **memory.limit_in_bytes** = 10000000;
  }
}
```

**Note:**

*   Comments should begin at the start of a line! The **#** character for comments must appear as the first character of a line. Else, *cgconfigparser* will have problem parsing it but will only report `cgroup change of group failed` as the error, unless you started *cgconfig* with [Systemd](/index.php/Systemd "Systemd")
*   The permissions section is optional.
*   The `/sys/fs/cgroup/` hierarchy directory containing all *controllers* sub-directories is already created and mounted at boot as a virtual file system. This gives the ability to create a new group entry with the `*$CONTROLLER-NAME { }*` command. If for any reason you want to create and mount hierachies in another place, you will then need to write a second entry in `/etc/cgconfig.conf` following this way :

```
 mount {    
   cpuset = /your/path/*groupname*;
 }

```

This is equivalent to these shell commands:

```
 # mkdir /your/path/*groupname*
 # mount -t /your/path -o cpuset *groupname* /your/path/*groupname*

```

## With the cgroup virtual filesystem

Starting with systemd 232, the *cgm* method described in the next section, this section will instead describe a manual method to limit memory usage.

Create a new cgroup named *groupname*:

```
# mkdir /sys/fs/cgroup/memory/*groupname*

```

Example: set the maximum memory limit to 100MB:

```
# echo 100000000 > /sys/fs/cgroup/memory/*groupname*/memory.limit_in_bytes

```

Move a process to the cgroup (note: only one PID can be written at a time, repeat this for each process that must be moved):

```
# echo *pid* > /sys/fs/cgroup/memory/*groupname*/cgroup.procs

```

## Examples

### Matlab

Doing large calculations in [MATLAB](/index.php/MATLAB "MATLAB") can crash your system, because Matlab does not have any protection against taking all your machine's memory or CPU. The following examples show a *cgroup* that constrains Matlab to first 6 CPU cores and 5 GB of memory.

#### With systemd

 `~/.config/systemd/user/matlab.slice` 
```
[Slice]
AllowedCPUs=0-5
MemoryHigh=6G
```

Launch Matlab like this (be sure to use the right path):

```
$ systemd-run --user --slice=matlab.slice /opt/MATLAB/2012b/bin/matlab -desktop

```

#### With libcgroup

 `/etc/cgconfig.conf` 
```
group matlab {
    perm {
        admin {
            uid = *username*;
        }
        task {
            uid = *username*;
        }
    }

    cpuset {
        cpuset.mems="0";
        cpuset.cpus="0-5";
    }
    memory {
        memory.limit_in_bytes = 5000000000;
    }
}
```

Change `*username*` to the user Matlab is run as.

You can also restrict the CPU share with the `cpu` constraint.

Launch Matlab like this (be sure to use the right path):

```
$ cgexec -g memory,cpuset:matlab /opt/MATLAB/2012b/bin/matlab -desktop

```

## Documentation

*   For information on controllers and what certain switches and tunables mean, refer to kernel's documentation [v1](https://www.kernel.org/doc/Documentation/cgroup-v1/) or [v2](https://www.kernel.org/doc/Documentation/cgroup-v2.txt) (or install linux-docs and see `/usr/src/linux/Documentation/cgroup`)
*   A detailed and complete Resource Management Guide can be found in the [fedora project documentation](http://docs.fedoraproject.org/en-US/Fedora/17/html-single/Resource_Management_Guide/index.html#sec-How_Control_Groups_Are_Organized).

For commands and configuration files, see relevant man pages, e.g. `man cgcreate` or `man cgrules.conf`

## See also

*   [systemd cgroups hacker guide](https://systemd.io/CGROUP_DELEGATION/)
*   [cgroups(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgroups.7)