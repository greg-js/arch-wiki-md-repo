**WARNING: 这将建立一个没有密码的VNC. 意思是任何人都可以通过网络访问你的VNC并且能看到你的X界面.可以非常简单的通过SSH连接来避免这样的事情.**

## Contents

*   [1 设置 x11vnc](#.E8.AE.BE.E7.BD.AE_x11vnc)
    *   [1.1 安装](#.E5.AE.89.E8.A3.85)
    *   [1.2 运行](#.E8.BF.90.E8.A1.8C)
        *   [1.2.1 startx](#startx)
        *   [1.2.2 GDM](#GDM)
    *   [1.3 访问](#.E8.AE.BF.E9.97.AE)
*   [2 SSH端口转发](#SSH.E7.AB.AF.E5.8F.A3.E8.BD.AC.E5.8F.91)

## 设置 x11vnc

### 安装

```
pacman -S x11vnc

```

### 运行

首先你需要运行一个x server服务器. 使用startx 或类似的. 完成后运行

#### startx

```
x11vnc -display :0 -auth ~/.Xauthority

```

如果失败，你可能需要作为root来运行

```
x11vnc -display :0 -autho /home/USER/.Xauthority

```

where USER is the username of the user who is running the X server.

#### GDM

作为root, 运行

```
x11vnc -display :0 -auth /var/lib/gdm/:0.Xauth

```

### 访问

在其他机器运行VNC客户端, 然后输入运行了x11vnc服务器的IP地址. 点击连接, 然后你需要设置.

## SSH端口转发

为了安全地使用`x11vnc`，您首先需要安装并且配置好[SSH](/index.php/SSH "SSH")。

在启动`x11vnc`的时候，指定命令行选项“`-localhost`”，这将导致VNC服务只能绑定到本地网络界面。此时从外界直接连入的连接将被拒绝。

当您需要从另一台电脑上访问这个VNC服务的时候，首先用[SSH](/index.php/SSH "SSH")登录到运行VNC的主机，将VNC服务监听的端口转发到您的本地主机。以下的例子中假设运行VNC的主机名为"foo"，VNC监听5900端口上：

```
ssh foo -L 5900:localhost:5900

```

SSH连接建立以后，打开VNC客户端程序，但是不要让它连接到foo的5900端口，而是连接到本机（localhost）的5900端口。

这样，您就可以通过加密渠道安全地访问远程X服务了。