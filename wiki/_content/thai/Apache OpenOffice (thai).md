บทความนี้จะแนะนำคุณในการติดตั้ง OpenOffice โดย Package ที่คุณจะติดตั้งเป็น package ที่พร้อมใช้งานจาก pacman

## Contents

*   [1 การติดตั้ง OpenOffice 2](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_OpenOffice_2)
    *   [1.1 ติดตั้งโปรแกรม](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B9.82.E0.B8.9B.E0.B8.A3.E0.B9.81.E0.B8.81.E0.B8.A3.E0.B8.A1)
    *   [1.2 ตั้งค่าโปรแกรม](#.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B9.82.E0.B8.9B.E0.B8.A3.E0.B9.81.E0.B8.81.E0.B8.A3.E0.B8.A1)
    *   [1.3 การใช้งาน](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99)
    *   [1.4 ปัญหาที่อาจจะเกิดขึ้น](#.E0.B8.9B.E0.B8.B1.E0.B8.8D.E0.B8.AB.E0.B8.B2.E0.B8.97.E0.B8.B5.E0.B9.88.E0.B8.AD.E0.B8.B2.E0.B8.88.E0.B8.88.E0.B8.B0.E0.B9.80.E0.B8.81.E0.B8.B4.E0.B8.94.E0.B8.82.E0.B8.B6.E0.B9.89.E0.B8.99)
*   [2 ติดตั้งและใช้งาน OpenOffice 1.1.4](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B9.81.E0.B8.A5.E0.B8.B0.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99_OpenOffice_1.1.4)
    *   [2.1 การติดตั้ง](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)
    *   [2.2 เพิ่มเติม](#.E0.B9.80.E0.B8.9E.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B9.80.E0.B8.95.E0.B8.B4.E0.B8.A1)
    *   [2.3 การตั้งค่า](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2)

# การติดตั้ง OpenOffice 2

## ติดตั้งโปรแกรม

*   ขั้นแรกคุณต้องติดตั้ง Java Runtime Environment (ไม่บังคับให้ติดตั้ง แต่แนะนำให้ติดตั้ง)

```
# pacman -S j2re

```

*   Download base:

```
# pacman -S openoffice-base

```

*   ติดตั้งชุดภาษาอื่นๆ (ยังไม่มีสำหรับภาษาไทย หากคุณเป็นนักพัฒนาและอยากที่จะสร้างชุดภาษาไทยสำหรับ OpenOffice บน Arch Linux โปรดสอบถามได้ในกระดานข่าว) และคุณไม่จำเป็นต้องติดตั้งชุดภาษาอังกฤษ เนื่องจากมันจะถูกติดตั้งมาให้เป็นที่เรียบร้อยแล้ว

```
# pacman -S openoffice-XX (XX คือภาษาที่คุณต้องการ)

```

*   ติดตั้งระบบตรวจการสะกดคำ (ไม่จำเป็น)

```
# pacman -S openoffice-spell-XX (XX คือภาษาที่คุณต้องการ)

```

*   คุณสามารถค้นหาชุดอุปกรณ์ภาษา สำหรับภาษาอื่นๆ ได้จาก [AUR](/index.php/AUR "AUR")

## ตั้งค่าโปรแกรม

สั่งคำสั่ง '/opt/openoffice/program/soffice' เพื่อตั้งค่า OpenOffice2 สำหรับผู้ใช้งานธรรมดา **และ** เพื่อเริ่มต้นการใช้งาน OpenOffice2

OpenOffice2 มีความสามารถที่จะใช้ toolkit หลายๆ ตัวเพื่อใช้วาดภาพ และผสมเข้าเป็นส่วนหนึ่งของ desktop environment ที่แตกต่างกันด้วยวิธีที่ไม่ทำอันตรายต่อระบบ การเลือก toolkit เหล่านี้ คุณต้องตั้งค่าตัวแปร OOO_FORCE_DESKTOP ด้วยการตั้งค่าใน /etc/profile.d/ หรือด้วยการตั้งค่าใช้ shell ที่คุณใช้เริ่มต้น OpenOffice

ถ้าคุณต้องการใช้งาน OpenOffice กับ GTK2 ให้ใช้คำสั่งดังนี้ผ่านทาง bash shell

```
 # OOO_FORCE_DESKTOP=gnome soffice

```

หรือคุณจะใส่บรรทัดนี้เข้าไปในไฟล์ /usr/bin/soffice ก็ได้

```
 export OOO_FORCE_DESKTOP=gnome

```

## การใช้งาน

ถ้าคุณต้องใช้งานบางส่วนของ OpenOffice (แทนที่การใช้งานผ่าน soffice) เช่น โปรแกรมประมวลผลคำ (Write), โปรแกรมสเปรดชีท (Calc) และโปรแกมนำเสนอผลงาน (Impress) คุณสามารถสั่งงานได้ผ่านทาง script เหล่านี้

Writer

```
 /opt/openoffice/program/swriter

```

Calc

```
 /opt/openoffice/program/scalc

```

Impress

```
 /opt/openoffice/program/simpress

```

Math (โปรแกรมจัดการสูตรคณิตศาสตร์)

```
 /opt/openoffice/program/smath

```

Base (ระบบจัดการฐานข้อมูล)

```
 /opt/openoffice/program/sbase

```

ระบบจัดการ Printer (ควรใช้งานเป็น root)

```
 /opt/openoffice/program/spadmin 

```

## ปัญหาที่อาจจะเกิดขึ้น

*   ถ้าคุณมีปัญหาในการ upgrade จากเวอร์ชัน 1.1 เป็น 2 โปรดลองทำตามวิธีดังนี้

- ให้ปฏิเสธการใช้งานการตั้งค่าจากเวอร์ชัน 1.1.x
- ลบไดเรคทอรี .openoffice* จาก <home> ของคุณ
- ลบไดเรคทอรี OpenOffice* จาก <home> ของคุณ
- ลบ .sversionrc จาก <home> ของคุณ

*   หากคุณต้องการลบเมนูของ OO 1.1.x ใน KDE

- ลบ ~/.kde/share/applnk/OpenOffice*

*   หากคุณไม่สามารถอ่าน/เขียน จาก NFS ได้ ให้แก้ไขไฟล์ /opt/openoffice2/program/soffice คุณอาจจะต้องเลิกใช้งานการล็อคไฟล์ โดยใส่เครื่องหมาย # ไว้ด้านหน้า เช่น:

```
# file locking now enabled by default
#SAL_ENABLE_FILE_LOCKING=1
#export SAL_ENABLE_FILE_LOCKING

```

*   หากมันยังไม่ทำงาน หรือแสดงข้อผิดพลาด javaldx: Could not find a Java Runtime Environment! และแสดงกล่องข้อความผิดพลาดเกี่ยวกับ init ให้ลบไดเรคทอรี ~/.openoffice2 ออกไป
*   โปรดเช็คการตั้งค่าการใช้งาน /etc/X11/xorg.conf ว่าคุณได้รับอนุญาตให้ใช้ DRI หรือไม่
*   หากยังมีข้อสงสัย ตัวอย่างข้างล่างนี้อาจจะใช้งานได้

```
 Section "DRI"
 Group "users"
 Mode 0660
 EndSection

```

*   หรือถ้าคุณไม่อยากทำตามขั้นตอนข้างต้น ให้เริ่มต้นโปรแกรมเป็น root
*   ถ้ามี Setup wizard เปิดขึ้นมาทุกครั้งที่เริ่มใช้งาน (และโปรแกรมช้า และ ค้างในบางครั้ง) ให้ตรวจสอบ permission ของ ~/.openoffice2 มันอาจจะเป็นของ root

# ติดตั้งและใช้งาน OpenOffice 1.1.4

## การติดตั้ง

*   Download โปรแกรมพื้นฐาน

```
# pacman -S openoffice-base

```

*   **คุณต้องติดตั้งชุดภาษา แม้ว่าจะเป็นภาษาอังกฤษก็ตาม ระบบจะไม่ทำงานถ้าไม่ติดตั้งชุดภาษาluded)**

```
# pacman -S openoffice-XX (XX คือภาษาที่คุณต้องการ)

```

*   **การตรวจสะกดคำ** ต้องติดตั้ง package เพิ่มเติม

```
# pacman -S openoffice-spell-XX (XX คือภาษาที่คุณต้องการ)

```

## เพิ่มเติม

OpenOffice quickstarter สามารถใช้งานได้ใน KDE

```
# pacman -S oooqs

```

## การตั้งค่า

1.  สั่งคำสั่ง '/opt/openoffice/setup' เพื่อเริ่มตั้งค่าสำหรับผู้ใช้ทั่วไป
2.  ใช้คำสั่ง 'soffice' เพื่อเริ่มใช้งาน