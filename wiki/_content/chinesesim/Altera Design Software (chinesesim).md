Quartus是[altera](http://www.altera.com.cn)公司推出的，针对Altera公司的可编程器件设计套件。可针对Altera全系列产品综合、适配、仿真、下载。适用于Windows、Linux、SunOS等平台。针对Windows平台有免费的网络版，针对所有平台有可免费适用一个月的订购版。具体可参考其官方网站！

## 下载安装

Quartus II 可以从Altera官方网站下载，下载地址： [[1]](ftp://ftp.altera.com/outgoing/release/)

*   准备一个空闲空间大于7G的空间，用于下载和解压Quartus：

```
$mkdir ~/quartus

```

*   下载Quartus II 9.0 For Linux

```
$wget [ftp://ftp.altera.com/outgoing/release/90_quartus_linux.tar](ftp://ftp.altera.com/outgoing/release/90_quartus_linux.tar)

```

这里会下载很长很长很长一段时间，想一想普通的ADSL上线300K Vs 3000MB，所以这个时候你可以出去吃饭了，吃完回来差不多该下载完了。

*   依赖关系，Quartus使用的是tcsh，所以需要先安装tcsh

```
#pacman -S tcsh

```

*   安装

```
$cd ~/quartus
#./install

```

*   注意这里安装需要用root权限，安装过程很简单，需要回答三个问题：

1.  安装位置，默认是*/opt/altera9.0/*
2.  器件仿真库选择，默认是全部库，你可以选择其中一个或者几个，比如*cycii cyciii*代表选择cyclone II和cyclone III
3.  阅读授权文件

到这里，就安装完成了，但是这时还不能立即使用。必须作下一步的处理，如果不处理，就会出现[#常见错误 莫名其妙的错误](#常见错误_莫名其妙的错误)

## 安装后的处理

*   首先，去掉/etc/issue中为inputrc设置的特殊字符（用于agent启动的自动清屏的）：

```
echo "Arch Linux  \r  (
) (\l)" > /etc/issue

```

*   然后，检查一下你的主机名是否已经添加到/etc/hosts了，如果没有一定要加上

```
echo "127.0.0.1 myhost.localdomain myhost" >> /etc/hosts

```

用你自己的IP地址和主机名替换掉上面的127.0.0.1和myhost