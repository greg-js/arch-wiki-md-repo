本文描述了如何安装、配置和使用**lm_sensors**来监控CPU和主板温度以及风扇速度。

# 安装lm_sensors

使用Pacman安装软件包

```
# pacman -S lm_sensors

```

# 配置lm_sensors

使用**sensors-detect**检测并生成内核模块列表

```
# sensors-detect

```

这将在**/etc/sysconfig/lm_sensors**里创建配置

在**/etc/rc.conf**的DAEMONS列表里加入**sensors**，使得启动时自动加载内核模块：

```
DAEMONS=(syslog-ng crond ... sensors ...)

```

为了测试配置是否成功，现在就运行初始化脚本加载内核模块

```
# /etc/rc.d/sensors start

```

然后执行**sensors**命令

```
$ sensors

```

你会看到象这样的输出显式：

```
lm85-i2c-0-2e
Adapter: SMBus I801 adapter at c800
V1.5:       +1.47 V  (min =  +0.00 V, max =  +3.32 V)
VCore:      +1.34 V  (min =  +0.00 V, max =  +2.99 V)
V3.3:       +3.32 V  (min =  +0.00 V, max =  +4.38 V)
V5:        +5.05 V  (min =  +0.00 V, max =  +6.64 V)
V12:      +11.94 V  (min =  +0.00 V, max = +15.94 V)
CPU_Fan:   1760 RPM  (min =    0 RPM)
fan2:         0 RPM  (min =    0 RPM)
fan3:         0 RPM  (min =    0 RPM)
fan4:         0 RPM  (min =    0 RPM)
CPU Temp:    +51°C  (low  =  -127°C, high =  +127°C)
Board Temp:
             +46°C  (low  =  -127°C, high =  +127°C)
Remote Temp:
             +45°C  (low  =  -127°C, high =  +127°C)
CPU_PWM:    77 
Fan2_PWM:   87 
Fan3_PWM:   87 
vid:      +1.088 V  (VRM Version 10.0)

```

# 使用lm_sensors

现在你应该可以使用lm_sensors的前端工具程序如**gkrellm**、**xfce4-sensors-plugin**、**GNOME Computer Temperature Monitor**以及**ksensors**。