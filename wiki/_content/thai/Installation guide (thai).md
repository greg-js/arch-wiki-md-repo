นี่คือเอกสารแนะนำการติดตั้ง [Arch Linux](/index.php/Arch_Linux_(%E0%B9%84%E0%B8%97%E0%B8%A2) "Arch Linux (ไทย)") โดยใช้ installation image อย่างเป็นทางการ ก่อนติดตั้ง เราแนะนำให้คุณอ่าน [คำถามที่พบบ่อย](/index.php/FAQ "FAQ") และถ้าคุณกำลังมองหาวิธีการติดตั้งแบบละเอียด ลองไปดูที่ [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch")

คุณสามารถขอความช่วยเหลือจากวิกิหรืออ่าน [man page](/index.php/Man_page "Man page") ของโปรแกรมต่าง ๆ; ดูที่ [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) สำหรับภาพโดยรวมในการตั้งค่า และสำหรับความช่วยเหลือเชิงโต้ตอบ คุณสามารถใช้ [ช่อง IRC](/index.php/IRC_channel "IRC channel") และ [กระดานข่าว](https://bbs.archlinux.org/) ได้

## Contents

*   [1 ก่อนเริ่มติดตั้ง](#.E0.B8.81.E0.B9.88.E0.B8.AD.E0.B8.99.E0.B9.80.E0.B8.A3.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)
    *   [1.1 ตั้งค่าเลย์เอาต์ของคีย์บอร์ด](#.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B9.80.E0.B8.A5.E0.B8.A2.E0.B9.8C.E0.B9.80.E0.B8.AD.E0.B8.B2.E0.B8.95.E0.B9.8C.E0.B8.82.E0.B8.AD.E0.B8.87.E0.B8.84.E0.B8.B5.E0.B8.A2.E0.B9.8C.E0.B8.9A.E0.B8.AD.E0.B8.A3.E0.B9.8C.E0.B8.94)
    *   [1.2 เชื่อมต่ออินเทอร์เน็ต](#.E0.B9.80.E0.B8.8A.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.A1.E0.B8.95.E0.B9.88.E0.B8.AD.E0.B8.AD.E0.B8.B4.E0.B8.99.E0.B9.80.E0.B8.97.E0.B8.AD.E0.B8.A3.E0.B9.8C.E0.B9.80.E0.B8.99.E0.B9.87.E0.B8.95)
    *   [1.3 อัพเดตเวลาของระบบ](#.E0.B8.AD.E0.B8.B1.E0.B8.9E.E0.B9.80.E0.B8.94.E0.B8.95.E0.B9.80.E0.B8.A7.E0.B8.A5.E0.B8.B2.E0.B8.82.E0.B8.AD.E0.B8.87.E0.B8.A3.E0.B8.B0.E0.B8.9A.E0.B8.9A)
    *   [1.4 แบ่งพาร์ทิชั่นของดิสก์](#.E0.B9.81.E0.B8.9A.E0.B9.88.E0.B8.87.E0.B8.9E.E0.B8.B2.E0.B8.A3.E0.B9.8C.E0.B8.97.E0.B8.B4.E0.B8.8A.E0.B8.B1.E0.B9.88.E0.B8.99.E0.B8.82.E0.B8.AD.E0.B8.87.E0.B8.94.E0.B8.B4.E0.B8.AA.E0.B8.81.E0.B9.8C)
    *   [1.5 ฟอร์แมตพาร์ทิชั่น](#.E0.B8.9F.E0.B8.AD.E0.B8.A3.E0.B9.8C.E0.B9.81.E0.B8.A1.E0.B8.95.E0.B8.9E.E0.B8.B2.E0.B8.A3.E0.B9.8C.E0.B8.97.E0.B8.B4.E0.B8.8A.E0.B8.B1.E0.B9.88.E0.B8.99)
    *   [1.6 Mount พาร์ทิชั่น](#Mount_.E0.B8.9E.E0.B8.B2.E0.B8.A3.E0.B9.8C.E0.B8.97.E0.B8.B4.E0.B8.8A.E0.B8.B1.E0.B9.88.E0.B8.99)
*   [2 การติดตั้ง](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)
    *   [2.1 เลือก mirror](#.E0.B9.80.E0.B8.A5.E0.B8.B7.E0.B8.AD.E0.B8.81_mirror)
    *   [2.2 ติดตั้งแพคเกจพื้นฐาน](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B9.81.E0.B8.9E.E0.B8.84.E0.B9.80.E0.B8.81.E0.B8.88.E0.B8.9E.E0.B8.B7.E0.B9.89.E0.B8.99.E0.B8.90.E0.B8.B2.E0.B8.99)
    *   [2.3 ตั้งค่าระบบ](#.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B8.A3.E0.B8.B0.E0.B8.9A.E0.B8.9A)
    *   [2.4 ติดตั้งบู๊ตโหลดเดอร์](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.9A.E0.B8.B9.E0.B9.8A.E0.B8.95.E0.B9.82.E0.B8.AB.E0.B8.A5.E0.B8.94.E0.B9.80.E0.B8.94.E0.B8.AD.E0.B8.A3.E0.B9.8C)
    *   [2.5 รีบู๊ตเครื่อง](#.E0.B8.A3.E0.B8.B5.E0.B8.9A.E0.B8.B9.E0.B9.8A.E0.B8.95.E0.B9.80.E0.B8.84.E0.B8.A3.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.87)
*   [3 หลังการติดตั้ง](#.E0.B8.AB.E0.B8.A5.E0.B8.B1.E0.B8.87.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)

## ก่อนเริ่มติดตั้ง

ดาวน์โหลดและบู๊ตจากสื่อการติดตั้งตามวิธีในหน้า [Category:Getting and installing Arch](/index.php/Category:Getting_and_installing_Arch "Category:Getting and installing Arch") จากนั้นจึงกลับมาทำตามขั้นตอนในหน้านี้

การติดตั้งจำเป็นต้องดึงแพคเกจมาจากอินเทอร์เน็ต ดังนั้นคุณต้องมีการเชื่อมต่ออินเทอร์เน็ตที่ใช้งานได้

### ตั้งค่าเลย์เอาต์ของคีย์บอร์ด

เลย์เอาต์เริ่มต้นของคีย์บอร์ดคือ US แต่คุณสามารถเพิ่มเลย์เอาต์ที่ต้องการได้โดยใช้คำสั่ง `loadkeys *keymap_file*`: ซึ่งอยู่ใน `/usr/share/kbd/keymaps/` (ไม่ต้องระบุ path และนามสกุลไฟล์ก็ได้)

### เชื่อมต่ออินเทอร์เน็ต

ปกติคุณจะใช้อินเทอร์เน็ตได้โดยอัตโนมัติผ่าน DHCP discovery หลังบู๊ตสื่อการติดตั้งอยู่แล้ว (ถ้าเป็นการเชื่อมต่อแบบใช้สาย)   แต่ถ้าใช้เครือข่ายแบบไร้สาย คุณต้องเรียกใช้โปรแกรม `wifi-menu` เพื่อตั้งค่าเครือข่ายก่อน; อ่านข้อมูลเพิ่มเติมที่ [การตั้งค่าเครือข่ายไร้สาย](/index.php/Wireless_network_configuration "Wireless network configuration")   และถ้าคุณต้องการใช้ static IP หรือใช้เครื่องมือจัดการเครือข่ายอื่น คุณต้องหยุดใช้ DHCP ด้วยคำสั่ง `systemctl stop dhcpcd@*eth0*.service` แล้วค่อยทำตามวิธีในหน้า [Netctl](/index.php/Netctl "Netctl")

### อัพเดตเวลาของระบบ

อ่าน [systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")

### แบ่งพาร์ทิชั่นของดิสก์

อ่านรายละเอียดที่หน้า [การแบ่งพาร์ทิชั่น](/index.php/Partitioning "Partitioning"); คุณอาจต้องสร้างพาร์ทิชั่นพิเศษขึ้นอยู่กับแต่ละกรณี ลองอ่านหน้า [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI") และ [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB")    และถ้าคุณต้องการใช้ stacked block devices สำหรับ [LVM](/index.php/LVM "LVM"), [การเข้ารหัสดิสก์](/index.php/Disk_encryption "Disk encryption") หรือ [RAID](/index.php/RAID "RAID") ก็ให้ทำในขั้นตอนนี้ด้วย

### ฟอร์แมตพาร์ทิชั่น

อ่าน [ระบบไฟล์](/index.php/File_systems#Create_a_file_system "File systems") และ [Swap](/index.php/Swap "Swap") สำหรับรายละเอียดและวิธีการ

### Mount พาร์ทิชั่น

Mount พาร์ทิชั่น root ที่ `/mnt` หลังจากนั้นให้สร้างและ mount ไดเร็คทอรี่อื่น ๆ (ถ้ามี) (เช่น `/mnt/boot`, `/mnt/home`, ...) จากนั้นให้เปิดใช้พาร์ทิชั่น *swap* ถ้าต้องการให้ *genfstab* มองเห็น

## การติดตั้ง

### เลือก mirror

แก้ไข `/etc/pacman.d/mirrorlist` และเลือก download mirror ที่ต้องการ เราแนะนำให้ใช้ mirror ในท้องถิ่นจะเร็วที่สุด; ลองอ่านรายละเอียดที่หน้า [Mirrors](/index.php/Mirrors "Mirrors")   เนื่องจากการตั้งค่าในไฟล์ `mirrorlist` จะถูกนำไปใช้ในระบบใหม่ด้วยเมื่อคุณใช้สคริปต์ *pacstrap* เราแนะนำให้คุณตั้งค่า mirror ให้ถูกต้องเลยในขั้นตอนนี้เพิ่มความสะดวก

*หมายเหตุ: mirror ที่ใช้ได้ดีในประเทศไทย เช่น ของ[ม.เกษตรศาสตร์](http://mirror.uni.net.th/)*

### ติดตั้งแพคเกจพื้นฐาน

ใช้สคริปต์ [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) เพื่อติดตั้งโปรแกรมจากกลุ่ม [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

ถ้าต้องการติดตั้งแพคเกจหรือกลุ่มแพคเกจอื่น ให้เพิ่มชื่อที่ต้องการติดตั้งต่อท้ายไปในคำสั่งด้านบนโดยเว้นช่องไฟระหว่างแต่ละชื่อ

### ตั้งค่าระบบ

สร้าง [fstab](/index.php/Fstab "Fstab") (ใช้ตัวเลือก `-U` หรือ `-L` ถ้าต้องการใช้ UUID หรือ label ในไฟล์):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

[Change root](/index.php/Change_root "Change root") เข้าไปในรากของระบบใหม่:

```
# arch-chroot /mnt

```

ตั้ง [ชื่อเครื่อง](/index.php/Hostname "Hostname"):

```
# echo *computer_name* > /etc/hostname

```

ตั้ง [โซนเวลา](/index.php/Time_zone "Time zone"):

```
# ln -s /usr/share/zoneinfo/*zone*/*subzone* /etc/localtime

```

เปิดใช้ [locales](/index.php/Locale "Locale") ที่ต้องการใน `/etc/locale.gen` จากนั้นก็สร้าง locale โดยใช้คำสั่ง:

```
# locale-gen

```

ตั้ง locale เริ่มต้นใน `/etc/locale.conf` และ `$HOME/.config/locale.conf`:

```
# echo LANG=*your_locale* > /etc/locale.conf

```

เพิ่ม [keymap](/index.php/Keymap "Keymap") และ [font](/index.php/Fonts#Console_fonts "Fonts") สำหรับคอนโซลใน `/etc/vconsole.conf`

ตั้งค่าเครือข่ายสำหรับเครื่องใหม่: อ่านหน้า [การตั้งค่าเครือข่าย](/index.php/Network_configuration "Network configuration") และ [การตั้งค่าเครือข่ายแบบไร้สาย](/index.php/Wireless_network_configuration "Wireless network configuration")

ตั้งค่า [/etc/mkinitcpio.conf](/index.php/Mkinitcpio "Mkinitcpio") เพิ่มเติมถ้าต้องการ จากนั้นสร้าง RAM disk ใหม่ด้วยคำสั่ง:

```
# mkinitcpio -p linux

```

กำหนดรหัสผ่านสำหรับผู้ใช้ root:

```
# passwd

```

### ติดตั้งบู๊ตโหลดเดอร์

อ่านหน้า [บู๊ตโหลดเดอร์](/index.php/Boot_loaders "Boot loaders") เพื่อดูวิธีการติดตั้งและการตั้งค่า

### รีบู๊ตเครื่อง

ออกจาก chroot โดยพิมพ์ `exit` หรือกดปุ่ม `Ctrl+D`

Unmount พาร์ทิชั่นทั้งหมดด้วยคำสั่ง `umount -R /mnt`: ขั้นตอนนี้จะทำให้คุณพบพาร์ทิชั่นที่ยังถูกใช้งานอยู่และไม่สามารถ unmount ได้ จะได้หาสาเหตุได้โดยใช้ [fuser](https://en.wikipedia.org/wiki/fuser_(Unix) "wikipedia:fuser (Unix)")

สุดท้ายให้รีบู๊ตเครื่องโดยพิมพ์คำสั่ง `reboot`: พาร์ทิชั่นที่ยังถูก mount อยู่จะถูก *systemd* ปลดออกโดยอัตโนมัติ   อย่าลืมดึงแผ่นซีดีหรือสื่อที่คุณใช้ในการบู๊ตเพื่อติดตั้งออกหลังรีบู๊ตด้วย  หลังรีบู๊ตเสร็จ คุณสามารถล็อกอินด้วยผู้ใช้ root

## หลังการติดตั้ง

ลองอ่าน [คำแนะนำทั่วไป](/index.php/General_recommendations "General recommendations") สำหรับวิธีการจัดการระบบและสิ่งที่คุณอาจอยากทำหลังติดตั้งเสร็จ (เช่น การติดตั้ง graphical user interface, เสียง, หรือ touchpad)

นอกจากนั้นยังมีแอพพลิเคชั่นอีกมากมายที่คุณอาจสนใจ ลองดูที่ [รายชื่อแอพพลิเคชั่น](/index.php/List_of_applications "List of applications")