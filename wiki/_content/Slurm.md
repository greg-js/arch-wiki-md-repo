# Slurm

**Slurm** (also referred as Slurm Workload Manager or slurm-llnl) is an open-source workload manager designed for Linux clusters of all sizes, used by many of the world's supercomputers and computer clusters. It provides three key functions. First it allocates exclusive and/or non-exclusive access to resources (computer nodes) to users for some duration of time so they can perform work. Second, it provides a framework for starting, executing, and monitoring work (typically a parallel job) on a set of allocated nodes. Finally, it arbitrates contention for resources by managing a queue of pending work.

## Contents

*   [1 Installation](#Installation)
*   [2 Setup](#Setup)
    *   [2.1 Client (compute node) configuration](#Client_.28compute_node.29_configuration)
    *   [2.2 Server (head node) configuration](#Server_.28head_node.29_configuration)
*   [3 See also](#See_also)

## Installation

**Note:** Although slurm is a very powerful job scheduler, if the goal of the cluster is solely to increase compilation throughput, [distcc](/index.php/Distcc "Distcc") is a much easier and elegant solution.

[Install](/index.php/Install "Install") the [slurm-llnl](https://aur.archlinux.org/packages/slurm-llnl/)<sup><small>AUR</small></sup> package found in the [AUR](/index.php/AUR "AUR"). It pulls in [munge](https://aur.archlinux.org/packages/munge/)<sup><small>AUR</small></sup>, an authenticatin service, as a dependecy. It is started as a requierement through slurmd's systemd service and encrypts the connection between the various hosts. Therefore make sure that all nodes in your cluster have the same key in `/etc/munge/munge.key`.

The package slurm itself has many more optional dependencies, though slurm has to be recompiled to make use of them, after they have been installed.

## Setup

The configuration files for slurm-llnl reside under `/etc/slurm-llnl`. Prior to starting any slurm-services, it has to be configure properly by creating a config file `/etc/slurm-llnl/slurm.conf`. Client and server may use the same configuration file, which can either be generated at [https://computing.llnl.gov/linux/slurm/configurator.html](https://computing.llnl.gov/linux/slurm/configurator.html) or by copying `/etc/slurm-llnl/slurm.conf.example` to `/etc/slurm-llnl/slurm.conf` and adapting it to ones liking.

By default the slurm user, which was introduced to your system in the installation process, has 64030 as UID and GID, this simplicifes the setup on multiple systems. UID and GID matches the one used in Debian, therefore they may be used side-by-side, but remember that binaries are not in the same directories on each and every distribution.

### Client (compute node) configuration

On the client-side one may now safely start `slurmd.service` (enable the service to make it start at bootup).

To validate that slurmd is up and running, use

```
systemctl status slurmd

```

### Server (head node) configuration

Start/enable the `slurmctld.service`.

To complete an entrerprise like solution you may want to start/enable `slurmdbd.service`, which handles a mysql database for easier management thereby logging somewhat essential process information.

**Note:** Additional arguments may be passed to the program by adapting `/etc/default/slurm-llnl` though still utilizing the power of systemd. This file is handled as the environment file for the various services and simply passes any arguments on to the program.

## See also

*   [slurm tutorials](http://slurm.schedmd.com/tutorials.html) - Introduction to the Slurm Workload Manager for users and system administrators, plus some material for Slurm programmers.
*   [Quick Start Administrator Guide](http://slurm.schedmd.com/quickstart_admin.html) - More or less deatailed setup guide.
*   [SLURM to manage jobs](https://rc.fas.harvard.edu/resources/documentation/convenient-slurm-commands/) - Convenient SLURM Commands.
*   [Running Jobs](https://rc.fas.harvard.edu/resources/running-jobs/) - How slurm is used at harvard university.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Slurm&oldid=415006](https://wiki.archlinux.org/index.php?title=Slurm&oldid=415006)"