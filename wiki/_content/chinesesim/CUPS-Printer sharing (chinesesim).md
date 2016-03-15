**翻译状态：** 本文是英文页面 [CUPS_printer_sharing](/index.php/CUPS_printer_sharing "CUPS printer sharing") 的[翻译](/index.php/ArchWiki_Translation_Team_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "ArchWiki Translation Team (简体中文)")，最后翻译时间：2015-08-23，点击[这里](https://wiki.archlinux.org/index.php?title=CUPS_printer_sharing&diff=0&oldid=392936)可以查看翻译后英文页面的改动。

这篇文章是在系统间共享打印机的操作指南，支持GNU/Linux系统与GNU/Linux系统间共享，以及GNU/Linux系统与Microsoft Windows系统间共享。

## Contents

*   [1 GNU/Linux系统间共享](#GNU.2FLinux.E7.B3.BB.E7.BB.9F.E9.97.B4.E5.85.B1.E4.BA.AB)
    *   [1.1 使用网页操作界面](#.E4.BD.BF.E7.94.A8.E7.BD.91.E9.A1.B5.E6.93.8D.E4.BD.9C.E7.95.8C.E9.9D.A2)
    *   [1.2 手动操作](#.E6.89.8B.E5.8A.A8.E6.93.8D.E4.BD.9C)
        *   [1.2.1 如果您的客户端CUPS版本为1.6.x而服务器端CUPS版本<= 1.5.x](#.E5.A6.82.E6.9E.9C.E6.82.A8.E7.9A.84.E5.AE.A2.E6.88.B7.E7.AB.AFCUPS.E7.89.88.E6.9C.AC.E4.B8.BA1.6.x.E8.80.8C.E6.9C.8D.E5.8A.A1.E5.99.A8.E7.AB.AFCUPS.E7.89.88.E6.9C.AC.3C.3D_1.5.x)
*   [2 Between GNU/Linux and Windows](#Between_GNU.2FLinux_and_Windows)
    *   [2.1 Linux server - Windows client](#Linux_server_-_Windows_client)
        *   [2.1.1 Sharing via IPP](#Sharing_via_IPP)
        *   [2.1.2 Sharing via Samba](#Sharing_via_Samba)
    *   [2.2 Windows server - Linux client](#Windows_server_-_Linux_client)
        *   [2.2.1 Sharing via LPD](#Sharing_via_LPD)
        *   [2.2.2 Sharing via IPP](#Sharing_via_IPP_2)
        *   [2.2.3 Sharing via Samba](#Sharing_via_Samba_2)
            *   [2.2.3.1 Configuration using the web interface](#Configuration_using_the_web_interface)
            *   [2.2.3.2 Manual configuration](#Manual_configuration)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Cannot print with GTK applications](#Cannot_print_with_GTK_applications)
    *   [3.2 Unable to add/modify a printer via SAMBA](#Unable_to_add.2Fmodify_a_printer_via_SAMBA)
*   [4 Other operating systems](#Other_operating_systems)

## GNU/Linux系统间共享

在作为打印服务器的GNU/Linux系统（服务器端）上安装好CUPS之后，建议您通过网页操作界面与另一个GNU/Linux系统（客户端）共享打印机；当然您也可以选择手动操作共享。

在启动cupsd之前，您需要保证avahi-daemon处于运行状态。

您的客户端需要支持Avahi主机名解析，否则客户端可能报错称“找不到打印机”("Unable to locate printer")。详情请参考[avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi")。

### 使用网页操作界面

用浏览器访问CUPS管理页面：[http://localhost:631](http://localhost:631)

点击页面上方的*Administration*按钮, 在Printer下选择“add printer”，将会自动检测已连接的打印机。如果打印机无法被检测，请尝试将打印机重启后重新检测。

打印机设置好之后，将*Server*下的"Share printers connected to this system"改为选中状态，然后点击下方的*change settings*保存修改。这时打印服务器将自动重启。

选择"Edit Configuration File"即可直接修改配置文件`cups.conf`。通过修改文件您可以选择仅将打印机共享到特定用户或IP地址，下文中有详细说明。

### 手动操作

在打印服务器端（即与打印机直接相连的那端）编辑配置文件 `/etc/cups/cupsd.conf`，使共享打印机的系统能连接到服务器端。比如添加如下内容：

```
<Location />
   Order allow,deny
   Allow localhost
   Allow 192.168.0.*
</Location>

```

其中“Allow”后面为允许与打印服务器相连的系统。"Allow all"将允许局域网内所有系统与打印服务器连接。

此外我们需要保证服务器端正在监听客户端所在的IP地址。在"# Listen <serverip>:631"之后添加如下内容（注意：“Listen”后面为服务器的IP地址，而非客户端IP地址）：

```
Listen 192.168.0.101:631

```

为了“让打印机在局域网中可见”("Show shared printers on the local network")，请添加如下内容以保证Browsing指令可以使用：

```
Browsing On

```

完成修改后重启CUPS。

在客户端的`/etc/cups/client.conf`文件中（如果文件不存在则新建）新建一行，将服务器的名称或IP地址添加到"ServerName"（服务器名称）后面：

```
ServerName 192.168.0.101

```

还有很多其他可行的配置方式，在http://localhost:631/help/network.html 中有详细介绍。

完成修改后重启CUPS。

**注意:** 在客户端添加打印机时，如果采用的是IPP协议（Internet Printing Protocol）, 请采用如下形式的URI： ipp://192.168.0.101:631/printers/<打印机名称>

#### 如果您的客户端CUPS版本为1.6.x而服务器端CUPS版本<= 1.5.x

在CUPS 1.6及其之后的版本中, 客户端默认采用IPP 2.0。如果服务器端的CUPS版本<=1.5/IPP版本<= 1.1，由于客户端不会自动使用较早版本的通信协议，客户端将无法与服务器端交流。一个可行的方法是在`/etc/cups/client.conf`中添加如下内容(此方法于2013-05-07被指有误, 可以参考[错误报告](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=704238)):

```
ServerName HOSTNAME-OR-IP-ADDRESS[:PORT]/version=1.1

```

## Between GNU/Linux and Windows

### Linux server - Windows client

#### Sharing via IPP

The **preferred way** to connect a Windows client to a Linux print server is using [IPP](https://en.wikipedia.org/wiki/Internet_Printing_Protocol "wikipedia:Internet Printing Protocol"). It is a standard printer protocol based on HTTP, allowing you all ways to profit from port forwarding, tunneling etc. The configuration is **very easy** and this way is less error-prone than using Samba. IPP is natively supported by Windows **since Windows 2000**.

To configure the server side proceed as described in the section above to enable browsing.

On the Windows computer, go to the printer control panel and choose to 'Add a New Printer'. Next, choose to give a URL. For the URL, type in the location of the printer:

```
http://*host_ip_address*:631/printers/*printer_name*

```

(where *host_ip_address* is the GNU/Linux server's IP address and *printer_name* is the name of the printer being connected to, you can also use the server's fully qualified domain name, if it has one, but you may need to set `ServerAlias my_fully_qualified_domain_name` in *cupsd.conf* for this to work).

**Note:** The add printer dialog in windows is quite sensitive to the path to the printer, the dialogue box itself suggests:
```
http://servername:631/printers/printer_name/.printer

```

which will work in a web-browser but **not** in the add printer dialogue. (At least, not when using cups as an ipp server). The syntax suggested above:

```
http://host_ip_address:631/printers/printer_name

```
**will** work.

After this, install the native printer drivers for your printer on the Windows computer. If the CUPS server is set up to use its own printer drivers, then you can just select a generic postscript printer for the Windows client(e.g. 'HP Color LaserJet 8500 PS' or 'Xerox DocuTech 135 PS2'). Then test the print setup by printing a test page.

#### Sharing via Samba

If your client's Windows version is below Windows 2000 or if you experienced troubles with IPP you can also use Samba for sharing. Note of course that with Samba this involves another complex piece of software. This makes this way **more difficult to configure** and thus sometimes also **more error-prone**, mostly due to authentication problems.

To configure Samba on the Linux server, edit `/etc/samba/smb.conf` file to allow access to printers. File `smb.conf` can look something like this:

 `/etc/samba/smb.conf` 
```
[global]
workgroup=Heroes
server string=Arch Linux Print Server
security=user

[printers]
    comment=All Printers
    path=/var/spool/samba
    browseable=yes
    # to allow user 'guest account' to print.
    guest ok=no
    writable=no
    printable=yes
    create mode=0700
    write list=@adm root yourusername
```

That should be enough to share the printer, yet adding an individual printer entry may be desirable:

 `/etc/samba/smb.conf` 
```
[ML1250]
    comment=Samsung ML-1250 Laser Printer
    printer=ml1250
    path=/var/spool/samba
    printing=cups
    printable=yes
    printer admin=@admin root yourusername
    user client driver=yes
    # to allow user 'guest account' to print.
    guest ok=no
    writable=no
    write list=@adm root yourusername
    valid users=@adm root yourusername
```

Please note that this assumes configuration was made so that users must have a valid account to access the printer. To have a public printer, set *guest ok* to *yes*, and remove the *valid users* line. To add accounts, set up a regular GNU/Linux account and then set up a Samba password on the server. For instance:

```
# useradd yourusername
# smbpasswd -a yourusername

```

After this, restart the Samba daemon.

Obviously, there are a lot of tweaks and customizations that can be done with setting up a Samba print server, so it is advised to look at the Samba and CUPS documentation for more help. The `smb.conf.example` file also has some good samples that might warrant imitating.

### Windows server - Linux client

**Warning:** CUPS cannot handle spaces in printer URIs. If your Windows printer name or user passwords have spaces, CUPS will throw "lpadmin: Bad device-uri" error

#### Sharing via LPD

Windows 7 has a built-in LPD server - using it will probably be the easiest approach as it does neither require an installation of *Samba* on the client nor heavy configuration on the server. It can be activated in the *Control Panel* under *Programs* -> *Activate Windows functions* in the section *Print services*. The printer must have *shared* activated in its properties. Use a share name without any special characters like spaces, commas, etc.

Then the printer can be added in CUPS, choosing LPD protocol. The printer address will look like this:

```
# lpd://windowspc/printersharename

```

Before adding the printer, you will most likely have to install an appropriate printer driver depending on your printer model. Generic PostScript or RAW drivers might also work.

#### Sharing via IPP

As above, IPP is also the **preferred** protocol for printer sharing. However this way might be a bit **more difficult** than the native Samba approach below, since you need a greater effort to set up an IPP-Server on Windows. The commonly chosen server software is Microsoft's Internet Information Services (IIS).

**Note:** This section is incomplete. Here is a description how to set up ISS in Windows XP and Windows 2000, unfortunately in German [[1]](http://www.heise.de/netze/artikel/Ueberall-drucken-221652.html)

#### Sharing via Samba

A **much simpler way** is using Window's native printer sharing via Samba. There is almost no configuration needed, and all of it can be done from the CUPS Backend. As above noted, if there are any problems the reason is mostly related to authentication trouble and Windows access restrictions.

On the server side enable sharing for your desired printer and ensure that the user on the client machine has the right to access the printer.

The following section describes how to set up the client, assuming that both daemons (cupsd and smbd) are running.

##### Configuration using the web interface

The Samba CUPS back-end is enabled by default, if for any reason it is not activate it by entering the following command and restarting CUPS.

```
# ln -s $(which smbspool) /usr/lib/cups/backend/smb

```

Next, simply log in on the CUPS web interface and choose to add a new printer. As a device choose "Windows Printer via SAMBA".

For the device location, enter:

```
smb://username:password@hostname/printer_name

```

Or without a password:

```
smb://username@hostname/printer_name

```

Make sure that the user actually has access to the printer on the Windows computer and select the appropriate drivers. If the computer is located on a domain, make sure the user-name includes the domain:

```
smb://username:password@domain/hostname/printer_name

```

If the network contains many printers you might want to set a preferred printer. To do so use the web interface, go into the printer tab, choose the desired printer and select 'Set as default' from the drop-down list.

##### Manual configuration

For manual configuration stop the CUPS daemon and add your printer to `/etc/cups/printers.conf`, which might for example look like this

 `/etc/cups/printers.conf` 
```
<DefaultPrinter MyPrinter>
AuthInfoRequired username,password
Info My printer via SAMBA
Location In my Office
MakeModel Samsung ML-1250 - CUPS+Gutenprint v5.2.7        # <= use 'lpinfo -m' to list available models
DeviceURI smb://username:password@hostname/printer_name   # <= server URI as described in previous section
State Idle
Type 4
Accepting Yes
Shared No
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
AllowUser yourusername                                    # <= do not forget to change this
OpPolicy default
ErrorPolicy stop-printer
</Printer>
```

Then restart the CUPS daemon an try to print a test page.

To set the preferred printer use the following command

```
# lpoptions -d desired_default_printer_name

```

## Troubleshooting

See [CUPS/Troubleshooting](/index.php/CUPS/Troubleshooting "CUPS/Troubleshooting") for general troubleshooting tips.

### Cannot print with GTK applications

If you get "getting printer information failed" when you try to print from gtk-applications, add this line to your `/etc/hosts`:

```
 # serverip 	some.name.org 	ServersHostname

```

### Unable to add/modify a printer via SAMBA

When adding a or modifying a printer via SAMBA, the interface hangs at 100% CPU for about 30 seconds and then returns the message

```
Unable to get list of printer drivers: Success

```

This is a known bug in Gutenprint ([https://bugs.archlinux.org/task/43708](https://bugs.archlinux.org/task/43708)). The workaround is to uninstall Gutenprint and install only foomatic-db.

```
 lpinfo -m

```

should then return the list of drivers instead of just the "Success" message.

## Other operating systems

More information on interfacing CUPS with other printing systems can be found in the CUPS manual, e.g. on [http://localhost:631/sam.html#PRINTING_OTHER](http://localhost:631/sam.html#PRINTING_OTHER)