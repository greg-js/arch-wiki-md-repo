เอกสารเรื่องนี้จะแนะนำท่านในการติดตั้งโปรแกรม Alsa ซึ่งเป็นระบบการจัดการเสียง กับ Kernel เวอร์ชัน 2.6 ท่านอาจจะอยากศึกษา [วิธีการทำให้หลายๆ โปรแกรมส่งเสียงพร้อมกัน](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

## Contents

*   [1 การติดตั้ง](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B4.E0.B8.94.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87)
    *   [1.1 Kernel drivers](#Kernel_drivers)
    *   [1.2 โปรแกรมส่วนของผู้ใช้](#.E0.B9.82.E0.B8.9B.E0.B8.A3.E0.B9.81.E0.B8.81.E0.B8.A3.E0.B8.A1.E0.B8.AA.E0.B9.88.E0.B8.A7.E0.B8.99.E0.B8.82.E0.B8.AD.E0.B8.87.E0.B8.9C.E0.B8.B9.E0.B9.89.E0.B9.83.E0.B8.8A.E0.B9.89)
*   [2 การตั้งค่า](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2)
    *   [2.1 การตรวจสอบว่า Module ระบบเสียงได้ถูกเรียกใช้งานแล้ว](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.A3.E0.B8.A7.E0.B8.88.E0.B8.AA.E0.B8.AD.E0.B8.9A.E0.B8.A7.E0.B9.88.E0.B8.B2_Module_.E0.B8.A3.E0.B8.B0.E0.B8.9A.E0.B8.9A.E0.B9.80.E0.B8.AA.E0.B8.B5.E0.B8.A2.E0.B8.87.E0.B9.84.E0.B8.94.E0.B9.89.E0.B8.96.E0.B8.B9.E0.B8.81.E0.B9.80.E0.B8.A3.E0.B8.B5.E0.B8.A2.E0.B8.81.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99.E0.B9.81.E0.B8.A5.E0.B9.89.E0.B8.A7)
    *   [2.2 เปิดใช้งาน channel และทดสอบการ์ดเสียง](#.E0.B9.80.E0.B8.9B.E0.B8.B4.E0.B8.94.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99_channel_.E0.B9.81.E0.B8.A5.E0.B8.B0.E0.B8.97.E0.B8.94.E0.B8.AA.E0.B8.AD.E0.B8.9A.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.8C.E0.B8.94.E0.B9.80.E0.B8.AA.E0.B8.B5.E0.B8.A2.E0.B8.87)
    *   [2.3 การตั้งค่าสิทธิ](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B8.AA.E0.B8.B4.E0.B8.97.E0.B8.98.E0.B8.B4)
    *   [2.4 การตั้งค่าระดับเสียงอัตโนมัติเมื่อระบบเริ่มต้น](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B8.A3.E0.B8.B0.E0.B8.94.E0.B8.B1.E0.B8.9A.E0.B9.80.E0.B8.AA.E0.B8.B5.E0.B8.A2.E0.B8.87.E0.B8.AD.E0.B8.B1.E0.B8.95.E0.B9.82.E0.B8.99.E0.B8.A1.E0.B8.B1.E0.B8.95.E0.B8.B4.E0.B9.80.E0.B8.A1.E0.B8.B7.E0.B9.88.E0.B8.AD.E0.B8.A3.E0.B8.B0.E0.B8.9A.E0.B8.9A.E0.B9.80.E0.B8.A3.E0.B8.B4.E0.B9.88.E0.B8.A1.E0.B8.95.E0.B9.89.E0.B8.99)
    *   [2.5 การใช้งาน SPDIF](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B9.83.E0.B8.8A.E0.B9.89.E0.B8.87.E0.B8.B2.E0.B8.99_SPDIF)
*   [3 ยังคงไม่มีเสียงอะไรออกมา](#.E0.B8.A2.E0.B8.B1.E0.B8.87.E0.B8.84.E0.B8.87.E0.B9.84.E0.B8.A1.E0.B9.88.E0.B8.A1.E0.B8.B5.E0.B9.80.E0.B8.AA.E0.B8.B5.E0.B8.A2.E0.B8.87.E0.B8.AD.E0.B8.B0.E0.B9.84.E0.B8.A3.E0.B8.AD.E0.B8.AD.E0.B8.81.E0.B8.A1.E0.B8.B2)
*   [4 การตั้งค่ากับ KDE](#.E0.B8.81.E0.B8.B2.E0.B8.A3.E0.B8.95.E0.B8.B1.E0.B9.89.E0.B8.87.E0.B8.84.E0.B9.88.E0.B8.B2.E0.B8.81.E0.B8.B1.E0.B8.9A_KDE)

## การติดตั้ง

### Kernel drivers

Alsa ได้ถูกรวมมาใน Kernel เวอร์ชัน 2.6 และได้ถูกรวมมาใน Kernel ของ Arch ที่ขึ้นต้นด้วย kernel26 หากคุณกำลังสร้าง kernel ของคุณเอง อย่าลืมเพิ่มความสามารถ alsa มาด้วย

Module ที่สำคัญๆ ควรจะถูกตรวจพบและติดตั้งโดยอัตโนมัติโดย udev คุณไม่ควรที่จะต้องตั้งค่าอะไรเพิ่มเติมอีก นอกจากคุณกำลังใช้การ์ด ISA **โปรดอย่าเรียกใช้** alsaconf ถ้าคุณกำลังใช้การ์ดเสียงชนิด PCI หรือ ISAPNP เนื่องจาก alsaconf อาจจะทำให้ระบบการตรวจสอบของ udev มีปัญหาได้

### โปรแกรมส่วนของผู้ใช้

*   โปรแกรมที่ต้องติดตั้ง

```
# pacman -S alsa-lib alsa-utils

```

*   โปรแกรมที่ควรติดตั้ง หากต้องการใช้โปรแกรมที่ต้องการความสารถของ OSS และ dmix

```
# pacman -S alsa-oss

```

โปรแกรมที่เกี่ยวข้องกับ Alsa น่าจะบังคับให้คุณลง alsa-lib ด้วย

## การตั้งค่า

### การตรวจสอบว่า Module ระบบเสียงได้ถูกเรียกใช้งานแล้ว

คุณสามารถปล่อยให้ udev ตรวจสอบระบบเสียงของคุณให้อัตโนมัติ พร้อมทั้งตรวจสอบความเข้ากันได้กับ OSS หากต้องการตรวจสอบ ก็ใช้คำสั่งดังนี้

```
$ lsmod|grep '^snd'
snd_usb_audio          69696  0 
snd_usb_lib            13504  1 snd_usb_audio
snd_rawmidi            20064  1 snd_usb_lib
snd_hwdep               7044  1 snd_usb_audio
snd_seq_oss            29412  0 
snd_seq_midi_event      6080  1 snd_seq_oss
snd_seq                46220  4 snd_seq_oss,snd_seq_midi_event
snd_seq_device          6796  3 snd_rawmidi,snd_seq_oss,snd_seq
snd_pcm_oss            45216  0 
snd_mixer_oss          15232  1 snd_pcm_oss
snd_intel8x0           27932  0 
snd_ac97_codec         87648  1 snd_intel8x0
snd_ac97_bus            1792  1 snd_ac97_codec
snd_pcm                76296  4 snd_usb_audio,snd_pcm_oss,snd_intel8x0,snd_ac97_codec
snd_timer              19780  2 snd_seq,snd_pcm
snd                    43776  12 snd_usb_audio,snd_rawmidi,snd_hwdep,snd_seq_oss,snd_seq,snd_seq_device,snd_pcm_oss,snd_mixer_oss,snd_intel8x0,snd_ac97_codec,snd_pcm,snd_timer
snd_page_alloc          7944  2 snd_intel8x0,snd_pcm

```

หากคุณได้ผลลัพธ์คล้ายๆ กับแบบนี้ แสดงว่า driver ของระบบเสียงคุณได้ถูกตรวจพบและติดตั้งเป็นที่เรียบร้อยแล้ว (โปรดสังเกตว่าในตัวอย่างนี้ snd_intel8x0 และ snd_usb_audio เป็น driver สำหรับ hardware)คุณสามารถดู directory **/dev/snd** สำหรับไฟล์ device

```
$ ls -l /dev/snd/
total 0
crw-rw----  1 root audio 116,  0 Apr  8 14:17 controlC0
crw-rw----  1 root audio 116, 32 Apr  8 14:17 controlC1
crw-rw----  1 root audio 116, 24 Apr  8 14:17 pcmC0D0c
crw-rw----  1 root audio 116, 16 Apr  8 14:17 pcmC0D0p
crw-rw----  1 root audio 116, 25 Apr  8 14:17 pcmC0D1c
crw-rw----  1 root audio 116, 56 Apr  8 14:17 pcmC1D0c
crw-rw----  1 root audio 116, 48 Apr  8 14:17 pcmC1D0p
crw-rw----  1 root audio 116,  1 Apr  8 14:17 seq
crw-rw----  1 root audio 116, 33 Apr  8 14:17 timer

```

ถ้าอย่างน้อยคุณมี **controlC0** และ **pcmC0D0p** หรือที่คล้ายๆ กัน แสดงว่าระบบเสียงของคุณได้ถูกตรวจพบและติดตั้งเป็นที่เรียบร้อยแล้ว

หากไม่เป็นไปตามนี้ แสดงว่าการ์ดเสียงของคุณยังไม่ถูกตรวจพบ **หากคุณต้องการความช่วยเหลือจาก IRC กรุณาใส่ผลลัพธ์จากการใช้คำสั่งข้างต้นไว้ด้วย** การแก้ปัญหาในตอนนี้คือ คุณสามารถสั่งให้เครื่อง load driver ของระบบเสียงด้วยตัวคุณเอง

*   ค้นหา module สำหรับการ์ดเสียงของคุณที่ [http://www.alsa-project.org/alsa-doc/](http://www.alsa-project.org/alsa-doc/) โดยโมดูลจะนำหน้าด้วย 'snd-' เช่น 'snd-via82xx'
*   Load โมดูล

```
 # modprobe snd-ชื่อของโมดูลของคุณ
 # modprobe snd-pcm-oss

```

*   ตรวจสอบหา device file ใน **/dev/snd** (ดูรายละเอียดทางด้านบน) และ/หรือ ทดลองใช้คำสั่ง **alsamixer** หรือ **amixer** แล้วดูผลลัพธ์ที่ออกมา
*   เพิ่ม **snd-pcm-oss** และ **snd-ชื่อโมลดูล** เข้าไปในส่วนของ MODULES ในไฟล์ **/etc/rc.conf** เพื่อให้ระบบเรียกใช้โมดูลเหล่านี้ในการเริ่มทำงานครั้งหน้า

### เปิดใช้งาน channel และทดสอบการ์ดเสียง

ในส่วนนี้ โปรดเข้าใช้งานเป็น root หากคุณต้องการใช้งานส่วนนี้ โดยไม่เป็น root โปรดข้ามไปอ่านขั้นตอนการตั้งค่าสิทธิก่อน

*   เปิดใช้งานการ์ดเสียง

เราแนะนำให้คุณใช้ 'alsamixer' ในการตั้งค่าระดับเสียงและเปิดใช้งาน channel

**คำแนะนำ** หากคุณกำลังใช้ **alsamixer** โปรดแน่ใจว่าคุณได้ **unmute** หรือเปิดใช้งาน channel นั้นๆ (กด M) ด้วย เพื่อให้สามารถใช้งานเสียงได้

คุณสามารถใช้งาน 'amixer' ก็ได้ แต่มันเป็นวิธีที่สะดวกน้อยกว่า

```
 # amixer set Master 75 unmute
 # amixer set PCM 75 unmute

```

*   ทดลองเล่นไฟล์เสียง

```
 # aplay mywav.wav

```

*   [การตั้งค่าให้หลายๆ โปรแกรมสามารถใช้งานเสียงได้พร้อมกัน](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

### การตั้งค่าสิทธิ

การอนุญาตให้ผู้ใช้ธรรมดาสามารถตั้งค่าเสียงได้ ทำตามขั้นตอนดังนี้

*   เพิ่มผู้ใช้เข้าไปในกลุ่ม audio:

```
# gpasswd -a ชื่อผู้ใช้ audio

```

*   ให้ผู้ใช้ของท่านออกจากระบบ แล้วเข้าสู่ระบบอีกครั้ง เพื่อให้ระบบตั้งค่าสิทธิ

### การตั้งค่าระดับเสียงอัตโนมัติเมื่อระบบเริ่มต้น

*   ใช้งานคำสั่ง 'alsactl' หนึ่งครั้งเพื่อสร้างไฟล์ '/etc/asound.state'

```
alsactl store

```

*   แก้ไขไฟล์ '/etc/rc.conf' เพิ่ม 'alsa' เข้าไปในส่วนของ DAEMONS โดยมันจะเก็บรายละเอียดการตั้งค่าเสียงของคุณทุกครั้งที่ปิดเครื่อง และเรียกใช้ใหม่เมื่อเริ่มต้นใช้เครื่อง

### การใช้งาน SPDIF

(ได้มาจากผู้ใช้ชื่อ gralves ในกระดานข่าวของ Gentoo)

*   ใน Gnome Volume Control, เปลี่ยน IEC958 ให้เป็น PCM ในส่วนของ Options tab
    *   แก้ไฟล์ **/etc/asound.state** ซึ่งเป็นไฟล์ที่เก็บการตั้งค่าของ Alsa
    *   หาบรรทัดที่เขียนว่า : 'IEC958 Playback Switch'. ใกล้ๆ กันนั้นคุณจะเจอบรรทัดที่เขียนว่า value:false เปลี่ยนมันให้เป็น value:true
    *   หาบรรทัด 'IEC958 Playback AC97-SPSA' และเปลี่ยนค่ามันเป็น 0
    *   Restart alsa

อีกวิธีหนึ่งในการเรียกใช้งาน SPDIF อัตโนมัติ (ใช้งานได้บน SoundBlaster Audigy)

*   เพิ่มคำสั่งนี้ในไฟล์ /etc/rc.local:

```
 # Use COAX-digital output
 amixer set 'IEC958 Optical' 100 unmute
 amixer set 'Audigy Analog/Digital Output Jack' on

```

คุณสามารถดูชื่อของการ์ดเสียงของคุณได้จากคำสั่ง

```
 amixer scontrols

```

## ยังคงไม่มีเสียงอะไรออกมา

ถ้าคุณติดตั้ง driver เรียบร้อยแล้ว ตั้งค่าระดับเสียงแล้ว และไม่มี channel ใดๆ ที่ปิดเสียงอยู่ แล้วคุณยังไม่ได้ยินเสียงอะไรเลย การใส่บรรทัดเหล่านี้เข้าไปในไฟล์ `/etc/modprobe.d/modprobe.conf` อาจจะช่วยแก้ปัญหาได้ (อย่างน้อยก็กับโมดูล `via82xx`)

```
options snd-ชื่อของโมดูล ac97_quirk=0

```

## การตั้งค่ากับ KDE

*   เรียกใช้ KDE

```
# startx

```

*   ตั้งค่าเสียงสำหรับผู้ใช้แต่ละคนด้วยคำสั่ง

```
# alsamixer

```

*   **KDE 3.3** ไปที่ K Menu > Multimedia > KMix
    *   เลือก Settings > Configure KMix...
    *   ไม่เลือกตัวเลือก "Restore volumes on logon"
    *   กด OK เป็นอันเสร็จสิ้น