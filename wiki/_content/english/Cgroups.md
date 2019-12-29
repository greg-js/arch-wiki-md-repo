Related articles

*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Docker](/index.php/Docker "Docker")
*   [limits.conf](/index.php/Limits.conf "Limits.conf")

**cgroups** (abbreviated from **control groups**) is a Linux kernel feature to limit, police and account the resource usage for a set of processes. Compared to other approaches like the 'nice' command or `/etc/security/limits.conf`, cgroups are more flexible as they can operate on (sub)sets of processes (possibly with different system users) and support advanced features such as limiting processes to certain CPUs. When a cgroup gets closed all of its children will get closed as well.

[systemd](/index.php/Systemd "Systemd") uses groups in multiple ways:

*   Every `.service` spawns its own cgroup
*   Services are grouped under `.slice` and `.scope`
*   cgroups are hierarchical, child groups can not acquire more resources than parent

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Configuration](#Configuration)
    *   [2.1 Information](#Information)
        *   [2.1.1 Hierarchy](#Hierarchy)
        *   [2.1.2 Find cgroup of a process](#Find_cgroup_of_a_process)
        *   [2.1.3 cgroup resource usage](#cgroup_resource_usage)
    *   [2.2 Custom cgroups](#Custom_cgroups)
    *   [2.3 As service](#As_service)
        *   [2.3.1 Service unit file](#Service_unit_file)
        *   [2.3.2 Grouping unit under a slice](#Grouping_unit_under_a_slice)
    *   [2.4 As root](#As_root)
    *   [2.5 As unprivileged user](#As_unprivileged_user)
        *   [2.5.1 Disabling cgroups v1](#Disabling_cgroups_v1)
        *   [2.5.2 Controller types](#Controller_types)
        *   [2.5.3 User Delegation](#User_Delegation)
        *   [2.5.4 User defined slices](#User_defined_slices)
    *   [2.6 Run-time adjustment](#Run-time_adjustment)
*   [3 Examples](#Examples)
    *   [3.1 Matlab](#Matlab)
*   [4 See also](#See_also)

## Installing

cgroups are part of [Linux](/index.php/Linux "Linux") kernel and are controlled with [systemd](/index.php/Systemd "Systemd").

## Configuration

### Information

#### Hierarchy

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

#### Find cgroup of a process

The cgroup name of a process can be found in `/proc/*PID*/cgroup`.

For example, the cgroup of the shell:

 `cat /proc/self/cgroup` 
```
0::/user.slice/user-1000.slice/session-3.scope

```

#### cgroup resource usage

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

#### Disabling cgroups v1

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

#### User defined slices

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

## Examples

### Matlab

Doing large calculations in [MATLAB](/index.php/MATLAB "MATLAB") can crash your system, because Matlab does not have any protection against taking all your machine's memory or CPU. The following example shows a *cgroup* that constrains Matlab to first 6 CPU cores and 5 GB of memory.

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

## See also

*   [systemd cgroups hacker guide](https://systemd.io/CGROUP_DELEGATION/)
*   [cgroups(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/cgroups.7)