## Contents

*   [1 גישה לקריאה/כתיבה במחיצות NTFS=](#.D7.92.D7.99.D7.A9.D7.94_.D7.9C.D7.A7.D7.A8.D7.99.D7.90.D7.94.2F.D7.9B.D7.AA.D7.99.D7.91.D7.94_.D7.91.D7.9E.D7.97.D7.99.D7.A6.D7.95.D7.AA_NTFS.3D)
    *   [1.1 הערות](#.D7.94.D7.A2.D7.A8.D7.95.D7.AA)
    *   [1.2 הוספת מאגר](#.D7.94.D7.95.D7.A1.D7.A4.D7.AA_.D7.9E.D7.90.D7.92.D7.A8)
    *   [1.3 התקנת חבילות](#.D7.94.D7.AA.D7.A7.D7.A0.D7.AA_.D7.97.D7.91.D7.99.D7.9C.D7.95.D7.AA)
    *   [1.4 השיגו את הקבצים ntfs.sys ו-ntoskrnl.exe](#.D7.94.D7.A9.D7.99.D7.92.D7.95_.D7.90.D7.AA_.D7.94.D7.A7.D7.91.D7.A6.D7.99.D7.9D_ntfs.sys_.D7.95-ntoskrnl.exe)
    *   [1.5 הכנת קבצי תצורה אחדים](#.D7.94.D7.9B.D7.A0.D7.AA_.D7.A7.D7.91.D7.A6.D7.99_.D7.AA.D7.A6.D7.95.D7.A8.D7.94_.D7.90.D7.97.D7.93.D7.99.D7.9D)
    *   [1.6 עיגון](#.D7.A2.D7.99.D7.92.D7.95.D7.9F)

## גישה לקריאה/כתיבה במחיצות NTFS=

מסמך זה יתאר כיצד לאפשר גישה לצורך קריאה/כתיבה במחיצות NTFS של מערכת ההפעלה Windows בעזרת Captive-NTFS.

#### הערות

את אתם משתמשים בקרנלים 2.6.10 או 2.6.11 עליכם להתקין את הטלאי הבא:

[http://www.datiku.com/documents/files/export_kpi.diff](http://www.datiku.com/documents/files/export_kpi.diff)

#### הוספת מאגר

קראו Server configuration והוסיפו את השרת הבא:

[ftp://ftp.archlinux.org/tur/punkrockguy318](ftp://ftp.archlinux.org/tur/punkrockguy318)

#### התקנת חבילות

```
# pacman -S captive

```

#### השיגו את הקבצים ntfs.sys ו-ntoskrnl.exe

הפעילו את הפקודות הבאות בקונסול, כמשתמש root:

```
# captive-install-acquire

```

לחצו על Forward, Skip, Skip, Yes, Start the download. לאחר שהקבצים ירדו תקבלו הודעות שגיאה שניתן להתעלם ממנה.

#### הכנת קבצי תצורה אחדים

```
 # /usr/share/lufs/prepmod

```

צרו ספריה בתוכה תרצו לעגון את המחיצה (למשל, /mnt/windows) לאחר מכן הוסיפו את הכניסה הבאה בקובץ etc/fstab, באחד משני הפורמאטים הבאים:

```
 #/dev/hdb1  /mnt/windows  captive-ntfs  defaults,users,uid="user"  0 0

```

או

```
 #/dev/discs/disc1/part1  /mnt/windows   captive-ntfs  defaults,users,uid="user"  0 0

```

החליפו את ההוראה 'user' בחשבון המשתמש שלכם ללא הגרשים. אם אינכם מעוניינים לאפשר גישה למשתמשים רגילים, מחקו אותה.

#### עיגון

```
 # mount /mnt/windows

```