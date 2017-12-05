Related articles

*   [Codecs (简体中文)](/index.php/Codecs_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Codecs (简体中文)")
*   [MPlayer (简体中文)](/index.php/MPlayer_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "MPlayer (简体中文)")

摘自 [Wikipedia](https://en.wikipedia.org/wiki/Optical_disc_drive "wikipedia:Optical disc drive"):

	在计算机中，光盘驱动器（ODD）指使用激光或可见光谱内或附近的电磁波来从光盘写入或读取数据的驱动器。有的光盘驱动器只能读取，但现在的驱动器都普遍能够读取和记录，也叫做烧录或写入。小型光盘，DVD和蓝光碟都是可以用这类驱动器读取写入的光学介质。光驱是普遍叫法；驱动器往往被描述成“CD” “DVD”，或者“Blu-ray”，后面跟上“drive” “write”，等等。

## Contents

*   [1 烧录](#.E7.83.A7.E5.BD.95)
    *   [1.1 安装烧录工具](#.E5.AE.89.E8.A3.85.E7.83.A7.E5.BD.95.E5.B7.A5.E5.85.B7)
    *   [1.2 Making an ISO image from existing files on hard disk](#Making_an_ISO_image_from_existing_files_on_hard_disk)
    *   [1.3 从硬盘上已存在的文件创建ISO映像](#.E4.BB.8E.E7.A1.AC.E7.9B.98.E4.B8.8A.E5.B7.B2.E5.AD.98.E5.9C.A8.E7.9A.84.E6.96.87.E4.BB.B6.E5.88.9B.E5.BB.BAISO.E6.98.A0.E5.83.8F)
        *   [1.3.1 基本选项](#.E5.9F.BA.E6.9C.AC.E9.80.89.E9.A1.B9)
        *   [1.3.2 移植点](#.E7.A7.BB.E6.A4.8D.E7.82.B9)
    *   [1.4 挂载一个ISO映像](#.E6.8C.82.E8.BD.BD.E4.B8.80.E4.B8.AAISO.E6.98.A0.E5.83.8F)
    *   [1.5 将img/ccd转换为ISO映像](#.E5.B0.86img.2Fccd.E8.BD.AC.E6.8D.A2.E4.B8.BAISO.E6.98.A0.E5.83.8F)
    *   [1.6 获取你光驱的名字](#.E8.8E.B7.E5.8F.96.E4.BD.A0.E5.85.89.E9.A9.B1.E7.9A.84.E5.90.8D.E5.AD.97)
    *   [1.7 读取CD/DVD的卷标](#.E8.AF.BB.E5.8F.96CD.2FDVD.E7.9A.84.E5.8D.B7.E6.A0.87)
    *   [1.8 从CD，DVD或BD读取ISO映像](#.E4.BB.8ECD.EF.BC.8CDVD.E6.88.96BD.E8.AF.BB.E5.8F.96ISO.E6.98.A0.E5.83.8F)
    *   [1.9 擦除CD-RW和DVD-RW](#.E6.93.A6.E9.99.A4CD-RW.E5.92.8CDVD-RW)
    *   [1.10 格式化DVD-RW](#.E6.A0.BC.E5.BC.8F.E5.8C.96DVD-RW)
    *   [1.11 格式化BD-RE和BD-R](#.E6.A0.BC.E5.BC.8F.E5.8C.96BD-RE.E5.92.8CBD-R)
    *   [1.12 向CD，DVD或BD烧录ISO映像](#.E5.90.91CD.EF.BC.8CDVD.E6.88.96BD.E7.83.A7.E5.BD.95ISO.E6.98.A0.E5.83.8F)
    *   [1.13 校验已烧录的ISO映像](#.E6.A0.A1.E9.AA.8C.E5.B7.B2.E7.83.A7.E5.BD.95.E7.9A.84ISO.E6.98.A0.E5.83.8F)
    *   [1.14 ISO 9660和即时烧录](#ISO_9660.E5.92.8C.E5.8D.B3.E6.97.B6.E7.83.A7.E5.BD.95)
    *   [1.15 Multi-session](#Multi-session)
        *   [1.15.1 Multi-session by cdrecord](#Multi-session_by_cdrecord)
        *   [1.15.2 Multi-session by growisofs](#Multi-session_by_growisofs)
        *   [1.15.3 Multi-session by xorriso](#Multi-session_by_xorriso)
    *   [1.16 BD缺陷管理](#BD.E7.BC.BA.E9.99.B7.E7.AE.A1.E7.90.86)
    *   [1.17 烧录音频CD](#.E7.83.A7.E5.BD.95.E9.9F.B3.E9.A2.91CD)
    *   [1.18 烧录BIN/CUE](#.E7.83.A7.E5.BD.95BIN.2FCUE)
        *   [1.18.1 TOC/CUE/BIN for mixed-mode disks](#TOC.2FCUE.2FBIN_for_mixed-mode_disks)
    *   [1.19 Burn backend problems](#Burn_backend_problems)
    *   [1.20 用GUI程序烧录CD/DVD/BD](#.E7.94.A8GUI.E7.A8.8B.E5.BA.8F.E7.83.A7.E5.BD.95CD.2FDVD.2FBD)
*   [2 回放](#.E5.9B.9E.E6.94.BE)
    *   [2.1 CD](#CD)
    *   [2.2 DVD](#DVD)
*   [3 Ripping](#Ripping)
    *   [3.1 CD](#CD_2)
    *   [3.2 DVD](#DVD_2)
        *   [3.2.1 dvd::rip](#dvd::rip)
*   [4 疑难解答](#.E7.96.91.E9.9A.BE.E8.A7.A3.E7.AD.94)
    *   [4.1 Brasero fails to normalize audio CD](#Brasero_fails_to_normalize_audio_CD)
    *   [4.2 VLC: Error "... could not open the disc /dev/dvd"](#VLC:_Error_.22..._could_not_open_the_disc_.2Fdev.2Fdvd.22)
    *   [4.3 DVD设备噪音大](#DVD.E8.AE.BE.E5.A4.87.E5.99.AA.E9.9F.B3.E5.A4.A7)
    *   [4.4 Playback does not work with new computer (new DVD-Drive)](#Playback_does_not_work_with_new_computer_.28new_DVD-Drive.29)
    *   [4.5 None of the above programs are able to rip/encode a DVD to my hard disk!](#None_of_the_above_programs_are_able_to_rip.2Fencode_a_DVD_to_my_hard_disk.21)
    *   [4.6 GUI program log indicates problems with backend program](#GUI_program_log_indicates_problems_with_backend_program)
        *   [4.6.1 Special case: medium error / write error](#Special_case:_medium_error_.2F_write_error)
    *   [4.7 AHCI](#AHCI)
    *   [4.8 BD-R DL 50GB errors on trying to burn second layer](#BD-R_DL_50GB_errors_on_trying_to_burn_second_layer)
    *   [4.9 Disc tray autocloses](#Disc_tray_autocloses)
*   [5 另请参阅](#.E5.8F.A6.E8.AF.B7.E5.8F.82.E9.98.85)

## 烧录

**Warning:** 光驱的质量和光碟本身差异很大。一般来说，低速烧录更可靠，也是推荐的做法。如果你的光碟有什么意想不到的情况，试试用你的刻录机能支持的最低速度进行烧录。

光驱烧录的步骤包括创建或获取一个映像并将其写入一个光学介质。这个映像原则上可以使任何数据文件。如果你想挂载目标介质的话，其通常是一个有ISO 9660文件系统的映像文件。 音频和多媒体CD通常由一个 *.bin* 文件烧录而成，并由一个 *.toc* 文件或 *.cue* 文件控制目标轨道排布。

### 安装烧录工具

如果你想使用有GUI的程序的话，请阅读 [#用GUI程序烧录CD/DVD/BD](#.E7.94.A8GUI.E7.A8.8B.E5.BA.8F.E7.83.A7.E5.BD.95CD.2FDVD.2FBD).

列在这里的程序都是基于命令行的。他们是大多数免费光碟操作（CD, DVD和BD）GUI程序使用的后端。GUI用户可能会在故障处理或写烧录脚本时碰到它们。

你需要至少两个程序，一个来创建文件系统映像，另一个用于向你期望的介质中烧录数据。

可用的创建ISO 9660映像的程序有：

*   *mkisofs* 来自于 [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   *xorriso* 和 *xorrisofs* 来自于 [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

一般选择 *mkisofs*。

用于烧录的程序有：

*   *cdrdao* 来自于 [cdrdao](https://www.archlinux.org/packages/?name=cdrdao) （仅支持CD，仅支持TOC/CUE/BIN）
*   *cdrecord* 来自于 [cdrtools](https://www.archlinux.org/packages/?name=cdrtools)
*   *cdrskin* 来自于 [libburn](https://www.archlinux.org/packages/?name=libburn)
*   *growisofs* 来自于m [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) （仅支持DVD和BD）
*   *xorriso* 和 *xorrecord* 来自于 [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

CD一般选择 *cdrecord*，*growisofs* 用于DVD和蓝光碟。要向CD写入TOC/CUE/BIN文件的话，安装 [cdrdao](https://www.archlinux.org/packages/?name=cdrdao)。

免费光碟操作（CD, DVD和BD）GUI程序依赖于上面至少一个包。

*xorrisofs* 支持在此文章中展示的 *mkisofs* 选项。

*cdrskin* 支持展示的 *cdrecord* 选项；*xorrecord* 也支持不涉及音频CD的选项。

### Making an ISO image from existing files on hard disk

### 从硬盘上已存在的文件创建ISO映像

创建一个ISO映像最简单的方法是把需要的文件复制进一个目录，例如： `./for_iso`。

再用 *mkisofs* 生成映像文件：

```
$ mkisofs -V "*ARCHIVE_2013_07_27*" -J -r -o *isoimage.iso* *./for_iso*

```

所有的选项都在下面进行了解释。

#### 基本选项

	`-V`

	指定文件系统的名字。ISO 9660标准规定了32个字符的长度限制，其也适用于："A"到"Z"，"0"到"9"和"_"。这个卷标会在介质自动挂载时显示。

	`-J`

	启用 [Joliet](https://en.wikipedia.org/wiki/Joliet_(file_system) 拓展，其会分配特殊空间用于存储Unicode文件名（每个文件最多64个UTF-16 字符）。

	`-joliet-long`

	在Joliet中将文件名最大长度从64增加到103个UTF-16字符。不符合Joliet规范的不被支持。

	`-r`

	启用 [Wikipedia:Rock Ridge](https://en.wikipedia.org/wiki/Rock_Ridge "wikipedia:Rock Ridge") 拓展，其会向映像添加POSIX文件系统语义，包括255个字符的文件名支持Unix风格文件权限。

	`-o`

	设置目标映像的路径。

#### 移植点

也可以让 *mkisofs* 从不同的路径收集文件和目录。

```
$ mkisofs -V "*BACKUP_2013_07_27*" -J -r -o *backup_2013_07_27.iso* \
  -graft-points \
  */photos=/home/user/photos \*
  /mail=/home/user/mail \
  /photos/holidays=/home/user/holidays/photos

```

	`-graft-points`

	Enables the recognition of *pathspecs* which consist of a target address in the ISO file system (e.g. `/photos`) and a source address on hard disk (e.g. `/home/user/photos`). 两者都用"="分隔。

So this example puts the disk directory `/home/user/photos`, `/home/user/mail` and `/home/user/holidays/photos`, respectively in the ISO image as `/photos`, `/mail` and `/photos/holidays`.

*mkisofs* 和 *xorrisofs* 接受相同的选项。For secure backups, consider using *xorrisofs* with option `--for_backup`, which records eventual ACLs and stores an MD5 checksum for each data file.

了解更多有关ISO 9660程序选项的信息，请查看man手册：

*   [mkisofs](http://cdrtools.sourceforge.net/private/man/cdrecord/index.html)
*   [xorrisofs](https://www.gnu.org/software/xorriso/man_1_xorrisofs.html)

### 挂载一个ISO映像

如果你想浏览一个ISO映像里面的文件的话可以将其挂载。 挂载ISO映像，我们可以：

```
# mount -t iso9660 -o ro,loop */path/to/file.iso* */mount-point*

```

完成后别忘了卸载映像：

```
# umount /mount-point

```

对于无root权限进行挂载，请参阅 [Mounting images as user](/index.php/Mounting_images_as_user "Mounting images as user")。

### 将img/ccd转换为ISO映像

转换一个 `img`/`ccd` 映像，你可以使用 [ccd2iso](https://www.archlinux.org/packages/?name=ccd2iso)：

```
$ ccd2iso *~/image.img* *~/image.iso*

```

### 获取你光驱的名字

假设你的录制设备名为 `/dev/sr0`。

检查：

```
$ cdrecord dev=*/dev/sr0* -checkdrive

```

这会报告设备的 `Vendor_info` 和 `Identification` 字段。

如果找不到任何设备，检查是否存在任何 `/dev/sr*` 并且它们是否向你和你的组提供任何读/写 (`wr-`) 权限 。 如果没有任何 `/dev/sr*` 存在，尝试手动 [加载](/index.php/Kernel_modules_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87) "Kernel modules (简体中文)") `sr_mod` 模块。

### 读取CD/DVD的卷标

如果你想获取介质的名字/标签，使用 *dd*：

```
$ dd if=*/dev/sr0* bs=1 skip=32808 count=32

```

### 从CD，DVD或BD读取ISO映像

你应该决定ISO文件系统的大小，再将其复制到硬盘上。大多数介质类型承载着比最近一次烧录写入数据更多的数据。

使用来自 [util-linux](https://www.archlinux.org/packages/?name=util-linux) 的 *isosize* 来获取需要读取的块数目：

```
$ blocks=$(isosize -d 2048 */dev/sr0*)

```

看看获取的块数目是不是可信的

 `$ echo "That would be $(expr $blocks / 512) MB"` 
```
That would be 589 MB

```

再从介质向硬盘复制决定的数据：

```
$ dd if=*/dev/sr0* of=*isoimage.iso* bs=2048 count=$blocks status=progress

```

没有决定大小的话就忽略 `count=$blocks`。你可能会得到比需要的更多的数据。The resulting file will nevertheless be mountable. It should still fit onto a medium of the same type as the medium from which the image was copied.

如果原光盘是可启动的，那么复制后的数据也是可启动的。你可以将其作为虚拟机的伪光盘或者刻录成可启动的光盘。

### 擦除CD-RW和DVD-RW

用过的CD-RW介质在向之前录制的数据上写入数据之前需要先擦除之前的数据。这样：

```
$ cdrecord -v dev=*/dev/sr0* blank=fast

```

blank有两个选项： `blank=fast` 和 `blank=full`。full和完全写入持续的时间一样长。It overwrites the payload data on the CD. Nevertheless this should not be considered as securely making those data unreadable. For that purpose, several full write runs with random data are advised.

可选的命令有：

```
$ cdrskin -v dev=*/dev/sr0* blank=fast
$ xorriso -outdev */dev/sr0* -blank as_needed

```

擦除DVD-RW使用来自 [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) 的 *dvd+rw-format*：

```
$ dvd+rw-format -blank=fast */dev/sr0*

```

可选的命令有：

```
$ cdrecord -v dev=*/dev/sr0* blank=fast
$ cdrskin -v dev=*/dev/sr0* blank=deformat_sequential_quickest
$ xorriso -outdev */dev/sr0* -blank deformat_quickest

```

Such fastly blanked DVD-RW are not suitable for multi-session and cannot take input streams of unpredicted length. For that purpose one has to use one of:

```
$ cdrecord -v dev=*/dev/sr0* blank=all
$ dvd+rw-format -blank=full */dev/sr0*
$ cdrskin -v dev=*/dev/sr0* blank=as_needed
$ xorriso -outdev */dev/sr0* -blank as_needed

```

其它的介质类型不是只能写入一次（CD-R, DVD-R, DVD+R, BD-R）就是可以在不需要擦除的情况下重写（DVD-RAM, DVD+RW, BD-RE）。

### 格式化DVD-RW

Formatted DVD-RW media can be overwritten without previous erasure. So consider to apply once in their life time

```
$ dvd+rw-format -force */dev/sr0*
$ cdrskin -v dev=*/dev/sr0* blank=format_if_needed
$ xorriso -outdev */dev/sr0* -format as_needed

```

Unlike DVD-RAM, DVD+RW, and BD-RE, formatted DVD-RW cannot be used as (slow) hard disk directly, but rather need the mediation of driver pktcdvd. See man pktsetup.

### 格式化BD-RE和BD-R

BD-RE第一次使用需要被格式化。当烧录程序检测到未格式化状态时这会自动完成。Nevertheless the size of the payload area can be influenced by expert versions of the format commands shown above for DVD-RW.

格式化或未格式化BD-R都能被使用。Unformatted they are written with full nominal speed and offer maximum storage capacity. Formatted they get checkread during write operations and bad blocks get replaced by blocks from the Spare Area. This reduces write speed to a half or less of nominal speed. The default sized Spare Area reduces the storage capacity by 768 MiB.

growisofs formats BD-R by default. The others do not. growisofs can be kept from formatting. cdrskin and xorriso can write with full nominal speed on formatted BD-RE or BD-R:

```
 $ growisofs -use-the-force-luke=spare:none ...growisofs.or.mkisofs.options...
 $ cdrskin stream_recording=on ...cdrecord.options...
 $ xorriso -stream_recording on ...xorriso.commands...

```

### 向CD，DVD或BD烧录ISO映像

要把已准备好的ISO映像文件 `isoimage.iso` 烧录到光盘介质，对于CD：

```
$ cdrecord -v -sao dev=*/dev/sr0* *isoimage.iso*

```

对于DVD或BD：

```
$ growisofs -dvd-compat -Z */dev/sr0*=*isoimage.iso*

```

**Note:**

*   确保介质在写入时未被挂载。如果介质有可读的文件系统，挂载会自动进行。在最好的情况下，这会阻止烧录程序使用烧录设备。最坏的情况下，读操作会导致误写。所以有疑问的话，直接: `# umount /dev/sr0` 
*   *growisofs* 对于空白的BD-R介质有一个 [小bug](https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=713016)。在烧录完成时它会发出一条错误信息。一些程序像 *k3b* 会直接认为整个烧录过程失败。为了防止这样，要么
    *   format the blank BD-R by `dvd+rw-format */dev/sr0*` before submitting it to *growisofs*
    *   在用 *growisofs* 之前用 `dvd+rw-format */dev/sr0*` 格式化空白BD-R
    *   要么使用 *growisofs* 的 `-use-the-force-luke=spare:none` 选项

### 校验已烧录的ISO映像

你可以校验以烧录介质的完整性以确保没有错误。别忘了总在校验之前弹出介质并重新插入。这会确保没有任何内核缓存会被用来读取数据。

首先计算原ISO映像的MD5校验和：

 `$ md5sum isoimage.iso` 
```
 e5643e18e05f5646046bb2e4236986d8 isoimage.iso

```

然后计算介质中ISO文件系统的MD5校验和： 虽然有的介质类型存储了和被提交给烧录程序的完全一样数量的数据，但其它的会在被读取时附加尾随的垃圾。所以你应该ISO映像文件读取的大小。

```
$ blocks=$(expr $(du -b isoimage.iso | awk '{print $1}') / 2048)

```
 `$ dd if=/dev/sr0 bs=2048 count=$blocks | md5sum` 
```
 43992+0 records in
 43992+0 records out
 90095616 bytes (90 MB) copied, 0.359539 s, 251 MB/s
 e5643e18e05f5646046bb2e4236986d8  -

```

Both runs should yield the same MD5 checksum (here: `e5643e18e05f5646046bb2e4236986d8`). If they do not, you will probably also get an I/O error message from the `dd` run. `dmesg` might then tell about SCSI errors and block numbers, if you are interested.

### ISO 9660和即时烧录

It is not necessary to store an emerging ISO file system on hard disk before writing it to optical media. Only very old CD drives at very old computers could suffer failed burns due to empty drive buffer.

If you omit option `-o` from *mkisofs* then it writes the ISO image to standard output. This can be piped into the standard input of burn programs.

```
$ mkisofs -V "ARCHIVE_2013_07_27" -J -r ./for_iso | \
  cdrecord -v dev=/dev/sr0 -waiti -

```

这里其实不需要选项 `-waiti`。It prevents *cdrecord* from writing to the medium before *mkisofs* starts its output. This would allow *mkisofs* to read the medium without disturbing an already started burn run. See next section about multi-session.

On DVD and BD, you may let *growisofs* operate *mkisofs* for you and burn its output on-the-fly

```
$ growisofs -Z */dev/sr0* -V "*ARCHIVE_2013_07_27*" -r -J *./for_iso*

```

### Multi-session

ISO 9660 multi-session means that a medium with readable file system is still writable at its first unused block address, and that a new ISO directory tree gets written to this unused part. The new tree is accompanied by the content blocks of newly added or overwritten data files. The blocks of data files, which shall stay as in the old ISO tree, will not be written again.

Linux and many other operating systems will mount the directory tree in the last session on the medium. This youngest tree will normally show the files of the older sessions, too.

#### Multi-session by cdrecord

如果cdrecord的选项 `-multi` 被使用了，CD-R和CD-RW会保持可写（又称为“可附加”）

```
$ cdrecord -v -multi dev=*/dev/sr0* *isoimage.iso*

```

Then the medium can be inquired for the parameters of the next session

```
$ m=$(cdrecord dev=*/dev/sr0* -msinfo)

```

By help of these parameters and of the readable medium in the drive you can produce the add-on ISO session

```
$ mkisofs -M */dev/sr0* -C "$m" \
   -V "*ARCHIVE_2013_07_28*" -J -r -o *session2.iso* *./more_for_iso*

```

Finally append the session to the medium and keep it appendable again

```
$ cdrecord -v -multi dev=*/dev/sr0* *session2.iso*

```

Programs *cdrskin* and *xorrecord* do this too with DVD-R, DVD+R, BD-R and unformatted DVD-RW. Program *cdrecord* does multi-session with at least DVD-R and DVD-RW. They all do with CD-R and CD-RW, of course.

Most re-usable media types do not record a session history that would be recognizable for a mounting kernel. But with ISO 9660 it is possible to achieve the multi-session effect even on those media.

*growisofs* and *xorriso* can do this and hide most of the complexity.

#### Multi-session by growisofs

By default, *growisofs* uses *mkisofs* as a backend for creating ISO images forwards most of its program arguments to . See above examples of *mkisofs*. It bans option `-o` and deprecates option `-C`. By default it uses the *mkisofs*. You may specify to use one of the others compatible backend program by setting environment variable `MKISOFS`:

```
$ export MKISOFS="xorrisofs"

```

The wish to begin with a new ISO file system on the optical medium is expressed by option `-Z`

```
$ growisofs -Z */dev/sr0* -V "*ARCHIVE_2013_07_27*" -r -J *./for_iso*

```

The wish to append more files as new session to an existing ISO file system is expressed by option `-M`

```
$ growisofs -M */dev/sr0* -V "*ARCHIVE_2013_07_28*" -r -J *./more_for_iso*

```

For details see the [growisofs(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/growisofs.1) manual and the manuals of *mkisofs* and *xorrisofs*.

#### Multi-session by xorriso

*xorriso* learns the wish to begin with a new ISO file system from the blank state of the medium. So it is appropriate to blank it if it contains data. The command `-blank as_needed` applies to all kinds of re-usable media and even to ISO images in data files on hard disk. It does not cause error if applied to a blank write-once medium.

```
$ xorriso -outdev */dev/sr0* -blank as_needed \
          -volid "*ARCHIVE_2013_07_27*" -joliet on -add *./for_iso* --

```

On non-blank writable media *xorriso* appends the newly given disk files if command `-dev` is used rather than `-outdev`. Of course, no command `-blank` should be given here

```
$ xorriso -dev */dev/sr0* \
          -volid "*ARCHIVE_2013_07_28*" -joliet on -add *./more_for_iso* --

```

For details see the [manual page](https://www.gnu.org/software/xorriso/man_1_xorriso.html) and especially its [examples](https://www.gnu.org/software/xorriso/man_1_xorriso.html#EXAMPLES)

### BD缺陷管理

正常情况下BD-RE和已格式化的BD-R会在启用缺陷管理时写入。 This feature reads the written blocks while they are still stored in the drive buffer. In case of poor read quality the blocks get written again or redirected to the *Spare Area* where the data get stored in replacement blocks.

This checkreading reduces write speed to at most half of the nominal speed of drive and BD medium. Sometimes it is even worse. Heavy use of the Spare Area causes long delays during read operations. So Defect Management is not always desirable.

*cdrecord* does not format BD-R. It has no means to prevent Defect Management on BD-RE media, though.

*growisofs* formats BD-R by default. The Defect Management can be prevented by option `-use-the-force-luke=spare:none`. It has no means to prevent Defect Management on BD-RE media, though.

*cdrskin*, *xorriso* and *xorrecord* do not format BD-R by default. They do with `cdrskin blank=format_if_needed`, resp. `xorriso -format as_needed`, resp. `xorrecord blank=format_overwrite`. These three programs can disable Defect Management with BD-RE and already formatted BD-R by `cdrskin stream_recording=on`, resp. `xorriso -stream_recording on`, resp. `xorrecord stream_recording=on`.

### 烧录音频CD

创建你的音频轨道并保存为未压缩、16位、立体声的WAV文件。要把MP3转为WAV，确保已安装 [lame](https://www.archlinux.org/packages/?name=lame)，*cd* 进入有MP3文件的目录，运行：

```
$ for i in *.mp3; do lame --decode "$i" "$(basename "$i" .mp3)".wav; done

```

为了确保烧录用LAME转换的WAV文件时不报错，试试用 [mpg123](https://www.archlinux.org/packages/?name=mpg123) 编码：

```
$ for i in *.mp3; do mpg123 --rate 44100 --stereo --buffer 3072 --resync -w $(basename $i .mp3).wav $i; done

```

将音频文件命名为可以让它们在以字母顺序排列时变成想要的轨道顺序的样子，比如 `01.wav`，`02.wav`，`03.wav`，等等。用下面的命令来模拟将WAV文件烧录为音频CD：

```
$ cdrecord **-dummy** -v -pad speed=1 dev=*/dev/sr0* -dao -swab *.wav

```

如果一切顺利，你可以去掉 `dummy` 来真正烧录。

用 [MPlayer](/index.php/MPlayer "MPlayer") 来测试新的音频CD：

```
$ mplayer cdda://

```

### 烧录BIN/CUE

烧录一个BIN/CUE映像，运行：

```
$ cdrdao write --device */dev/sr0* *image.cue*

```

#### TOC/CUE/BIN for mixed-mode disks

ISO images only store a single data track. If you want to create an image of a mixed-mode disk (data track with multiple audio tracks) then you need to make a TOC/BIN pair:

```
$ cdrdao read-cd --read-raw --datafile *image.bin* --driver generic-mmc:0x20000 --device */dev/cdrom* *image.toc*

```

Some software only likes CUE/BIN pair, you can make a CUE sheet with *toc2cue* (part of [cdrdao](https://www.archlinux.org/packages/?name=cdrdao)):

```
$ toc2cue *image.toc* *image.cue*

```

### Burn backend problems

If you're experiencing problems, you may ask for advise at mailing list [cdwrite@other.debian.org](mailto:cdwrite@other.debian.org), or try to write to the one of support mail addresses if some are listed near the end of the program's man page.

Tell the command lines you tried, the medium type (e.g. CD-R, DVD+RW, ...), and the symptoms of failure (program messages, disappointed user expectation, ...). You will possibly get asked to obtain the newest release or development version of the affected program and to make test runs. But the answer might as well be, that your drive dislikes the particular medium.

### 用GUI程序烧录CD/DVD/BD

有若干个在图形环境下烧录CD的程序：

另请参阅 [Wikipedia:Comparison of disc authoring software](https://en.wikipedia.org/wiki/Comparison_of_disc_authoring_software "wikipedia:Comparison of disc authoring software").

*   **[AcetoneISO](https://en.wikipedia.org/wiki/AcetoneISO "wikipedia:AcetoneISO")** — 一体化ISO工具（支持BIN，MDF，NRG，IMG，DAA，DMG，CDI，B5I，BWI，PDI和ISO）。

	[http://sourceforge.net/projects/acetoneiso](http://sourceforge.net/projects/acetoneiso) || [acetoneiso2](https://www.archlinux.org/packages/?name=acetoneiso2)

*   **BashBurn** — Lightweight terminal based menu frontend for CD/DVD burning tools.

	[http://bashburn.dose.se/](http://bashburn.dose.se/) || [bashburn](https://www.archlinux.org/packages/?name=bashburn)

*   **[Brasero](https://en.wikipedia.org/wiki/Brasero_(software) "wikipedia:Brasero (software)")** — GNOME桌面的光碟烧录程序，被设计得尽可能简单易用。[gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/)的一部分。

	[https://wiki.gnome.org/Apps/Brasero](https://wiki.gnome.org/Apps/Brasero) || [brasero](https://www.archlinux.org/packages/?name=brasero)

*   **cdw** — *cdrecord*，*mkisofs*，*growisofs*，*dvd+rw-mediainfo*，*dvd+rw-format* 和*xorriso*的前端。

	[http://cdw.sourceforge.net/](http://cdw.sourceforge.net/) || [cdw](https://aur.archlinux.org/packages/cdw/)

*   **[GnomeBaker](https://en.wikipedia.org/wiki/GnomeBaker "wikipedia:GnomeBaker")** — Full featured CD/DVD burning application for the GNOME desktop.

	[http://gnomebaker.sourceforge.net/](http://gnomebaker.sourceforge.net/) || [gnomebaker](https://aur.archlinux.org/packages/gnomebaker/)

*   **Graveman** — GTK-based CD/DVD burning application. It requires configuration to point to correct devices.

	[http://graveman.tuxfamily.org/](http://graveman.tuxfamily.org/) || [graveman](https://aur.archlinux.org/packages/graveman/)

*   **[isomaster](https://en.wikipedia.org/wiki/ISO_Master "wikipedia:ISO Master")** — ISO image editor.

	[http://littlesvr.ca/isomaster](http://littlesvr.ca/isomaster) || [isomaster](https://aur.archlinux.org/packages/isomaster/)

*   **[K3b](https://en.wikipedia.org/wiki/K3b "wikipedia:K3b")** — Feature-rich and easy to handle CD burning and ripping application based on KDElibs.

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **[X-CD-Roast](https://en.wikipedia.org/wiki/X-CD-Roast "wikipedia:X-CD-Roast")** — Lightweight *cdrtools* front-end for CD and DVD writing.

	[http://www.xcdroast.org/](http://www.xcdroast.org/) || [xcdroast](https://aur.archlinux.org/packages/xcdroast/)

*   **Xfburn** — Simple front-end to the libburnia libraries with support for CD/DVD(-RW), ISO images, and BurnFree.

	[http://goodies.xfce.org/projects/applications/xfburn](http://goodies.xfce.org/projects/applications/xfburn) || [xfburn](https://www.archlinux.org/packages/?name=xfburn)

*   **xorriso-tcltk** — Graphical front-end to ISO and CD/DVD/BD burn tool xorriso

	[https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif](https://www.gnu.org/software/xorriso/xorriso-tcltk-screen.gif) || [libisoburn](https://www.archlinux.org/packages/?name=libisoburn)

## 回放

### CD

音频CD回放需要 [libcdio](https://www.archlinux.org/packages/?name=libcdio) 。

### DVD

如果你想播放加密的DVD，你必须安装libdvd*包：

*   [libdvdread](https://www.archlinux.org/packages/?name=libdvdread)
*   [libdvdcss](https://www.archlinux.org/packages/?name=libdvdcss)
*   [libdvdnav](https://www.archlinux.org/packages/?name=libdvdnav)

此外，你必须安装播放器软件。比较出名的播放器有 [MPlayer](/index.php/MPlayer "MPlayer")，[xine](https://en.wikipedia.org/wiki/Xine "wikipedia:Xine") 和 [VLC](/index.php/VLC "VLC")。参阅 [video players](/index.php/List_of_applications/Multimedia#Video_players "List of applications/Multimedia") 和 [MPlayer](/index.php/MPlayer#DVD_playing "MPlayer") 的详细说明。

## Ripping

[Ripping](https://en.wikipedia.org/wiki/Ripping "wikipedia:Ripping") is the process of copying audio or video content to a hard disk, typically from removable media or media streams.

### CD

*   **[Abcde](https://en.wikipedia.org/wiki/ABCDE "wikipedia:ABCDE")** — Comprehensive command-line tool for ripping audio CDs.

	[https://abcde.einval.com/](https://abcde.einval.com/) || [abcde](https://www.archlinux.org/packages/?name=abcde)

*   **[Asunder](https://en.wikipedia.org/wiki/Asunder "wikipedia:Asunder")** — GTK+-based CD ripping program.

	[http://littlesvr.ca/asunder/](http://littlesvr.ca/asunder/) || [asunder](https://www.archlinux.org/packages/?name=asunder)

*   **[cdparanoia](https://en.wikipedia.org/wiki/cdparanoia "wikipedia:cdparanoia")** — Compact Disc Digital Audio (CDDA) Digital Audio Extraction (DAE) tool.

	[https://xiph.org/paranoia/index.html](https://xiph.org/paranoia/index.html) || [cdparanoia](https://www.archlinux.org/packages/?name=cdparanoia)

*   **Goobox** — CD player and ripper for GNOME.

	[https://people.gnome.org/~paobac/goobox/](https://people.gnome.org/~paobac/goobox/) || [goobox](https://www.archlinux.org/packages/?name=goobox)

*   **[Grip](https://en.wikipedia.org/wiki/Grip_(software) "wikipedia:Grip (software)")** — Fast and light CD ripper within the GNOME project that resembles [Audiograbber](https://en.wikipedia.org/wiki/Audiograbber "wikipedia:Audiograbber").

	[https://sourceforge.net/projects/grip/](https://sourceforge.net/projects/grip/) || [grip](https://aur.archlinux.org/packages/grip/).

*   **[K3b](https://en.wikipedia.org/wiki/K3b "wikipedia:K3b")** — Feature-rich and easy to handle CD/DVD burning and ripping application based on KDElibs.

	[http://www.k3b.org/](http://www.k3b.org/) || [k3b](https://www.archlinux.org/packages/?name=k3b)

*   **morituri** — CD ripper aiming for accuracy over speed. Uses cdparanoia, MusicBrainz, AccurateRip.

	[http://thomas.apestaart.org/morituri/trac/](http://thomas.apestaart.org/morituri/trac/) || [morituri-git](https://aur.archlinux.org/packages/morituri-git/)

*   **ripperX** — GTK+ program to rip CD audio tracks and encode them to the Ogg, MP3, or FLAC formats.

	[https://sourceforge.net/projects/ripperx/](https://sourceforge.net/projects/ripperx/) || [ripperx](https://www.archlinux.org/packages/?name=ripperx)

*   **ripright** — Minimal CD ripper modeled on autorip.

	[http://www.mcternan.me.uk/ripright/](http://www.mcternan.me.uk/ripright/) || [ripright](https://aur.archlinux.org/packages/ripright/)

*   **ripit** — Command-line ripper that supports MusicBrainz, freeddb and various codecs.

	[http://www.suwald.com/ripit/news.php](http://www.suwald.com/ripit/news.php) || [ripit](https://aur.archlinux.org/packages/ripit/)

*   **rubyripper** — Audiodisk ripper that tries to deliver a secure rip through multiple rippings of the same track and corrections of any differences.

	[https://code.google.com/archive/p/rubyripper/](https://code.google.com/archive/p/rubyripper/) || [rubyripper](https://aur.archlinux.org/packages/rubyripper/)

*   **shnsplit** — Splits .wav and .flac files according to a CUE sheet and encodes the resulting pieces. A useful companion to ABCDE.

	[http://www.etree.org/shnutils/shntool/](http://www.etree.org/shnutils/shntool/) || [shntool](https://www.archlinux.org/packages/?name=shntool)

*   **[Sound Juicer](https://en.wikipedia.org/wiki/Sound_Juicer "wikipedia:Sound Juicer")** — CD ripper for GNOME.

	[https://wiki.gnome.org/Apps/SoundJuicer](https://wiki.gnome.org/Apps/SoundJuicer) || [sound-juicer](https://www.archlinux.org/packages/?name=sound-juicer)

*   **soundKonverter** — Front-end to various audio converters.

	[https://www.linux-apps.com/content/show.php?content=29024](https://www.linux-apps.com/content/show.php?content=29024) || [soundkonverter](https://www.archlinux.org/packages/?name=soundkonverter)

### DVD

Often, the process of ripping a DVD can be broken down into two subtasks:

1.  **Data extraction** — Copying the audio and/or video data to a hard disk,
2.  [Transcoding](https://en.wikipedia.org/wiki/Transcode "wikipedia:Transcode") — Converting the extracted data into a suitable format.

Some utilities perform both tasks, whilst others focus on one aspect or the other:

*   **Avidemux** — Multithreaded video transcoder, which offers both a graphical and command-line interface with many preset configurations. Influenced by Handbrake.

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-qt-git](https://aur.archlinux.org/packages/avidemux-qt-git/)

*   **dvd-vr** — Tool which easily converts VRO files extracted from a [DVD-VR](https://en.wikipedia.org/wiki/DVD-VR "wikipedia:DVD-VR") and splits them in regular VOB files.

	[http://www.pixelbeat.org/programs/dvd-vr/](http://www.pixelbeat.org/programs/dvd-vr/) || [dvd-vr](https://aur.archlinux.org/packages/dvd-vr/)

*   **[dvdbackup](/index.php/Dvdbackup "Dvdbackup")** — Tool for pure data extraction which does not transcode. It is useful for creating *exact* copies of encrypted DVDs in conjunction with **libdvdcss** or for decrypting video for other utilities unable to read encrypted DVDs.

	[http://dvdbackup.sourceforge.net/](http://dvdbackup.sourceforge.net/) || [dvdbackup](https://www.archlinux.org/packages/?name=dvdbackup)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Complete and free Internet live audio and video broadcasting solution for Linux/Unix, capable to do a direct rip in any format (audio/video) from a DVD-Video ISO image, just select the input as the ISO image and proceed with the desired options. It also allows to downmixing, shrinking, spliting, selecting streams among other features.

	[http://ffmpeg.org/](http://ffmpeg.org/) || See [article](/index.php/FFmpeg#Package_installation "FFmpeg")

*   **HandBrake** — Multithreaded video transcoder, which offers both a graphical and command-line interface with many preset configurations.

	[https://handbrake.fr/](https://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **Hybrid** — Multi platform Qt based frontend for a bunch of other tools which can convert nearly every input to x264/Xvid/VP8 + ac3/ogg/mp3/aac/flac inside an mp4/m2ts/mkv/webm/mov/avi container, a Blu-ray or an AVCHD structure.

	[http://www.selur.de/](http://www.selur.de/) || [hybrid-encoder](https://aur.archlinux.org/packages/hybrid-encoder/)

*   **[MEncoder](/index.php/MEncoder "MEncoder")** — Free command line video decoding, encoding and filtering tool released under the GNU GPL. It is a close sibling to MPlayer and can convert all the formats that MPlayer understands into a variety of compressed and uncompressed formats using different codecs. Wrapper programs like [h264enc](https://aur.archlinux.org/packages/h264enc/) and [undvd](https://aur.archlinux.org/packages/undvd/) can provide an assistive interface. Many [GUI frontends](/index.php/MEncoder#GUI_frontends "MEncoder") are available.

	[http://www.mplayerhq.hu/](http://www.mplayerhq.hu/) || [mencoder](https://www.archlinux.org/packages/?name=mencoder)

*   **Transcode** — Video/DVD ripper and encoder with the CLI.

	[http://transcoding.org/](http://transcoding.org/) || [transcode](https://www.archlinux.org/packages/?name=transcode)

#### dvd::rip

dvd::rip是[transcode](https://www.archlinux.org/packages/?name=transcode)的前端，用来将DVD提取到硬盘并解码或者实时转码。

以下的包应被安装：

*   [dvdrip](https://www.archlinux.org/packages/?name=dvdrip): [transcode](https://www.archlinux.org/packages/?name=transcode) 的GTK前端，可以抓取并解码。
*   [libdv](https://www.archlinux.org/packages/?name=libdv): DV视频软件解码器。
*   [xvidcore](https://www.archlinux.org/packages/?name=xvidcore): 可以转码为 XviD 的开源 MPEG-4 视频编码解码器(DivX 的自由替代)
*   [divx4linux](https://aur.archlinux.org/packages/divx4linux/): If you want to encode your ripped files as DivX.
*   [subtitleripper](https://aur.archlinux.org/packages/subtitleripper/): If you want to read and process subtitles.

The dvd::rip preferences are mostly well-documented/self-explanatory. If you need help with something, see [http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp](http://www.exit1.org/dvdrip/doc/gui-gui_pref.cipp).

抓取 DVD 只需选择需要的编码格式，设置标题并点击 "Rip" 按钮。

## 疑难解答

### Brasero fails to normalize audio CD

If you try to burn it may stop at the first step called Normalization.

As a workaround you can disable the normalization plugin using the *Edit > Plugins* menu

### VLC: Error "... could not open the disc /dev/dvd"

如果你收到类似这样的错误

```
vlc dvdread could not open the disc "/dev/dvd"

```

it may be because there is no device node `/dev/dvd` on your system. Udev no longer creates `/dev/dvd` and instead uses `/dev/sr0`. To fix this, edit the VLC configuration file (`~/.config/vlc/vlcrc`):

```
# DVD device (string)
dvd=/dev/sr0

```

### DVD设备噪音大

如果播放DVD导致系统很吵，可能是因为光碟转地比需要的速度更快。暂时改变设备的转速，运行：

```
# eject -x 12 /dev/dvd

```

有时：

```
# hdparm -E12 /dev/dvd

```

可以使用设备所支持的任何速度，或者0来表示最大速度。

[设置CD-ROM和DVD-ROM设备的转速](http://michal.kosmulski.org/computing/tips/cd-rom-speed.html)

### Playback does not work with new computer (new DVD-Drive)

If playback does not work and you have a new computer (new DVD-Drive) the reason might be that the [region code](https://en.wikipedia.org/wiki/DVD_region_code "wikipedia:DVD region code") is not set. You can read and set the region code with the [regionset](https://aur.archlinux.org/packages/regionset/) package.

### None of the above programs are able to rip/encode a DVD to my hard disk!

Make sure the region of your DVD reader is set correctly; otherwise, you will get loads of inexplicable [CSS](https://en.wikipedia.org/wiki/Content_Scramble_System "wikipedia:Content Scramble System")-related errors. Use the [regionset](https://aur.archlinux.org/packages/regionset/) package to do so.

### GUI program log indicates problems with backend program

If you use a GUI program and experience problems which the program's log blames on some backend program, then try to reproduce the problem by the logged backend program arguments. Whether you succeed with reproducing or not, you may report the logged lines and your own findings to the places mentioned in [#Burn backend problems](#Burn_backend_problems) section.

#### Special case: medium error / write error

Here are some typical messages about the drive disliking the medium. This can only be solved by using a different drive or a different medium. A different program will hardly help.

Brasero with backend growisofs:

```
BraseroGrowisofs stderr: :-[ WRITE@LBA=0h failed with SK=3h/ASC=0Ch/ACQ=00h]: Input/output error

```

Brasero with backend libburn:

```
BraseroLibburn Libburn reported an error SCSI error on write(16976,16): [3 0C 00] Write error

```

### AHCI

如果你的新DVD设备已被检测到但不能挂载光盘，检查你的BIOS是否使用了 [AHCI](/index.php/AHCI "AHCI") 并将模块添加到内核映像。

编辑 `/etc/mkinitcpio.conf` 并将 `ahci` 添加到 `MODULES` 变量(更多信息参阅 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio"))：

```
MODULES="ahci"

```

重构内核映像以包括新添加的模块：

```
# mkinitcpio -p linux

```

### BD-R DL 50GB errors on trying to burn second layer

Using *growisofs* from [dvd+rw-tools](https://www.archlinux.org/packages/?name=dvd%2Brw-tools) for burning 50GB BD-R DL discs might result in a fatal error and damaged media, such as:

 `$ growisofs -Z /dev/sr0 -J -R -V "label" files` 
```
Executing 'mkisofs -J -R -V label files | builtin_dd of=/dev/sr0 obs=32k seek=0'
I: -input-charset not specified, using utf-8 (detected in locale settings)
  0.03% done, estimate finish Fri Jan 29 19:50:36 2016
  0.05% done, estimate finish Fri Jan 29 19:50:36 2016
  0.08% done, estimate finish Fri Jan 29 19:50:36 2016
/dev/sr0: pre-formatting blank BD-R for 49.8GB...
/dev/sr0: "Current Write Speed" is 8.2x4390KBps.
  0.11% done, estimate finish Sat Jan 30 03:29:13 2016
  0.13% done, estimate finish Sat Jan 30 02:10:01 2016
...
 63.20% done, estimate finish Fri Jan 29 20:43:45 2016
:-[ WRITE@LBA=b6d820h failed with SK=3h/WRITE ERROR]: Input/output error
:-( write failed: Input/output error
/dev/sr0: flushing cache
/dev/sr0: closing track
/dev/sr0: closing session
:-[ CLOSE SESSION failed with SK=5h/INVALID FIELD IN CDB]: Input/output error
/dev/sr0: reloading tray

```

This happened at the 25GB boundary when starting to write the second layer. Using *cdrecord* from [cdrtools](https://www.archlinux.org/packages/?name=cdrtools) works with no problems. Tested with a 'HL-DT-ST BD-RE WH16NS40' LG burner, and Verbatim BD-R DL 6x discs (#96911). [FS#47797](https://bugs.archlinux.org/task/47797)

### Disc tray autocloses

If after ejecting a cd, either by using the `eject` command, or pushing the drive button, the drive disc tray autocloses before being able to remove the disc, try the following command:

```
# sysctl -w dev.cdrom.autoclose=0

```

如果问题解决，使改动永久生效：

 `/etc/sysctl.d/60-cdrom-autoclose.conf`  `dev.cdrom.autoclose = 0` 

## 另请参阅

*   在美国，backup of physically obtained media is allowed under these conditions: [About Piracy - RIAA](https://www.riaa.com/resources-learning/about-piracy/).
*   [Convert any Movie to DVD Video](/index.php/Convert_any_Movie_to_DVD_Video "Convert any Movie to DVD Video")
*   [Libburnia项目的主页](http://libburnia-project.org/)