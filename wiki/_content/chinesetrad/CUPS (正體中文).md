## Contents

*   [1 前言](#.E5.89.8D.E8.A8.80)
    *   [1.1 CUPS 是什麼?](#CUPS_.E6.98.AF.E4.BB.80.E9.BA.BC.3F)
    *   [1.2 疑難排解和CUPS的組成](#.E7.96.91.E9.9B.A3.E6.8E.92.E8.A7.A3.E5.92.8CCUPS.E7.9A.84.E7.B5.84.E6.88.90)
*   [2 安裝 CUPS](#.E5.AE.89.E8.A3.9D_CUPS)
    *   [2.1 軟體套件](#.E8.BB.9F.E9.AB.94.E5.A5.97.E4.BB.B6)
    *   [2.2 為核心加載印表機模組](#.E7.82.BA.E6.A0.B8.E5.BF.83.E5.8A.A0.E8.BC.89.E5.8D.B0.E8.A1.A8.E6.A9.9F.E6.A8.A1.E7.B5.84)
        *   [2.2.1 USB 埠印表機](#USB_.E5.9F.A0.E5.8D.B0.E8.A1.A8.E6.A9.9F)
        *   [2.2.2 並列埠印表機](#.E4.B8.A6.E5.88.97.E5.9F.A0.E5.8D.B0.E8.A1.A8.E6.A9.9F)
    *   [2.3 啟動 CUPS](#.E5.95.9F.E5.8B.95_CUPS)
    *   [2.4 列印驅動： Foomatic](#.E5.88.97.E5.8D.B0.E9.A9.85.E5.8B.95.EF.BC.9A_Foomatic)
    *   [2.5 列印驅動：hplip](#.E5.88.97.E5.8D.B0.E9.A9.85.E5.8B.95.EF.BC.9Ahplip)
    *   [2.6 列印驅動：Gutenprint](#.E5.88.97.E5.8D.B0.E9.A9.85.E5.8B.95.EF.BC.9AGutenprint)
    *   [2.7 在 X 下設定 CUPS](#.E5.9C.A8_X_.E4.B8.8B.E8.A8.AD.E5.AE.9A_CUPS)
*   [3 印表機的共享](#.E5.8D.B0.E8.A1.A8.E6.A9.9F.E7.9A.84.E5.85.B1.E4.BA.AB)
    *   [3.1 Linux 對 Linux](#Linux_.E5.B0.8D_Linux)
    *   [3.2 Linux to Windows](#Linux_to_Windows)
    *   [3.3 Windows to Linux](#Windows_to_Linux)
    *   [3.4 Windows 2000 and Windows XP to Linux](#Windows_2000_and_Windows_XP_to_Linux)
    *   [3.5 Others to Linux, Linux to others](#Others_to_Linux.2C_Linux_to_others)
*   [4 Appendix](#Appendix)
    *   [4.1 Alternative CUPS Interfaces](#Alternative_CUPS_Interfaces)
    *   [4.2 PDF Virtual Printer](#PDF_Virtual_Printer)
    *   [4.3 Online Resources](#Online_Resources)
    *   [4.4 Specialized Cases](#Specialized_Cases)
        *   [4.4.1 Printing does not work/aborts with the HP Deskjet 700 Series Printers.](#Printing_does_not_work.2Faborts_with_the_HP_Deskjet_700_Series_Printers.)
        *   [4.4.2 Getting HP LaserJet 1010 to work](#Getting_HP_LaserJet_1010_to_work)
        *   [4.4.3 Getting HP LaserJet 1020 to work](#Getting_HP_LaserJet_1020_to_work)
        *   [4.4.4 Printer connected to an Airport Express Station](#Printer_connected_to_an_Airport_Express_Station)
        *   [4.4.5 Performing Utility Functions on Epson Printers](#Performing_Utility_Functions_on_Epson_Printers)
            *   [4.4.5.1 Escputil](#Escputil)
            *   [4.4.5.2 Mtink](#Mtink)
    *   [4.5 Another Source for Printer Drivers](#Another_Source_for_Printer_Drivers)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 As a result of upgrade](#As_a_result_of_upgrade)
        *   [5.1.1 Error with gnutls](#Error_with_gnutls)
        *   [5.1.2 All jobs are "stopped"](#All_jobs_are_.22stopped.22)

# 前言

## CUPS 是什麼?

CUPS是蘋果公司發展的一套開源標準的列印系統，其支援MacOSX以及其他Unix-like作業系統，其使用"Internet Printing Protocol"並且對大部分的雷射印表機、噴墨印表機提供完整的列印服務。CUPS遵循GNU GPL條款。雖然也有很多列印軟體(例：LPRNG)，但是CUPS仍然是相對主流，而且簡單操作。許多Linux的發行板(包括Arch)都已經預設CUPS為預設列印系統。

## 疑難排解和CUPS的組成

最佳列印的方法是在'/etc/cups/cupsd.conf'中設定'LogLevel'。

```
LogLevel debug2

```

然後注意看'/var/log/cups/error_log'中的訊息，可以用下令命令常看

```
tail -n 100 -f /var/log/cups/error_log

```

左側的字元其意義如下：

```
D = Debug(臭蟲)
E = Error(錯誤)
I = Information(資訊)
etc...

```

這些檔案提供的訊息非常有用。

```
在這裡'/var/log/cups/page_log'每次成功列印都會列出資訊
在這裡'/var/log/cups/access_log'列出所有CUPS http1.1服務的狀態

```

如果要確定CUPS是否正常運作，以及要做疑難排解，上述的資訊是非常重要的。

1.  一般應用程式在你壓下"列印"時，會送.ps檔案(PostScript)給CUPS。
2.  之後CUPS會察看你的列印機的PPD檔案(printer description)，再決定如何把.ps檔案轉換成印表機能了解的語言，像是PJL、PCL...等。這個步驟一般需要ghostscript。
3.  GhostScript接收到訊息後會決定使用不同的filter，並且將.ps透過filter轉換成印表機可以接受的格式。
4.  最後送到後端(backend)。例：如果你的印表機是用USB聯接電腦的，那麼就會送到USB後端(backend)。

找份檔案列印，同時注意'error_log'可以的到列印過程中的更多細節

# 安裝 CUPS

## 軟體套件

你至少需要CUPS和Ghostscript：

```
# pacman -S cups ghostscript gsfonts

```

*   **cups** - CUPS套件
*   **ghostscript** - 一個對Posrscript的翻譯器
*   **gsfonts** - Ghostscript standard Type1 fonts

依據你的列印設備的不同，可能需要下列驅動程式套件。如果你不確定，建議使用gutenprint。

*   **gutenprint** - 一個蒐集了大多數Canon, Epson, Lexmark, Sony, Olympus,PCL列印機的驅動程式套件，並且可以支援Ghostscript, CUPS, Foomatic,Gimp。
*   **foomatic**, **foomatic-db**, **foomatic-db-engine**, **foomatic-db-ppd** and **foomatic-filters** - Foomatic是Unix下，以資料庫驅動系統(database-driven system)去整合自由軟體列印驅動，並且支援一般的列印緩衝(spooler)的套件。
*   如果error.log回報"stopped with status 22!"，安裝 **foomatic-filters**可以解決這個問題。
*   **hplip** - HP Linux inkjet driver的縮寫。提供HP DeskJet, OfficeJet, Photosmart, Business Inkjet和一些LaserJet印表機的模組。
*   **cups-pdf** - 一個虛擬的PDF印表機套件，可以讓你產生PDF檔案，而不需要真實列印。

如果你是透過samba通訊協定網路服務來列印的，或是你的列印系統將提供給windows的客戶端使用，請安裝samba。

```
# pacman -S samba

```

## 為核心加載印表機模組

連接好印表機機，並打開電源，隨後：

### USB 埠印表機

```
# modprobe usblp                      （2.6.x 核心）
# modprobe printer                    （2.4.x 核心）
# tail /var/log/messages.log          （看看安裝成功了沒有）

```

### 並列埠印表機

```
# modprobe lp parport parport_pc      （2.6.x 核心）
# modprobe parport parport_pc         （2.4.x 核心）
# tail /var/log/messages.log          （看看安裝成功了沒有）

```

將這些模組加入/etc/rc.conf中的MODULES中去，以便開機時自動加載。

## 啟動 CUPS

```
# /etc/rc.d/cupsd start

```

可將cupsd加入/etc/rc.conf中的DAEMONS中去，以便開機時自動加載.

這個時候，就可以用CUPS在控制檯下做一些簡單的列印了，如：

```
$ cat ~/.xinitrc > /dev/usb/lp0      (USB 埠印表機)

```

當然僅僅依靠CUPS列印，如果在X下，肯定是不方便的。主要是因為缺少驅動，Linux下的列印驅動是PPD檔案。

## 列印驅動： Foomatic

Foomatic是一個資料庫驅動的列印系統，它將Unix下的通用後臺列印系統與開源的印表機驅動整合在一起。 只要有任一在開源驅動下能夠正常工作的印表機，它就能支援了。它支援CUPS, LPRng, LPD, GNUlpr, Solaris LP, PPR, PDQ, CPS 這些底層的列印系統，也能直接列印（既是驅動也是列印工具）。 Foomatic列印速度快，列印質量也挺不錯。不過缺點是，有個別的印表機可能沒有PPD檔案驅動。

```
# pacman -S foomatic-***

```

Foomatic包含五個安裝包： foomatic-filters (幫助後臺列印系統將PostScript轉成印表機語言)， foomatic-db (foomatic-db-engine生成PPD檔案時要用到的一切資料)， foomatic-db-PPD (已經獲支援的列印驅動) foomatic-db-engine (將 Foomatic XMLo資料庫中的數據生成PPD檔案)， foomatic-db-hpijs (專為HP列印驅動生成Foomatic XML 數據)。

一般來說，安裝前四個包就可以了。如果沒有惠普印表機，就不必安裝foomatic-db-hpijs了。

## 列印驅動：hplip

惠普DeskJet, OfficeJet, Photosmart, Business Inkjet 和一些 LaserJet 印表機型號，需要安裝hplip。只用於惠普印表機。 也可同時安裝上面的Foomatic，對比一下兩者的列印速度。

```
# pacman -S hplip

```

## 列印驅動：Gutenprint

也許以上的列印驅動仍然不行（不過安裝foomatic一定是必要的，能提高列印速度）。在設定CUPS時（即將講到） 沒有找到自己的印表機型號。那麼可能還需要接著安裝Gutenprint。 Gutenprint 是GIMP的列印擴充功能模組，過去叫"gimp-print"，它能夠為GIMP提供流行的列印驅動，能 讓佳能、愛普生、惠普、利盟、索尼、奧林巴斯，以及其他基於PCL技術的印表機，列印出更出色的品質。用於高品質的圖像列印是在好不過了。 它支援的印表機型號列表可見於：[http://gutenprint.sourceforge.net/p_Supported_Printers.php3](http://gutenprint.sourceforge.net/p_Supported_Printers.php3) 不過Gutenprint的列印品質是沒得說，但速度就不敢恭維了。但有foomatic的支援就會快很多。

```
# pacman -S gutenprint

```

## 在 X 下設定 CUPS

列印基礎系統CUPS和列印驅動安裝好的，就要開始設定印表機了。 可以通過設定CUPS來設定印表機。設定CUPS的方法適用於一切印表機及其驅動。因此推薦使用。 進入X，打開一個網頁瀏覽器，訪問： [http://localhost:631](http://localhost:631) （也可以用在/etc/hosts中設置好的hostname來代替localhost） 按照提示，一步一步的設定好印表機： Manage Printers ---> Add Printer ---> root密碼驗證 ---> 輸入印表機名稱 ---> 選擇設備類型 （印表機型號及其連接介面：USB埠 or 並列埠印表機） ---> 選擇你的印表機 ---> 通過印表機型號來選擇適當的印表機驅動，並Add （如果列印驅動的名稱中出現了foomatic字樣，一定要優先選擇） ---> 列印選項的設置 ---> 完成

也可以使用另外的設定界面，不過可能要另外安裝：

```
tupac -S gnome-cups-manager     (Gnome下)
tupac -S gtklp                  (KDE下)

```

# 印表機的共享

## Linux 對 Linux

Once you have CUPS setup on your Linux print server, sharing the printer with another Linux box is relatively easy. There are several ways to configure such a scenario, here we will describe the manual setup. On the server computer (the one managing and connecting to the printer) simply open up the _/etc/cups/cupsd.conf_ file and allow access to the server by modifying the location lines. For instance:

```
<Location />
  Order Deny,Allow
  Deny From All
  Allow From 127.0.0.1
  Allow From 10.0.0.*
</Location>

```

You will also need to make sure the server is listening on the IP address your client will be addressing. Add the following line after "Listen localhost:631":

```
Listen 10.0.0.1:631

```

using your server's IP address instead of 10.0.0.1.

Add the IP address of the client computer by doing Allow From client_ip_address. After you make your modifications, you will want to restart CUPS by doing:

```
# /etc/rc.d/cupsd restart

```

On the client side, open up _/etc/cups/client.conf_ and edit the ServerName option to match the ip address or the name of your server. For instance I named my server beast and have entry in my hosts file to point to it. So in my _client.conf_ file, I just edited this line:

```
ServerName beast

```

Next, run the following command to update the client computer:

```
# lpq

```

You should see something like this:

```
ml1250 is ready
no entries

```

There are more configuration possibilities including an automatic configuration which are described in detail on [http://localhost:631/sam.html#CLIENT_SETUP](http://localhost:631/sam.html#CLIENT_SETUP) (this link works on your printer server).

when prompted for username and password use root to access then follow the instructions from here [http://www.digitalhermit.com/linux/printing/](http://www.digitalhermit.com/linux/printing/) if its a TCP/IP printer use Jetdirect

That's it for Linux to Linux printer sharing.

## Linux to Windows

If you are connected to a Windows print server (or any other Samba capable print server), you can skip the section about kernel modules and such. All you have to do is start the CUPS daemon and complete the web interface as specified in section 3.3 and 3.4\. Before this, you need to activate the Samba CUPS backend. You can do this by entering the following command:

```
# ln -s `which smbspool` /usr/lib/cups/backend/smb

```

Note that the symbol before is ` (underneath the ~ on a standard US keyboard) and not '. After this, you will have to restart CUPS using the command specified in the previous section. Next, simply login into the CUPS web interface and choose to add a new printer. For device, there should be an option that says something to the effect Windows Printer Via Samba near the button of the device list. For the device location enter:

```
smb://username:password@hostname/printer_name

```

Or without a password:

```
smb://username@hostname/printer_name

```

Make sure that the user actually has access to the printer on Windows computer. Select the appropriate drivers and that's about it. If the computer is located on a domain, make sure the username includes the domain:

```
smb://username:password@domain/hostname/printer_name

```

Note: if your network contains many printers use "lpoptions -d your_desired_default_printer_name" to set your preferred printer

Note: I, thepizzaking, was having 'NT_STATUS_ACCESS_DENIED' errors and to fix them I needed to use a slightly different syntax:

```
smb://workgroup/username:password@hostname/printer_name

```

## Windows to Linux

Sometimes, you might want to allow a Windows computer to connect to your computer. There are a few ways to do this, and the one I am most familiar with is using Samba. In order to do this, you will have to edit your _/etc/samba/smb.conf_ file to allow access to your printers. Your smb.conf can look something like this:

```
[global]
workgroup = Heroes
server string = Arch Linux Print Server
security = user

[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = yes
    # to allow user 'guest account' to print.
    guest ok = no
    writable = no
    printable = yes
    create mode = 0700
    write list = @adm root neocephas

```

That should be enough to share your printer, but you just might want to add an individual printer entry:

```
[ML1250]
    comment = Samsung ML-1250 Laser Printer
    printer=ml1250
    path = /var/spool/samba
    printing = cups
    printable = yes
    printer admin = @admin root neocephas
    user client driver = yes
    # to allow user 'guest account' to print.
    guest ok = no
    writable = no
    write list = @adm root neocephas
    valid users = @adm root neocephas

```

Please note that in my configuration I made it so that users must have a valid account to access the printer. To have a public printer, set guest ok to yes, and remove the valid users line. To add accounts, you must setup a regular Linux account and then setup a Samba password on the server. For instance:

```
# useradd neocephas
# smbpasswd -a neocephas

```

After setting up any user accounts that you need, you will also need to set up the samba spool folder:

```
# mkdir /var/spool/samba
# chmod 777 /var/spool/samba

```

The next items that need changing are /etc/cups/mime.convs and /etc/cups/mime.types:

mime.convs:

```
# The following line is found at near the end of the file. Uncomment it.
application/octet-stream        application/vnd.cups-raw        0       -

```

mime.types:

```
# Again near the end of the file.
application/octet-stream

```

The changes to mime.convs and mime.types are needed to make CUPS print Microsoft Office document files. Many people seem to need that.

After this restart your Samba daemon:

```
# /etc/rc.d/samba restart

```

Obvious, there are a lot of tweaks and customization that can be done with setting up a Samba print server, so I advise you to look at the Samba and CUPS documentation for more help. The _smb.conf.example_ file also has some good samples to that you might want to look at.

## Windows 2000 and Windows XP to Linux

For the most modern flavors of Windows an alternative way of connecting to your Linux printer server is to use the CUPS protocol directly. The Windows client will need to be using Windows 2000 or Windows XP. Make sure you allows the clients to access the print server by editing the location settings as specified in section 4.1.

On the Windows computer, go to the printer control panel and choose to Add a New Printer. Next, choose to give an url. For the url type in the location of your printer:

_[http://host_ip_address:631/printers/printer_name](http://host_ip_address:631/printers/printer_name)_

where host_ip_address is the Linux server's IP address and printer_name is the name of the printer you are connecting to. After this, install the printer drivers for the Windows computer. If you setup the CUPS server to use its own printer drivers, then you can just select a generic postscript printer for the Windows client. You can then test your print setup by printing a test page.

## Others to Linux, Linux to others

More information on interfacing CUPS with other printing systems can be found in the CUPS manual, e.g. on [http://localhost:631/sam.html#PRINTING_OTHER](http://localhost:631/sam.html#PRINTING_OTHER)

# Appendix

## Alternative CUPS Interfaces

If you are a GNOME user, you can manage and configure your printer by using the gnome-cups-manager.

Update: this package is now available through pacman if you have the "community" repository uncommented in /etc/pacman.conf

```
pacman -S gnome-cups-manager

```

The package is also still available from the [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=66&O=0&L=0&C=0&K=cups&SB=&SO=&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd).

KDE users can modify their printers from the Control Center. Both should refer the those desktop environments' documentation for more information on how to use the interfaces.

There is also [gtklp](https://aur.archlinux.org/packages/gtklp/). It is in the [extra] repository.

## PDF Virtual Printer

A nice little package that I submitted to the incoming folder ([ftp://ftp.archlinux.org/incoming](ftp://ftp.archlinux.org/incoming)) is CUPS-PDF. This package allows one to setup a virtual printer that will generate a PDF from anything sent to it. For example, I wrote this document in AbiWord and then printed it to the Virtual Printer which generated a PDF in my _/var/spool/cups-pdf/neocephas_ folder. Obviously, this package is not necessary, but it can be quite useful. After downloading the package from the FTP server and installing it, you can set it up as you would for any other printer in the web interface. Select Virtual PDF Printer as the device and choose Postscript -> Postscript Color Printer for the drivers.

## Online Resources

Here is a listing of websites that may be of use to you:

*   **Official CUPS documentation on your computer** [http://localhost:631/documentation.html](http://localhost:631/documentation.html)
*   **Official CUPS Website** - [http://www.cups.org/](http://www.cups.org/)
*   **Linux Printing** - [http://www.linuxprinting.org/](http://www.linuxprinting.org/)
*   **Tips and Suggestions on common CUPS problems** - [http://home.nyc.rr.com/computertaijutsu/cups.html](http://home.nyc.rr.com/computertaijutsu/cups.html)
*   **Gentoo's Printing Guide** - [http://www.gentoo.org/doc/en/printing-howto.xml](http://www.gentoo.org/doc/en/printing-howto.xml)
*   **Arch Linux User Forums** - [https://bbs.archlinux.org/](https://bbs.archlinux.org/)
*   [Minolta toner cartridge](http://uniteddigitalsolutions.com/?page=prcat&cid=83)
*   [Tektronix print cartridge](http://uniteddigitalsolutions.com/index.php?page=prcat&cid=91)
*   [Pitney Bowes ink cartridge](http://uniteddigitalsolutions.com/?page=prcat&cid=87)

## Specialized Cases

This section is dedicated to specific problems and their solutions. If you managed to get some _unusual_ printer working, please put the solution here.

### Printing does not work/aborts with the HP Deskjet 700 Series Printers.

*   The solution is to install **pnm2ppa** printer filter for the HP Deskjet 700 series. Without this the print jobs will be aborted by the system. A [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) can be found in the [AUR](/index.php/AUR "AUR").

### Getting HP LaserJet 1010 to work

I had to compile ghostscript myself because ESP gs in rep was 7.07 and had not fixed some bugs like ESP 8.15.1 had. I never downloaded 'foomatic' in rep. I think that is an old package.

```
$ pacman -Qs cups a2ps psutils foo ghost
local/cups 1.1.23-3
    The CUPS Printing System
local/a2ps 4.13b-3
    a2ps is an Any to PostScript filter
local/psutils p17-3
    A set of postscript utilities.
local/foomatic-db 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/foomatic-db-engine 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/foomatic-db-ppd 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/foomatic-filters 3.0.2-1
    Foomatic is a system for using free software printer drivers with common
    spoolers on Unix
local/espgs 8.15.1-1
    ESP Ghostscript

```

I also had to set LogLevel in /etc/cups/cupsd.conf to debug2 before i saw that I missed some "Nimbus" fonts. Then I had to rename & put them where the log told me to. Some fancy google searching had to be applied, example: [http://www.google.com/search?q=n019003l+filetype%3Apfb](http://www.google.com/search?q=n019003l+filetype%3Apfb) since the fonts turned out to be proprietary (i'm sure windows comes with these default). Nevertheless after downloading them(about 7 fonts) and putting them in the correct folder printing started working.

Before that i were getting all the errors said here: [http://linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1010](http://linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1010) 'Unsupport PCL' etc...

I'm sure it could have worked with ESP gs 7.07 too(in rep) if i was smart enough to turn on DebugLevel2 sooner :/ UPDATE: yeah it did... maybe this info is useful for someone else though.. sorry for the inconvenience.

### Getting HP LaserJet 1020 to work

After a lot of tries with hplib and gutenprint I finally found the solution to get my printer HP Laserjet 1020 printing.

First of all you only need to install cups and ghostscript. Then follow the link on [http://www.linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1020](http://www.linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1020) to the [http://foo2zjs.rkkda.com/](http://foo2zjs.rkkda.com/) printer driver page and follow the install instructions. Log in as root. After you downloaded the package and extracted the archive, change into the foo2zjs directory. Now you can follow the original installation instructions with a minor modification to change the userid for printing:

```
$ make
$ ./getweb 1020

```

Open the _Makefile_

```
$ nano Makefile

```

and search for the line

```
# LPuid=-olp

```

and modify it to

```
# LPuid=-oroot

```

then continue with the script

```
$ make install
$ make install-hotplug
$ make cups

```

Or you can use the package foo2zjs from AUR and modify the PKGBUILD: change the line

```
./getweb all

```

to

```
./getweb 1020

```

(or if you're setting another printer change this line to what you need).

As a last step add and configure the printer in the CUPS manager. The printer should be recognized automatically. It works fine for root and all users. When booting the operating system, the printer is initialized and indicates its working.

### Printer connected to an Airport Express Station

The first thing to do is to scan the airport express station. It seems that there are different addresses depending on the model.

```
[root@somostation somos]# nmap 192.168.0.4

Starting Nmap 4.20 ( http://insecure.org ) at 2007-06-26 00:50 CEST
Interesting ports on 192.168.0.4:
Not shown: 1694 closed ports
PORT      STATE SERVICE
5000/tcp  open  UPnP
9100/tcp  open  jetdirect
10000/tcp open  snet-sensor-mgmt
MAC Address: 00:14:51:70:D5:66 (Apple Computer)

Nmap finished: 1 IP address (1 host up) scanned in 25.815 seconds

```

With my station the port is 9100\. The airport station is accessed like an HP JetDirect printer. After, you can edit your printer.conf file in this way:

```
# Printer configuration file for CUPS v1.2.11
# Written by cupsd on 2007-06-26 00:44
<Printer LaserSim>
Info SAMSUNG ML-1510 gdi
Location SomoStation
DeviceURI socket://192.168.0.4:9100
State Idle
StateTime 1182811465
Accepting Yes
Shared Yes
JobSheets none none
QuotaPeriod 0
PageLimit 0
KLimit 0
OpPolicy default
ErrorPolicy stop-printer
</Printer>

```

It should work. I had a few problems. There were resolved by removing foomatic and installing foomatic-db, foomatic-db-engine, foomatic-db-ppd instead.

### Performing Utility Functions on Epson Printers

#### Escputil

Here we explain how to perform some of the utility functions such as nozzle cleaning and nozzle checks on Epson printers. We will use the escputil utility, which is part of the gutenprint package.

There is a man page ("man escputil") that provides pretty good information, but it does not include necessary information on how to identify your printer. There are two parameters that can be used. One is --printer; what it expects is the name you used to identify your printer when you configured it. The other is --raw-device. What this option expects is is something beginning with "/dev". If your printer is a serial printer, and the only serial printer, it is "/dev/lp0". If it is an usb printer, it is "/dev/usb/lp0". If you have more than one printer, they will have names ending in "lp1", "lp2", etc.

*   To clean the printer heads:

```
  escputil -u --clean-head

```

*   To prints the nozzle-check pattern, allowing you to verify that the previous head cleaning worked. (Or to determine that you need to clean the heads)

```
  escputil -u --nozzle-check

```

If you want to perform an operation that requires 2-way communication with a printer, you must use the "--raw-device" specification, and your user must root or be a member of the group "lp".

*   The following is an example of getting the printer's internal identification:

```
  sudo escputil --raw-device=/dev/usb/lp0 --identify

```

*   To prints out the ink levels of the printer:

```
  sudo escputil --raw-device=/dev/usb/lp0 --ink-level

```

#### Mtink

This is a printer status monitor which enables to get the remaining ink quantity, to print test patterns, to reset printer and to clean nozzle. It use an intuitive graphical user interface. Package can be downloaded from [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=476&O=0&L=0&C=0&K=mtink&SB=n&SO=a&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd).

## Another Source for Printer Drivers

On _[http://www.turboprint.de/english.html](http://www.turboprint.de/english.html)_ is a really good printer driver for many printers not yet supported by Linux (especially Canon i*). The only problem is that high-quality-prints are either marked with a turboprint-logo or you have to pay for it... It's not Open-Source.

[Wikipedia:Common_Unix_Printing_System](https://en.wikipedia.org/wiki/Common_Unix_Printing_System "wikipedia:Common Unix Printing System")

# Troubleshooting

## As a result of upgrade

### Error with gnutls

After updating, if you get something like :

```
 /usr/sbin/cupsd: error while loading shared libraries: libgnutls.so.13: cannot open shared object file: No such file or directory

```

You need to update gnutls:

```
 pacman -S gnutls

```

In addition, in /etc/cups, there will be a file named cupsd.conf.pacnew. Rename it cupsd.conf.

### All jobs are "stopped"

After updating CUPS, if all jobs sent to the printer become "stopped", delete the printer and add it again. Using the CUPS web interface ([http://localhost:631](http://localhost:631)), go to Printers > Delete Printer.

_Note:_ If you don't remember your printer's settings, go to Printers > Modify Printer. Copy down the information displayed, click 'Modify Printer' to proceed to the next page(s), etc.