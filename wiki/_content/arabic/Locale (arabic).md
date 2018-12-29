تُستخدم المحليّات في لينكس لتعريف لغات المستخدم. بما أن المحليّات تعرّف أطقم المحارف المُستخدمة، إعداد المحليّة الصحيحة مهمّ، خاصةً إن كانت اللغة تحوي محارف ليست ASCII.

تُعرّف أسماء المحليّات بالتنسيق التالي:

```
<lang>_<territory>.<codeset>[@<modifiers>]

```

## Contents

*   [1 تمكين المحليّات الضرورية](#تمكين_المحليّات_الضرورية)
    *   [1.1 مثال الإنجليزية الأمريكية](#مثال_الإنجليزية_الأمريكية)
*   [2 تعيين المحليّة على مستوى النظام](#تعيين_المحليّة_على_مستوى_النظام)
*   [3 تعيين المحليّات البديلة](#تعيين_المحليّات_البديلة)
*   [4 تعيين محليّة لكل مستخدم](#تعيين_محليّة_لكل_مستخدم)
*   [5 تعيين الترتيب](#تعيين_الترتيب)
*   [6 تعيين اليوم الأول من الأسبوع](#تعيين_اليوم_الأول_من_الأسبوع)
*   [7 إصلاح المشاكل](#إصلاح_المشاكل)
    *   [7.1 طرفيّتي لا تدعم UTF-8](#طرفيّتي_لا_تدعم_UTF-8)
        *   [7.1.1 Xterm لا تدعم UTF-8](#Xterm_لا_تدعم_UTF-8)
        *   [7.1.2 طرفية جنوم أو rxvt-unicode لا تدعمان UTF-8](#طرفية_جنوم_أو_rxvt-unicode_لا_تدعمان_UTF-8)
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

طالع [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1) و [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) للتفاصيل.

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
*   [http://wikigentoo.ksiezyc.pl/Locales.htm](http://wikigentoo.ksiezyc.pl/Locales.htm)
*   [ICU's interactive collation testing](http://demo.icu-project.org/icu-bin/locexp?_=en_US&x=col)
*   [Free Standards Group Open Internationalisation Initiative](http://www.openi18n.org/)
*   [*The Single UNIX Specification* definition of Locale](http://pubs.opengroup.org/onlinepubs/007908799/xbd/locale.html) by The Open Group
*   [Locale environment variables](https://help.ubuntu.com/community/EnvironmentVariables#Locale_setting_variables)