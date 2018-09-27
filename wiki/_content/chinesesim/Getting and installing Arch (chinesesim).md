此分类中的文章介绍各种下载和安装 Arch Linux 的方法。

最新的官方Arch Linux安装媒介和他们的[GnuPG](/index.php/GnuPG "GnuPG")签名可以从 [下载页面](https://archlinux.org/download/)获取。ISO 镜像文件同时支持32位与64位构架。

## 验证安装文件

安装镜像有数字签名，强烈建议安装前校验签名。尤其是 HTTP 镜像中的文件可能被恶意篡改。在一个已经安装 [GnuPG](/index.php/GnuPG "GnuPG") 的系统上，下载 *PGP signature* (在校验和下面），把它放到 *.iso* 相同的文件夹下。在Arch Linux上，运行`pacman-key -v *iso-file*.sig`命令；在其他环境上，运行`gpg2 --verify *iso-file.sig*`。

如果没有找到公钥，gpg2校验会失败，可以通过 `gpg --recv-keys *key id*` 进行[导入](http://sparewotw.wordpress.com/2012/10/31/how-to-verify-signature-using-sig-file/).

## 安装方式

下面表格汇总了各种安装方式，安装的时候需要连接网络下载安装包。如果没有网络，请参考[离线安装](/index.php/Offline_installation_of_packages "Offline installation of packages")。

| 方法 | 文章 | 条件 |
| 将镜像写入 U 盘或光盘，然后启动. | 

*   [USB flash installation media](/index.php/USB_flash_installation_media "USB flash installation media")
*   [Optical disc drive#Burning](/index.php/Optical_disc_drive#Burning "Optical disc drive")

 | 

*   安装一台或较少数量
*   可以直接从系统启动

 |
| 在服务器机器上挂载镜像，客户端通过网络启动. | 

*   [PXE](/index.php/PXE "PXE")
*   [Diskless system](/index.php/Diskless_system "Diskless system")

 | 

*   客户端-服务器模式
*   网络速度较好

 |
| 在 Linux 系统中挂载安装镜像，从 chroot 环境安装 Arch. | 

*   [Install from existing Linux](/index.php/Install_from_existing_Linux "Install from existing Linux")
*   [Install from SSH](/index.php/Install_from_SSH "Install from SSH")

 | 

*   短时间就可以替换已经存在的系统
*   在本地机器上安装，或者通过 [VNC](/index.php/VNC "VNC") 或 [SSH](/index.php/SSH "SSH") 安装

 |
| 建立虚拟环境，并在虚拟机中安装 Arch. | 

*   [Category:Hypervisors](/index.php/Category:Hypervisors "Category:Hypervisors")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

 | 

*   操作系统要和虚拟机兼容
*   获取隔离的系统，进行学习、测试或者测试

 |

## 参阅

*   [README.transfer](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer)
*   [README.altbootmethods](https://projects.archlinux.org/archiso.git/tree/docs/README.altbootmethods)