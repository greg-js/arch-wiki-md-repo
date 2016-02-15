מסמך זה מתאר כיצד ניתן להתקין ולאפשר את מערכת הקול ALSA עם קרנלים 2.4 ו-2.6\. ראו גם [כיצד ניתן לאפשר למספר תוכנות להשתמש בכרטיס הקול בו-בזמן](/index.php?title=Index.php/Allow_multiple_programs_to_play_sound_at_once&action=edit&redlink=1 "Index.php/Allow multiple programs to play sound at once (page does not exist)").

מסמך זה מתבסס על מסמך התקנת ALSA של Arjan Timmerman: [http://www.soulfly.nl/~arjan/archlinux/alsa-setup.html](http://www.soulfly.nl/~arjan/archlinux/alsa-setup.html) עם מידע נוסף: [https://bbs.archlinux.org/viewtopic.php?t=2544](https://bbs.archlinux.org/viewtopic.php?t=2544) אם יש לכם מחשב מתוצרת חברת Dell המצוייד בכרטיס Creative Labs Sound Blaster Live! תאלצו להדר את ALSA מקוד מקור בכוחות עצמכם.

## Contents

*   [1 התקנה](#.D7.94.D7.AA.D7.A7.D7.A0.D7.94)
*   [2 תצורה](#.D7.AA.D7.A6.D7.95.D7.A8.D7.94)
*   [3 עדיין לא ניתן לשמוע קול?](#.D7.A2.D7.93.D7.99.D7.99.D7.9F_.D7.9C.D7.90_.D7.A0.D7.99.D7.AA.D7.9F_.D7.9C.D7.A9.D7.9E.D7.95.D7.A2_.D7.A7.D7.95.D7.9C.3F)
    *   [3.1 הגדרת הרשאות](#.D7.94.D7.92.D7.93.D7.A8.D7.AA_.D7.94.D7.A8.D7.A9.D7.90.D7.95.D7.AA)
    *   [3.2 שחזור הגדרות המיקסר של ALSA לאחר אתחול](#.D7.A9.D7.97.D7.96.D7.95.D7.A8_.D7.94.D7.92.D7.93.D7.A8.D7.95.D7.AA_.D7.94.D7.9E.D7.99.D7.A7.D7.A1.D7.A8_.D7.A9.D7.9C_ALSA_.D7.9C.D7.90.D7.97.D7.A8_.D7.90.D7.AA.D7.97.D7.95.D7.9C)
    *   [3.3 פלט SPDIF](#.D7.A4.D7.9C.D7.98_SPDIF)
    *   [3.4 הגדרות עבור KDE](#.D7.94.D7.92.D7.93.D7.A8.D7.95.D7.AA_.D7.A2.D7.91.D7.95.D7.A8_KDE)

## התקנה

*   דרוש עבור קרנלים 2.4 או 2.6:

```
 # pacman -S alsa-lib alsa-utils

```

*   דרוש עבור קרנלים מסידרה 2.4:

```
 # pacman -S alsa-driver
 # depmod -a

```

*   מומלץ, אך לא נדרש:

```
 # pacman -S alsa-oss

```

יש לשים לב לכך שהחבילה 'alsa-driver' כוללת את המודולים הדרושים על בסיס קרנל מקורי של Arch! אם הידרתם קרנל 2.4 משלכם, קרוב לודאי שהסבר זה אינו מתאים ויהיה עליכם להדר את החבילה 'alsa-driver' מקוד מקור בעזרת ABS בזמן שהמערכת משתמשת בקרנל שלכם, ולהתקין את החבילה שנוצרה במקום.

## תצורה

_הערה: אם מערכת hotplug זיהתה את הכרטיס שלכם בהצלחה, אין צורך לטעון מודולים באופן ידני. במקרה כזה יש לעקוב אחר ההנחיות בצעדים 3 (ו-4). אם לא ידוע אם כרטיס הקול זוהה, הקלידו כמשתמש root את הפקודה "lsmod". תראו מספר מודולים שנטענו לזיכרון והם מתחילים עם המחרוזת "snd-"._

*   אתרו את המודול עבור כרטיס הקול שלכם: [http://www.alsa-project.org/alsa-doc/](http://www.alsa-project.org/alsa-doc/) המודול יתחיל עם המחרוזת 'snd-' (לדוגמה: 'snd-via82xx'). לחלופין, הריצו את הפקודה 'alsaconf' כמשתמש root.

*   טעינת מודולים:

```
 # modprobe snd-NAME-OF-MODULE
 # modprobe snd-pcm-oss

```

*   הגברת עוצמת הקול (unmute):

```
 # amixer set Master 75 unmute
 # amixer set PCM 75 unmute

```

תוכלו לעשות זאת מתוך ממשק באמצעות 'alsamixer'
שימו לב: אם אתם משתמשים ב-'alsamixer', אל תשכחו לבטל **השתקת קול** (לחצו על M) והגבירו את עוצמת הקול.

*   בידקו את עוצמת הקול עם קובץ wave שנמצא במערכת:

```
 # aplay mywav.wav

```

*   הוסיפו את ההוראות `snd-pcm-oss` ו- 'snd-NAME-OF-MODULE' לרשימת המודולים בקובץ '/etc/rc.conf'

*   [כיצד ניתן לאפשר למספר תוכנות להשתמש בכרטיס הקול בו-בזמן](/index.php/Allow_multiple_programs_to_play_sound_at_once "Allow multiple programs to play sound at once")

## עדיין לא ניתן לשמוע קול?

גם אם הדרייברים נטענו לזיכרון בהצלחה ועוצמת הקול סבירה ובוטלה השתקת הקול, ייתכן שלא תשמעו כל צליל! הוספת השורות הבאות לקובץ `/etc/modprobe.d/modprobe.conf` תטפל בבעיה זו(לפחות כאשר מדובר בדרייבר `via82xx`).

```
options snd-NAME-OF-MODULE ac97_quirk=0

```

### הגדרת הרשאות

*   הוסיפו את חשבון המשתמש שלכם לקבוצה audio:

```
 # gpasswd -a USERNAME audio

```

*   צאו והכנסו שוב כדי להבטיח טעינת ההרשאות עבור קבוצה זו.

### שחזור הגדרות המיקסר של ALSA לאחר אתחול

*   הריצו את הפקודה 'alsactl' פעם אחת כדי ליצור את הקובץ '/etc/asound.state'

```
 alsactl store

```

*   ערכו את הקובץ '/etc/rc.conf' והוסיפו 'alsa' לרשימת השירותים שמופעלים באתחול

### פלט SPDIF

*   (מקור: gralves בפורומים של gentoo)
*   באמצעות Gnome Volume Control, תחת הטאב Options, שנו את הערך IEC958 ל-PCM. ניתן לאפשר תכונה זו מתפריט ההעדפות.
*   אם Gnome Volume Control לא מותקנת
    *   ערכו את הקובץ /etc/asound.state. בקובץ זה ALSA שומרת את הגדרות המיקסר שלכם.
    *   אתרו את השורה: 'IEC958 Playback Switch'. לידה תמצאו שורה שאומרת value:false. שנו אותה ל: value:true.
    *   עכשיו אתרו שורה זו: 'IEC958 Playback AC97-SPSA' ושנו את הערך ל-0\.
    *   הפעילו את ALSA מחדש.

### הגדרות עבור KDE

*   הפעלת KDE:

```
 # startx

```

*   הגדירו את עוצמת הקול עבור המשתמש (לכל משתמש הגדרות משלו):

```
 # alsamixer

```

*   **KDE 3.3** מתפריט K Menu > Multimedia > KMix
    *   בחרו Settings > Configure KMix...
    *   בטלו את הסימון ליד "Restore volumes on logon"
    *   לחצו על OK, ואתם מוכנים. מעכשיו, עוצמת הקול תהיה זהה ב-KDE ובשורת הפקודה.