Related articles

*   [Reporting bug guidelines (简体中文)](/index.php/Reporting_bug_guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Reporting bug guidelines (简体中文)")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Debug - Getting Traces (简体中文)](/index.php/Debug_-_Getting_Traces_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Debug - Getting Traces (简体中文)")
*   [IRC Collaborative Debugging](/index.php/IRC_Collaborative_Debugging "IRC Collaborative Debugging")

**翻译状态：** 本文是英文页面 [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2018-04-02，点击[这里](https://wiki.archlinux.org/index.php?title=General+troubleshooting&diff=0&oldid=515594)可以查看翻译后英文页面的改动。

本文介绍了一些常规的故障排除方法。有关特定应用程序的问题，请参阅该特定程序的 wiki 页面。

## Contents

*   [1 常用手段](#.E5.B8.B8.E7.94.A8.E6.89.8B.E6.AE.B5)
    *   [1.1 注意细节](#.E6.B3.A8.E6.84.8F.E7.BB.86.E8.8A.82)
    *   [1.2 常见问题 / 检查项](#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98_.2F_.E6.A3.80.E6.9F.A5.E9.A1.B9)
    *   [1.3 寻求解决](#.E5.AF.BB.E6.B1.82.E8.A7.A3.E5.86.B3)
    *   [1.4 额外支援](#.E9.A2.9D.E5.A4.96.E6.94.AF.E6.8F.B4)
*   [2 系统启动问题](#.E7.B3.BB.E7.BB.9F.E5.90.AF.E5.8A.A8.E9.97.AE.E9.A2.98)
    *   [2.1 控制台的输出信息](#.E6.8E.A7.E5.88.B6.E5.8F.B0.E7.9A.84.E8.BE.93.E5.87.BA.E4.BF.A1.E6.81.AF)
        *   [2.1.1 输出流控制](#.E8.BE.93.E5.87.BA.E6.B5.81.E6.8E.A7.E5.88.B6)
        *   [2.1.2 回滚显示](#.E5.9B.9E.E6.BB.9A.E6.98.BE.E7.A4.BA)
        *   [2.1.3 Debug 输出](#Debug_.E8.BE.93.E5.87.BA)
    *   [2.2 故障恢复控制台](#.E6.95.85.E9.9A.9C.E6.81.A2.E5.A4.8D.E6.8E.A7.E5.88.B6.E5.8F.B0)
    *   [2.3 Intel 显卡造成的黑屏](#Intel_.E6.98.BE.E5.8D.A1.E9.80.A0.E6.88.90.E7.9A.84.E9.BB.91.E5.B1.8F)
    *   [2.4 加载内核时卡住](#.E5.8A.A0.E8.BD.BD.E5.86.85.E6.A0.B8.E6.97.B6.E5.8D.A1.E4.BD.8F)
    *   [2.5 调试内核模块](#.E8.B0.83.E8.AF.95.E5.86.85.E6.A0.B8.E6.A8.A1.E5.9D.97)
    *   [2.6 调试硬件](#.E8.B0.83.E8.AF.95.E7.A1.AC.E4.BB.B6)
*   [3 内核崩溃 (Kernel panics)](#.E5.86.85.E6.A0.B8.E5.B4.A9.E6.BA.83_.28Kernel_panics.29)
    *   [3.1 查看 panic 信息](#.E6.9F.A5.E7.9C.8B_panic_.E4.BF.A1.E6.81.AF)
        *   [3.1.1 示例场景：模块损坏](#.E7.A4.BA.E4.BE.8B.E5.9C.BA.E6.99.AF.EF.BC.9A.E6.A8.A1.E5.9D.97.E6.8D.9F.E5.9D.8F)
    *   [3.2 重启至 root shell 并修复故障](#.E9.87.8D.E5.90.AF.E8.87.B3_root_shell_.E5.B9.B6.E4.BF.AE.E5.A4.8D.E6.95.85.E9.9A.9C)
*   [4 软件包管理](#.E8.BD.AF.E4.BB.B6.E5.8C.85.E7.AE.A1.E7.90.86)
*   [5 fuser](#fuser)
*   [6 会话权限](#.E4.BC.9A.E8.AF.9D.E6.9D.83.E9.99.90)
*   [7 错误信息： "error while loading shared libraries"](#.E9.94.99.E8.AF.AF.E4.BF.A1.E6.81.AF.EF.BC.9A_.22error_while_loading_shared_libraries.22)
*   [8 错误信息： "file: could not find any magic files!"](#.E9.94.99.E8.AF.AF.E4.BF.A1.E6.81.AF.EF.BC.9A_.22file:_could_not_find_any_magic_files.21.22)
    *   [8.1 错误原因](#.E9.94.99.E8.AF.AF.E5.8E.9F.E5.9B.A0)
    *   [8.2 解决方法](#.E8.A7.A3.E5.86.B3.E6.96.B9.E6.B3.95)
*   [9 参阅](#.E5.8F.82.E9.98.85)

## 常用手段

### 注意细节

为了解决遇到的问题，对当前使用的这个程序，你应该有一个基本的了解，这是 *至关重要* 的。它是如何工作的，它依赖什么才能正常运行？如果不能很好地回答这些问题，最好阅读一下这些出错程序的 [Archwiki](/index.php/Table_of_contents_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Table of contents (简体中文)") 文章。一旦你觉得你已经理解了它，你将更容易找出问题的原因。

### 常见问题 / 检查项

下面列出了许多常见问题，用于排查故障。在每个问题下都有注释，说明你该如何回答这个问题，紧接着的是一些如何收集数据的简单示例，还有查看各种日志的工具。

1.  出现了什么故障？

    	请尽可能精确地描述问题，这将帮助你在查找特定信息的时候不至感到困惑或扯到别的方面去。

2.  是否显示了错误信息？（如果有的话）

    	将包含相关 **错误信息** 的 *完整输出* 复制并粘贴到类似 `$HOME/issue.log` 这样单独的文件中。例如，可以将以下 [mkinitcpio](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)") 命令的输出转发到 `$HOME/issue.log`：

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  可以复现这个故障码？

    	如果是这样，请 **按步骤** 给出 *确切的* 指示/命令来做到这一点。

4.  第一次遇到这些故障的时间，以及从没有故障到故障发生之间你修改了什么内容？

    	如果这种情况发生在某次升级之后，可以列出 **所有已升级的包**。包括 *版本号*，同时粘贴 [pacman](/index.php/Pacman "Pacman").log (`/var/log/pacman.log`) 的升级日志。使用 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 的 systemctl 工具检查故障程序依赖的 *所有* 服务的运行状态。例如，可以将 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#systemd_.E5.9F.BA.E6.9C.AC.E5.B7.A5.E5.85.B7 "Systemd (简体中文)") 命令的输出转发到 `$HOME/issue.log`：

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **注意:** 使用 `**>>**` 可以保证 `$HOME/issue.log` 中之前保存的内容不会被覆盖。

### 寻求解决

不要通过这样的表述来寻求问题的解决：

*程序 X 不工作了。*

描述整个系统的环境更有助于解决问题，比如：

*应用程序 X 在执行 Z 任务时，会报出 Y 错误，条件是 A 和 B。*

### 额外支援

利用你眼前的所有信息，你应该对系统里发生了什么有一个较好的认识，并且可以开始着手修复了。

如果需要额外支援，[官方论坛](https://bbs.archlinux.org) 或 IRC （irc.freenode.net 上的 #archlinux 频道） 都可以提供帮助。更多频道可参考 [IRC channels](/index.php/IRC_channels "IRC channels")。

**注意:** [技术支持 *仅限于* Arch Linux](/index.php/Code_of_conduct_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E4.BB.85.E6.94.AF.E6.8C.81_Arch_Linux "Code of conduct (简体中文)") 而非 [基于 Arch 的发行版](/index.php/Arch-based_distributions_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Arch-based distributions (简体中文)")。

当要求贴出 **完整** 的 输出 / 日志 时，不能仅仅贴出你认为的重要部分。信息来源应该包括：

*   所有涉及到的命令的完整输出，不要只选择你认为相关的东西。
*   来自 systemd 的 `journalctl` 的输出。要获取更多的输出，请使用 `systemd.log_level=debug` 引导参数。
*   日志文件（看一下 `/var/log` 目录）
*   相关的配置文件
*   相关的驱动程序
*   相关软件包的版本
*   内核相关：`dmesg`。对于启动问题，至少贴出最后 10 行，多贴一些当然更好。
*   网络相关：相关命令的完整输出，再加上所有相关配置文件。
*   Xorg 相关： `/var/log/Xorg.0.log`，如果你已经覆盖了出问题的日志，就贴在这之前的日志。
*   Pacman 相关：如果最近的更新弄坏了什么东西，请到 `/var/log/pacman.log` 找它。

贴出这些信息有一个更好的方式，就是使用在线剪贴板 (pastebin)。你可以 [安装](/index.php/Install "Install") [pbpst](https://www.archlinux.org/packages/?name=pbpst) 或 [gist](https://www.archlinux.org/packages/?name=gist) 来自动上传信息。例如，要上传这次启动以来的 systemd 日志，可以这么做：

```
# journalctl -xb | pbpst -S

```

这将返回一个链接，你可以把它贴到论坛或 IRC。

另外，在提问之前，请先阅读 [提问的智慧](http://www.catb.org/esr/faqs/smart-questions.html) 和 [行为准则](/index.php/Code_of_conduct_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Code of conduct (简体中文)")。

## 系统启动问题

诊断 [启动过程](/index.php/Boot_process_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Boot process (简体中文)") 中的问题主要是修改 [内核参数](/index.php/Kernel_parameters_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel parameters (简体中文)")，然后重启系统。

如果系统无法启动，可以从 [live 镜像](https://www.archlinux.org/download/) 启动并 [chroot](/index.php/Change_root_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Change root (简体中文)") 到现有系统。

### 控制台的输出信息

在启动过程完成以后，屏幕会被清空并显示登录提示符，这使得用户无法看到初始化过程中的输出和其中的错误信息。这一默认特性可以使用接下来几节中的方法进行修改。

请注意，无论选择下面哪个方法，在启动后通过使用 `dmesg` 或 `journalctl -b` 都可以显示内核消息，用于检查错误。

#### 输出流控制

以下是适用于大多数终端模拟器的基本操作，包括虚拟终端 (vc)：

*   按 `Ctrl+S` 暂停输出
*   按 `Ctrl+Q` 继续输出

这样不仅会暂停输出，而且会暂停尝试打印到终端的程序，即暂停输出时会阻塞 `write()` 调用。 如果你的 *init* 进程出现冻结，请确保系统控制台没有暂停。

要查看已经显示过的错误信息，参见 [Getty#Have boot messages stay on tty1](/index.php/Getty#Have_boot_messages_stay_on_tty1 "Getty")。

#### 回滚显示

回滚显示允许用户查看已经从控制台滚动过去并消失的文字内容。这通常是在视频适配器和显示设备之间创建缓冲（称为回滚缓冲区）实现的。默认情况下，将缓冲的内容上下滚动的快捷键是 `Shift+PageUp` 和 `Shift+PageDown`。

如果回滚内容没有完全包含足够的信息，可能需要扩大回滚缓冲区的大小来容纳更多输出。这可以通过配置内核的 framebuffer console（fbcon，帧缓冲控制台）来实现，修改 [内核参数](/index.php/Kernel_parameter "Kernel parameter") `fbcon=scrollback:Nk` 即可，其中 `N` 是缓冲区大小，单位是 kB，默认是 32k。

如果这不奏效，你的 framebuffer console 可能没有正确地启用。参阅 [Framebuffer Console documentation](https://www.kernel.org/doc/Documentation/fb/fbcon.txt) 来查找其他影响参数，比如修改帧缓冲驱动。

#### Debug 输出

在启动时，大部分来自内核的消息都是隐藏的，可以加入不同的内核参数来输出更多信息。最简单的是这些：

*   `debug` 可以同时启用来自内核和 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 的调试信息
*   `ignore_loglevel` 强制显示 *所有* 内核消息

在特定情况下有用的其他参数如下：

*   `earlyprintk=vga,keep` 在早期启动过程中就输出内核消息，用于内核在有输出前就崩溃的情况下。在 [EFI](/index.php/Unified_Extensible_Firmware_Interface_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Unified Extensible Firmware Interface (简体中文)") 系统上要把 `vga` 改成 `efi`。
*   `log_buf_len=16M` 用于分配一个更大 (16MB) 的内核消息缓冲区，用来保证 debug 输出不被覆盖。

还有很多独立的调试参数，用于在特定的子系统中启用调试，例如 `bootmem_debug` 和 `sched_debug`。更多详细信息请参考 [kernel parameter documentation](https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt)。

**注意:** 如果无法回滚的足够远以查看所需的启动输出，你需要扩大 [回滚缓冲区](#.E5.9B.9E.E6.BB.9A.E6.98.BE.E7.A4.BA) 的大小。

### 故障恢复控制台

在启动过程中的某个阶段获取一个交互式 shell 可以帮助你准确找出问题出在哪里，以及为何失败。有几个内核参数可以做到这一点，但它们都启动了一个正常的shell，可以随时 `exit` 让内核恢复正在执行的操作：

*   `rescue` 在根文件系统刚刚被挂载为读写模式的时候启动一个 shell
*   `emergency` 可以在更早的时候启动 shell，早于大部分文件系统挂载之前
*   `init=/bin/sh`（作为最后的选择）把 init 程序改成 root shell。因为 `rescue` 和 `emergency` 都依赖于 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)")，而这可以在 *systemd* 坏掉的时候工作

还有一个选择，那就是 systemd 的 debug-shell，它在 `tty9` 上新增了一个 root shell，可以按 Ctrl+Alt+F9 来使用。这个功能可以通过在 [内核参数](/index.php/Kernel_parameters "Kernel parameters") 中添加 `systemd.debug-shell`，或者是 [启用](/index.php/Enabling "Enabling") `debug-shell.service` 来打开。注意在使用完后禁用该服务，避免在每次启动时都打开 root shell 而带来安全风险。

### Intel 显卡造成的黑屏

这很可能是 [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") 的问题造成的。尝试 [disabling modesetting](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting") 或者修改 [video port](/index.php/Intel#KMS_Issue:_console_is_limited_to_small_area "Intel")。

### 加载内核时卡住

尝试添加 `acpi=off` 内核参数来关闭 ACPI。

### 调试内核模块

参见 [Kernel modules#Obtaining information](/index.php/Kernel_modules#Obtaining_information "Kernel modules")。

### 调试硬件

*   按照 [udev#Debug output](/index.php/Udev#Debug_output "Udev") 的说明可以显示额外硬件调试信息。
*   确保你的系统已经安装了 [Microcode](/index.php/Microcode_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Microcode (简体中文)") 更新。
*   使用 [Memtest86+](http://www.memtest.org/) 来测试设备的 RAM，不可靠的 RAM 可能会导致一些非常奇怪的问题，从随机崩溃到数据损坏都有可能。

## 内核崩溃 (Kernel panics)

Linux 内核进入不可恢复的故障状态时，即发生了“内核崩溃” (*kernel panic*)。这种状态通常来源于错误的硬件驱动程序，导致内核死锁，无响应并需要重新启动。在死锁之前，会生成一条诊断消息，其中包括：发生崩溃时的*机器状态*，导致崩溃的内核函数的*调用栈*，以及当前加载的模块的列表。庆幸的是，使用 *mainline（主线）* 版本的内核（比如官方仓库提供的内核）不会经常发生内核崩溃，但是当它们发生时，你需要知道如何处理它们。

**注意:** Kernel panics 有时被称为 *oops* 或 *Kernel oops*，虽然 panics 和 oops 都是在出错的状态下才会发生，但是 *oops* 更为通用，因为它并不一定会导致内核死锁，有时内核可以通过结束出错的任务来恢复并继续运行。

**提示：** 在启动时传递参数 `oops=panic` 或者在 `/proc/sys/kernel/panic_on_oops` 中写入 `1` 来强制用 panic 代替可恢复的 oops。如果你认为自动恢复 oops 导致了小概率的系统不稳定，进而导致了后来的错误难以被诊断，那么建议你这样做。

### 查看 panic 信息

如果在早期启动过程中发生了 kernel panic，你或许会在控制台上看到包含 "Kernel panic - not syncing:" 的消息，一旦 [Systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 开始运行，内核消息就会被捕捉到并写入系统日志。但是，当 Kernel panic 发生时，内核发出的诊断信息 *几乎不会* 被写入硬盘上的日志文件，因为在 `system-journald` 运作前内核就死锁了。因此，检查内核崩溃消息的唯一方法是在崩溃时从控制台看错误信息（如果没有设置 *kdump crashkernel* 的话）。可以用以下内核参数来启动，这样就能重现 tty1 上的错误信息：

 `systemd.journald.forward_to_console=1 console=tty1` 
**提示：** 如果崩溃信息滚动得太快导致无法阅读，可以在启动时尝试添加 `pause_on_oops=*seconds*` 内核参数。

#### 示例场景：模块损坏

根据诊断信息，我们可以大致推断出是哪个子系统或者模块导致了崩溃。在这个示例中，我们假设机器在启动时发生了 panic。注意那些用 **粗体** 标记的行：

```
**kernel: BUG: unable to handle kernel NULL pointer dereference at (null)** [1]
**kernel: IP: fw_core_init+0x18/0x1000 [firewire_core]** [2]
kernel: PGD 718d00067 
kernel: P4D 718d00067 
kernel: PUD 7b3611067 
kernel: PMD 0 
kernel: 
kernel: Oops: 0002 [#1] PREEMPT SMP
**kernel: Modules linked in: firewire_core(+) crc_itu_t cfg80211 rfkill ipt_REJECT nf_reject_ipv4 nf_log_ipv4 nf_log_common xt_LOG nf_conntrack_ipv4 ...** [3] 
kernel: CPU: 6 PID: 1438 Comm: modprobe Tainted: P           O    4.13.3-1-ARCH #1
kernel: Hardware name: Gigabyte Technology Co., Ltd. H97-D3H/H97-D3H-CF, BIOS F5 06/26/2014
kernel: task: ffff9c667abd9e00 task.stack: ffffb53b8db34000
kernel: RIP: 0010:fw_core_init+0x18/0x1000 [firewire_core]
kernel: RSP: 0018:ffffb53b8db37c68 EFLAGS: 00010246
kernel: RAX: 0000000000000000 RBX: 0000000000000000 RCX: 0000000000000000
kernel: RDX: 0000000000000000 RSI: 0000000000000008 RDI: ffffffffc16d3af4
kernel: RBP: ffffb53b8db37c70 R08: 0000000000000000 R09: ffffffffae113e95
kernel: R10: ffffe93edfdb9680 R11: 0000000000000000 R12: ffffffffc16d9000
kernel: R13: ffff9c6729bf8f60 R14: ffffffffc16d5710 R15: ffff9c6736e55840
kernel: FS:  00007f301fc80b80(0000) GS:ffff9c675dd80000(0000) knlGS:0000000000000000
kernel: CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
kernel: CR2: 0000000000000000 CR3: 00000007c6456000 CR4: 00000000001406e0
kernel: Call Trace:
**kernel:  do_one_initcall+0x50/0x190** [4]
kernel:  ? do_init_module+0x27/0x1f2
kernel:  do_init_module+0x5f/0x1f2
kernel:  load_module+0x23f3/0x2be0
kernel:  SYSC_init_module+0x16b/0x1a0
kernel:  ? SYSC_init_module+0x16b/0x1a0
kernel:  SyS_init_module+0xe/0x10
kernel:  entry_SYSCALL_64_fastpath+0x1a/0xa5
kernel: RIP: 0033:0x7f301f3a2a0a
kernel: RSP: 002b:00007ffcabbd1998 EFLAGS: 00000246 ORIG_RAX: 00000000000000af
kernel: RAX: ffffffffffffffda RBX: 0000000000c85a48 RCX: 00007f301f3a2a0a
kernel: RDX: 000000000041aada RSI: 000000000001a738 RDI: 00007f301e7eb010
kernel: RBP: 0000000000c8a520 R08: 0000000000000001 R09: 0000000000000085
kernel: R10: 0000000000000000 R11: 0000000000000246 R12: 0000000000c79208
kernel: R13: 0000000000c8b4d8 R14: 00007f301e7fffff R15: 0000000000000030
kernel: Code: <c7> 04 25 00 00 00 00 01 00 00 00 bb f4 ff ff ff e8 73 43 9c ec 48 
kernel: RIP: fw_core_init+0x18/0x1000 [firewire_core] RSP: ffffb53b8db37c68
kernel: CR2: 0000000000000000
kernel: ---[ end trace 71f4306ea1238f17 ]---
**kernel: Kernel panic - not syncing: Fatal exception** [5]
kernel: Kernel Offset: 0x80000000 from 0xffffffff810000000 (relocation range: 0xffffffff800000000-0xfffffffffbffffffff
kernel: ---[ end Kernel panic - not syncing: Fatal exception
```

*   [1] 表明了导致 panic 的错误类型。此处表示一个程序 bug。
*   [2] 表明 panic 发生在 *firewire_core* 模块中的 *fw_core_init* 函数中。
*   [3] 表明 *firewire_core* 模块是最后一个要加载的模块。
*   [4] 表明调用 *fw_core_init* 的函数是 *do_one_initcall*。
*   [5] 表明这个 *oops* 消息事实上是一次 kernel panic 并且系统已经死锁。

我们可以猜测，panic 发生在模块 *firewire_core* 加载后的初始化例程中。（我们或许可以认为，由于程序错误，这台机器的火线 (IEEE 1394) 相关硬件与这一版本的驱动模块不兼容，并且需要等待下一个版本的驱动发布）与此同时，让机器运行起来的最简单方法，就是不要加载这个模块。我们可以通过以下两种方式之一来完成这个操作：

*   如果这个模块在加载 *initramfs* 时就会被加载，那就在重启时加上内核参数 `rd.blacklist=firewire_core`。
*   否则就用这个内核参数重启 `module_blacklist=firewire_core`。

### 重启至 root shell 并修复故障

为了更改系统设置使得 panic 不再发生，你需要一个 root shell。如果 panic 发生在启动时，有几种方法可以在内核死锁前获得一个 root shell：

*   使用内核参数 `emergency`、`rd.emergency` 或 `-b` 重启电脑，这样可以在根文件系统挂载且 `systemd` 启动后就收到登录提示符。

**注意:** 此时，根文件系统将会以**只读**方式挂载。执行 `# mount -o remount,rw /` 来改变这一设置。

*   使用内核参数 `rescue`、`rd.rescue`、`single`、`s`、`S` 或 `1` 在本地文件系统挂载完成后就得到登录提示符。
*   使用内核参数 `systemd.debug-shell=1` 在 tty9 上获得一个早期 root shell，然后按 `Ctrl-Alt-F9` 切换到它。
*   通过使用不同的内核参数重新引导来尝试禁用导致 panic 的内核功能。尝试“备用参数” `acpi=off` 和 `nolapic`。

**提示：** 参阅 Linux 内核源码树中的 `Documentation/admin-guide/kernel-parameters.txt` 文件来查找所有内核参数。

*   作为最后的手段，你还可以使用 **Arch Linux Installation CD** 启动电脑，把根文件系统挂载到 `/mnt`，然后运行 `# arch-chroot /mnt`。

禁用导致 panic 的服务或程序，回滚有故障的更新或修复配置问题。

## 软件包管理

参阅适用于一般主题的 [Pacman#Troubleshooting](/index.php/Pacman#Troubleshooting "Pacman")，以及适用于 PGP 密钥问题的 [pacman/Package signing#Troubleshooting](/index.php/Pacman/Package_signing#Troubleshooting "Pacman/Package signing")。

## fuser

*fuser* 是一个用于识别进程占用的资源（如打开的文件、文件系统和 TCP/UDP 端口）的命令行工具。

*fuser* 由软件包 [psmisc](https://www.archlinux.org/packages/?name=psmisc) 提供，已经由 [base](https://www.archlinux.org/groups/x86_64/base/) 组安装。更多信息请查看 [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1)。

## 会话权限

**注意:** 你必须使用 [systemd](/index.php/Systemd_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Systemd (简体中文)") 作为你的 init 进程，本地会话才能正常工作。[[1]](https://www.archlinux.org/news/d-bus-now-launches-user-buses/) 它是各种设备的 polkit 权限和 ACL 所必需的 （参见 `/usr/lib/udev/rules.d/70-uaccess.rules` 和 [[2]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/)）

首先，确保你有一个带 X 的可用本地会话：

```
$ loginctl show-session $XDG_SESSION_ID

```

在输出中需要带有 `Remote=no` and `Active=yes` 字样。如果没有，确保 X 运行在和登录时一样的 tty 里面。这是保留登录会话所必须的。

D-Bus 会话也必须随 X 一起启动。关于这个的更多信息参见 [D-Bus#Starting the user session](/index.php/D-Bus#Starting_the_user_session "D-Bus")。

基本 [polkit](/index.php/Polkit "Polkit") 操作不需要额外的配置。但有一些 polkit 操作需要请求额外的身份认证，即使是本地会话也是如此。为了达成这项工作，必须运行一个 polkit 身份认证组件。更多信息可参见 [polkit (简体中文)#身份认证组件](/index.php/Polkit_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E8.BA.AB.E4.BB.BD.E8.AE.A4.E8.AF.81.E7.BB.84.E4.BB.B6 "Polkit (简体中文)")。

## 错误信息： "error while loading shared libraries"

如果在运行程序时遇到类似于这样的错误：

```
error while loading shared libraries: libusb-0.1.so.4: cannot open shared object file: No such file or directory

```

使用 [pacman](/index.php/Pacman "Pacman") 或 [pkgfile](/index.php/Pkgfile "Pkgfile") 来查找包含丢失共享库的软件包：

 `$ pacman -Fs libusb-0.1.so.4` 
```
extra/libusb-compat 0.1.5-1
    usr/lib/libusb-0.1.so.4

```

在上述例子中，需要 [安装](/index.php/Installed "Installed") 软件包 [libusb-compat](https://www.archlinux.org/packages/?name=libusb-compat)。

这个错误也有可能意味着你用来安装这个软件的 [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") 里没有将这个共享库作为它的依赖库：如果来自官方源，请 [报告一个 bug](/index.php/Reporting_bug_guidelines_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Reporting bug guidelines (简体中文)")；如果来自 [AUR](/index.php/AUR "AUR")，请在 AUR 网站相关页面上把它报告给维护者。

## 错误信息： "file: could not find any magic files!"

如果看到这条消息，则可能表示软件包更新破坏了动态链接程序的运行时依赖文件，并且系统现在已经基本瘫痪。在修复之前，你将无法重新编译或重新安装软件包或重建 [initramfs](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")。

### 错误原因

某次软件更新可能在 `/etc/ld.so.conf.d` 目录中添加了非法的 `*filename*.conf` 文件，或是错误地编辑了 `/etc/ld.so.conf` 文件。其后果就是动态链接程序的运行时依赖文件 `/etc/ld.so.cache` 使用了错误的数据重新生成了。这可能导致系统中所有依赖共享库的程序都出错（即几乎所有程序出错）。

### 解决方法

1.  使用 ***Arch Linux Installation CD*** 启动。
2.  挂载根文件系统 `/` 到 `/mnt`，挂载 `/boot` 文件系统到 `/mnt/boot`，然后用命令 `# arch-chroot /mnt` 切换到受损的系统中。
3.  检查 `/etc/ld.so.conf` 文件，删除所有不正确的内容。
4.  检查放在 `/etc/ld.so.conf.d/` 目录里的文件，删除所有不正确的文件。
5.  使用命令 `# ldconfig` 重新生成动态链接程序的运行时依赖文件 `/etc/ld.so.cache`。
6.  使用命令 `# mkinitcpio -p linux` 重新生成 [Initramfs](/index.php/Mkinitcpio_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Mkinitcpio (简体中文)")。
7.  退出 chroot 环境，卸载文件系统，然后重启到原来的系统中。

## 参阅

*   [Fix the Most Common Problems](http://www.tuxradar.com/content/how-fix-most-common-linux-problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)
*   [List of Tools for UBCD](http://wiki.ultimatebootcd.com/index.php?title=Tools) - Memtest-like tools to add to grub.cfg on UltimateBootCD.com
*   [Wikipedia:BIOS Boot partition](https://en.wikipedia.org/wiki/BIOS_Boot_partition "wikipedia:BIOS Boot partition")
*   [REISUB](/index.php/REISUB "REISUB")
*   [Debug Logging to a Serial Console](http://freedesktop.org/wiki/Software/systemd/Debugging#Debug_Logging_to_a_Serial_Console) on Freedesktop.org
*   [How to Isolate Linux ACPI Issues](https://web.archive.org/web/20120217124742/http://www.lesswatts.org/projects/acpi/debug.php) on Archive.org