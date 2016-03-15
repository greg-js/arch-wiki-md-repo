เอกสารชุดนี้จะช่วยคุณในการติดตั้ง Arch Linux ขั้นพื้นฐาน โดยการจัดทำจะอ้างอิงจาก installation script ของเวอร์ชัน 0.6 (widget)

## Contents

*   [1 คำแนะนำเบื้องต้น](#.E0.B8.84.E0.B8.B3.E0.B9.81.E0.B8.99.E0.B8.B0.E0.B8.99.E0.B8.B3.E0.B9.80.E0.B8.9A.E0.B8.B7.E0.B9.89.E0.B8.AD.E0.B8.87.E0.B8.95.E0.B9.89.E0.B8.99)
*   [2 สิ่งที่จำเป็นสำหรับการติดตั้ง](#.E0.B8.AA.E0.B8.B4.E0.B9.88.E0.B8.87.E0.B8.97.E0.B8.B5.E0.B9.88.E0.B8.88.E0.B8.B3.E0.B9.80.E0.B8.9B.E0.B9.87.E0.B8.99.E0.B8.AA.E0.B8.B3.E0.B8.AB.E0.B8.A3.E0.B8.B1.E0.B8.9A.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)
*   [3 การติดตั้งจาก Arch-CD](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.88.E0.B8.B2.E0.B8.81_Arch-CD)
    *   [3.1 การจัดการ partition ของฮาร์ดดิสค์](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.88.E0.B8.B1.E0.B8.94.E0.B8.81.E0.B8.B2.E0.B8.A3_partition_.E0.B8.82.E0.B8.AD.E0.B8.87.E0.B8.AE.E0.B8.B2.E0.B8.A3.E0.B9.8C.E0.B8.94.E0.B8.94.E0.B8.B4.E0.B8.AA.E0.B8.84.E0.B9.8C)
    *   [3.2 ตั้งค่า Mountpoints](#.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2_Mountpoints)
    *   [3.3 เลือก Packages](#.E0.B9.80.E0.B8.A5.E0.B8.B7.E0.B8.AD.E0.B8.81_Packages)
    *   [3.4 ติดตั้ง Packages](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_Packages)
    *   [3.5 ติดตั้ง Kernel](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_Kernel)
    *   [3.6 แก้ไขการตั้งค่า Config Files](#.E0.B9.81.E0.B8.81.E0.B9.89.E0.B9.84.E0.B8.82.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2_Config_Files)
    *   [3.7 ติดตั้ง Bootloader](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_Bootloader)
    *   [3.8 พร้อมแล้วที่จะ reboot](#.E0.B8.9E.E0.B8.A3.E0.B9.89.E0.B8.AD.E0.B8.A1.E0.B9.81.E0.B8.A5.E0.B9.89.E0.B8.A7.E0.B8.97.E0.B8.B5.E0.B9.88.E0.B8.88.E0.B8.B0_reboot)
*   [4 การติดตั้ง Arch ในรูปแบบอื่นๆ](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_Arch_.E0.B9.83.E0.B8.99.E0.B8.A3.E0.B8.B9.E0.B8.9B.E0.B9.81.E0.B8.9A.E0.B8.9A.E0.B8.AD.E0.B8.B7.E0.B9.88.E0.B8.99.E0.B9.86)
*   [5 ก้าวแรกของคุณ กับ Arch](#.E0.B8.81.E0.B9.89.E0.B8.B2.E0.B8.A7.E0.B9.81.E0.B8.A3.E0.B8.81.E0.B8.82.E0.B8.AD.E0.B8.87.E0.B8.84.E0.B8.B8.E0.B8.93_.E0.B8.81.E0.B8.B1.E0.B8.9A_Arch)

## คำแนะนำเบื้องต้น

นี่เป็นการแนะนำอย่างง่ายและรวดเร็ว สำหรับผู้ที่ยังไม่รู้จัก Arch เป็นอย่างดี นอกจากนี้บทความนี้ยังคำนึงถึงผู้ใช้ที่มี ระบบปฏิบัติการ Windows อยู่ในเครื่อง และอยากติดตั้ง Arch Linux โดยไม่เป็นอันตรายของส่วนอื่นๆ

คู่มือนี้สำหรับฮาร์ดแวร์ "ธรรมดา" เท่านั้น และจะไม่มีการอ้างอิงถึงอุปกรณ์พิเศษเช่น SCSI

คู่มือนี้สันนิษฐานว่าระบบปฏิบัติการ Windows จะอยู่ใน Partition แรกของฮาร์ดดิสค์ มิเช่นนั้น GRUB (โปรแกรม load ระบบปฏิบัติการ) จะไม่สามารถหามันได้

## สิ่งที่จำเป็นสำหรับการติดตั้ง

*   Archlinux Base Installation CD หรือ Full-Installation-CD

*   ฮาร์ดดิสค์เปล่าหรือพื้นที่ว่างใน partition ใด partition หนึ่งบนฮาร์ดดิสค์ คุณต้องแยกพื้นที่ว่างดังกล่าวออกจาก partition ที่มีอยู่ใน Windows โดยการใช้โปรแกรมจัดการ partition (เช่น Partition Magic)

## การติดตั้งจาก Arch-CD

*   ใส่ CD เข้าไปใน drive ของคุณ reboot เครื่องและตรวจสอบว่า BIOS ถูกตั้งให้ boot เครื่องจาก CD-ROM drive เป็นอันดับแรก

*   คุณควรจะเห็นหน้าจอแบบนี้:

[http://home.arcor.de/Langeland/1.png](http://home.arcor.de/Langeland/1.png) หน้าหลักในการ Boot ของ Arch

*   กด `Enter`
*   หลังจากเสร็จสิ้นขั้นตอนการเริ่มต้นระบบ พิมพ์:

```
/arch/setup

```

คุณจะเริ่มตั้นการติดตั้งจาก CD ก่อน ดังนั้น driver สำหรับ network card จึงยังไม่จำเป็น

หลังจากนั้นหน้าจอจะแสดงเมนูหลัก:

[http://home.arcor.de/Langeland/6.png](http://home.arcor.de/Langeland/6.png) เมนูหลัก

### การจัดการ partition ของฮาร์ดดิสค์

หากคุณมีฮาร์ดดิสค์เปล่า คุณสามารถข้ามขั้นตอนนี้ไปได้ และเลือกตัวเลือก Auto-Partitioning โปรดจำไว้ว่าตัวเลือกนี้จะลบ partition ทุกอันบนฮาร์ดดิสค์ของคุณ! หากคุณต้องการเก็บ partition ใดๆ ก็ตามไว้บนฮาร์ดดิสค์ โปรดทำตามขั้นตอนต่อไปนี้:

*   เลือก Prepare Hard-Drive.
*   เลือก Partition Hard-Drive.
*   เลือกฮาร์ดดิสค์ที่คุณต้องการติดตั้ง Arch-Linux
*   โปรแกรม cfdisk จะถูกเรียกใช้งานและคุณสามารถสร้าง partition สำหรับติดตั้งได้ โดยการติดตั้ง Arch-Base-Installation จะต้องการอย่างน้อยสอง partition:

```
 * partition สำหรับ swap หนึ่ง partition
 * partition สำหรับข้อมูลหนึ่ง partition

```

*   ณ จุดนี้หน้าจอของคุณอาจจะดูคล้ายคลึงกับหน้าจอนี้ (ถ้าคุณมี NTFS partition สำหรับระบบปฏิบัติการ Windows):

[http://home.arcor.de/Langeland/9.png](http://home.arcor.de/Langeland/9.png) cfdisk

*   ห้ามยุ่งกับ NTFS หรือ VFAT เด็ดขาด ไม่เช่นนั้น Windows ของคุณอาจจะไม่สามารถทำงานได้อีก
*   type ของ swap partition ต้องถูกตั้งให้เป็น 82
*   หากคุณต้องการออกจาก cfdisk โดยไม่แก้ไขอะไรเลย ให้เลือก quit แต่ถ้าต้องการแก้ไขให้เลือก write
*   หลังจากการใช้งาน cfdisk คุณควรจะเจอกับหน้าจอคล้ายคลึงกับหน้าจอนี้:

[http://home.arcor.de/Langeland/10.png](http://home.arcor.de/Langeland/10.png) รูปแบบการจัด Partition

### ตั้งค่า Mountpoints

*   เลือกที่: Set Filesystem Mountpoints
*   เลือก partition ที่คุณตั้งให้เป็น swap
*   เลือก partition ที่เหลือสำหรับใช้เป็น partition ของระบบ (เพื่อที่จะ mount ให้เป็น /)
*   เลือก ext3 เป็น Filesystem
*   เลือก DONE !!

*ขั้นตอนสุดท้ายเป็นขั้นตอนที่สำคัญ หลายๆ คนข้ามขั้นตอนนี้ไป ระบบติดตั้งจะไม่ติดตั้งข้อมูลใดๆ หากท่านไม่เลือกที่ DONE*

### เลือก Packages

*   เลือก CD
*   คุณควรจะเห็นหน้าจอคล้ายหน้าจอนี้:

[http://home.arcor.de/Langeland/11.png](http://home.arcor.de/Langeland/11.png) Package ประเภทต่างๆ

*   สำหรับตอนนี้คุณควรเลือกแค่ base และ editors เท่านั้น
*   และคุณควรจะเลือกลง package ทุกตัวในแต่ละประเภทตามที่ระบบแนะนำ
*   กด OK

### ติดตั้ง Packages

*   นี่เป็นขั้นตอนที่ง่ายมาก: เพียงกด Install Packages และกด OK ทุกอย่างจะถูกติดตั้งจาก CD ลงในเครื่องของคุณ

### ติดตั้ง Kernel

*   เลือก "Kernel 2.6.x for IDE/SCSI systems" นอกจากคุณต้องการติดตั้ง kernel ประเภทอื่นๆ

### แก้ไขการตั้งค่า Config Files

*   เลือกใช้ nano ในการแก้ไขไฟล์ตั้งค่าต่างๆ

**คุณต้องแก้ไขไฟล์ rc.conf** ถ้าคุณต้องการแก้ keyboard layout ของคุณ ตัวอย่างเช่น th คือรูปแบบคีย์บอร์ดภาษาไทย

*   ถ้าคุณใช้ router คุณสามารถลองใช้การตั้งค่านี้ใน /etc/rc.conf:

```
#Router address
gateway="default gw 192.168.0.1"
ROUTES=(gateway) #ลบเครื่องหมาย ! หน้าคำว่า gateway ออกไป

```

*   ใน /etc/resolf.conf

```
nameserver 192.168.0.1

```

*   nano นั้นเป็นโปรแกรม text editor ที่สามารถเข้าใจได้ง่าย: Strg-o ( Ctrl-o ) บันทึกไฟล์, Strg-x ( Ctrl-x ) บันทึกไฟล์และออกจาก nano.

**คุณต้องแก้ไขไฟล์** menu.lst*.

*   ไฟล์ menu.lst ใช้สร้าง bootloader ซึ่งจะทำหน้าที่เรียกระบบปฏิบัติการขึ้นมา คุณสามารถเลือกที่จะใช้ Windows หรือ Arch ได้จากไฟล์นี้
*   คุณจะพบกับหน้าจอดังนี้:

[http://home.arcor.de/Langeland/13.png](http://home.arcor.de/Langeland/13.png) Menu.lst

*   ทุกสิ่งทุกอย่างควรจะถูกตั้งค่าเรียบร้อยแล้วสำหรับการใช้งาน Arch คุณเพียงต้องเพิ่มคำสั่งเหล่านี้เข้าไป เพื่อที่จะสามารถใช้งาน Windows ได้:

```
title Windows
rootnoverify (hd0,0)
chainloader +1

```

กด Strg-O และ Strg-X เพื่อบันทึกไฟล์และออกจาก nano

### ติดตั้ง Bootloader

*   เลือก grub
*   เลือกรายการบนสุด เพื่อติดตั้ง bootloader ที่ Master Boot Record (MBR)

### พร้อมแล้วที่จะ reboot

*   ออกจากเมนูหลัก พิมพ์คำว่า reboot แล้วกด enter เครื่องของคุณจะ reboot
*   เอาแผ่น CD ออก
*   คุณสามารถเลือกระบบปฏิบัติการที่จะใช้ได้ระหว่าง Windows และ Arch โดย Arch จะถูกเลือกก่อนเป็นอันดับแรก

## การติดตั้ง Arch ในรูปแบบอื่นๆ

*   [Fast Arch Install from existing Linux System](/index.php/Fast_Arch_Install_from_existing_Linux_System "Fast Arch Install from existing Linux System")
*   [The Official Arch Linux Installation Guide](https://www.archlinux.org/static/docs/arch-install-guide.html)

## ก้าวแรกของคุณ กับ Arch

*   Login เป็น root.
*   พิมพ์คำสั่ง `passwd` เพื่อตั้งรหัสผ่านสำหรับผู้ใช้งานชื่อ root.

```
# passwd

```

*   เพิ่มผู้ใช้งาน โดยคุณสามารถใช้ script ชื่อ adduser ได้ โดยผู้ใช้ของคุณควรจะอยู่ใน group ชื่อ users, audio และ optical

```
# adduser

```

ตอนนี้คุณสามารถเริ่มติดตั้ง Internet และใช้งาน package ด้วย pacman ได้แล้ว ขอให้คุณสนุกกับ Arch Linux