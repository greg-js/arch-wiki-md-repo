来自 [CUPS' site](http://www.cups.org/index.php):

	"*[CUPS](https://en.wikipedia.org/wiki/CUPS "wikipedia:CUPS") 是苹果公司为Mac OS® X 和其他类 UNIX® 的操作系统开发的基于标准的、开源的打印系统*".

虽然有其他的打印程序包例如LPRNG，但CUPS是相当流行和相对容易使用的。它是Arch linux及许多其他Linux发行版缺省的打印系统。

## Contents

*   [1 安装 CUPS](#.E5.AE.89.E8.A3.85_CUPS)
    *   [1.1 打印机驱动](#.E6.89.93.E5.8D.B0.E6.9C.BA.E9.A9.B1.E5.8A.A8)
        *   [1.1.1 下载PPD文件](#.E4.B8.8B.E8.BD.BDPPD.E6.96.87.E4.BB.B6)
*   [2 配置](#.E9.85.8D.E7.BD.AE)
    *   [2.1 Kernel Modules](#Kernel_Modules)
    *   [2.2 USB 打印机](#USB_.E6.89.93.E5.8D.B0.E6.9C.BA)
        *   [2.2.1 Parallel port printers](#Parallel_port_printers)
        *   [2.2.2 Auto-loading](#Auto-loading)
    *   [2.3 CUPS 守护进程](#CUPS_.E5.AE.88.E6.8A.A4.E8.BF.9B.E7.A8.8B)
    *   [2.4 Web 接口和工具](#Web_.E6.8E.A5.E5.8F.A3.E5.92.8C.E5.B7.A5.E5.85.B7)
        *   [2.4.1 CUPS administration](#CUPS_administration)
        *   [2.4.2 Remote access to web interface](#Remote_access_to_web_interface)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Problems resulting from upgrades](#Problems_resulting_from_upgrades)
        *   [3.1.1 CUPS stops working](#CUPS_stops_working)
        *   [3.1.2 Error with gnutls](#Error_with_gnutls)
        *   [3.1.3 All jobs are "stopped"](#All_jobs_are_.22stopped.22)
        *   [3.1.4 All jobs are "The printer is not responding"](#All_jobs_are_.22The_printer_is_not_responding.22)
        *   [3.1.5 The PPD version is not compatible with gutenprint](#The_PPD_version_is_not_compatible_with_gutenprint)
    *   [3.2 Other](#Other)
        *   [3.2.1 CUPS permission errors](#CUPS_permission_errors)
        *   [3.2.2 HPLIP printer sends "/usr/lib/cups/backend/hp failed" error](#HPLIP_printer_sends_.22.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed.22_error)
        *   [3.2.3 hp-toolbox sends an error, "Unable to communicate with device"](#hp-toolbox_sends_an_error.2C_.22Unable_to_communicate_with_device.22)
        *   [3.2.4 CUPS returns '"foomatic-rip" not available/stopped with status 3' with a HP printer](#CUPS_returns_.27.22foomatic-rip.22_not_available.2Fstopped_with_status_3.27_with_a_HP_printer)
        *   [3.2.5 Printing fails with unauthorised error](#Printing_fails_with_unauthorised_error)
        *   [3.2.6 Print button greyed-out in GNOME print dialogs](#Print_button_greyed-out_in_GNOME_print_dialogs)
        *   [3.2.7 Unknown supported format: application/postscript](#Unknown_supported_format:_application.2Fpostscript)
        *   [3.2.8 Finding URIs for Windows Print Servers](#Finding_URIs_for_Windows_Print_Servers)
        *   [3.2.9 Print-Job client-error-document-format-not-supported](#Print-Job_client-error-document-format-not-supported)
        *   [3.2.10 /usr/lib/cups/backend/hp failed](#.2Fusr.2Flib.2Fcups.2Fbackend.2Fhp_failed)
        *   [3.2.11 Samsung Printer won't print certain documents](#Samsung_Printer_won.27t_print_certain_documents)
        *   [3.2.12 Local USB printer does not show up](#Local_USB_printer_does_not_show_up)
        *   [3.2.13 "Unable to get list of printer drivers"](#.22Unable_to_get_list_of_printer_drivers.22)
*   [4 Appendix](#Appendix)
    *   [4.1 Alternative CUPS interfaces](#Alternative_CUPS_interfaces)
*   [5 PDF virtual printer](#PDF_virtual_printer)
    *   [5.1 Print to PostScript](#Print_to_PostScript)
    *   [5.2 Another source for printer drivers](#Another_source_for_printer_drivers)
*   [6 Resources](#Resources)

## 安装 CUPS

首先要安装这3个包[cups](https://www.archlinux.org/packages/?name=cups), [ghostscript](https://www.archlinux.org/packages/?name=ghostscript),以及 [gsfonts](https://www.archlinux.org/packages/?name=gsfonts)，从[官方软件仓库](/index.php/%E5%AE%98%E6%96%B9%E8%BD%AF%E4%BB%B6%E4%BB%93%E5%BA%93 "官方软件仓库")中[安装](/index.php/%E5%AE%89%E8%A3%85 "安装")它们。

如果正常的cups不起作用，你可以试试从 [AUR](/index.php/AUR "AUR") 安装　[cups-usblp](https://aur.archlinux.org/packages/cups-usblp/) 。

*   **cups** - 就是传说中的CUPS软件
*   **ghostscript** - Postscript语言的解释器
*   **gsfonts** - Ghostscript标准Type1字体
*   **hpoj** - 如果你使用 HP Officejet, 你应该再安装这个包，遵循指导避免发生错误. 更多信息见 [thread at launchpad/hplip](http://answers.launchpad.net/hplip/+question/133425).

如果你的系统要通过 [Samba](/index.php/Samba "Samba") 使用网络打印机，或者这台机器要作为打印服务器向其它windows客户端提供服务，你还需要安装[samba](https://www.archlinux.org/packages/?name=samba).

### 打印机驱动

这是一些驱动包。根据你的打印机选择合适的包安装。

*   **[gutenprint](https://www.archlinux.org/packages/?name=gutenprint)** - 一组质量非常好的驱动集合，支持的目标机型包括 Canon, Epson, Lexmark, Sony, Olympus；以及配合CUPS/GhostSscript/Foomatic/GIMP使用的 PCL printers。
*   **[foomatic-db](https://www.archlinux.org/packages/?name=foomatic-db), [foomatic-db-engine](https://www.archlinux.org/packages/?name=foomatic-db-engine),[foomatic-db-nonfree](https://www.archlinux.org/packages/?name=foomatic-db-nonfree), and [foomatic-filters](https://www.archlinux.org/packages/?name=foomatic-filters)** - Foomatic 是一个基于数据库的，集成自由软件打印机驱动和脱机打印程序的系统。安装 foomatic-filters 可以解决 cups error_log 报告错误 "stopped with status 22!".
*   **[foo2zjs](https://aur.archlinux.org/packages/foo2zjs/)** - Drivers for ZjStream protocol printers such as the HP Laserjet 1018\. More info [here](http://foo2zjs.rkkda.com), Foo2zsj is available in the [foo2zjs](https://aur.archlinux.org/packages/foo2zjs/).
*   **[hplip](https://www.archlinux.org/packages/?name=hplip)** - HP GNU/Linux 驱动. 支持 DeskJet, OfficeJet, Photosmart, Business Inkjet 和一些 LaserJet printer 型的, 以及一些兄弟打印机。
*   **[splix](https://www.archlinux.org/packages/?name=splix)** - 三星驱动，支持SPL打印机(SPL：Samsung Printer Language) (USB打印机要配合使用 [AUR](/index.php/AUR "AUR") 的 [cups-usblp](https://aur.archlinux.org/packages/cups-usblp/) )
*   **[cndrvcups-lb](https://aur.archlinux.org/packages/cndrvcups-lb/)** - 佳能 UFR2 驱动，支持LBP, iR 和 MF 系列打印机. 在 [AUR](/index.php/AUR "AUR") 能找到这个包。
*   **[cups-pdf](https://www.archlinux.org/packages/?name=cups-pdf)** - PDF虚拟打印机，这个东西可以把发送给他的打印任务输出为PDF文件。

If unsure of what driver package to install or if the current driver is not working, it may be easiest to just install all of drivers, since some of the packages are misleading because printers of other makes may rely on them. For instance, the Brother HL-2140 needs the hplip driver installed.

#### 下载PPD文件

取决于你的打印机，不一定需要进行这个步骤，如果没什么问题可以直接跳到下一节进行配置了。因为标准的CUPS安装已经携带了很多PPD(Postscript Printer Description)。 另外，*foomatic-filters*, *gimp-print* and *hplip* 已经自带了很多 PPD 文件，CUPS会自动检测他们.

这是一句来自 "Linux 打印网站" 的内容解释什么是 PPD 文件:

	"*For every PostScript printer the manufacturers provide a PPD file which contains all printer-specific information about the particular printer model: Basic printer capabilities as whether the printer is a color printer, fonts, PostScript level, etc., and especially the user-adjustable options, as paper size, resolution, etc.*"

如果打印机需要的PPD文件 *不* 在CUPS中, 那么:

*   去 [AUR](/index.php/AUR "AUR") 寻找为打印机/制造商提供的包。
*   去这个网站 [OpenPrinting database](http://www.openprinting.org/printers) 选择你需要的制造商和型号。
*   浏览制造商的网站寻找GNU/Linux驱动程序。

**注意:** PPD文件放在这个路径 `/usr/share/cups/model/`

## 配置

现在CUPS已经安装好了, 有很多选择可以供你安装一个打印机实例. 一直以来你都可以选用非常可靠的命令行的方式. 同样，Gnome和KDE也都提供了实用的用户界面的配置工具. 为了让最广大的群众方便地配置成功，本文将解释CUPS提供的web界面.

如果你要连接到一个网络打印机而不是直接连到你机器上的, 你应该先读一读这一页 [CUPS printer sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing"). 在GNU/Linux系统间共享打印机非常简单，只需要少许配置，而在linux和Windows之间共享打印机就需要多费一些功夫了.

USB printers can get accessed with two methods: The usblp kernel module and libusb. The former is the classic way. It is simple: Data is sent to the printer by writing it to a device file as a simple serial data stream. Reading the same device file allows bi-di access, at least for things like reading out ink levels, status, or printer capability information (PJL). It works very well for simple printers, but for multi-function devices (printer/scanner) it is not suitable and manufacturers like HP supply their own backends. (source: [here](http://lists.linuxfoundation.org/pipermail/printing-architecture/2012/002412.html))

### Kernel Modules

我们首先需要安装合适的内核模块才能使用web界面。以下是一些相关的步骤。

根据你使用的不同内核，这些步骤不一定是必要的. 当你连上打印机时内核会自动加载合适的模块. 用 `tail` 命令 (后文会说明) 看看打印机是否已经连上了。 `lsmod` 命令可以查看哪些模块已经被加载了。

### USB 打印机

USB printer users may need to blacklist the `usblp` module. Keep in mind that there seems to be a lot of [uncertainty](https://bbs.archlinux.org/viewtopic.php?pid=660601) regarding blacklisting `usblp`, as some USB printers, including some Canon and Epson printer series, are not recognized without it. Several user reported issues with Samsung printers when using `cups` with blacklisted `usblp` module, the solution was to re-enable `usblp` and install `cups-usblp` from aur instead of regular `cups` package ([https://bbs.archlinux.org/viewtopic.php?pid=778104](https://bbs.archlinux.org/viewtopic.php?pid=778104))

To blacklist the module:

 `/etc/modprobe.d/blacklist.conf`  `blacklist usblp` 

Custom kernel users may need to manually load the `usbcore` module before proceeding:

```
# modprobe usbcore

```

Once the modules are installed, plug in the printer and check if the kernel detected it by running the following:

```
# tail /var/log/messages.log

```

or

```
# dmesg

```

If you're using `usblp`, the output should indicate that the printer has been detected like so:

```
Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

If you blacklisted `usblp`, you will see something like:

```
usb 3-2: new full speed USB device using uhci_hcd and address 3
usb 3-2: configuration #1 chosen from 1 choice

```

#### Parallel port printers

To use a parallel port printer the configuration is pretty much the same, except for the modules:

```
# modprobe lp
# modprobe parport
# modprobe parport_pc

```

Once again, check the setup by running:

```
# tail /var/log/messages.log

```

It should display something like this:

```
lp0: using parport0 (polling).

```

If you are using a USB to parallel port adapter, CUPS will not be able to detect the printer. As a workaround, add the printer using a different connection type and then change DeviceID in /etc/cups/printers.conf:

```
DeviceID = parallel:/dev/usb/lp0

```

#### Auto-loading

It is convenient to have the system automatically load the kernel module every time the it starts up. To do so, use a text editor to open up `/etc/[rc.conf](/index.php/Rc.conf "Rc.conf")` and add the appropriate module to the `MODULES=()` line. Here is an example:

```
MODULES=(!usbserial scsi_mod sd_mod snd-ymfpci snd-pcm-oss **lp parport parport_pc** ide-scsi)

```

### CUPS 守护进程

相关的内核模块安装后，你就可以启动[start the cupsd daemon](/index.php/Daemon#Performing_daemon_actions_manually "Daemon")。添加“cupsd”到你的[DAEMONS array](/index.php/Daemons#Starting_on_Boot "Daemons")后它就可以开机自动启动。

### Web 接口和工具

只要cupsd这个服务在线了, 你就可以打开浏览器前往: [http://localhost:631](http://localhost:631) (*The **localhost** string may need to be replaced with the hostname found in* `/etc/hostname`).

从这开始，跟着向导就可以一步步地添加打印机了. 一般的步骤是点击 *Adding Printers and Classes* -> *Add Printer*. 提示需要用户名和密码时，使用root账户。然后让你填写的哪些描述性信息都无关紧要。紧接着，一个列表会提示你选择打印机型号。 Finally, choose the appropriate drivers and the configuration is complete.

配置好以后，点击 *Maintenance* 下拉菜单，然后点击 *Print Test Page* 打印一个测试页。如果打印不正常则说明存在一些配置的问题，问题很可能是选择的驱动不合适。

**Tip:** See: [#Alternative CUPS interfaces](#Alternative_CUPS_interfaces) for other other frontends.

**Note:** When setting up a USB printer, you should see your printer listed on *Add Printer* page. If you can only see a "SCSI printer" option, it probably means that CUPS has failed to recognize your printer.

#### CUPS administration

A user-name and password will be required when administering the printer in the web interface, such as: adding or removing printers, stopping print tasks, etc. The default user-name is the one assigned in the *sys* group, or root (change this by editing `/etc/cups/cupsd.conf` in the line of *SystemGroup*).

If the root account has been locked (i.e. when using sudo), it is not possible to log in the CUPS administration interface with the default user-name and password. In this case, follow [these instructions](http://www.cups.org/articles.php?L237+T+Qprintadmin) on the CUPS FAQ. You might also want to read [this post](https://bbs.archlinux.org/viewtopic.php?id=35567).

#### Remote access to web interface

By default, the CUPS web interface can only be accessed by the *localhost*; i.e. the computer that it is installed on. To remotely access the interface, make the following changes to the `/etc/cups/cupsd.conf` file. Replace the line:

```
Listen localhost:631

```

with

```
port 631

```

so that CUPS listens to incoming requests.

Three levels of access can be granted:

```
<Location />           #access to the server
<Location /admin>	#access to the admin pages
<Location /admin/conf>	#access to configuration files

```

To give remote hosts access to one of these levels, add an `Allow` statement to that level's section. An `Allow` statement can take one or more of the forms listed below:

```
Allow all
Allow host.domain.com
Allow *.domain.com
Allow ip-address
Allow ip-address/netmask

```

Deny statements can also be used. For example, if wanting to give all hosts on the 192.168.1.0/255.255.255.0 subnet full access, file `/etc/cups/cupsd.conf` would include this:

```
# Restrict access to the server...
# By default only localhost connections are possible
<Location />
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Restrict access to the admin pages...
<Location /admin>
   # Encryption disabled by default
   #Encryption Required
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

# Restrict access to configuration files...
<Location /admin/conf>
   AuthType Basic
   Require user @SYSTEM
   Order allow,deny
   Allow From localhost
   **Allow From 192.168.1.0/255.255.255.0**
</Location>

```

You might also need to add:

```
DefaultEncryption Never

```

This should avoid the error: 426 - Upgrade Required when using the CUPS web interface from a remote machine.

## Troubleshooting

在‘/etc/cups/cupsd.conf’文件中设置‘LogLevel’是让打印机工作最好的方法：The best way to get printing working is to set 'LogLevel' in '/etc/cups/cupsd.conf' to:

```
LogLevel debug2

```

然后像这样查看'/var/log/cups/error_log'文件的输出：And then viewing the output from '/var/log/cups/error_log' like this:

```
tail -n 100 -f /var/log/cups/error_log

```

在输出中左边的字符排列如下：The characters at the left of the output stands for:

```
D = Debug
E = Error
I = Information
等等...
```

这些文件也可能被证明是有用的。These files may also prove useful.

```
/var/log/cups/page_log '每次打印成功后增加的词条spits out a new entry each time a print is successful.'
/var/log/cups/access_log '所有活跃的cupsd http1.1服务器列表lists all cupsd http1.1 server activity'

```

当然，如果想解决你的问题，重要的是知道CUPS怎样工作，这多多少少是正确的：Of course it's important to know how CUPS work if you want to solve your problems, this is somewhat correct:

1.  当你选择‘打印’时，应用程序会发送一个.ps文件（PostScript，是主要用于电子产业和桌面出版领域的一种页面描述语言。）给CUPS（99%的程序会这样做）。An application sends a .ps file(PostScript, a script language that details how the page will look) to CUPS when you select 'print'(99% of apps do).
2.  CUPS然后读取你打印机的PPD文件（打印机描述文件）并且计算出它需要哪种解释器去将.ps文件转换成一种打印机认识的语言（像PJL，PCL）。通常它需要ghostscript。CUPS then looks at your printers PPD file(printer description file) and figures out what filters it needs to use to convert the .ps file to a language that the printer understands(like PJL,PCL). Usually it needs ghostscript.
3.  GhostScript取得输入并且计算出它需要哪个过滤器，然后将它们转变成打印机能读懂的.ps格式。GhostScript takes the input and figures out which filters it should use,then applies them and converts the .ps file to a format understood by the printer.
4.  然后它被发送到后端。举个例子，如果你有打印机连接到USB端口，它就用USB后端。 Then it is sent to the backend. For example, if you have your printer connected to a USB port, it uses the USB backend.

打印一个文档并且查看'error_log'文件来得到关于打印队列更多的细节和正确地印象。Print a document and watch 'error_log' to get a more detailed and correct image of the printing process.

### Problems resulting from upgrades

*Issues that appeared after CUPS and related program packages underwent a version increment*

#### CUPS stops working

The chances are that a new configuration file is needed for the new version to work properly. Messages such as "404 - page not found" my result from trying to manage CUPS via localhost:631, for example.

To use the new configuration, copy /etc/cups/cupsd.conf.default to /etc/cups/cupsd.conf (backup the old the configuration if needed):

```
# cp /etc/cups/cupsd.conf.default /etc/cups/cupsd.conf

```

and restart CUPS to employ the new settings.

#### Error with gnutls

If receiving errors such as:

```
/usr/sbin/cupsd: error while loading shared libraries: libgnutls.so.13: cannot open shared object file: No such file or directory

```

gnutls may be in need of updating:

```
# pacman -S gnutls

```

After updating, there may be a file named `cupsd.conf.pacnew` in `/etc/cups`. This is the unmodified original configuration file that has been placed as part of the update. Compare it with the currently installed version and adjust to preference.

#### All jobs are "stopped"

If all jobs sent to the printer become "stopped", delete the printer and add it again. Using the [CUPS web interface](http://localhost:631), go to Printers > Delete Printer.

To check the printer's settings go to *Printers*, then *Modify Printer*. Copy down the information displayed, click 'Modify Printer' to proceed to the next page(s), and so on.

#### All jobs are "The printer is not responding"

On networked printers, you should check that the name that CUPS uses as its connection URI resolves to the printer's IP via DNS. E.g. If your printer's connection looks like this:

```
lpd://BRN_020554/BINARY_P1

```

then the hostname 'BRN_020554' needs to resolve to the printer's IP from the server running CUPS

#### The PPD version is not compatible with gutenprint

Run:

```
# /usr/sbin/cups-genppdupdate

```

And restart CUPS (as pointed out in gutenprint's post-install message)

### Other

##### CUPS permission errors

*   Some users fixed 'NT_STATUS_ACCESS_DENIED' (Windows clients) errors by using a slightly different syntax:

```
smb://workgroup/username:password@hostname/printer_name

```

*   Sometimes, the block device has wrong permissions:

```
# ls /dev/usb/
lp0
# chgrp lp /dev/usb/lp0

```

#### HPLIP printer sends "/usr/lib/cups/backend/hp failed" error

Make sure dbus is installed and running, e.g. check DAEMONS in `/etc/rc.conf` or run `ls /var/run/daemons`.

The avahi-daemon might be required if this error persists and the dbus is already running.

#### hp-toolbox sends an error, "Unable to communicate with device"

If running hp-toolbox as a regular user results in:

```
# hp-toolbox
# error: Unable to communicate with device (code=12): hp:/usb/<printer id>

```

or, "`Unable to communicate with device"`", then it may be needed to add the user to the lp group by running the following command:

```
# gpasswd -a <username> lp

```

This can also be caused by printers such as the P1102 that provide a virtual cd-rom drive for MS-Windows drivers. The lp dev appears and then disappears. In that case try the **usb-modeswitch** and **usb-modeswitch-data** packages, that lets one switch off the "Smart Drive" (udev rules included in said packages).

#### CUPS returns '"foomatic-rip" not available/stopped with status 3' with a HP printer

If receiving any of the following error messages in `/var/log/cups/error_log` while using a HP printer, with jobs appearing to be processed while they all end up not being completed with their status set to 'stopped':

```
Filter "foomatic-rip" for printer "<printer_name>" not available: No such file or director

```

or:

```
PID 5771 (/usr/lib/cups/filter/foomatic-rip) stopped with status 3!

```

make sure **hplip** has been installed, in addition to [the packages mentioned above](#Packages), **net-snmp** is also needed. See [this forum post](https://bbs.archlinux.org/viewtopic.php?id=65615).

```
# pacman -S hplip

```

#### Printing fails with unauthorised error

If the user has been added to the lp group, and allowed to print (set in `cupsd.conf`), then the problem lies in `/etc/cups/printers.conf`. This line could be the culprit:

```
AuthInfoRequired negotiate

```

Comment it out and restart CUPS.

#### Print button greyed-out in GNOME print dialogs

	*<small>Source: [I can't print from gnome applications. - Arch Forums](https://bbs.archlinux.org/viewtopic.php?id=70418)</small>*

Be sure the package: **libgnomeprint** is installed

Edit `/etc/cups/cupsd.conf` and add

```
# HostNameLookups Double

```

Restart CUPS:

```
# /etc/rc.d/cupsd restart

```

#### Unknown supported format: application/postscript

Comment the lines:

```
application/octet-stream        application/vnd.cups-raw        0      -

```

from `/etc/cups/mime.convs`, and:

```
application/octet-stream

```

in `/etc/cups/mime.types`.

#### Finding URIs for Windows Print Servers

Sometimes Windows is a little less than forthcoming about exact device URIs (device locations). If having trouble specifying the correct device location in CUPS, run the following command to list all shares available to a certain windows username:

```
$ smbtree -U *windowsusername*

```

This will list every share available to a certain Windows username on the local area network subnet, as long as Samba is set up and running properly. It should return something like this:

```
 WORKGROUP
	\\REGULATOR-PC   		
		\\REGULATOR-PC\Z              	
		\\REGULATOR-PC\Public         	
		\\REGULATOR-PC\print$         	Printer Drivers
		\\REGULATOR-PC\G              	
		\\REGULATOR-PC\EPSON Stylus CX8400 Series	EPSON Stylus CX8400 Series
```

What is needed here is first part of the last line, the resource matching the printer description. So to print to the EPSON Stylus printer, one would enter:

```
smb://username.password@REGULATOR-PC/EPSON Stylus CX8400 Series

```

as the URI into CUPS. Notice that whitespaces are allowed in URIs, whereas backslashes get replaced with forward slashes.

#### Print-Job client-error-document-format-not-supported

Try installing the foomatic packages and use a foomatic driver.

#### /usr/lib/cups/backend/hp failed

Change

```
 SystemGroup sys root

```

to

```
 SystemGroup lp root

```

in /etc/cups/cupsd.conf

Following steps 1-3 in the Alternative CUPS interfaces below may be a better solution, since newer versions of cups will not allow the same group for both normal and admin operation.

#### Samsung Printer won't print certain documents

Your Samsung printer may work fine with `cups` refuse to print certain documents (Inkscape file with text) and even crash completely, causing a restart. The solution is to use mentioned the [cups-usblp](https://www.archlinux.org/packages/?name=cups-usblp) package and to blacklist the `usblp` module as described in this article.

#### Local USB printer does not show up

In case your printer does not show up you might need to replace cups with cups-usblp from AUR. Then try it again, once with the usblp module loaded and once with the module blacklisted.

#### "Unable to get list of printer drivers"

Try to remove Foomatic drivers.

## Appendix

### Alternative CUPS interfaces

If using [GNOME](/index.php/GNOME "GNOME"), a possibility is to manage and configure the printer by using system-config-printer-gnome. This package is available through pacman:

```
# pacman -S system-config-printer-gnome

```

For system-config-printer to work as it should, running as root may be required, or alternatively set up a "normal" user to administer CUPS (if so **follow steps 1-3**)

*   1\. Create group, and add a user to it

```
# groupadd lpadmin
# usermod -aG lpadmin <username>

```

*   2\. Add "lpadmin" (without the quotes) to this line in `/etc/cups/cupsd.conf`

```
SystemGroup sys root <insert here>

```

*   3\. Restart cups, log out and in again (or restart computer)

 `# rc.d restart cupsd` 

[KDE](/index.php/KDE "KDE") users can modify their printers from the Control Center. Both should refer to those desktop environments' documentation for more information on how to use the interfaces.

There is also [gtklp](https://aur.archlinux.org/packages.php?ID=43505) in the [AUR](/index.php/AUR "AUR")

## PDF virtual printer

CUPS-PDF is a nice package that allows one to setup a virtual printer that will generate a PDF from anything sent to it. This package is not necessary, but it can be quite useful. It can be installed using the following command:

```
# pacman -S cups-pdf

```

After installing the package, set it up as if it were for any other printer by using the web interface. Access the cups print manager: [http://localhost:631](http://localhost:631) and select:

```
Administration -> Add Printer
Select CUPS-PDF (Virtual PDF), choose for the make and driver:
Make:	Generic
Driver:	Generic CUPS-PDF Printer

```

Find generated PDF documents in a sub-directory located at `/var/spool/cups-pdf`. Normally, the subdirectory is named after the user who performed the job. A little tweak helps you to find your printed PDF documents more easily. Edit `/etc/cups/cups-pdf.conf` by changing the line

```
#Out /var/spool/cups-pdf/${USER}

```

to

```
Out ${HOME}

```

### Print to PostScript

The CUPS-PDF (Virtual PDF Printer) actually creates a PostScript file and then creates the PDF using the ps2pdf utility. To print to PostScript, just print as usual, in the print dialog choose "CUPS-PDF" as the printer, then select the checkbox for "print to file", hit print, enter the filename.ps and click save. This is handy for faxes, etc...

### Another source for printer drivers

[Turboprint](http://www.turboprint.de/english.html) is a proprietary driver for many printers not yet supported by GNU/Linux (Canon i*, for example). Unlike CUPS, however, high quality prints are either marked with a watermark or are a pay-only service.

## Resources

*   [Official CUPS documentation](http://localhost:631/documentation.html), *locally installed*
*   [Official CUPS Website](http://www.cups.org/)
*   [Linux Printing](http://www.linuxprinting.org/), *[The Linux Foundation](http://www.linuxfoundation.org)*
*   [Gentoo's Printing Guide](http://www.gentoo.org/doc/en/printing-howto.xml), *[Gentoo Documentation Resources](http://www.gentoo.org/doc/en)*
*   [Arch Linux User Forums](https://bbs.archlinux.org/)