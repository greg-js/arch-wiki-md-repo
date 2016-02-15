本文描述如何在系统启动时为root文件系统做LVM快照，这些快照可以用来在最短时间内进行[全系统备份](/index.php/Full_System_Backup_with_tar "Full System Backup with tar")，或者是测试系统的更新以便于按需回滚。

## Contents

*   [1 前提条件](#.E5.89.8D.E6.8F.90.E6.9D.A1.E4.BB.B6)
*   [2 安装](#.E5.AE.89.E8.A3.85)
*   [3 用法](#.E7.94.A8.E6.B3.95)
    *   [3.1 备份](#.E5.A4.87.E4.BB.BD)
    *   [3.2 更新回滚](#.E6.9B.B4.E6.96.B0.E5.9B.9E.E6.BB.9A)
*   [4 已知的问题](#.E5.B7.B2.E7.9F.A5.E7.9A.84.E9.97.AE.E9.A2.98)

## 前提条件

你需要一个root文件系统为[LVM](/index.php/LVM "LVM")分区并且利用[systemd](/index.php/Systemd "Systemd")进行引导的系统，确认[LVM快照](/index.php/LVM#Snapshots "LVM")相关的前提条件已经正确安装。

## 安装

在系统启动过程中，利用一个新的systemd service创建一个干净的root卷的快照，创建`/etc/systemd/system/mk-lvm-snapshots.service` 包含以下内容:

```
[Unit]
Description=make LVM snapshots
Requires=local-fs-pre.target
DefaultDependencies=no
Conflicts=shutdown.target
After=local-fs-pre.target
Before=local-fs.target

[Install]
WantedBy=make-snapshots.target

[Service]
Type=oneshot
ExecStart=/usr/sbin/lvcreate -L10G -n snap-root -s lvmvolume/root
```

将上述`lvcreate`命令中的root卷的卷组名和卷名改成你系统中的相关名字，如有必要修改上述快照的大小。如果还有其它的文件系统需要进行快照，则将上述`ExecStart`属性扩展为多条命令，用分号隔开(注意在分号前后均要留有一个空格，详见[systemd service manual](http://www.freedesktop.org/software/systemd/man/systemd.service.html#Command%20lines))。

**Note:** 你可以在运行的系统上测试一下`# lvcreate`命令直到得到的结果如你所需。可以用`# lvremove`删除此快照。在运行的系统上做的快照不如在单用户模式下或是在系统启动时做的快照一致性更好。

创建一个新的systemd target `/etc/systemd/system/make-snapshots.target`:

```
[Unit]
Description=Make Snapshots
Requires=multi-user.target
```

如果`multi-user.target`不是你的缺省target，则进行相应的修改。

将此新的服务生效：`# systemctl enable mk-lvm-snapshots.service`。

如果系统启动一个新的target，LVM快照会在挂载完本地文件系统后进行创建，为此，创建一个[GRUB](/index.php/GRUB "GRUB") menu entry来启动这个新的target，基于正常启动的`grub.cfg`创建`/boot/grub/custom.cfg`，并在其中传递给内核启动`make-snapshots.target`的参数。

```
### make snapshots ###
menuentry 'Arch GNU/Linux, make snapshots' --class arch --class gnu-linux --class gnu --class os {
...
        echo    'Loading Linux core repo kernel ...'
        linux   /boot/vmlinuz-linux root=/dev/mapper/lvmvolume-root ro **systemd.unit=make-snapshots.target**
        echo    'Loading initial ramdisk ...'
        initrd  /boot/initramfs-linux.img
} 
```

如果{{ic|grub.cfg}发生了变更，记着相应修正`custom.cfg`。

系统通过此grub entry启动后`# lvs`应该可以看到新创建的快照。

**Tip:** 利用`# journalctl -u mk-lvm-snapshots.service`命令可以看到新的服务启动过程的相关输出。

## 用法

### 备份

如要进行全系统的备份，首先以上述创建快照的target重启系统，挂载快照卷（and further volumes, if required)，最好以只读的方式 (<tt>-o</tt>) 挂载，便可以进行全系统备份，例如可以采用[Full System Backup with tar](/index.php/Full_System_Backup_with_tar "Full System Backup with tar")文章中的办法进行备份。

在备份的过程中并不影响现有系统的使用，因为所有正常卷的修改都反应在了快照里了。备份完后不要忘记删除这个快照，copy-on-write的快照模式会使正常root卷的所有修改用光你的快照卷空间。如果快照卷空间用光，LVM并不能自动增长快照空间，则LVM会拒绝进一步向正常卷中写入数据或者直接丢掉快照，都应该避免。

### 更新回滚

另外一个LVM快照的用法是进行系统更新的测试和回滚，即为已知正常使用的系统先做一个快照，再进行更新。

如果想要固化更新的内容，则可以通过`# lvremove`删除快照的方式；如果想要回滚到更新前的状态，可以通过`# lvconvert --merge`恢复快照，在下次系统启动时快照会被合并到正常卷中，创建快照之后所有对正常卷的修改均被撤消。

**Note:** 快照合并会快照卷也将不复存在，如果想进一步测试则必须再创建一个快照卷。

## 已知的问题

根据[bug 681582](https://bugzilla.redhat.com/show_bug.cgi?id=681582)关闭一个有活动的快照卷的系统会很长时间（目前是1..3分钟）。有个变通的方法，在`/etc/systemd/system`中创建一个`/usr/lib/systemd/system/dmeventd.service`的拷由，并插入以下内容：

`JobTimeoutSec=10`:

```
[Unit]
Description=Device-mapper event daemon
Documentation=man:dmeventd(8)
Requires=dmeventd.socket
After=dmeventd.socket
DefaultDependencies=no
**JobTimeoutSec=10**

[Service]
Type=forking
ExecStart=/usr/sbin/dmeventd
ExecReload=/usr/sbin/dmeventd -R
Environment=SD_ACTIVATION=1
PIDFile=/run/dmeventd.pid
OOMScoreAdjust=-1000
```