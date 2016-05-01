## Contents

*   [1 ขั้นตอนแรก](#.E0.B8.82.E0.B8.B1.E0.B9.89.E0.B8.99.E0.B8.95.E0.B8.AD.E0.B8.99.E0.B9.81.E0.B8.A3.E0.B8.81)
*   [2 การติดตั้ง](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)
    *   [2.1 Drivers](#Drivers)
        *   [2.1.1 wlan-ng](#wlan-ng)
        *   [2.1.2 rt2x00](#rt2x00)
        *   [2.1.3 madwifi](#madwifi)
        *   [2.1.4 ipw2100 และ ipw2200](#ipw2100_.E0.B9.81.E0.B8.A5.E0.B8.B0_ipw2200)
        *   [2.1.5 ipw3945](#ipw3945)
        *   [2.1.6 orinoco](#orinoco)
        *   [2.1.7 ndiswrapper](#ndiswrapper)
        *   [2.1.8 prism54](#prism54)
        *   [2.1.9 ACX100/111](#ACX100.2F111)
        *   [2.1.10 BCM43XX](#BCM43XX)
*   [3 การตั้งค่าและเริ่มต้นระบบ](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B9.81.E0.B8.A5.E0.B8.B0.E0.B9.80.E0.B8.A3.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B8.95.E0.B9.89.E0.B8.99.E0.B8.A3.E0.B8.B0.E0.B8.9A.E0.B8.9A)
    *   [3.1 การใช้งาน Arch Linux กับการตั้งค่า Wireless Network](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99_Arch_Linux_.E0.B8.81.E0.B8.B1.E0.B8.9A.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2_Wireless_Network)
    *   [3.2 การใช้งาน Roaming Network Profiles](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99_Roaming_Network_Profiles)
        *   [3.2.1 ติดตั้งแบบเร็ว](#.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B9.81.E0.B8.9A.E0.B8.9A.E0.B9.80.E0.B8.A3.E0.B9.87.E0.B8.A7)
    *   [3.3 Wifi-radar](#Wifi-radar)
    *   [3.4 NetworkManager](#NetworkManager)
*   [4 Link เพิ่มเติม](#Link_.E0.B9.80.E0.B8.9E.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B9.80.E0.B8.95.E0.B8.B4.E0.B8.A1)

## ขั้นตอนแรก

1.  ตรวจสอบว่าอุปกรณ์ของคุณสามารถใช้งานกับ Linux ได้หรือไม่ โดยคุณสามารถดูชื่อของอุปกรณ์ของคุณโดยใช้คำสั่ง lshwd
    *   [wlan-ng](http://www.linux-wlan.org/docs/wlan_adapters.html.gz) สนับสนุนการ์ดมากพอสมควร โปรดตรวจสอบที่นี่ก่อน
    *   [madwifi](http://madwifi.org) สำหรั Atheros chipset (AR5210, AR5211, AR5212 and AR5213)
    *   [rt2x00](http://rt2x00.serialmonkey.com/wiki/index.php/Main_Page) สำหรัล Ralink rt2400, rt2500, และ rt2570
    *   [ipw2100](http://ipw2100.sourceforge.net/) สำหรับ Intel Pro/Wireless 2100 Mini PCI
    *   [ipw2200](http://ipw2200.sourceforge.net/) สำหรับ Intel Pro/Wireless 2200 Mini PCI
    *   [ipw3945](http://ipw3945.sourceforge.net/) สำหรับ Intel Pro/Wireless 3945 AB/G Mini PCI-E
    *   [orinoco](http://www.nongnu.org/orinoco/devices/) สำหรับการ์ดที่ใช้ Prism 2 บางตัว
    *   [prism54](http://prism54.org/) สำหรับ Prism 54
    *   โปรดดู [Linux Wireless Support](http://linux-wless.passys.nl/) สำหรับคำถามอื่นๆ และ [hardware compatibility list](http://www.linuxquestions.org/hcl/index.php?cat=10) (HCL) ซึ่งมีรายชื่อของอุปกรณ์ที่ทำงานกับ Linux ได้
2.  ถ้าอุปกรณ์ของคุณทำงานได้กับ Windows เท่านั้น
    *   [ndiswrapper](http://ndiswrapper.sourceforge.net/wiki/index.php/List) สำหรับฮาร์ดแวร์ที่ทำงานได้บน Windows อย่างเดียว (Broadcom, 3com, etc)
    *   คุณต้องการไฟล์ .inf และ .sys จาก Windows Driver ของคุณ [ดูรายละเอียดที่นี่](http://ndiswrapper.sourceforge.net/mediawiki/index.php/List)
3.  แต่ถ้าฮาร์ดแวร์ของคุณไม่อยู่ในรายชื่อใดๆ เลย
    *   เราว่าคุณโดนหลอกขายของมาแน่ๆ
    *   ทดลองค้นหาเว็บไซท์ โดยใส่เลขรุ่นของอุปกรณ์ของคุณ พร้อมกับคำว่า Linux หรือคุณสามารถถามคำถามได้ที่กระดานข่าว [the forums](https://bbs.archlinux.org)

## การติดตั้ง

คุณต้องติดตั้ง **wireless-tools** ก่อน

```
pacman -S wireless_tools

```

คุณจะไม่สามารถใช้งาน Wireless Hardware ได้ถ้าไม่มีโปรแกรมนี้

### Drivers

ต่อไปนี้เป็นรายละเอียดวิธีการติดตั้ง Driver สำหรับอุปกรณ์ของคุณ ซึ่งมีหลายทางเลือก คุณสามารถดูที่ [HCL](http://www.linuxquestions.org/hcl/index.php?cat=10%7CLQ) สำหรับคำแนะนำในการเลือก Driver

#### wlan-ng

```
pacman -S wlan-ng24

```

หรือ

```
pacman -S wlan-ng26

```

#### rt2x00

โปรดดู [หน้า Wiki ของ rt2x00](/index.php/Using_the_new_rt2x00_beta_driver "Using the new rt2x00 beta driver")

#### madwifi

```
pacman -S madwifi

```

Module มีชื่อว่า ath_pci **คุณอาจจะต้องใส่รหัสประเทศระหว่างการติดตั้ง Driver เพื่อให้ระบบสามารถตั้งค่า Channel และกำลังส่งที่ถูกกฎหมายสำหรับประเทศนั้นๆ** เช่น 764 สำหรับประเทศไทย ดังนั้น คุณต้องทำการเรียกใช้ Module แบบนี้

```
modprobe ath_pci countrycode=764

```

คุณสามารถตรวจสอบการตั้งค่าของคุณได้ด้วยคำสั่ง **iwlist** ดูรายละเอียดของคำสั่งได้จาก **man iwlist** และหน้า [http://madwifi.org/wiki/UserDocs/CountryCode%7C](http://madwifi.org/wiki/UserDocs/CountryCode%7C) รหัสประเทศ จาก MadWifi wiki] หากคุณต้องการให้การตั้งค่าเหล่านี้ทำงานพร้อมกับการเปิดเครื่อง ใส่บรรทัดนี้เข้าไปในไฟล์ **/etc/modprobe.d/modprobe.conf**

```
options ath_pci countrycode=528

```

#### ipw2100 และ ipw2200

การเลือกใช้ขึ้นอยู่กับ Chipset ที่คุณเลือกใช้

```
pacman -S ipw2100-fw

```

หรือ

```
pacman -S ipw2200-fw

```

#### ipw3945

```
pacman -S ipw3945

```

คำสั่งจะติดตั้ง ipw3945-ucode, ipw3945, และ daemon ชื่อ ipw3945d

การสั่งให้ Driver เริ่มทำงานพร้อมกับเครื่อง ทำได้โดยเพิ่ม **ipw3945** เข้าไปใน MODULES และ **ipw3945d** เข้าไปใน DAEMONS ในไฟล์ /etc/rc.conf

Module ipw3945 ควรจะถูกเรียกใช้ระหว่างขั้นตอน "Loading Modules..." และคุณควรจะเห็นคำว่า "Starting IPW3945d" ในส่วนของขั้นตอนการเรียก daemon และคุณควรจะเห็น ethX

#### orinoco

Driver นี้เป็นส่วนหนึ่งของ Kernel แล้ว

#### ndiswrapper

Ndiswrapper ไม่ใช่ driver ที่แท้จริง แต่มันเป็นเพียงโปรแกรมที่จำลองการทำงานของ Windows driver กับ การ์ด Wireless Network ของคุณ ดังนั้นในกรณีที่อุปกรณ์ของคุณไม่มี Linux driver การใช้งาน ndiswrapper จึงมีความจำเป็นเป็นอย่างมาก ในการใช้งาน ndiswrapper คุณต้องการไฟล์ .inf และ .sys จาก Windows driver ของคุณ ขั้นตอนการติดตั้ง ndiswrapper สามารถทำได้ดังนี้

ติดตั้ง ndiswrapper ผ่าน pacman

```
pacman -S ndiswrapper ndiswrapper-utils

```

*คำเตือน:* หากคุณใช้ Kernel ArchCK และ Beyond คุณต้องใช้ package ชื่อ ndiswrapper-archck และ ndiswrapper-beyond

*คำแนะนำ:* ถ้าคุณไม่ได้เชื่อมต่อกับอินเตอร์เน็ทบนเครื่องที่ใช้งาน Arch คุณสามารถที่จะ Download package ใส่ไว้ใน diskette ได้จาก Mirror เช่น [http://www2.cddc.vt.edu/linux/distributions/archlinux/extra/os/i686/](http://www2.cddc.vt.edu/linux/distributions/archlinux/extra/os/i686/) คุณต้องการ ndiswrapper (หรือ ndiswrapper-archck หรือ ndiswrapper-beyond) และ ndiswrapper-utils และคุณอาจจะอยากต้องการ download package ชื่อ kernel26 ที่เป็น kernel ที่ทันสมัยที่สุด เนื่องจาก kernel ที่มากับ CD นั้นมักจะไม่ใช่รุ่นที่ทันสมัย

หลังจากติดตั้งเสร็จเรียบร้อยแล้ว ให้ทำตามขั้นตอนดังนี้

```
ndiswrapper -i filename.inf
ndiswrapper -l
ndiswrapper -m
depmod -a

```

หลังจากนั้นให้คุณแก้ไขไฟล์ /etc/rc.conf เพื่อให้ระบบเรียกใช้งาน ndiswrapper ตอนเริ่มต้น โดยให้ใส่ ndiswrapper ในส่วนของ MODULES ดังตัวอย่างด้านล่าง

```
MODULES=(ndiswrapper snd-intel8x0 !usbserial)

```

สิ่งที่สำคัญคือให้แน่ใจว่ามี ndiswrapper อยู่ในบรรทัดนี้ การทดสอบว่ามันสามารถทำงานได้หรือไม่เป็นสิ่งที่ดี ทดลองทำได้ด้วยคำสั่ง

```
modprobe ndiswrapper
iwconfig

```

คุณควรจะเห็น wlan0 หากคุณมีปัญหา ให้ดูที่หน้านี้ [Ndiswrapper installation wiki](http://ndiswrapper.sourceforge.net/mediawiki/index.php/Installation)

#### prism54

ให้คุณ download firmware driver ที่เหมาะสมกับอุปกรณ์ของคุณจาก [ที่นี่](http://www.prism54.org/) และเปลี่ยนชื่อให้เป็น 'isl3890' หากยังไม่มี ให้สร้าง directory ชื่อ /lib/firmware แล้วคัดลอกไฟล์ 'isl3890' ไปเก็บไว้ นี่ควรจะทำให้ระบบทำงานได้ ([กระดานข่าวเกี่ยวกับเรื่องนี้](https://bbs.archlinux.org/viewtopic.php?t=16569&start=0&postdays=0&postorder=asc&highlight=siocsifflags+such+file++directory))

#### ACX100/111

คุณสามารถหา ACX100/111 driver ได้จาก [ที่นี่](http://acx100.sourceforge.net/) ซึ่งมันสามารถทำงานได้กับการ์ดที่ใช้ Chipset ACX100/111 จาก Texas Instruments

ตรงกันข้ามกับสิ่งที่คุณคิด การติดตั้งระบบสามารถทำได้อย่างง่ายดาย มีคำแนะนำที่เขียนโดย Craig [ที่นี่](http://www.houseofcraig.net/acx100_howto.php) อย่างไรก็ดี ไฟล์ README ที่มาพร้อมกับ driver ได้มีคำอธิบายที่เข้าใจง่ายไว้แล้ว

1.  Download driver เวอร์ชันล่าสุด
2.  แตกไฟล์ออกไปยัง directory ที่คุณต้องการ โปรดระวัง เนื่องจากไฟล์ที่ถูกบีบอัดอยู่ไม่มี path หรือโครงสร้าง directory อยู่ ดังนั้นถ้าคุณไม่แตกไฟล์ออกไปยัง directory ที่สร้างใหม่ ไฟล์จะกระจัดกระจายไปทุกที่
3.  เข้าไปยัง directory ที่แตกไฟล์ไว้
4.  สั่งคำสั่ง `make -C /lib/modules/`uname -r`/build M=`pwd`` 
5.  แปลงตัวเองเป็น root
6.  สั่งคำสั่ง `make -C /lib/modules/`uname -r`/build M=`pwd` modules_install` 
7.  สั่งคำสั่ง `depmod -ae` เพื่อให้ kernel สร้าง module ขึ้นมาใหม่
8.  ใส่แผ่น Driver CD ที่มากับอุปกรณ์เข้าไปในคอมพิวเตอร์
9.  Mount CD Drive ด้วยคำสั่ง `mount <device>` 
10.  คัดลอก Firmware จากแผ่น cd ไปยัง /lib/firmware.
11.  เปลี่ยนชื่อ firmware ให้เป็น 'tiacxNNNcMM' (NNN=100/111, MM=radio module ID (ในรูปแบบเลขฐานสิบหก ตัวใหญ่)) สำหรับ PCI driver และ tiacxNNNusbcMM สำหรับ USB driver
12.  Load acx module โดยใช้คำสั่ง `modprobe acx` 
13.  เพิ่ม acx เข้าไปใน MODULES ใน /etc/rc.conf เพื่อให้ระบบเรียกใช้ตอนเริ่มทำงาน
14.  ทำตามคำแนะนำของ iwconfigเพื่อเชื่อมต่อกับระบบของคุณ

โปรดสังเกต: คุณสามารถสร้าง driver ให้เข้าไปเป็นส่วนหนึ่งของ kernel tree ได้ โดยสามารถอ่านรายละเอียดได้จากไฟล์ README ที่มากับ Driver

#### BCM43XX

เป็น Driver สำหรับผู้ใช้ Broadcom ซึ่งใช้ชิปรุ่น 43xx นอกเหนือจากการใช้งาน ndiswrapper โดยมันได้ถูกแนะนำพร้อมกับ kernel เวอร์ชัน 2.6.17 การติดตั้งสามารถทำได้อย่างง่ายดาย

1.  ใช้คำสั่ง `iwconfig` หรือ `hwd -s` เพื่อตรวจสอบว่าคุณมีอุปกรณ์ที่ถูกต้อง ผลที่ได้จากการใช้คำสั่ง น่าจะดูคล้ายกับผลดังนี้ `Network    : Broadcom Corp.|BCM94306 802.11g NIC module: unknown` 
2.  ใช้คำสั่ง `pacman -S bcm43xx-fwcutter` เพื่อติดตั้งโปรแกรม firmware cutter
3.  Download windows driver สำหรับอุปกรณ์ของคุณ เพื่อใช้งาน firmware
    *   คุณสามารถ download [[1]](http://drinus.net/airport/wl_apsta.o) ได้ เพียง save มันไว้บน Desktop ของคุณ
4.  ใช้คำสั่ง `bcm43xx-fwcutter -w /lib/firmware /home/<ชื่อผู้ใช้>/Desktop/wl_apsta.o` คุณอาจจะต้องสร้าง /lib/firmware ก่อน
5.  Restart เครื่อง และตั้งค่าอุปกรณ์ของคุณตามปกติ คุณอาจจะใส่ bcm43xx ในส่วนของ MODULES ในไฟล์ rc.conf เพื่อให้มันเริ่มต้นพร้อมกับระบบ

## การตั้งค่าและเริ่มต้นระบบ

มีสองวิธีสำหรับ Arch Linux ในการใช้งานระบบเครือข่ายไร้สาย วิธีแรกคือการอ้างอิงจาก network script เพื่อใช้งานในกรณีที่อยู่กับที่ หรือไม่มีการเปลี่ยนแปลงสถานที่ทำงานมากนัก (non-roaming) อีกวิธีหนึ่งคือการใช้ Network Profiles ซึ่งทำให้คุณสามารถเรียกใช้รูปแบบการตั้งค่าที่แตกต่างกันได้อย่างง่ายดาย

### การใช้งาน Arch Linux กับการตั้งค่า Wireless Network

*   การตั้งค่าโดยทั่วไปของ Arch Linux Wireless Configuration นั้นสามารถเข้าใจได้ง่าย โดยการตั้งค่าสำหรับ Wireless Network นั้นไม่แตกต่างอะไรกับการตั้งค่าระบบ Network ธรรมดา โดยอยู่ในไฟล์ /etc/rc.conf ตัวอย่างเช่น

```
# /etc/rc.conf
wlan0="dhcp"
INTERFACES=(lo eth0 wlan0)

```

*   นอกเหนือไปกว่านี้ networking script ต้องการบางวิธีเพื่อที่จะตรวจสอบว่า wlan0 เป็น wireless network interfcace (เนื่องจาก wireless interface ทั้งหมดไม่ได้มีแค่ชื่อ wlan*) การตั้งค่าส่วนนี้จะอยู่ในไฟล์ /etc/conf.d/wireless การตั้งค่านั้นสามารถทำได้ง่ายมาก สำหรับแต่ละ wireless interface คุณเพียงแค่ประกาศค่า wlan_<ชื่อ interface> เช่น ถ้า wireless interface ของคุณชื่อ "wlan0" ก็ให้ประกาศค่า wlan_wlan0 หรือหาก interface ของคุณชื่อ eth0 ก็จะเป็น wlan_eth0 เป็นต้น ค่าต่างๆ ในการตั้งค่านี้จะถูกใช้เป็นตัวแปรในการตั้งค่า iwconfig (ใช้คำสั่ง man iwconfig สำหรับข้อมูลเพิ่มเติม) *ต้องใส่ชื่อ interface name ด้วย*
*   ตัวอย่างง่ายๆ ของการตั้งค่าตามคำแนะนำด้านบน

```
# /etc/conf.d/wireless
wlan_wlan0="wlan0 essid MyEssid"

```

### การใช้งาน Roaming Network Profiles

#### ติดตั้งแบบเร็ว

1.  สร้าง Profile ใหม่
    1.  สร้าง network profile ใน <tt>/etc/network-profiles/</tt> โดยใช้โครงร่างจากไฟล์ <tt>template</tt> โดยให้ชื่อว่า home (เป็นตัวอย่าง) โปรดจำชื่อนี้ไว้ เพราะมันจะถูกเรียกใช้อีกรอบ
    2.  ตั้งค่ารายละเอียดต่างๆ ใน network profile
2.  ลบการตั้งค่าที่ไม่ได้ใช้งานแล้วออกจาก <tt>rc.conf</tt>
    1.  ลบชื่อ interface ที่จะถูกจัดการโดย network profile ออกจากส่วนของ INTERFACES
    2.  ลบ route ที่ไม่เกี่ยวข้องออกจากส่วนของ ROUTE
    3.  ปล่อย **lo** ไว้ที่เดิม
3.  เพิ่มการตั้งค่า Network Profile ใหม่เข้าไปใน <tt>rc.conf</tt>
    1.  ใส่ชื่อของ Network Profile ลงไปใน <tt>NET_PROFILES=()</tt> เช่น `NET_PROFILES=(home)` 

ถือเป็นการเสร็จสิ้นการติดตั้งแบบเร็ว คุณสามารถตั้ง <tt>NET_PROFILES</tt> ให้เป็น "menu" และมันจะแสดง dialog ให้คุณเลือก Network Profile ในขณะที่เครื่องกำลังเริ่มทำงาน

อีกทางเลือกหนึ่ง คุณสามารถผ่านค่า <tt>NET=</tt> ให้กับ kernel ในขณะที่กำลังเริ่มต้นทำงาน เพื่อบอกให้ kernel ทราบว่าจะต้องใช้ network profile อันใดที่คุณต้องการใช้ เช่น

```
vmlinuz root=/dev/hda3 vga=773 ro NET=home

```

ได้มาจาก [คำอธิบายของ Judd](https://www.archlinux.org/pipermail/arch/2005-June/004855.html)

**การตรวจสอบหาระบบเครือข่ายไร้สายแบบอัตโนมัติ**

iphitus ได้สร้าง patch สำหรับ initscripts ซึ่งได้รวมเข้ามาอยู่ในมาตรฐานแล้ว โปรดดู [ที่นี่](https://www.archlinux.org/pipermail/arch/2005-July/005251.html) สำหรับคำอธิบายในการใช้งาน

**การสนับสนุน WPA**

phydeaux ได้สร้าง patch สำหรับการสนับสนุน WPA ซึ่งได้ถูกรวมเข้าไปอยู่ในมาตรฐาน และจะรวมไปกับ Arch Linux เวอร์ชันหลังจาก 0.7.1 สำหรับคำแนะนำในการใช้งาน WPA กับ Network Profile กรุณาดูที่ [Ndiswrapper and wpa supplicant](/index.php/Ndiswrapper_and_wpa_supplicant "Ndiswrapper and wpa supplicant")

**Netcfg GUI**

GUI script เพื่อใช้ในการเปลี่ยน Network Profile สำหรับ GNOME (หรือ window manager อื่นๆ) สามารถดูได้ที่ [AUR](https://aur.archlinux.org/packages.php?ID=4197) ([ตัวอย่างหน้าจอ](http://mac-cain13.livejournal.com/tag/netswitch))

### Wifi-radar

**Wifi-radar** เป็นโปรแกรมที่จะช่วยให้ผู้ใช้งานสามารถสับเปลี่ยนระบบเครือข่ายไร้สายได้อย่างง่ายดาย การติดตั้ง Wifi-radar สามารถทำได้ดังนี้

1.  # pacman -S wifi-radar
2.  # visudo

```
   หลังจากนั้น ให้ใส่ข้อมูลดังนี้
       yourusername     ALL=(ALL) NOPASSWD: /usr/sbin/wifi-radar
   และกดปุ่ม ESC และ colon (:)และ x จากนั้นกด Enter เพื่อบันทึกข้อมูลและออกจากโปรแกรม

```

1.  ใส่ wifi-radar เข้าไปในส่วนของ DAEMONS=() ในไฟล์ /etc/rc.conf และสั่งใช้งานโปรแกรมจากเมนู หากคุณต้องการเปลี่ยน network profile หลังจากการเริ่มต้นการใช้งาน ให้ใช้คำสั่ง netcfg โดยคุณเป็น root
2.  คุณอาจจะต้องการแก้ไขไฟล์ /etc/conf.d/wifi-radar เพื่อตั้งค่า network interface ที่คุณต้องการใช้เป็นบางตัว

### NetworkManager

**NetworkManager** เป็นระบบจัดการ network ที่มีความสามารถมากสำหรับ Linux ซึ่งมันได้ถูกบรรจุมากับ Linux Distributions หลายตัว และแน่นอน Arch Linux มันช่วยทำให้ผู้ใช้งานแบบ roaming สามารถเลือกระบบเครือข่ายที่ต้องการใช้งานได้ ข้อเสียอย่างเดียวคือคุณจะถูกบังคับให้ใส่รหัสผ่านทุกครั้งที่คุณเข้าสู่ระบบ GNOME และเริ่มใช้งานโปรแกรม ซึ่งปัญหานี้อาจจะยังไม่ถูกแก้ไขจนกว่าโปรแกรมจะออกเวอร์ชันต่อไป ข้อมูลเพิ่มเติมของ NetworkManager สามารถดูได้ที่ [NetworkManager](/index.php/NetworkManager "NetworkManager")

## Link เพิ่มเติม

*   [หน้า HOWTO ที่อาจจะช่วยคุณได้](http://www.hpl.hp.com/personal/Jean_Tourrilhes/Linux/Wireless.html)
*   [วิธีการติดตั้ง madwifi หากคุณไม่สามารถทำตาม The Arch Way ได้](http://madwifi.org/wiki/UserDocs/FirstTimeHowTo)