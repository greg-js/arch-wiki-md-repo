Bootchart 是一个分析Linux启动流程的方便工具，结果可以用来优化启动速度。包含 bootchartd 服务和负责生成分析结果的 bootchart-render 两部分。

**注意:** Bootchart 已经成为 systemd 的一部分，请参考 [Systemd#Optimization](/index.php/Systemd#Optimization "Systemd") 页面。

## Contents

*   [1 安装Bootchart](#.E5.AE.89.E8.A3.85Bootchart)
*   [2 运行Bootchart](#.E8.BF.90.E8.A1.8CBootchart)
    *   [2.1 启动引导器设置](#.E5.90.AF.E5.8A.A8.E5.BC.95.E5.AF.BC.E5.99.A8.E8.AE.BE.E7.BD.AE)
*   [3 生成分析结果图表](#.E7.94.9F.E6.88.90.E5.88.86.E6.9E.90.E7.BB.93.E6.9E.9C.E5.9B.BE.E8.A1.A8)
    *   [3.1 问题解决](#.E9.97.AE.E9.A2.98.E8.A7.A3.E5.86.B3)
*   [4 参考资料](#.E5.8F.82.E8.80.83.E8.B5.84.E6.96.99)

## 安装Bootchart

[bootchart](https://www.archlinux.org/packages/?name=bootchart)可以在源里找到.

**注意:** 另外一个可供选择的是 [bootchart2](https://github.com/mmeeks/bootchart).它使用python来生成最终的图表而不是JVM.

## 运行Bootchart

要使bootchart运行，你需要将他添加到引导器的初始化进程选项，或者手动在init脚本（通常是rc.sysinit）中手动添加。不过需要注意的是，如果你是手动添加到init脚本的，那么也要手动停止它，总之，这种情况需要特别留意！

### 启动引导器设置

下面我们介绍常用的方法，即将原有引导选项复制一份，并在内核项后面添加`init=/usr/bin/bootchartd`. 方法参阅[kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). 然后通过启动引导器引导bootchart。这样bootchart会在登录提示符出现的时候自动停止。

## 生成分析结果图表

你可以通过运行下面的命令来生成分析结果图：

```
bootchart-render

```

确保运行命令的目录有写权限，程序就会生成一个名为'bootchart.png'的图像，这就是分析结果图。

你需要事先安装Java运行环境并且在此之前设置正确。

### 问题解决

Bootchart-render 如果无法生成 'bootchart.png' 图片并显示如下错误信息：

```
/var/log/bootchart.tgz not found

```

主要原因是 bootchartd 无法检测到启动过程何时停止。如该使用非 KDM 或 GDM 的启动管理器如 [SLIM](/index.php/SLiM_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "SLiM (简体中文)") 或 entrance 时会发生这个问题。可以打开 `/sbin/bootchartd` 脚本并将这些程序加到 `exit_proc` 变量中：

```
# The processes we have to wait for
local exit_proc="gdmgreeter gdm-binary kdm_greet kdm slim"

```

如果没有使用启动管理器，修改 `exit_proc` 变量为：

```
# The processes we have to wait for
local exit_proc="login"

```

## 参考资料

*   [Bootchart主页](http://www.bootchart.org/)
*   [如何快速启动上网本的 LWN 文章](http://lwn.net/Articles/299483/) 写得很好，提供了许多快速启动的技巧，尽管许多不适合一般用户使用。(修改 X.org 内核 kernel 等)。