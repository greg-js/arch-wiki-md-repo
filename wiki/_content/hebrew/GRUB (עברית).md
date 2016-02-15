GRand Unified Bootloader (GRUB)

## Contents

*   [1 התקנה ב-Master Boot Record](#.D7.94.D7.AA.D7.A7.D7.A0.D7.94_.D7.91-Master_Boot_Record)
*   [2 הגדרות](#.D7.94.D7.92.D7.93.D7.A8.D7.95.D7.AA)
    *   [2.1 LiLO and GRUB interaction](#LiLO_and_GRUB_interaction)
        *   [2.1.1 Troubleshooting](#Troubleshooting)
*   [3 External Resources](#External_Resources)

# התקנה ב-Master Boot Record

```
grub-install -root-directory _Mount-Point_ (hd_n_) 

```

יגרום לכך ש-GRUB תותקן ב-MBR של הדיסק הקשיח. האופציה מציינת את הנתיב לקובץ הקרנל, אם הוא אינו בספריית השורש, אלא בספרייה **/boot**. (hd_n_) מציין את הדיסק הקשיח, כאשר 'n' הוא מספר החל ב-0.

דוגמה:

```
 grub-install --root-directory=/boot '(hd0)'
 grub-install /dev/hda

```

# הגדרות

ההגדרות של GRUB נמצאות בקובץ זה:

```
/boot/grub/menu.lst

```

*   _(hdn,m)_ היא מחיצה m בדיסק n, ספרות מתחילות עם 0
*   _splashimage (hdn,m)/grub/Name.xpm.gz_ קובץ הספלאש
*   _default n_ פריט ברירת המחדל בתפריט האתחול, שייבחר לאחר פרק זמן מוגדר אם המשתמש לא בחר אפשרות אחרות מהתפריט
*   _timeout m_ פרק הזמן בשניות שיחלוף לפני שתופעל ברירת המחדל ללא התערבות המשתמש
*   _password -md5 str_ סיסמת אתחול מוצפנת 'str'
*   _title str_ מחרוזת 'str' עבור הכניסה בתפריט
*   _root (hdn,m)_ מחיצת בסיס, בה מאוכסן הקרנל

base partition, where the kernel is stored to

*   _kernel /path ro root=/dev/device initrd /initrd.img_ use the root option, if the kernel not placed in /
*   _makeactive
    chainloader +1_ sets root active and gives booting procedure to its boot-loader (for Windows, f.e.)
*   _map (hd0) (hd1)
    map (hd1) (hd0)_ changes primary and secondary disc for a boot, necessary to boot Windows from a secondary disc
*   _root (hdn,m,z)
    kernel /boot/loader_ boots the FreeBSD-Partition x
*   _default saved_ remebers each current boot selection and makes it the new default. Place "savedefault" at the end of each boot section, for that you want this feature shall be used.

For those who like eye-candy, there is [Graphical GRUB](/index.php/Graphical_GRUB "Graphical GRUB").

## LiLO and GRUB interaction

If you once had used [lilo](/index.php/Lilo "Lilo") Don't forget to remove it from master boot record with

```
pacman -R lilo

```

as some tasks (f.e. kernel compilation using `make all`) will make a lilo call, and then lilo is installed over grub.

#### Troubleshooting

*   If you are having problems like grub freezing when you do a grub install, use the command abs to get the PKGBUILS of the arch base packages and then use the command as root:

```
cd /var/abs/base/grub/
./install-grub

```

# External Resources

*   [אתר GRUB](http://www.gnu.org/software/grub/)