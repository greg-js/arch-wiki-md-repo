קל מאוד לאפשר זאת, והתהליך שמתואר בהמשך יאפשר לכם להוסיף מנהל כניסה גרפי למערכת, כך שיופעל באופן אוטומטי לאחר אתחול המערכת. כל שדרוש הן הרשאות root.

תזכורת: מנהלי המסכים (Display Managers) השונים לא מאפשרים כניסה למערכת עם סיסמה ריקה, או מנהלי הכניסה!

## הוראות התקנה

1\. התחברו למערכת כמשתמש *root*.

2\. פתחו את הקובץ */etc/rc.conf* עם עורך טקסט כלשהו.

3\. חפשו בתוך הקובץ שורה דומה לשורה הבאה (יש להניח שהיא תמצא לקראת סוף הקובץ):

```
DAEMONS=(syslogd klogd !pcmcia network netfs crond)

```

4\. הוסיפו בסוף השורה את מנהל המסכים הרצוי, בין אם KDM, GDM, או XDM, באופן הבא:

```
# This would load KDM on startup
DAEMONS=(syslogd klogd !pcmcia network netfs crond kdm)

```

```
# This would load GDM on startup
DAEMONS=(syslogd klogd !pcmcia network netfs crond gdm)

```

```
# This would load XDM on startup
DAEMONS=(syslogd klogd !pcmcia network netfs crond xdm)

```

5\. שמרו את הקובץ וסגרו את עורך הטקסט. בפעם הבאה שתאתחלו את המחשב, מנהל המסך יופעל עבורכם. אם לא, חזרו ובדקו את הקובץ וודאו שהתוכנה הרצויה אכן מותקנת.

## הוראות נוספות

החבילה שמכילה את KDM היא חלק מהחבילה **kdebase**. תוכלו להתקינה בעזרת [pacman](/index.php/Pacman "Pacman") כמשתמש root:

```
pacman -S kdebase

```

## שיטות חליפיות

השיטה שמתוארת לעיל צפוי שתעבוד, אך תוצאת הלוואי היא שלא יהיה הבדל בין runlevel 3 ו-5 וייתכן ש-XDM ו-KDM יופעלו שניהם, בכפוף לתוכן הקובץ **/etc/inittab**. כדי למנוע זאת, במקום ההוראות לעיל, עשו כך:

1\. התחברו כמשתמש **root**.

2\. פתחו את הקובץ **/etc/inittab'** בעורך הטקסט

3\. החליפו את השורה

```
id:3:initdefault:

```

בשורה:

```
id:5:initdefault:

```

4\. ודאו כי השורה:

```
x:5:respawn:/usr/X11R6/bin/xdm -nodaemon

```

מופיעה בקובץ.

5\. רשות. אם אתם מסתפקים בהפעלת XDM, דלגו על שלב זה. אם אתם רוצים להפעיל את GDM או KDM, החליפו את השורה:

```
x:5:respawn:/usr/X11R6/bin/xdm -nodaemon

```

באחת מהשורות הבאות:

```
x:5:respawn:/opt/gnome/sbin/gdm -nodaemon

```

```
x:5:respawn:/opt/kde/bin/kdm -nodaemon

```

6\. שמרו את הקובץ וסגרו את העורך.

זה הכל. בפעם הבאה שתאתחלו את המחשב, יופעל מנהל המסך שבחרתם. כדי להפעילו עכשיו, ללא צורך באתחול, הפעילו את הפקודה הבאה בשורת הפקודה (כמשתמש root):

```
/sbin/telinit 5

```

אם תצטרכו לסגור את X מתישהו בעתיד (למשל כדי לשדרג את הדרייברים של הכרטיס הגרפי), תוכלו להפעיל את הפקודה הבאה (כמשתמש root):

```
/sbin/telinit 3

```

כדי לחזור לשיטת ההתחברות הטקסטואלית הרגילה. לאחר שסיימתם, תוכל לחזור ל-runlevel 5 ללא צורך באתחול המחשב.