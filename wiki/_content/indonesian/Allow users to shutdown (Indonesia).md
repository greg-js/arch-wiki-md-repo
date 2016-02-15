Jika anda ingin mengijinkan penguna(user) untuk shutdown atau reboot sistem dan anda tidak menggunakan DE yang mendukung HAL ataupun karena memang tidak ingin mengunakan HAL ada beberapa cara yang dapat anda lakukan antara lain:

* * *

Dengan merubah ijin permisi dari perintah halt, reboot tidak perlu diubah karena merupakan _symlink_ ke halt. Sebagai root lakukan perintah di bawah ini:

```
chmod +s /sbin/halt

```

**Topic:** [https://bbs.archlinux.org/viewtopic.php?t=2787](https://bbs.archlinux.org/viewtopic.php?t=2787)

* * *

Cara lain dengan menggunakan `sudo`. Pertama-tama install sudo:

```
# pacman -S sudo

```

Setelah itu sebagai root tambahkan baris dibawah ini di file `/etc/sudoers` dengan menggunakan `visudo` (ketikkan visudo lalu file akan terbuka, jangan mengedit secara manual!). Rubah _pengguna_ dengan nama user yang ingin anda ijinkan dan _hostname_ dengan nama hostname komputer anda.

```
pengguna hostname = NOPASSWD: /sbin/shutdown -h now
pengguna hostname = NOPASSWD: /sbin/reboot

contoh:
dudung localhost = NOPASSWD: /sbin/shutdown -h now
dudung localhost = NOPASSWD: /sbin/reboot

```

Atau apabila anda ingin memberikan ijin ini pada semua pengguna dalam group tertentu rubah format diatas menjadi seperti ini(sesuaikan _namagroup_ dengan group yang anda inginkan).

```
%namagroup hostname = NOPASSWD: /sbin/shutdown -h now
%namagroup hostname = NOPASSWD: /sbin/reboot

```

Sekarang penguna dapat shutdown dengan perintah `sudo shutdown -h now`, dan reboot dengan `reboot`.

* * *

Apabila anda menggunakan XFCE setelah install sudo. Tambahkan baris ini ke `/etc/sudoers` dengan perintah `visudo`. Untuk semua user dalam group users(sesuaikan bila group yang anda inginkan berbeda):

```
%users hostname=NOPASSWD:/usr/lib/xfce4/xfsm-shutdown-helper

```

Sesuaikan _hostname_ dengan hostname anda.

Untuk satu user saja(sesuikan user dengan user anda):

```
user hostname=NOPASSWD:/usr/lib/xfce4/xfsm-shutdown-helper

```

Sesuikan _hostname_ dengan hostname anda.

Hal diatas akan mengaktifkan pilihan "reboot" dan "turn off" pada dialog logout XFCE.