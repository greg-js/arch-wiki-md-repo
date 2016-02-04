# Realtime kernel

This article describes the Linux kernel realtime patch set, and how to configure, test, and troubleshoot realtime kernels.

## Contents

*   [1 What is realtime](#What_is_realtime)
*   [2 How does the realtime patch work](#How_does_the_realtime_patch_work)
*   [3 Installation](#Installation)
*   [4 Scheduling latency](#Scheduling_latency)
*   [5 Latency testing utilities](#Latency_testing_utilities)
    *   [5.1 cyclictest](#cyclictest)
    *   [5.2 hackbench](#hackbench)
    *   [5.3 hwlatdetect](#hwlatdetect)
*   [6 Configuration](#Configuration)
*   [7 Tips and Tricks](#Tips_and_Tricks)
*   [8 Troubleshooting](#Troubleshooting)
*   [9 Known issues](#Known_issues)

## What is realtime

[Realtime](https://en.wikipedia.org/wiki/Real-time_computing "wikipedia:Real-time computing") applications have operational deadlines between some triggering event and the application's response to that event. To meet these operational deadlines, programmers use realtime operating systems (RTOS) on which the maximum response time can be calculated or measured reliably for the given application and environment. A typical RTOS uses priorities. The highest priority task wanting the CPU always gets the CPU within a fixed amount of time after the event waking the task has taken place. On such an RTOS the [latency](https://en.wikipedia.org/wiki/Latency_(engineering) "wikipedia:Latency (engineering)") of a task only depends on the tasks running at equal or higher priorities, all other tasks can be ignored. On a normal OS (such as normal Linux) the latencies depend on everything running on the system, which of course makes it much harder to be convinced that the deadlines will be met every time on a reasonably complicated system. This is because [preemption](https://en.wikipedia.org/wiki/Preemption_(computing) "wikipedia:Preemption (computing)") can be switched off for an unknown amount of time. The high priority task wanting to run can thus be delayed for an unknown amount of time by low priority tasks running with preemption switched off.

## How does the realtime patch work

The RT-Preempt patch converts Linux into a fully preemptible kernel. This is done through:

*   Making in-kernel locking-primitives (using [spinlocks](https://en.wikipedia.org/wiki/Spinlock "wikipedia:Spinlock")) preemptible though reimplementation with rtmutexes.
*   [Critical sections](https://en.wikipedia.org/wiki/Critical_section "wikipedia:Critical section") protected by i.e. spinlock_t and rwlock_t are now preemptible. The creation of non-preemptible sections (in kernel) is still possible with raw_spinlock_t (same APIs like spinlock_t).
*   Implementing [priority inheritance](https://en.wikipedia.org/wiki/Priority_inheritance "wikipedia:Priority inheritance") for in-kernel spinlocks and [semaphores](https://en.wikipedia.org/wiki/Semaphore_(programming) "wikipedia:Semaphore (programming)").
*   Converting interrupt handlers into preemptible kernel threads: The RT-Preempt patch treats soft interrupt handlers in kernel thread context, which is represented by a task_struct like a common user space process. However it is also possible to register an IRQ in kernel context.
*   Converting the old Linux timer API into separate infrastructures for high resolution kernel timers plus one for timeouts, leading to user space POSIX timers with high resolution.

## Installation

There are many -rt patched kernels available from the [AUR](/index.php/AUR "AUR"). The main two are [linux-rt](https://aur.archlinux.org/packages/linux-rt/) and [linux-rt-lts](https://aur.archlinux.org/packages/linux-rt-lts/). Both are also available from the unsigned [archaudio-production](/index.php/Unofficial_user_repositories#archaudio "Unofficial user repositories") repository. Both have a configuration based on the main [linux](https://www.archlinux.org/packages/?name=linux) kernel package, linux-rt follows the development branch of the -rt patch, while linux-rt-lts tracks a stable branch of the rt patchset.

**Note:** Don't forget to add the newly installed kernel to your boot manager.

## Scheduling latency

In the context of the scheduler, latency is the time that passes from the occurrence of an event until the handling of said event. Often the delay from the firing of an interrupt until the interrupt handler starts running, but could also be from the expiration of a timer, etc.

Latency of itself is natural, there is always some latency, it becomes problematic when it exceeds the deadline given by your application's restraints. If it's less than the deadline, it's a success, if it's bigger, it's a failure.

There can be many varied causes for high scheduling latencies, Some worth mentioning (in no particular order) are: a misconfigured system, bad hardware, badly programmed kernel modules, CPU power management, faulty hardware timers, [SMIs](https://en.wikipedia.org/wiki/System_Management_Mode#Entering_SMM "wikipedia:System Management Mode"), [SMT](https://en.wikipedia.org/wiki/Simultaneous_multithreading "wikipedia:Simultaneous multithreading"), etc.

When trying to determine the system's maximum scheduling latency, the system needs to be put under load. A busy system will in general experience bigger latencies than an idle one. It would be recommendable to run tests for a long time and under different natural and artificial load conditions. It would also be recommendable to stress all sub systems that would be in use on the production system, like disk and net io, usb, the graphics sub system, etc.

## Latency testing utilities

There are several tools available to check kernel scheduling latencies, and to track down the causes of latency spikes. One set of tools comes in a package called [rt-tests](https://aur.archlinux.org/packages/rt-tests/) (also available from [archaudio-production](/index.php/Unofficial_user_repositories#archaudio "Unofficial user repositories")).

### cyclictest

One of the programs in rt-tests is called cyclictest, which can be used to verify the maximum scheduling latency, and for tracking down the causes of latency spikes. cyclictest works by measuring the time between the expiration of a timer a thread sets and when the thread starts running again.

Here is the result of a typical test run:

 `# cyclictest --smp -p98 -m` 

```
# /dev/cpu_dma_latency set to 0us
policy: fifo: loadavg: 239.09 220.49 134.53 142/1304 23799          

T: 0 (23124) P:98 I:1000 C: 645663 Min:      2 Act:    4 Avg:    4 Max:      23
T: 1 (23125) P:98 I:1500 C: 430429 Min:      2 Act:    5 Avg:    3 Max:      23
T: 2 (23126) P:98 I:2000 C: 322819 Min:      2 Act:    4 Avg:    3 Max:      15
T: 3 (23127) P:98 I:2500 C: 258247 Min:      2 Act:    5 Avg:    4 Max:      32
^C
```

It shows a four CPU core system running one thread (SCHED_FIFO) per core at priority 98, with memory locked, the system is also under a high load due to running hackbench in a separate terminal. What is most interesting is the max schedling latency detected, in this case 32 usecs on core 3.

[cyclictest(8)](http://man.cx/cyclictest(8)) man page.

### hackbench

An idle kernel will tend to show much lower scheduling latencies, it's essential to put some load on it to get a realistic result. This can be done with another utility in the rt-tests package called hackbench. It works by creating multiple pairs of threads or processes, that pass data between themselves either over sockets or pipes. To make it run longer add the -l parameter: `hackbench -l 1000000`.

[hackbench(8)](http://man.cx/hackbench(8)) man page.

### hwlatdetect

hwlatdetect can be used to detect SMIs taking an inordinate time, thus introducing latency by blocking normal kernel execution. It consists of a kernel module (present in both linux-rt and linux-rt-lts), and a python script to launch the process and report the results back to the user. To check if the system uses NMIs run the following command:

 `$ grep NMI /proc/interrupts` 

```

NMI:       3335       3336       3335       3335   Non-maskable interrupts
```

The hwlatdetect kernel module works by turning everything running on the CPUs off through the stop_machine() call. It then polls the TSC (Time Stamp Counter) looking for gaps in the generated data stream. Any gaps indicates that it was interrupted by a NMI, as they are the only possible mechanism (apart from a broken TSC implementation). To run the program for 120 secs, with a detection threshold of 15 usecs, execute the following:

 `# hwlatdetect --duration=120 --threshold=15` 

```
hwlatdetect:  test duration 120 seconds
   parameters:
        Latency threshold: 15us
        Sample window:     1000000us
        Sample width:      500000us
     Non-sampling period:  500000us
        Output File:       None

Starting test
test finished
Max Latency: 21us
Samples recorded: 16
Samples exceeding threshold: 16
1408928107.0286324723   18      17
.
.
1408928180.0296881126   15      21
.
.
1408928212.0300332889   18      18
```

The result shows 16 NMIs detected that exceeded the 15 usecs threshold specified, the maximum latency detected was 21 usecs.

[hwlatdetect(8)](http://man.cx/hwlatdetect) man page.

## Configuration

## Tips and Tricks

## Troubleshooting

## Known issues

*   bcache support is disabled due to how it uses locks.
*   A problem with the powernow-k8 module causing a hang at boot on some AMD CPUs.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Realtime_kernel&oldid=367042](https://wiki.archlinux.org/index.php?title=Realtime_kernel&oldid=367042)"