تُستخدم المحليّات في لينكس لتعريف لغات المستخدم. بما أن المحليّات تعرّف أطقم المحارف المُستخدمة، إعداد المحليّة الصحيحة مهمّ، خاصةً إن كانت اللغة تحوي محارف ليست ASCII.

تُعرّف أسماء المحليّات بالتنسيق التالي:

```
<lang>_<territory>.<codeset>[@<modifiers>]

```

## Contents

*   [1 تمكين المحليّات الضرورية](#.D8.AA.D9.85.D9.83.D9.8A.D9.86_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D9.91.D8.A7.D8.AA_.D8.A7.D9.84.D8.B6.D8.B1.D9.88.D8.B1.D9.8A.D8.A9)
    *   [1.1 مثال الإنجليزية الأمريكية](#.D9.85.D8.AB.D8.A7.D9.84_.D8.A7.D9.84.D8.A5.D9.86.D8.AC.D9.84.D9.8A.D8.B2.D9.8A.D8.A9_.D8.A7.D9.84.D8.A3.D9.85.D8.B1.D9.8A.D9.83.D9.8A.D8.A9)
*   [2 تعيين المحليّة على مستوى النظام](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D9.91.D8.A9_.D8.B9.D9.84.D9.89_.D9.85.D8.B3.D8.AA.D9.88.D9.89_.D8.A7.D9.84.D9.86.D8.B8.D8.A7.D9.85)
*   [3 تعيين المحليّات البديلة](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D9.91.D8.A7.D8.AA_.D8.A7.D9.84.D8.A8.D8.AF.D9.8A.D9.84.D8.A9)
*   [4 تعيين محليّة لكل مستخدم](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D9.85.D8.AD.D9.84.D9.8A.D9.91.D8.A9_.D9.84.D9.83.D9.84_.D9.85.D8.B3.D8.AA.D8.AE.D8.AF.D9.85)
*   [5 تعيين الترتيب](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.A7.D9.84.D8.AA.D8.B1.D8.AA.D9.8A.D8.A8)
*   [6 تعيين اليوم الأول من الأسبوع](#.D8.AA.D8.B9.D9.8A.D9.8A.D9.86_.D8.A7.D9.84.D9.8A.D9.88.D9.85_.D8.A7.D9.84.D8.A3.D9.88.D9.84_.D9.85.D9.86_.D8.A7.D9.84.D8.A3.D8.B3.D8.A8.D9.88.D8.B9)
*   [7 إصلاح المشاكل](#.D8.A5.D8.B5.D9.84.D8.A7.D8.AD_.D8.A7.D9.84.D9.85.D8.B4.D8.A7.D9.83.D9.84)
    *   [7.1 طرفيّتي لا تدعم UTF-8](#.D8.B7.D8.B1.D9.81.D9.8A.D9.91.D8.AA.D9.8A_.D9.84.D8.A7_.D8.AA.D8.AF.D8.B9.D9.85_UTF-8)
        *   [7.1.1 Xterm لا تدعم UTF-8](#Xterm_.D9.84.D8.A7_.D8.AA.D8.AF.D8.B9.D9.85_UTF-8)
        *   [7.1.2 طرفية جنوم أو rxvt-unicode لا تدعمان UTF-8](#.D8.B7.D8.B1.D9.81.D9.8A.D8.A9_.D8.AC.D9.86.D9.88.D9.85_.D8.A3.D9.88_rxvt-unicode_.D9.84.D8.A7_.D8.AA.D8.AF.D8.B9.D9.85.D8.A7.D9.86_UTF-8)
*   [8 See also](#See_also)

## تمكين المحليّات الضرورية

قبل أن تُستخدم محليّة على النظام، يجب تمكينها أولًا. لفرز كل المحليّات المتوفرة، استخدم:

```
$ locale -a

```

لتمكين محليّة، أزل التعليق عن اسم المحليّة في الملف `/etc/locale.gen`. يحوي هذا الملف كل المحليّات المتوفّرة التي يمكن للنظام استخدامها. اعكس العملية لتعطيل محليّة. بعد تمكين المحليّات الضرورية، يجب أن يُحدّث النظام بالمحليّات الجديدة:

```
# locale-gen

```

لعرض المحليّات المُستخدَمة حاليًّا، استخدم:

```
$ locale

```

**Tip:** رغم أنه على الأرجح ستُستخدم لغة واحدة على الحاسوب، سيكون من المفيد بل وقد يكون ضروريًّا تمكين محليّات أخرى كذلك. إن كنت تشغّل نظامًا بعدّة مستخدمين، وبعضهم لا يتحدّثون en_US، يجب على الأقل دعم محليّتهم الوحيدة في النظام.

### مثال الإنجليزية الأمريكية

أولًا أزل التعليق عن المحليّات التالية في `/etc/locale.gen`:

```
en_US.UTF-8 UTF-8

```

ثمّ حدّث النظام وأنت جذر:

```
# locale-gen

```

## تعيين المحليّة على مستوى النظام

لتعريف المحليّة المستخدمة على مستوى النظام، عيّن `LANG` في `/etc/locale.conf`.

`locale.conf` يحوي قائمة مفصولة بأسطر جديدة لتعيينات متغيّر البيئة: بالإضافة إلى `LANG`، فهو يدعم كل متغيّرات `LC_*`، ما عدا `LC_ALL`.

**ملاحظة:** `/etc/locale.conf` غير موجود افتراضيًّا ويجب إنشاءه يدويًّا .

**Tip:** إن كان مَخرج `locale` is to your liking during installation, تستطيع توفير الوقت بعمل: `# locale > /etc/locale.conf` وأنت chrooted.
 `/etc/locale.conf`  `LANG="en_US.UTF-8"` 

يمكن لهذا أن يكون مثال ضبط متقدّم:

 `/etc/locale.conf` 
```
# Enable UTF-8 with Australian settings.
LANG="en_AU.UTF-8"

# Keep the default sort order (e.g. files starting with a '.'
# should appear at the start of a directory listing.)
LC_COLLATE="C"

# Set the short date to YYYY-MM-DD (test with "date +%c")
LC_TIME="en_DK.UTF-8"
```

يمكنك تعيين المحليّة الافتراضية في `locale.conf` أثناء استخدام `localectl`، مثلًا:

```
# localectl set-locale LANG="de_DE.utf8"

```

طالع [localectl(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) و [locale.conf(5)](http://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) للتفاصيل.

سيأخذون تأثيرهم بعد إعادة إقلاع النظام وسيُعيّنون كجلسات مفردة أثناء الولوج.

## تعيين المحليّات البديلة

البرامج التي تستخدم gettext للترجمات تحترم الخيار `LANGUAGE` بالإضافة إلى المتغيّرات المعتادة. هذا يسمح للمستخدمين بتحديد [قائمة](http://www.gnu.org/software/gettext/manual/gettext.html#The-LANGUAGE-variable) من المحليّات المُستخدمة بذلك الترتيب. إن لم تتوفّر ترجمة للمحليّة المفضّلة، ستُستخدم محليّة أخرى شبيهة بدلًا من الافتراضية. على سبيل المثالـ المستخدم الأسترالي قد يُبدِل إلى البريطانية بدلًا من الإنجليزية الأمريكية:

 `~/.bashrc`  `export LANGUAGE="en_AU:en_GB:en"` 

أو على مستوى النظام

 `/etc/locale.conf` 
```
LANG="en_AU"
LANGUAGE="en_AU:en_GB:en"
```

## تعيين محليّة لكل مستخدم

كما ذكرنا سابقًا، بعض المستخدمين قد يعرّفون محليّة مختلفة عن المحليّة على مستوى النظام. لعمل ذلك، صدّر المتغيّر `LANG` بالمحليّة المعيّنة في الملف `~/.bashrc`. كمثال، لاستخدام المحليّة `en_AU.UTF-8`:

```
export LANG=en_AU.UTF-8

```

ستُحدّث المحليّات عند sourced `~/.bashrc`. للتحديث، أمّا أعد الولوج أو source it يدويًّا:

```
$ source ~/.bashrc

```

## تعيين الترتيب

الترتيب أو الفرز، يختلفان قليلًا. الفرز وحش أبله والمحليّات المختلفة تفعل الأشياء بطريقة مختلفة. للإلتفاف حول المشاكل المحتملة، تعيّن آرتش `LC_COLLATE="C"` إلى `/etc/profile`. على أيّ حال، هذه الطريقة أُهمِلت الآن. لتمكين هذا السلوك، ببساطة أضف التالي إلى `/etc/locale.conf`:

```
LC_COLLATE="C"

```

سيفرز الآن الأمر ls الملفات ذات النقاط أولًا، متبوعة بأسماء الملفات بأحرف كبيرة وصغيرة. لاحظ أنه دون الإعداد `LC_COLLATE`، تقول المحليّة للتطبيقات بالفرز عبر `LC_ALL` أو `LANG`، لكن الإعدادات `LC_COLLATE` ستُتَجاوز إن عُيّن `LC_ALL`. إن كانت هذه مشكلة، تأكّد أن LC_ALL لم يُعيّن بإضافة التالي إلى `/etc/profile` بدلًا منه:

```
export LC_ALL=

```

لاحظ أن LC_ALL متغيّر LC الوحيد الذي "لا يمكن" تعيينه في `/etc/locale.conf`.

## تعيين اليوم الأول من الأسبوع

هناك العديد من الدول التي يكون فيها بداية الأسبوع يوم الإثنين. لضبط هذا، غيّر أو أضف الأسطر التالية في القسم `LC_TIME` في `/usr/share/i18n/locales/<your_locale>`:

```
week            7;19971130;5
first_weekday   2
first_workday   2

```

وثمّ حدّث النظام:

```
# locale-gen

```

**Tip:** إن واجهتك أنواع من المشاكل مع النظام وودت السؤال في المنتدى، القائمة البريدية أو غيرهما، فضلًا ضمّن المَخرج من المشكلة سيئة السلوك عبر `export LC_MESSAGES=C` قبل اللصق. ستعيِّن رسائل المَخرج (الأخطاء والتحذيرات) إلى الإنجليزية، وبالتالي فهم أناسٍ أكثر لمشكتك. لا يُطبّق ذلك إن كنت تلصق في منتدى بلغة غير الإنجليزية.

## إصلاح المشاكل

### طرفيّتي لا تدعم UTF-8

للأسف بعض الطرفيات لا تدعم UTF-8\. في هذه الحالة، عليك استخدام طرفية مختلفة. هذه بعض الطرفيات التي تدعم UTF-8:

*   vte-based terminals
*   gnustep-terminal
*   konsole
*   [mlterm](/index.php/Mlterm "Mlterm")
*   [rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode")
*   [xterm](/index.php/Xterm "Xterm")

#### Xterm لا تدعم UTF-8

xterm تدعم UTF-8 فقط إن شُغِّل كـ `uxterm` أو `xterm -u8`.

#### طرفية جنوم أو rxvt-unicode لا تدعمان UTF-8

عليك إطلاق بعض التطبيقات من محليّة UTF-8 وإلّا ستُسقطا دعم UTF-8\. مكّن المحليّة `en_US.UTF-8` (أو بديل UTF-8 لديك) بالتعليمات أعلاه وعيّنها كمحليّة افتراضيّة، ثم أعد الإقلاع.

## See also

*   [Gentoo Linux Localization Guide](http://www.gentoo.org/doc/en/guide-localization.xml)
*   [Gentoo Wiki Archives: Locales](http://www.gentoo-wiki.info/Locales)
*   [ICU's interactive collation testing](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definition of Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) by The Open Group
*   [Locale environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)