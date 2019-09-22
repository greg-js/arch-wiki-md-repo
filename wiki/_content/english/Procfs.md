<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Description](#Description)
*   [2 Content](#Content)
    *   [2.1 Kernel & system information](#Kernel_&_system_information)
    *   [2.2 Processes](#Processes)
*   [3 Usage](#Usage)

## Description

Procfs is pseudo filesystem (/proc) containing information about the system resources, including currently running processes, kernel, hardware. Since procfs is pseudo(meaning false) filesystem that means it is not really existent(only exist in memory). Altering files in **/proc** allows us to manipulate kernel in runtime. If we take a look at the sizes of files inside procfs we can notice that their size is 0, reason for that is they are only populated when requested by user(on the fly). It is suggested to use sysfs over procfs because it has defined structure and procfs became a mess over time.

## Content

### Kernel & system information

There are many files under the /proc which tells us a lot of information about the system as well as the kernel. There are a lot of them to talk about every single one of them, but some of them are listed below with brief information what they are.

*   **/proc/cpuinfo** - informations about CPU
*   **/proc/meminfo** - information about the physical memory
*   **/proc/vmstats** - information about the virtual memory
*   **/proc/mounts** - information about the mounts([mount](/index.php/Mount "Mount"))
*   **/proc/filesystems** - information about active filesystems
*   **/proc/uptime** - current system uptime
*   **/proc/cmdline** - kernel command line

### Processes

Inside **/proc/<pid>** is stored information about every process currently running. Below is example showing some of the PIDs currently running

 `$ ls -l /proc` 
```
total 0
dr-xr-xr-x  9 root    root                  0 Sep  8 18:17 1
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 10
dr-xr-xr-x  9 daemonx daemonx               0 Sep  9 03:02 1057
dr-xr-xr-x  9 daemonx daemonx               0 Sep  8 18:18 1077
dr-xr-xr-x  9 daemonx daemonx               0 Sep  9 03:02 1087
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 11
dr-xr-xr-x  9 daemonx daemonx               0 Sep  9 03:02 1103
dr-xr-xr-x  9 daemonx daemonx               0 Sep  9 03:02 1107
dr-xr-xr-x  9 daemonx daemonx               0 Sep  9 03:02 1159
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 12
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 124
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 125
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 127
dr-xr-xr-x  9 root    root                  0 Sep  9 03:02 128
...

```

Lets take for example pid 1057 and see what's inside

 `$ ls -l /proc/1057` 
```
total 0
dr-xr-xr-x 2 daemonx daemonx 0 Sep  9 03:12 attr
-rw-r--r-- 1 daemonx daemonx 0 Sep  9 03:12 autogroup
-r-------- 1 daemonx daemonx 0 Sep  9 03:12 auxv
-r--r--r-- 1 daemonx daemonx 0 Sep  9 03:12 cgroup
--w------- 1 daemonx daemonx 0 Sep  9 03:12 clear_refs
-r--r--r-- 1 daemonx daemonx 0 Sep  9 03:12 cmdline
-rw-r--r-- 1 daemonx daemonx 0 Sep  9 03:12 comm
-rw-r--r-- 1 daemonx daemonx 0 Sep  9 03:12 coredump_filter
-r--r--r-- 1 daemonx daemonx 0 Sep  9 03:12 cpuset
lrwxrwxrwx 1 daemonx daemonx 0 Sep  9 03:12 cwd -> /home/daemonx
-r-------- 1 daemonx daemonx 0 Sep  9 03:12 environ
lrwxrwxrwx 1 daemonx daemonx 0 Sep  9 03:12 exe -> /usr/lib/gvfsd-metadata
dr-x------ 2 daemonx daemonx 0 Sep  9 03:12 fd
dr-x------ 2 daemonx daemonx 0 Sep  9 03:12 fdinfo
-rw-r--r-- 1 daemonx daemonx 0 Sep  9 03:12 gid_map
-r-------- 1 daemonx daemonx 0 Sep  9 03:12 io
-r--r--r-- 1 daemonx daemonx 0 Sep  9 03:12 latency
-r--r--r-- 1 daemonx daemonx 0 Sep  9 03:12 limits
-rw-r--r-- 1 daemonx daemonx 0 Sep  9 03:12 loginuid
dr-x------ 2 daemonx daemonx 0 Sep  9 03:12 map_files
-r--r--r-- 1 daemonx daemonx 0 Sep  9 03:12 maps
-rw------- 1 daemonx daemonx 0 Sep  9 03:12 mem
...

```

Some of the fields:

*   **cmdline** - arguments used to start program
*   **cwd** - current working directory for the process
*   **environ** - environment variables inside the process
*   **fd/** - directory containing open file descriptors for the process
*   **exe** - symbolic link to process executable
*   **maps** - memory mapping of the process
*   **mem** - virtual memory of the process

## Usage

To read from proc file, we can use **cat**: `$ cat /proc/cmdline`. To write to the file, we can use **echo**: `# echo 1 > /proc/sys/kernel/sysrq`