Related articles

*   [Linux Containers](/index.php/Linux_Containers "Linux Containers")
*   [systemd-nspawn](/index.php/Systemd-nspawn "Systemd-nspawn")
*   [Docker](/index.php/Docker "Docker")
*   [limits.conf](/index.php/Limits.conf "Limits.conf")

**cgroups** (aka **control groups**) is a Linux kernel feature to limit, police and account the resource usage for a set of processes. Compared to other approaches like the 'nice' command or `/etc/security/limits.conf`, cgroups are more flexible as they can operate on (sub)sets of processes (possibly with different system users).

Control groups can be used in multiple ways:

*   By accessing the `cgroup` filesystem directly.
*   Using the `cgm` client (part of the [cgmanager](https://www.archlinux.org/packages/?name=cgmanager) package).
*   Via tools like `cgcreate`, `cgexec` and `cgclassify` (part of the [libcgroup](https://aur.archlinux.org/packages/libcgroup/) package).
*   the "rules engine daemon", to automatically move certain users/groups/commands to groups (`/etc/cgrules.conf` and `/usr/lib/systemd/system/cgconfig.service`) (part of the [libcgroup](https://aur.archlinux.org/packages/libcgroup/) package).
*   through other software such as [Linux Containers](/index.php/Linux_Containers "Linux Containers") (LXC) virtualization, tools like [playpen](https://www.archlinux.org/packages/?name=playpen) or systemd.

## Contents

*   [1 Installing](#Installing)
*   [2 Managing resource groups with systemd](#Managing_resource_groups_with_systemd)
*   [3 Simple usage](#Simple_usage)
    *   [3.1 Manual usage](#Manual_usage)
    *   [3.2 Ad-hoc groups](#Ad-hoc_groups)
    *   [3.3 Persistent group configuration](#Persistent_group_configuration)
*   [4 Useful examples](#Useful_examples)
    *   [4.1 Matlab](#Matlab)
*   [5 Documentation](#Documentation)

## Installing

[Install](/index.php/Install "Install") any of:

*   [libcgroup](https://aur.archlinux.org/packages/libcgroup/) - set of standalone tools (`cgcreate`, `cgclassify`, persistence via `cgconfig.conf`).
*   [cgmanager](https://www.archlinux.org/packages/?name=cgmanager) - simple client (`cgm`) that communicates with its daemon (`cgmanager`) to manage cgroups.
*   [systemd](https://www.archlinux.org/packages/?name=systemd) - for controlling resources of a systemd service.

After installation of the [cgmanager](https://www.archlinux.org/packages/?name=cgmanager) package, you need to [Start](/index.php/Start "Start") `cgmanager.service` before its `cgm` client can be used.

## Managing resource groups with systemd

You can [enable](/index.php/Enable "Enable") the `cgconfig` service with systemd. This gives you the capability to track more easily any errors in `cgconfig.conf`.

## Simple usage

### Manual usage

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

### Ad-hoc groups

One of the powers of cgroups is that you can create "ad-hoc" groups on the fly. You can even grant the privileges to create custom groups to regular users. `groupname` is the cgroup name:

```
# cgcreate -a *user* -t *user* -g memory,cpu:*groupname*

```

Alternatively, using `cgmanager` with user ID `1000` and system group *root* (GID 0):

```
# cgm create memory *groupname*
# cgm chown  memory *groupname* *1000* 0
# cgm create cpu    *groupname*
# cgm chown  cpu    *groupname* *1000* 0
# # the above only makes 'cgroup.procs' and 'tasks' writable
# chown *user* /sys/fs/cgroup/{memory,cpu}/*groupname*/*

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

Likewise, for `cgmanager`:

```
$ cgm create memory **groupname/foo**
$ cgm create cpu    **groupname/foo**
$ bash
$ cgm movepid memory groupname/foo $pid_of_bash
$ cgm movepid cpu    groupname/foo $pid_of_bash

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

Alternative invocation with `cgmanager`:

```
$ cgm setvalue memory groupname/foo memory.limit_in_bytes 10000000

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

## Useful examples

### Matlab

Doing large calculations in [Matlab](/index.php/Matlab "Matlab") can crash your system, because Matlab does not have any protection against taking all your machine's memory or CPU. The following example shows a *cgroup* that constrains Matlab to 6 CPU cores and 5 GB of memory.

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