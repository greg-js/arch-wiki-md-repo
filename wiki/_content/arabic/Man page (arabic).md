**man pages** الكُتيِّبات الإرشادية (اختصار لـ "manual pages") هي عبارة عن وثائق شاملة محملة مسبقاً مع غالبية أنظمة التشغيل المشابهة ليونِكس الأساسية ((UNIX-like))، بما فيها Arch Linux، والأمر المستخدم في إظهار الوثائق هو `man`.

على الرغم من إمكانياتها إلا أن الكُتيِّبات الإرشادية صممت لتكون وثائق مستقلة قائمة بذاتها، وبناءً على ذلك تم منع الإشارة ﻷي كتيِّبات إرشادية أخرى عند مناقشة مواضيع متصلة، وهذا اختلاف كبير مع "ملفات معلومات الوعي بالارتباطات التشعبية"((hyperlink-aware))، وهي محاولة "غنو" لاستبدال البنية التقليدية للكُتيِّبات الإرشادية.

## Contents

*   [1 الوصول إلى الكُتيِّبات الإرشادية](#.D8.A7.D9.84.D9.88.D8.B5.D9.88.D9.84_.D8.A5.D9.84.D9.89_.D8.A7.D9.84.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D9.8A.D8.A9)
*   [2 التصميم](#.D8.A7.D9.84.D8.AA.D8.B5.D9.85.D9.8A.D9.85)
*   [3 البحث في الكُتيِّبات](#.D8.A7.D9.84.D8.A8.D8.AD.D8.AB_.D9.81.D9.8A_.D8.A7.D9.84.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA)
*   [4 الكُتيِّبات الإرشادية الملونة](#.D8.A7.D9.84.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D9.8A.D8.A9_.D8.A7.D9.84.D9.85.D9.84.D9.88.D9.86.D8.A9)
    *   [4.1 استخدام less (ينصح به)](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_less_.28.D9.8A.D9.86.D8.B5.D8.AD_.D8.A8.D9.87.29)
    *   [4.2 استخدام most (لا ينصح به)](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_most_.28.D9.84.D8.A7_.D9.8A.D9.86.D8.B5.D8.AD_.D8.A8.D9.87.29)
    *   [4.3 الكُتيِّبات الإرشادية الملونة في xterm أو rxvt-unicode](#.D8.A7.D9.84.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D9.8A.D8.A9_.D8.A7.D9.84.D9.85.D9.84.D9.88.D9.86.D8.A9_.D9.81.D9.8A_xterm_.D8.A3.D9.88_rxvt-unicode)
        *   [4.3.1 xterm](#xterm)
        *   [4.3.2 rxvt-unicode](#rxvt-unicode)
*   [5 قراءة الكُتيِّبات الإرشادية المحلية](#.D9.82.D8.B1.D8.A7.D8.A1.D8.A9_.D8.A7.D9.84.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D9.8A.D8.A9_.D8.A7.D9.84.D9.85.D8.AD.D9.84.D9.8A.D8.A9)
    *   [5.1 التحويل إلى صيغة HTML](#.D8.A7.D9.84.D8.AA.D8.AD.D9.88.D9.8A.D9.84_.D8.A5.D9.84.D9.89_.D8.B5.D9.8A.D8.BA.D8.A9_HTML)
    *   [5.2 التحويل إلى PDF](#.D8.A7.D9.84.D8.AA.D8.AD.D9.88.D9.8A.D9.84_.D8.A5.D9.84.D9.89_PDF)
*   [6 الكُتيِّبات الإرشادية على الإنترنت](#.D8.A7.D9.84.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA_.D8.A7.D9.84.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D9.8A.D8.A9_.D8.B9.D9.84.D9.89_.D8.A7.D9.84.D8.A5.D9.86.D8.AA.D8.B1.D9.86.D8.AA)
*   [7 كُتيِّبات إرشادية جديرة بالاطلاع](#.D9.83.D9.8F.D8.AA.D9.8A.D9.90.D9.91.D8.A8.D8.A7.D8.AA_.D8.A5.D8.B1.D8.B4.D8.A7.D8.AF.D9.8A.D8.A9_.D8.AC.D8.AF.D9.8A.D8.B1.D8.A9_.D8.A8.D8.A7.D9.84.D8.A7.D8.B7.D9.84.D8.A7.D8.B9)
*   [8 انظر أيضاً](#.D8.A7.D9.86.D8.B8.D8.B1_.D8.A3.D9.8A.D8.B6.D8.A7.D9.8B)

## الوصول إلى الكُتيِّبات الإرشادية

لقراءة إحدى الكتيِّبات، أدخل التالي:

```
$ man *page_name*

```

تم تصنيف الكتيِّبات إلى عدة أقسام:

1.  الأوامر العامة
2.  استدعاءات النظام (دوال أو توابع تم تزويدها من قبل النواة)
3.  استدعاءات المكتبة ( دوال أو توابع لمكتبة C)
4.  ملفات خاصة (عادةً توجد في المسار dev/) وملفات التعريف Drivers
5.  صيغ واتفاقيات الملفات
6.  ألعاب
7.  متفرقات (بما فيها الاتفاقيات)
8.  أوامر إدارة النظام (عادة تتطلب صلاحيات الجذر root) والمخفيات daemons

عادة يشار إلى الكتيِّبات بأسمائها يليها رقم القسم المصنفة داخله ويوضع داخل أقواس، غالباً هناك كتيِّبات متعددة لنفس الاسم مثل man(1) و man(2) في هذه الحالة قم بإدخال رقم القسم ثم اسم الصفحة المطلوبة مثال:

```
$ man 5 passwd

```

لقراءة الكتِّيب الإرشادي الموجود في المسار `/etc/passwd/` بدلاً من عرض الكتيِّب الإرشادي الخاص بأداة `passwd`.

يمكن عرض وصف مختصر جداً للبرامج من كتيِّب محدد من دون عرض الكتيِّب كاملاً وذلك باستخدام الأمر `whatis`، على سبيل المثال لعرض وصف موجز لـ ls أكتب:

```
$ whatis ls

```

وسيقوم `whatis` بإظهار "list directory contents".

## التصميم

جميع الكتيِّبات تتبع تصميماً قياسياً إلى حد ما مما يساعد في التنقل بينها، تتضمن بعض الأقسام الموجودة في الكتيِّب الأشياء التالية غالباً:

*   NAME - اسم الأمر والغرض منه
*   SYNOPSIS - قائمة بالخيارات والمُعامِلات التي يتطلبها الأمر أو المتغيرات التي تتطلبها الدالة وملفها الأولي
*   DESCRIPTION - المزيد من الوصف الدقيق لوظيفة الأمر أو التعليمة
*   EXAMPLES - أمثلة عامة، عادة تتراوح بين البسيطة والمعقدة نسبياً
*   OPTIONS - وصف لكل خيار من الخيارات التي يستخدمها الأمر وما يمكنها القيام به
*   EXIT STATUS - معاني رموز المخرجات المختلفة
*   FILES - ملفات متصلة بالأمر أو الدالة
*   BUGS - مشكلات أو علل عند استخدام الأمر أو الدالة وهي قيد الإصلاح، تعرف أيضاً بـ KNOWN BUGS
*   SEE ALSO - قائمة بأوامر أو دوال مشابهة أو مرتبطة
*   AUTHOR, HISTORY, COPYRIGHT, LICENCE, WARRANTY - معلومات عن البرنامج وتاريخه وشروط استخدامه ومؤلفه

## البحث في الكُتيِّبات

في حين أن أداة `man` تمكن المستخدمين من عرض الكتيٍّب الإرشادي الخاص بأمر ما إلا أن المشكلة تظهر عندما لا يعرف المستخدم الاسم الدقيق للكتيِّب المراد عرضه، من حسن الحظ فإن خيارا `k-` أو `apropos--` يمكنا المستخدم من البحث باستخدام كلمة مفتاحية لوصف الكتيِّب المطلوب.

ميزة البحث هذه تقدمها ملفات مخبأة cache مخصصة، بشكل افتراضي فأنت لا تملك أي ملفات مخبأة cache وكل عمليات البحث التي ستقوم بها سترجع لك *nothing appropriate*، لكنك تستطيع إنشاء ملفات مخبأة cache أو تحديثها عن طريق إدخال:

```
# mandb

```

يجب عليك إدخال الأمر السابق في كل مرة تقوم بتثبيت كتيِّب جديد.

الآن تستطيع البدء بالبحث، على سبيل المثال للبحث عن صفحات تتعلق بـ "password":

```
$ man -k password

```

أو

```
$ man --apropos password

```

وهذا يماثل استدعاء الأمر `apropos`:

```
$ apropos password

```

الكلمة المفتاحية تم تفسيرها بشكل افتراضي على أنها تعبير عادي.

إذا أردت القيام ببحث أعمق عن طريق مطابقة الكلمات المفتاحية التي وجدت في المقال تستطيع استخدام خيار `K-`:

```
$ man -K password

```

## الكُتيِّبات الإرشادية الملونة

الكُتيِّبات الإرشادية "مفعلة الألوان" تعرض المعلومات بشكل أوضح مما يؤدي إلى فهم أسهل للمحتوى، هناك طريقتان شائعتان للحصول على كتيِّبات ملونة: استخدام `less` أو `most`.

### استخدام `less` (ينصح به)

	<small>*المصدر: [nion's blog - less colors for man pages](http://nion.modprobe.de/blog/archives/572-less-colors-for-man-pages.html)*</small>

هذه الطريقة لها الأفضلية حيث أن `less` تمتلك مجموعة ميزات أكثر من `most`، كما أنها تستخدم افتراضياً لعرض الكتيِّبات الإرشادية.

أضف التالي لملف تكوين shell ((shell configuration file)) ،باستخدام [Bash](/index.php/Bash "Bash") ستصبح بهذا الشكل:

 `~/.bashrc` 
```
man() {
    env LESS_TERMCAP_mb=$(printf "\e[1;31m") \
	LESS_TERMCAP_md=$(printf "\e[1;31m") \
	LESS_TERMCAP_me=$(printf "\e[0m") \
	LESS_TERMCAP_se=$(printf "\e[0m") \
	LESS_TERMCAP_so=$(printf "\e[1;44;33m") \
	LESS_TERMCAP_ue=$(printf "\e[0m") \
	LESS_TERMCAP_us=$(printf "\e[1;32m") \
	man "$@"
}

```

لتخصيص الألوان انظر [Wikipedia:ANSI escape code](https://en.wikipedia.org/wiki/ANSI_escape_code "wikipedia:ANSI escape code") لرؤية المرجع.

### استخدام `most` (لا ينصح به)

الوظيفة الأساسية لـ 'most' مشابهة لـ `less` و `more`، لكنها تمتلك مجموعة ميزات أقل، إعداد most لاستخدام الألوان أسهل من إعداد less لكن يوجد إعدادات إضافية ضرورية لجعل most تتصرف مثل less، قم بتثبيت [most](https://www.archlinux.org/packages/?name=most) باستخدام [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S most

```

قم بتعديل الملف الموجود في المسار `etc/man_db.conf/` وذلك بإلغاء تعليق السطر المتضمن على تعريف pager وقم بتغييرها لتصبح كالتالي:

```
DEFINE     pager     most -s

```

قم باختبار الإعداد الجديد بكتابة التالي:

```
$ man whatever_man_page

```

تعديل قيم الألوان يتطلب تعديل الملف `.mostrc/~` (يتم إنشاء الملف إذا لم يكن موجود) أو تعديل الملف `etc/most.conf/` من أجل تغيرات النظام الواسعة. مثال على `.mostrc/~` :

```
% Color settings
color normal lightgray black
color status yellow blue
color underline yellow black
color overstrike brightblue black

```

مثال آخر يُظهر أغلفة مفاتيح شبيهة بـ `less` (القفز إلى السطر تم تعيينه على'J').

```
% less-like keybindings
unsetkey "^K"
unsetkey "g"
unsetkey "G"
unsetkey ":"

```

```
setkey next_file ":n"
setkey find_file ":e"
setkey next_file ":p"
setkey toggle_options ":o"
setkey toggle_case ":c"
setkey delete_file ":d"
setkey exit ":q"

```

```
setkey bob "g"
setkey eob "G"
setkey down "e"
setkey down "E"
setkey down "j"
setkey down "^N"
setkey up "y"
setkey up "^Y"
setkey up "k"
setkey up "^P"
setkey up "^K"
setkey page_down "f"
setkey page_down "^F"
setkey page_up "b"
setkey page_up "^B"
setkey other_window "z"
setkey other_window "w"
setkey search_backward "?"
setkey bob "p"
setkey goto_mark "'"
setkey find_file "E"
setkey edit "v"

```

### الكُتيِّبات الإرشادية الملونة في xterm أو rxvt-unicode

	<small>*المصدر: [XFree resources file for XTerm program](http://pub.ligatura.org/fs/xfree86/xresources/xterm)*</small>

الطريقة السريعة لإضافة الألوان للكتيٍّبات المعروضة في [xterm](https://www.archlinux.org/packages/?name=xterm)/`uxterm` أو [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) تكون بتعديل `.Xresources/~` أو `.Xdefaults/~` .

#### xterm

```
*VT100.colorBDMode:     true
*VT100.colorBD:         red
*VT100.colorULMode:     true
*VT100.colorUL:         cyan

```

الأوامر السابقة *تستبدل* الزخرفة بالألوان، أيضاً قم بإضافة التالي:

```
*VT100.veryBoldColors: 6

```

إذا كنت تريد الألوان والزخارف (سميك أو تحته خط) *في نفس الوقت* انظر [xterm(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/xterm.1) لشرح مصدر `veryBoldColors`.

#### rxvt-unicode

```
URxvt.colorIT:      #87af5f
URxvt.colorBD:      #d7d7d7
URxvt.colorUL:      #87afd7

```

قم بالتالي:

```
$ xrdb -load ~/.Xresources

```

قم بتشغيل `xterm/uxterm` أو `rxvt-unicode` من جديد، يجب أن ترى الكتيِّبات ملونة،هذه المجموعة من الأوامر تجعل اللون **سميك** وتضع<u>خطاً</u> تحت الكلمات في `xterm/uxterm` أو بالإضافة إلى **السُمك** و<u>الخط</u> فهي تجعل الخط *مائلاً* في `rxvt-unicode`، تستطيع أن تعدل في المجموعات المختلفة من هذه السمات(انظر إلى [مصادر](http://pub.ligatura.org/fs/xfree86/xresources/xterm) لهذا الموضوع).

## قراءة الكُتيِّبات الإرشادية المحلية

عوضاً عن استخدام الواجهة القياسية فإن استخدام المتصفحات مثل lynx و [Firefox](/index.php/Firefox "Firefox") للاطلاع على الكتيِّبات يمكن المستخدمين من الحصول على الفوائد الرئيسية من الكتيِّبات الإرشادية: فالمتصفحات تعرض النصوص ذات الارتباطات التشعبية ((hyperlinked text)). مستخدمي [KDE](/index.php/KDE "KDE") يستطيعون قراءة الكتيِّبات داخل Konqueror باستخدام التالي:

```
man:<name>

```

[Official repositories](/index.php/Official_repositories "Official repositories") نستطيع الحصول على احتمالين آخرين لقراءة الكتيِّبات وذلك بتثبيت أحد البرامج التالية من المستودعات الرسمية:

1\. [xorg-xman](https://www.archlinux.org/packages/?name=xorg-xman) تقدم مظهراً منظماً للكتيِّبات في [X](/index.php/X "X").

2\. [GNOME](/index.php/GNOME "GNOME") Help Browser المسمى [yelp](https://www.archlinux.org/packages/?name=yelp) وهو أكثر تنظيماً لكن لديه بعض الاعتماديات.

### التحويل إلى صيغة HTML

في البداية قم بتثبيت [man2html](https://www.archlinux.org/packages/?name=man2html) من المستودعات الرسمية.

ثم قم بتحويل الكتيِّب:

```
$ man free | man2html -compress -cgiurl man$section/$title.$section$subsection.html > ~/man/free.html

```

يوجد استعمال آخر لـ `man2html` وهو التصدير إلى نص ذي صفوف وقابل للطباعة:

```
$ man free | man2html -bare > ~/free.txt

```

تطبيق man الخاص بـ "غنو" الموجود في مستودعات Arch له القدرة أيضاً على تنفيذ العملية السابقة من تلقاء نفسه:

```
$ man -H free

```

هذا الأمر سيقوم بقراءة متغيرات بيئة `BROWSER` لتحديد المتصفح، يمكنك تجاوز هذا بتمرير القيمة الثنائية إلى خيار `H-`.

### التحويل إلى PDF

الكتيِّبات دائماً قابلة للطباعة فهي مكتوبة بـ troff التي هي في الأساس لغة تنضيد((typesitting))، إذا كان لديك ghostscript مثبت على الجهاز فإن عملية تحويل الكتيِّبات الإرشادية إلى PDF سهلة جداً: `man -t <manpage> | ps2pdf - <pdf>` .[هذا البحث في google image](https://www.google.com/search?q=manpage+pdf+troff&num=100&hl=en&prmd=imvns&source=lnms&tbm=isch&sa=X&ei=5BZpUI3oH6rI2AXvx4CoAw&ved=0CAoQ_AUoAQ&biw=1321&bih=1100) سيعطيك فكرةً عن شكل الناتج من عملية التحويل، وقد لا يروق هذا الشكل للجميع.

محاذير: الخطوط تقتصر عادة على أحجام خطوط Times المضمنة، ولا يوجد ارتباطات تشعبية،بعض الكتيِّبات صممت خصيصاً لطريقة العرض في الطرفية ولن تظهر بشكل جيد بصيغة PS أو PDF.

السكربت التالي المكتوب بلغة Perl يقوم بتحويل الكتيِّبات إلى ملفات PDF ويخزن هذه الملفات في المسار `/HOME/.manpdf$` ومن ثم يشغل برنامج لعرض ملفات PDF وعلى وجه التحديد برنامج [mupdf](https://www.archlinux.org/packages/?name=mupdf).

 `Usage: manpdf [<section>] <manpage>` 
```
#!/usr/bin/perl
use File::stat;

$pdfdir = $ENV{"HOME"}."/.manpdf";
-d $pdfdir || mkdir $pdfdir || die "can't create $pdfdir";
$manpage = $ARGV[0];
chop($manpath = `man -w $manpage`);
die if $?;

$maninfo = stat($manpath) or die;
$manpath =~ s@.*/man./(.*)(\.(gz|bz2))?$@$1@;
$pdfpath = "$pdfdir/$manpath.pdf";
$pdftime = 0;
if (-f $pdfpath) {
    $pdfinfo = stat($pdfpath) or die;
    $pdftime = $pdfinfo->mtime;
}
if (!-f $pdfpath || $maninfo->mtime > $pdftime) {
    system "man -t $manpage | ps2pdf -dPDFSETTINGS=/screen - $pdfpath";
}
die if !-f $pdfpath;
if (!fork) {
    open(STDOUT, "/dev/null");
    open(STDERR, "/dev/null");
    exec "mupdf", "-r", "96", $pdfpath;
    #exec "acroread", $pdfpath;
}

```

## الكُتيِّبات الإرشادية على الإنترنت

هناك العديد من قواعد البيانات لكتيِّبات إرشادية متوفرة على الإنترنت، من ضمنها:

*   [*Debian GNU/Linux man pages*](http://manpages.debian.net/)
*   [*DragonFlyBSD manual pages*](http://leaf.dragonflybsd.org/cgi/web-man)
*   [*FreeBSD Hypertext Man Pages*](http://www.freebsd.org/cgi/man.cgi)
*   [*Linux and Solaris 10 Man Pages*](http://www.manpages.spotlynx.com/)
*   [*Linux/FreeBSD Man Pages*](http://manpagehelp.net) with user comments
*   [*Linux man pages at die.net*](http://linux.die.net/man/)
*   [The Linux man-pages project at kernel.org](http://www.kernel.org/doc/man-pages/)
*   [Man-Wiki: *Linux / Solaris / UNIX / BSD*](http://man-wiki.net/index.php/Main_Page)
*   [*NetBSD manual pages*](http://netbsd.gw.com/cgi-bin/man-cgi)
*   [*Mac OS X Manual Pages*](http://developer.apple.com/documentation/Darwin/Reference/ManPages/index.html)
*   [*On-line UNIX manual pages*](http://unixhelp.ed.ac.uk/alphabetical/index.html)
*   [*OpenBSD manual pages*](http://www.openbsd.org/cgi-bin/man.cgi)
*   [*Plan 9 Manual — Volume 1*](http://man.cat-v.org/plan_9/)
*   [*Inferno Manual — Volume 1*](http://man.cat-v.org/inferno/)
*   [*Storage Foundation Man Pages*](http://sfdoccentral.symantec.com/sf/5.0MP3/linux/manpages/index.html)
*   [*The UNIX and Linux Forums Man Page Repository*](http://www.unix.com/man-page/OpenSolaris/1/man/)
*   [*Ubuntu Manpage Repository*](http://manpages.ubuntu.com/)

## كُتيِّبات إرشادية جديرة بالاطلاع

في ما يلي قائمة غير حصرية لكتيِّبات جديرة بالاطلاع والتي قد تساعدك في فهم العديد من الأشياء بشكل أكبر، البعض منها تستطيع اعتباره مرجعاً (مثل جدول ascii):

*   ascii(7)
*   boot(7)
*   charsets(7)
*   chmod(1)
*   credentials(7)
*   fstab(5)
*   hier(7)
*   systemd(1)
*   locale(1P)(5)(7)
*   printf(3)
*   proc(5)
*   regex(7)
*   signal(7)
*   term(5)(7)
*   termcap(5)
*   terminfo(5)
*   utf-8(7)

ألقِ نظرة على كتيِّبات الفئة السابعة:

```
$ man -s 7 -k ".*" 

```

كتيِّبات Arch Linux المميزة:

*   archlinux(7)
*   mkinitcpio(8)
*   pacman(8)
*   pacman-key(8)
*   pacman.conf(5)

## انظر أيضاً

*   توصيات عامة لـ [General recommendations](/index.php/General_recommendations "General recommendations") - Arch