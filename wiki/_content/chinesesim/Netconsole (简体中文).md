**netconsole** 是一个通过网络发送所有内核日志消息（即dmesg）到另一台计算机的内核模块，且无需用户空间（如syslogd的）。 "netconsole" 这个名字不是很恰当，因为它不是一个真正的“控制台”，更像是一个远程日志服务。

它可以内建或者编译成模块使用.内建式的*netconsole*在网卡后立即初始化以尽快建立指定的接口. 模块方式一般用于获取无屏幕系统或用户空间无法工作时的 kernel panic 输出

文档位于内核代码当中：**[Documentation/networking/netconsole.txt](http://lxr.linux.no/linux+v2.6.32/Documentation/networking/netconsole.txt)**

## Contents

*   [1 发送器配置](#.E5.8F.91.E9.80.81.E5.99.A8.E9.85.8D.E7.BD.AE)
    *   [1.1 内建配置](#.E5.86.85.E5.BB.BA.E9.85.8D.E7.BD.AE)
    *   [1.2 运行时配置](#.E8.BF.90.E8.A1.8C.E6.97.B6.E9.85.8D.E7.BD.AE)
*   [2 接收器配置](#.E6.8E.A5.E6.94.B6.E5.99.A8.E9.85.8D.E7.BD.AE)
*   [3 引导时启动](#.E5.BC.95.E5.AF.BC.E6.97.B6.E5.90.AF.E5.8A.A8)

## 发送器配置

Install [gnu-netcat](https://www.archlinux.org/packages/?name=gnu-netcat) from the [official repositories](/index.php/Official_repositories "Official repositories").

### 内建配置

*Netconsole* and other modules' [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") can be passed from a bootloader to kernel at its startup via kernel command line by modifying the bootloader environment, which is type and version specific. Example for Uboot, where 1st address is Plug Computer ArchLinux device's netconsole Out Port & IP, and 2nd address is your PC's netconsole In Port & IP & adapter MAC:

```
fw_setenv usb_custom_params 'loglevel=7 netconsole=6666@192.168.1.28/eth0,6666@192.168.1.19/00:13:32:20:r9:a5'

```

Logging is done by your ArchLinux set logger like *syslog-ng*, so available loglevels (output details) are defined in that logger docs, and may differ for each log type. One can also pass *netconsole* string parameters at kernel runtime (no config file required), then start two *netconsole* instances on the monitoring PC (one to read output, another for input), and restart it on the PC or device you are logging as shown in *Dynamic Configuration*:

```
# set log level for kernel messages
dmesg -n 8

netconsole=6666@192.168.1.28/eth0,6666@192.168.1.19/00:13:32:20:r9:a5

nc -l -u -p 6666 &
nc -u 192.168.1.28 6666

```

One may need to switch off PC and router firewall, and setup proper router port forwarding to monitor and input data in *Netconsole*.

### 运行时配置

Netconsole can be loaded as one of *kernel modules* manually after boot or auto during boot depending on this module config. See [kernel modules](/index.php/Kernel_modules "Kernel modules") for configuring it to load at boot. For loading manually any time after boot:

```
# set log level for kernel messages
dmesg -n 8

modprobe configfs
modprobe netconsole
mount none -t configfs /sys/kernel/config

# 'netconsole' dir is auto created if the module is loaded 
mkdir /sys/kernel/config/netconsole/target1
cd /sys/kernel/config/netconsole/target1

# set local IP address
echo 192.168.0.111 > local_ip
# set destination IP address
echo 192.168.0.17 > remote_ip
# find destination MAC address
arping `cat remote_ip` -f |grep -o ..:..:..:..:..:.. > remote_mac

echo 1 > enabled

```

netconsole should now be configured. To verify, run 'dmesg |tail' and you should see "netconsole: network logging started". Check available log levels by running 'dmesg -h'.

## 接收器配置

```
nc -u -l 6666

```

or

```
nc -u -l -p 6666

```

## 引导时启动

只需将 netconsole 添加到内核引导命令行即可。内核按下列格式读取 "netconsole" 字符串参数：

```
  netconsole=[src-port]@[src-ip]/[<dev>],[tgt-port]@<tgt-ip>/[tgt-macaddr]
        src-port      source for UDP packets (defaults to 6665)
        src-ip        source IP to use (interface address)
        dev           network interface (eth0)
        tgt-port      port for logging agent (6666)
        tgt-ip        IP address for logging agent
        tgt-macaddr   ethernet MAC address for logging agent (broadcast)
```

例如：

```
linux /vmlinuz-linux root=UUID=a322511e-b028-4f11-87b6-e48b5d99bbd8 ro netconsole=514@10.0.0.1/eth1,514@10.0.0.2/12:34:56:78:9a:bc
linux /vmlinuz-linux root=/dev/disk/by-label/ROOT ro netconsole=514@10.0.0.2/12:34:56:78:9a:bc

```

引自： [Net Console for Boot Debugging](/index.php/Boot_debugging#Net_Console "Boot debugging").