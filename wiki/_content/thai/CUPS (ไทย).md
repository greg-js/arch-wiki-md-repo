## Contents

*   [1 คำแนะนำเบื้องต้น](#.E0.B8.84.E0.B8.B3.E0.B9.81.E0.B8.99.E0.B8.B0.E0.B8.99.E0.B8.B3.E0.B9.80.E0.B8.9A.E0.B8.B7.E0.B9.89.E0.B8.AD.E0.B8.87.E0.B8.95.E0.B9.89.E0.B8.99)
    *   [1.1 CUPS คืออะไร](#CUPS_.E0.B8.84.E0.B8.B7.E0.B8.AD.E0.B8.AD.E0.B8.B0.E0.B9.84.E0.B8.A3)
    *   [1.2 การแก้ปัญหา CUPS](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.81.E0.B8.81.E0.B9.89.E0.B8.9B.E0.B8.B1.E0.B8.8D.E0.B8.AB.E0.B8.B2_CUPS)
*   [2 การติดตั้ง CUPS](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_CUPS)
    *   [2.1 Packages](#Packages)
    *   [2.2 Download Printer PPD (ไฟล์รายละเอียดเครื่องพิมพ์)](#Download_Printer_PPD_.28.E0.B9.84.E0.B8.9F.E0.B8.A5.E0.B9.8C.E0.B8.A3.E0.B8.B2.E0.B8.A2.E0.B8.A5.E0.B8.B0.E0.B9.80.E0.B8.AD.E0.B8.B5.E0.B8.A2.E0.B8.94.E0.B9.80.E0.B8.84.E0.B8.A3.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.87.E0.B8.9E.E0.B8.B4.E0.B8.A1.E0.B8.9E.E0.B9.8C.29)
*   [3 การตั้งค่า CUPS](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2_CUPS)
    *   [3.1 ตัวเลือกต่างๆ](#.E0.B8.95.E0.B8.B1.E0.B8.A7.E0.B9.80.E0.B8.A5.E0.B8.B7.E0.B8.AD.E0.B8.81.E0.B8.95.E0.B9.88.E0.B8.B2.E0.B8.87.E0.B9.86)
    *   [3.2 Kernel Modules](#Kernel_Modules)
        *   [3.2.1 เครื่องพิมพ์ USB](#.E0.B9.80.E0.B8.84.E0.B8.A3.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.87.E0.B8.9E.E0.B8.B4.E0.B8.A1.E0.B8.9E.E0.B9.8C_USB)
        *   [3.2.2 เครื่องพิมพ์พอร์ทขนาน](#.E0.B9.80.E0.B8.84.E0.B8.A3.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.87.E0.B8.9E.E0.B8.B4.E0.B8.A1.E0.B8.9E.E0.B9.8C.E0.B8.9E.E0.B8.AD.E0.B8.A3.E0.B9.8C.E0.B8.97.E0.B8.82.E0.B8.99.E0.B8.B2.E0.B8.99)
        *   [3.2.3 การเรียกใช้งานโดยอัตโนมัติ](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.80.E0.B8.A3.E0.B8.B5.E0.B8.A2.E0.B8.81.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99.E0.B9.82.E0.B8.94.E0.B8.A2.E0.B8.AD.E0.B8.B1.E0.B8.95.E0.B9.82.E0.B8.99.E0.B8.A1.E0.B8.B1.E0.B8.95.E0.B8.B4)
    *   [3.3 CUPS Daemon](#CUPS_Daemon)
    *   [3.4 Web Interface และชุดเครื่องมือ](#Web_Interface_.E0.B9.81.E0.B8.A5.E0.B8.B0.E0.B8.8A.E0.B8.B8.E0.B8.94.E0.B9.80.E0.B8.84.E0.B8.A3.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.87.E0.B8.A1.E0.B8.B7.E0.B8.AD)
*   [4 ตั้งค่าการ Share เครื่องพิมพ์](#.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B8.81.E0.B8.B2.E0.B8.A3_Share_.E0.B9.80.E0.B8.84.E0.B8.A3.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.87.E0.B8.9E.E0.B8.B4.E0.B8.A1.E0.B8.9E.E0.B9.8C)
    *   [4.1 Linux กับ Linux](#Linux_.E0.B8.81.E0.B8.B1.E0.B8.9A_Linux)
    *   [4.2 Linux to Windows](#Linux_to_Windows)
    *   [4.3 Windows to Linux](#Windows_to_Linux)
    *   [4.4 Windows 2000 and Windows XP to Linux](#Windows_2000_and_Windows_XP_to_Linux)
    *   [4.5 Others to Linux, Linux to others](#Others_to_Linux.2C_Linux_to_others)
*   [5 Appendix](#Appendix)
    *   [5.1 Alternative CUPS Interfaces](#Alternative_CUPS_Interfaces)
    *   [5.2 PDF Virtual Printer](#PDF_Virtual_Printer)
    *   [5.3 Online Resources](#Online_Resources)
    *   [5.4 Specialized Cases](#Specialized_Cases)
        *   [5.4.1 Printing does not work/aborts with the HP Deskjet 700 Series Printers.](#Printing_does_not_work.2Faborts_with_the_HP_Deskjet_700_Series_Printers.)
        *   [5.4.2 Getting HP LaserJet 1010 to work](#Getting_HP_LaserJet_1010_to_work)
    *   [5.5 Another Source for Printer Drivers](#Another_Source_for_Printer_Drivers)
*   [6 Troubleshooting](#Troubleshooting)
    *   [6.1 As a result of upgrade](#As_a_result_of_upgrade)

## คำแนะนำเบื้องต้น

### CUPS คืออะไร

คัดมาจากเว็บไซท์ของ CUPS "The Common UNIX Printing System (CUPS) เป็นระบบการพิมพ์ cross-platform สำหรับสภาพแวดล้อมการทำงานบน UNIX มันถูกสร้างขึ้นมาให้รองรับกับ "Internet Printing Protocol" และสามารถทำงานได้อย่างสมบูรณ์แบบกับเครื่องพิมพ์แบบ Postscript และ Raster ส่วนใหญ่ CUPS เป็นโปรแกรม open-source ภายใต้ลิขสิทธิ์แบบ GNU GPL" ถึงแม้ว่าจะมีระบบการพิมพ์อื่นๆ เช่น LPRNG แต่ CUPS ก็ยังเป็นที่นิยมและยังง่ายต่อการใช้งาน CUPS เป็นระบบการพิมพ์มาตรฐานบน Arch Linux รวมถึง Linux distro อื่นๆ ด้วยเช่นกัน

### การแก้ปัญหา CUPS

วิธีที่ง่ายที่สุดในการแก้ปัญหาที่เกิดขึ้น คือตั้งค่า LogLevel ในไฟล์ `/etc/cups/cupsd.conf` ให้เป็น

```
LogLevel debug2

```

และดูรายละเอียดข้อผิดพลาดจากไฟล์ '/var/log/cups/error_log' ดังนี้

```
tail -n 100 -f /var/log/cups/error_log

```

ตัวอักษรทางซ้ายของการแสดงผลมีความหมายดังนี้

```
D = Debug
E = Error
I = Information
etc...

```

ไฟล์อื่นๆ เหล่านี้อาจจะมีประโยชน์ในการแก้ปัญหา

```
/var/log/cups/page_log 'แสดงรายละเอียดทุกครั้งที่การพิมพ์เสร็จสิ้น'
/var/log/cups/access_log 'แสดงรายละเอียดการเรียกใช้งาน web console'

```

และอีกสิ่งหนึ่งที่สำคัญคือ คุณต้องเข้าใจการทำงานของ CUPS เพื่อที่จะสามารถแก้ปัญหาที่เกิดขึ้นได้

1.  Application ส่งไฟล์ .ps (PostScript เป็นไฟล์ที่เก็บรายละเอียดของเอกสารแต่ละหน้า) ไปยัง CUPS เมื่อคุณสั่งพิมพ์งาน (99% ของโปรแกรม)
2.  ต่อจากนั้น CUPS จะค้นหาไฟล์ PPD (ไฟล์เก็บรายละเอียดของเครื่องพิมพ์) และพิจารณาว่าจะต้องใช้ filter อะไรในการแปลงข้อมูลจาก .ps ไปเป็นรูปแบบที่เครื่องพิมพ์เข้าใจ เช่น PJL หรือ PCL โดยส่วนมากจะเรียกใช้งาน ผ่านทาง GhostScript
3.  GhostScript รับข้อมูลและพิจารณาว่าต้องใช้งาน filter อะไรเพื่อแปลงเอกสารจาก .ps ให้อยู่ในรูปแบบที่เครื่องพิมพ์เข้าใจได้
4.  หลังจากนั้นข้อมูลก็จะถูกส่งกลับมาที่ backend ตัวอย่างเช่น หากคุณมีเครื่องพิม์เชื่อมต่ออยู่กับ USB port ระบบจะเรียกใช้งาน USB backend

คุณสามารถทดลองพิมพ์เอกสารและดูรายละเอียดในไฟล์ 'error_log' เพื่อความเข้าใจมากขึ้นในกระบวนการทำงานของ CUPS

## การติดตั้ง CUPS

### Packages

คุณต้องการ CUPS และ Ghostscript

```
# pacman -S cups ghostscript

```

*   **cups** - คือแพคเกจของ CUPS
*   **ghostscript** - ตัวแปลภาษา Postscript

เหล่านี้คือชุดของ driver ซึ่งสามารถทำงานได้กับเครื่องพิมพ์ของคุณ หากคุณไม่แน่ใจ ให้ติดตั้ง gutenprint

*   **gutenprint** - เป็นชุดของ driver ความละเอียดสูงสำหรับ Canon, Epson, Lexmark, Sony, Olympus และเครื่องพิมพ์ PCL สำหรับใช้งานกับ Ghostscript, CUPS, Foomatic และ the GIMP.
*   **foomatic**, **foomatic-db**, **foomatic-db-engine**, **foomatic-db-ppd** และ **foomatic-filters** - Foomatic เป็นระบบที่ทำงานบนฐานข้อมูล สำหรับการรวม driver ซอฟท์แวร์ฟรีเข้าไว้กับระบบการพิมพ์ของ Unix
*   การติดตั้ง **foomatic-filters** น่าจะแก้ปัญหาได้ หากคุณพบข้อผิดพลาด "stopped with status 22!" ในไฟล์ error.log
*   **hplip** - HP Linux inkjet driver สามารถใช้งานได้กับ DeskJet, OfficeJet, Photosmart, Business Inkjet และ LaserJet บางรุ่น
*   **cups-pdf** - แพคเกจที่ช่วยให้คุณสร้าง Virtual PDF Printer ซึ่งจะแปลงเอกสารต่างๆ ให้เป็นไฟล์ PDF

หากระบบของคุณเชื่อมต่ออยู่กับเครื่องพิมพ์ที่อยู่บนเครือข่ายซึ่งใช้โปรโตคอลของ samba (Windows Networking) หรือคุณต้องการให้เครื่องของคุณแบ่งปันเครื่องพิมพ์บนระบบเครือข่ายของ Windows คุณต้องติดตั้ samba

```
# pacman -S samba

```

### Download Printer PPD (ไฟล์รายละเอียดเครื่องพิมพ์)

ขั้นตอนนี้อาจจะไม่จำเป็นสำหรับเครื่องพิมพ์บางรุ่น เพราะ CUPS ได้มาพร้อมกับชุด driver มาตรฐาน (ส่วนใหญ่สำหรับเครื่องพิมพ์ PostScript) และที่มากไปกว่านั้น *foomatic-filters*, *gimp-print* และ *hplip* ได้รวมเอาไฟล์รายละเอียดเครื่องพิมพ์ไว้พอสมควร ซึ่ง CUPS จะตรวจพบได้เอง

นี่คือคำอธิบายความหมายของไฟล์ PPD หรือไฟล์รายละเอียดเครื่องพิมพ์ ซึ่งได้มาจากเว็บไซท์ Linux Printing "สำหรับเครื่องพิมพ์ PostScript ทุกตัว ผู้ผลิตจะให้ไฟล์ PPD ซึ่งประกอบไปด้วยรายละเอียดต่างๆ เกี่ยวกับเครื่องพิมพ์รุ่นนั้นๆ เช่น ความสามารถมาตรฐานที่เครื่องพิมพ์สามารถทำได้ ความสามารถในการพิมพ์สี Font ต่างๆ และอื่นๆ อีกมากมาย รวมถึงการตั้งค่าที่ผู้ใช้สามารถเลือกได้ เช่น ขนาดกระดาษ หรือ ความละเอียดเป็นต้น"

*   การ Download ไฟล์ PPD

ให้คุณเข้าไปยัง [http://www.linuxprinting.org/printer_list.cgi](http://www.linuxprinting.org/printer_list.cgi) และเลือกยี่ห้อกับรุ่นของเครื่องพิมพ์ของคุณ

*   หลังจากนั้น คุณต้องคัดลอกไฟล์ไปยัง directory ของ CUPS เพื่อให้ระบบสามารถตรวจสอบไฟล์ได้ ถ้าคุณอยู่ใน directory ที่คุณ download ไฟล์ PPD มา ให้ใช้คำสั่งดังนี้

```
# cp ชื่อไฟล์.ppd /usr/share/cups/model/

```

ถ้าคุณหายี่ห้อและรุ่นของเครื่องพิมพ์คุณไม่พบ คุณสามารถลองใช้งานไฟล์ของรุ่นที่คล้ายๆ กันได้ หรือสามารถลองใช้ Driver มาตรฐาน (Generic) โปรดหารายละเอียดเพิ่มเติมจาก Google หรือสอบถามจากผู้ผลิตเครื่องพิมพ์ของคุณ (เราขอให้คุณโชคดี)

## การตั้งค่า CUPS

### ตัวเลือกต่างๆ

หลังจากติดตั้งเสร็จสมบูรณ์ คุณมีตัวเลือกมากมายในการตั้งค่า CUPS คุณสามารถเรียกใช้งานการตั้งค่าจาก command line ได้ตลอดเวลา ในขณะเดียวกัน Desktop Environment ต่างๆ ได้รวมเครื่องมือที่มีประโยชน์ ซึ่งสามารถใช้ในการตั้งค่าเครื่องพิมพ์ได้ นอกจากนี้ CUPS ยังมี web interface เพื่อความสะดวกในการตั้งค่าและใช้งานอีกด้วย

หากคุณต้องการเชื่อมต่อกับเครื่องพิมพ์ที่อยู่ในระบบเครือข่าย คุณสามารถข้ามไปอ่านส่วนของ Printer Sharing ก่อน การ Share เครื่องพิมพ์ระหว่าง Linux กับ Linux เป็นเรื่องง่าย ในทางกลับกัน การ Share เครื่องพิมพ์ระหว่าง Windows กับ Linux ต้องการการตั้งค่าเพิ่มเติม แต่ก็ไม่ยากเกิดความสามารถของผู้ใช้ทั่วไป

### Kernel Modules

ก่อนที่เราจะสามารถใช้งาน Web Interface ของ CUPS ได้ เราต้องติดตั้ง kernel module ที่ถูกต้องลงไปในระบบก่อน ขันตอนต่างๆ เหล่านี้ได้มาจากคู่มือการพิมพ์ของ Gentoo

#### เครื่องพิมพ์ USB

ถ้าคุณต้องการใช้เครื่องพิมพ์ที่ใช้การเชื่อมต่อแบบ USB กับ Kernel รุ่น 2.6.x ให้ใช้คำสั่งดังนี้

```
# modprobe usblp

```

หากคุณต้องการใช้เครื่องพิมพ์ USB กับ Kernel รุ่น 2.4.x ให้ใช้คำสั่งดังนี้

```
# modprobe printer

```

ข้อสังเกต คำแนะนำนี้สำหรับผู้ใช้งานที่ใช้ Kernel ที่มากับตัว Arch เท่านั้น (Stock kernel) หากคุณใช้งาน kernel ของคุณเอง คุณอาจจะต้องเรียกใช้งานคำสั่งนี้

```
# modprobe usbcore

```

หลังจากที่คุณติดตั้ง module ต่างๆ เป็นที่เรียบร้อยแล้ว คุณสามารถเชื่อมต่อเครื่องพิมพ์เข้ากับเครื่องคอมพิวเตอร์ของคุณ และตรวจสอบว่าระบบปฏิบัติการได้ค้นพบเครื่องพิมพ์ของคุณ โดยใช้คำสั่งดังนี้

```
# tail /var/log/messages

```

หรือ

```
# dmesg

```

คุณควรจะได้รับผลลัพธ์ใกล้เคียงกับรูปแบบนี้

```
 Feb 19 20:17:11 kernel: printer.c: usblp0: USB Bidirectional
 printer dev 2 if 0 alt 0 proto 2 vid 0x04E8 pid 0x300E
 Feb 19 20:17:11 kernel: usb.c: usblp driver claimed interface cfef3920
 Feb 19 20:17:11 kernel: printer.c: v0.13: USB Printer Device Class driver

```

#### เครื่องพิมพ์พอร์ทขนาน

หากคุณต้องการใช้เครื่องพิมพ์ที่เชื่อมต่อผ่านทางพอร์ทขนาน (Parallel Port) การตั้งค่าส่วนใหญ่จะเหมือนเดิม สำหรับ kernel รุ่น 2.6.x ให้ใช้คำสั่งดังนี้

```
# modprobe lp

```

และสำหรับ kernel รุ่น 2.4 และ 2.6 ให้ใช้คำสั่งดังนี้ด้วย

```
# modprobe parport
# modprobe parport_pc

```

คุณสามารถตรวจสอบการทำงานของระบบได้จาก

```
# tail /var/log/messages

```

และคุณควรจะเห็นผลลัพธ์คล้ายๆ กับผลลัพธ์ดังนี้

```
# lp0: using parport0 (polling).

```

ข้อสังเกต ในบางกรณี การตั้งค่า Permission อาจจะผิดพลาด ซึ่งทำให้ระบบไม่สามารถพิมพ์งานได้ ตัวอย่างการแก้ไข permission มีดังนี้

```
[root@mihal usb]# cd /dev/usb/
[root@mihal usb]# ls
lp0
[root@mihal usb]# chgrp lp lp0

```

#### การเรียกใช้งานโดยอัตโนมัติ

คุณอาจจะอยากให้ระบบเรียกใช้งาน kernel module อัตโนมัติทุกครั้งที่เริ่มทำงาน คุณสามารถตั้งค่าเหล่านี้ได้โดยการแก้ไขไฟล์ `/etc/rc.conf` และเพิ่มรายละเอียดในส่วนของ *MODULES=()* นี่คือตัวอย่างการตั้งค่าในส่วนของ MODULES

```
MODULES=(!usbserial scsi_mod sd_mod snd-ymfpci snd-pcm-oss printer ide-scsi)

```

### CUPS Daemon

หลังจากที่ติดตั้ง Kernel Module เรียบร้อยแล้ว คุณสามารถเริ่มใช้งาน CUPS ได้ด้วยการใช้คำสั่งนี้

```
# /etc/rc.d/cupsd start

```

และหากคุณต้องการใช้ CUPS เริ่มต้นทำงานโดยอัตโนมัติทุกครั้งที่คุณเริ่มใช้งานคอมพิวเตอร์ ให้เพิ่มข้อมูลเข้าไปในส่วนของ DAEMONS=() ในไฟล์ */etc/rc.conf* ตัวอย่างเช่น

```
# DAEMONS=(pcmcia syslogd klogd !fam esd mono network autofs cupsd crond gdm)

```

### Web Interface และชุดเครื่องมือ

หลังจากที่คุณทำให้ Daemon ทำงานได้แล้ว คุณสามารถเข้าสู่ Web Interface ได้ โดยเปิด web browser แล้วเข้าไปยัง

*[http://localhost:631](http://localhost:631)*

หรือติดตั้ง "Gnome Cups Manager" ซึ่งเป็น GUI frontend (โปรดดูภาคผนวกที่ A.1 [การเรียกใช้งาน CUPS ในรูปแบบอื่นๆ](https://wiki.archlinux.org/index.php/CUPS#Alternative_CUPS_Interfaces))

จากจุดนี้ไป คุณเพียงแค่ทำตาม Wizard ต่างๆ เพื่อเพิ่มและจัดการกับเครื่องพิมพ์ของคุณ ตัวอย่างคร่าวๆ คือการคลิก *Manage Printers* และคลิกต่อไปที่ *Add Printer* เมื่อระบบถามหาชื่อผู้ใช้และรหัสผ่าน ให้ใส่ *root* และรหัสผ่านของ root จากนั้นใส่ชื่อ, ที่ตั้ง และคำอธิบายอื่นๆ ของเครื่องพิมพ์ หลังจากนั้นคุณจะต้องเลือกอุปกรณ์ และ Driver ที่เหมาะสมกับเครื่องพิมพ์ เป็นอันเสร็จสิ้นการติดตั้งเครื่องพิมพ์

คุณสามารถพิมพ์หน้าทดสอบได้โดยการกดที่ปุ่ม *Print Test Page*

## ตั้งค่าการ Share เครื่องพิมพ์

### Linux กับ Linux

หลังจากที่คุณติดตั้ง CUPS บนระบบ Linux ของคุณที่จะทำหน้าที่เป็นแม่ข่ายแล้ว การ share เครื่องพิมพ์กับระบบ Linux อื่นๆ สามารถทำได้อย่างง่ายดาย โดยมีหลายวิธีในการตั้งค่า ในที่นี้จะอธิบายการตั้งค่าด้วยมือแบบละเอียด บนเครื่องแม่ข่าย (เครื่องที่เชื่อมต่ออยู่กับเครื่องพิมพ์) ให้เปิดไฟล์ */etc/cups/cupsd.conf* และอนุญาตให้เครื่องคอมพิวเตอร์อื่นๆ สามารถเข้าสู่ระบบได้ด้วยการแก้ไขการตั้งค่า ตัวอย่างเช่น

```
<Location />
  Order Deny,Allow
  Deny From All
  Allow From 127.0.0.1
  Allow From 10.0.0.*
</Location>

```

คุณต้องแน่ใจด้วย ว่าเครื่องแม่ข่ายกำลังรับการติดต่อจาก IP address ที่เครื่องลูกข่ายจะเรียกหา ตัวอย่างเช่น (ให้ใส่ไว้หลังจากบรรทัดที่เขียนว่า "Listen localhost:631"

```
Listen 10.0.0.1:631

```

โดยใช้ IP Address ของเครื่องแม่ข่ายของคุณแทนที่ 10.0.0.1.

ใส่ IP Address ของเครื่องลูกข่ายในส่วนของ Allow From หลังจากนั้นคุณต้องเริ่มต้นใช้งาน CUPS ใหม่ โดยใช้คำสั่งดังนี้

```
# /etc/rc.d/cupsd restart

```

ในส่วนของเครื่องลูกข่าย ให้เปิดไฟล์ `/etc/cups/client.conf` และแก้ไขในส่วนของ ServerName ให้ตรงกับ IP Address หรือชื่อของเครื่องแม่ข่าย ตัวอย่างเช่นเครื่องแม่ข่ายมี IP Address คือ 192.168.0.1 การตั้งค่าจะดูคล้ายกับแบบนี้ ในไฟล์ *client.conf*

```
ServerName 192.168.0.1

```

ต่อจากนั้นให้เรียกใช้คำสั่งนี้เพื่อ Update เครื่องคอมพิวเตอร์

```
# lpq

```

คุณน่าจะเห็นผลลัพธ์ที่คล้ายๆ กับแบบนี้

```
ml1250 is ready
no entries

```

นอกจากนี้ยังมีการตั้งค่าอีกหลายแบบ ซึ่งรวมถึงการตั้งค่าอัตโนมัติ โดยคุณสามารถดูรายละเอียดได้จาก [http://localhost:631/sam.html#CLIENT_SETUP](http://localhost:631/sam.html#CLIENT_SETUP) (ลิงค์นี้จะทำงานบนเครื่องแม่ข่ายเท่านั้น)

หากคุณถูกถามรหัสผู้ใช้งาน ให้ใส่ชื่อผู้ใช้และรหัสผ่านสำหรับ root และหากคุณใช้เครื่องพิมพ์ JetDirect ให้เข้าไปดูยังหน้านี้ [http://www.digitalhermit.com/linux/printing/](http://www.digitalhermit.com/linux/printing/)

### Linux to Windows

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

### Windows to Linux

Sometimes, you might want to allow a Windows computer to connect to your computer. There are a few ways to do this, and the one I am most familiar with is using Samba. In order to do this, you will have to edit your */etc/samba/smb.conf* file to allow access to your printers. Your smb.conf can look something like this:

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

Obvious, there are a lot of tweaks and customization that can be done with setting up a Samba print server, so I advise you to look at the Samba and CUPS documentation for more help. The *smb.conf.example* file also has some good samples to that you might want to look at.

### Windows 2000 and Windows XP to Linux

For the most modern flavours of Windows an alternative way of connecting to your Linux printer server is to use the CUPS protocol directly. The Windows client will need to be using Windows 2000 or Windows XP. Make sure you allows the clients to access the print server by editing the location settings as specified in section 4.1.

On the Windows computer, go to the printer control panel and choose to Add a New Printer. Next, choose to give an url. For the url type in the location of your printer:

*[http://host_ip_address:631/printers/printer_name](http://host_ip_address:631/printers/printer_name)*

where host_ip_address is the Linux server's IP address and printer_name is the name of the printer you are connecting to. After this, install the printer drivers for the Windows computer. If you setup the CUPS server to use its own printer drivers, then you can just select a generic postscript printer for the Windows client. You can then test your print setup by printing a test page.

### Others to Linux, Linux to others

More information on interfacing CUPS with other printing systems can be found in the CUPS manual, e.g. on [http://localhost:631/sam.html#PRINTING_OTHER](http://localhost:631/sam.html#PRINTING_OTHER)

## Appendix

### Alternative CUPS Interfaces

If you are a GNOME user, you can manage and configure your printer by using the gnome-cups-manager.

Update: this package is now available through pacman if you have the "community" repository uncommented in /etc/pacman.conf

```
pacman -S gnome-cups-manager

```

The package is also still available from the [AUR](https://aur.archlinux.org/packages.php?do_Details=1&ID=66&O=0&L=0&C=0&K=cups&SB=&SO=&PP=25&do_MyPackages=0&do_Orphans=0&SeB=nd).

KDE users can modify their printers from the Control Center. Both should refer the those desktop environments' documentation for more information on how to use the interfaces.

There is also [gtklp](https://aur.archlinux.org/packages/gtklp/). It is in the [extra] repository.

### PDF Virtual Printer

A nice little package that I submitted to the incoming folder ([ftp://ftp.archlinux.org/incoming](ftp://ftp.archlinux.org/incoming)) is CUPS-PDF. This package allows one to setup a virtual printer that will generate a PDF from anything sent to it. For example, I wrote this document in AbiWord and then printed it to the Virtual Printer which generated a PDF in my `/var/spool/cups-pdf/neocephas` folder. Obviously, this package is not necessary, but it can be quite useful. After downloading the package from the ftp server and installing it, you can set it up as you would for any other printer in the web interface. Select Virtual PDF Printer as the device and choose Postscript -> Postscript Color Printer for the drivers.

### Online Resources

Here is a listing of websites that may be of use to you:

*   **Official CUPS documentation on your computer** [http://localhost:631/documentation.html](http://localhost:631/documentation.html)
*   **Official CUPS Website** - [http://www.cups.org/](http://www.cups.org/)
*   **Linux Printing** - [http://www.linuxprinting.org/](http://www.linuxprinting.org/)
*   **Tips and Suggestions on common CUPS problems** - [http://home.nyc.rr.com/computertaijutsu/cups.html](http://home.nyc.rr.com/computertaijutsu/cups.html)
*   **Gentoo's Printing Guide** - [http://www.gentoo.org/doc/en/printing-howto.xml](http://www.gentoo.org/doc/en/printing-howto.xml)
*   **Arch Linux User Forums** - [https://bbs.archlinux.org/](https://bbs.archlinux.org/)

### Specialized Cases

This section is dedicated to specific problems and their solutions. If you managed to get some *unusual* printer working, please put the solution here.

#### Printing does not work/aborts with the HP Deskjet 700 Series Printers.

*   The solution is to install [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) printer filter for the HP Deskjet 700 series. Without this the print jobs will be aborted by the system. A [PKGBUILD](/index.php/PKGBUILD "PKGBUILD") for [pnm2ppa](https://aur.archlinux.org/packages/pnm2ppa/) can be found in the [AUR](/index.php/AUR "AUR").

#### Getting HP LaserJet 1010 to work

I had to compile ghostscript myself because ESP gs in rep was 7.07 and had not fixed some bugs like ESP 8.15.1 had. I never downloaded 'foomatic' in rep. I think that is an old package.

kris|~/temp$ P -Qs cups a2ps psutils foo ghost local/cups 1.1.23-3

```
   The CUPS Printing System

```

local/a2ps 4.13b-3

```
   a2ps is an Any to PostScript filter

```

local/psutils p17-3

```
   A set of postscript utilities.

```

local/foomatic-db 3.0.2-1

```
   Foomatic is a system for using free software printer drivers with common
   spoolers on Unix

```

local/foomatic-db-engine 3.0.2-1

```
   Foomatic is a system for using free software printer drivers with common
   spoolers on Unix

```

local/foomatic-db-ppd 3.0.2-1

```
   Foomatic is a system for using free software printer drivers with common
   spoolers on Unix

```

local/foomatic-filters 3.0.2-1

```
   Foomatic is a system for using free software printer drivers with common
   spoolers on Unix

```

local/espgs 8.15.1-1

```
   ESP Ghostscript

```

I also had to set LogLevel in /etc/cups/cupsd.conf to debug2 before i saw that I missed some "Nimbus" fonts. Then I had to rename & put them where the log told me to. Some fancy google searching had to be applied, example: [http://www.google.com/search?q=n019003l+filetype%3Apfb](http://www.google.com/search?q=n019003l+filetype%3Apfb) since the fonts turned out to be propriatory(i'm sure windows comes with these default). Nevertheless after downloading them(about 7 fonts) and putting them in the correct folder printing started working.

Before that i were getting all the errors said here: [http://linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1010](http://linuxprinting.org/show_printer.cgi?recnum=HP-LaserJet_1010) 'Unsupport PCL' etc...

I'm sure it could have worked with ESP gs 7.07 too(in rep) if i was smart enough to turn on DebugLevel2 sooner :/ UPDATE: yeah it did... maybe this info is useful for someone else though.. sorry for the inconvienice

### Another Source for Printer Drivers

On *[http://www.turboprint.de/english.html](http://www.turboprint.de/english.html)* is a really good printer driver for many printers not yet supported by Linux (especially Canon i*). The only problem is that high-quality-prints are either marked with a turboprint-logo or you have to pay for it... It's not Open-Source.

[Wikipedia:Common_Unix_Printing_System](https://en.wikipedia.org/wiki/Common_Unix_Printing_System "wikipedia:Common Unix Printing System")

## Troubleshooting

### As a result of upgrade

After updating, if you get something like :

```
 /usr/sbin/cupsd: error while loading shared libraries: libgnutls.so.13: cannot open shared object file: No such file or directory

```

You need to update [gnutls](https://www.archlinux.org/packages/?name=gnutls).

In addition, in `/etc/cups`, there will be a file named `cupsd.conf.pacnew`. Rename it `cupsd.conf`.