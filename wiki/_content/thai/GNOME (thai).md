## Contents

*   [1 อะไรคือ GNOME?](#.E0.B8.AD.E0.B8.B0.E0.B9.84.E0.B8.A3.E0.B8.84.E0.B8.B7.E0.B8.AD_GNOME.3F)
*   [2 จะติดตั้ง GNOME Desktop ได้อย่างไร](#.E0.B8.88.E0.B8.B0.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87_GNOME_Desktop_.E0.B9.84.E0.B8.94.E0.B9.89.E0.B8.AD.E0.B8.A2.E0.B9.88.E0.B8.B2.E0.B8.87.E0.B9.84.E0.B8.A3)
*   [3 เริ่มต้นใช้งาน GNOME Desktop](#.E0.B9.80.E0.B8.A3.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B8.95.E0.B9.89.E0.B8.99.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99_GNOME_Desktop)
*   [4 GDM (GNOME Display Manager)](#GDM_.28GNOME_Display_Manager.29)
*   [5 ดูรายละเอียดเพิ่มเติมได้ที่](#.E0.B8.94.E0.B8.B9.E0.B8.A3.E0.B8.B2.E0.B8.A2.E0.B8.A5.E0.B8.B0.E0.B9.80.E0.B8.AD.E0.B8.B5.E0.B8.A2.E0.B8.94.E0.B9.80.E0.B8.9E.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B9.80.E0.B8.95.E0.B8.B4.E0.B8.A1.E0.B9.84.E0.B8.94.E0.B9.89.E0.B8.97.E0.B8.B5.E0.B9.88)
*   [6 Link อื่นๆ](#Link_.E0.B8.AD.E0.B8.B7.E0.B9.88.E0.B8.99.E0.B9.86)

## อะไรคือ GNOME?

โครงการ [GNOME](http://www.gnome.org/) คือโครงการพัฒนาระบบการทำงานแบบ Graphic หรือเรียกอีกชื่อหนึ่งว่า Desktop environment ซึ่งมีจุดประสงค์ในการสร้างระบบที่สวยงามและใช้งานได้ง่าย พร้อมทั้งมีต้นแบบการพัฒนาเพิ่มเติม ที่เรียกว่า GNOME development platform ซึ่งเป็นต้นแบบเพิ่มเติมที่สามารถใช้พัฒนาซอฟท์แวร์เพื่อใช้งานกับส่วนต่างๆ ของ Desktop ได้

## จะติดตั้ง GNOME Desktop ได้อย่างไร

การติดตั้ง GNOME Desktop ทำได้โดยพิมพ์คำสั่งต่อไปนี้ที่ command prompt:

```
pacman -S gnome

```

หากต้องการติดตั้งเครื่องมือเพิ่มเติมอื่นๆ ของ GNOME Desktop (แนะนำให้ติดตั้ง ดูรายละเอียดได้จาก [Gnome Tips](/index.php/Gnome_Tips "Gnome Tips")) พิมพ์คำสั่งต่อไปนี้ที่ command prompt:

```
pacman -S gnome-extra

```

หากต้องการเริ่มต้นระบบอย่างถูกต้อง ให้แก้ไขไฟล์ /etc/rc.conf และเพิ่ม "portmap", "fam", "dbus" และ "hal" เข้าไปในบรรทัด DAEMONS=()

## เริ่มต้นใช้งาน GNOME Desktop

การเริ่มต้นใช้งาน GNOME จาก console ให้พิมพ์คำสั่งดังนี้:

```
gnome-session

```

หากท่านใส่บรรทัดเหล่านี้เข้าไปในไฟล์ $HOME/.xinitrc (โปรดทำให้อยู่ในบรรทัดเดียว และขึ้นต้นด้วย "exec")

```
exec gnome-session

```

หมายเหตุ: ตั้งแต่ GNOME 2.14 เป็นต้นไป GNOME ต้องการการสนับสนุน dbus ให้เปลี่ยนบรรทัด exec เป็นดังนี้:

```
exec --exit-with-session /opt/gnome/bin/gnome-session

```

GNOME จะเริ่มทำงาน เมื่อท่านสั่งคำสั่งนี้

```
startx

```

## GDM (GNOME Display Manager)

หากท่านต้องการใช้งานหน้าจอ Login ที่อยู่ในรูปแบบ Graphic ท่านต้องติดตั้ง [GDM](http://www.gnome.org/projects/gdm/) (ซึ่งเป็นส่วนหนึ่งของ gnome-extra) หากท่านต้องการติดตั้ง พิมพ์คำสั่งนี้ที่ command prompt:

```
pacman -S gdm

```

ท่านต้องใส่ gdm เข้าไปในรายชื่อของ DAEMONS ในไฟล์ /etc/rc.conf เพื่อให้มันทำงานโดยอัตโนมัติ

หากท่านคุ้นเคยกับการใช้งานไฟล์ **$HOME/.xinitrc** เพื่อส่งค่าไปยัง X server เช่น **xmodmap** หรือ **xsetroot** ท่านสามารถเพิ่มคำสั่งแบบเดียวกันนี้เข้าไปได้ที่ **$HOME/.xprofile** ดังเช่นตัวอย่างไฟล์ .xprofile

```
#!/bin/sh

#
# ~/.xprofile
#
# Executed by gdm at login
#

xmodmap -e "pointer = 1 2 3 6 7 4 5"  #set mouse buttons up correctly
xsetroot -solid black                 #sets the background to black

```

สำหรับรายละเอียดเพิ่มเติม ในการใช้งานหน้า Login แบบ Graphic โปรดอ่าน [ที่หน้านี้](http://endor.clublinux.org/RHCE-21.html)

## ดูรายละเอียดเพิ่มเติมได้ที่

*   [Gnome Tips](/index.php/Gnome_Tips "Gnome Tips")
*   [Gnome Menu tweaking](/index.php/Gnome_Menu_tweaking "Gnome Menu tweaking")

## Link อื่นๆ

*   [เว็บไซท์หลักของ GNOME Project](http://www.gnome.org/)
*   [คู่มือการใช้งานอย่างเป็นทางการ](http://www.gnome.org/learn/)
*   [GnomeHelp.org](http://gnomehelp.org/)
*   Themes, icon และฉากหลัง Desktop:
    *   [Gnome Art](http://art.gnome.org/)
    *   [Gnome Look](http://www.gnome-look.org/)
*   GTK/Gnome programs:
    *   [Gnome Files](http://www.gnomefiles.org/)
    *   [Gnome Project Listing](http://www.gnome.org/projects/)