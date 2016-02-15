**ranger** **رينجر** عبارة عن مدير ملفات لا يستخدم واجهة رسومية بل يعمل في الطرفية، مكتوب بلغة Python ويعمل بأسلوب محرر vi لربط المفاتيح، ولديه مجموعة واسعة من الميزات، حيث تستطيع إدارة الملفات ومهامها باستعمال قليل من أزرار لوحة المفاتيح ومن دون الحاجة لاستعمال الفأرة.

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
*   [2 التشغيل](#.D8.A7.D9.84.D8.AA.D8.B4.D8.BA.D9.8A.D9.84)
*   [3 مقارنة مع مديري ملفات آخرين](#.D9.85.D9.82.D8.A7.D8.B1.D9.86.D8.A9_.D9.85.D8.B9_.D9.85.D8.AF.D9.8A.D8.B1.D9.8A_.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A2.D8.AE.D8.B1.D9.8A.D9.86)
*   [4 الوثائق](#.D8.A7.D9.84.D9.88.D8.AB.D8.A7.D8.A6.D9.82)
*   [5 التخصيص](#.D8.A7.D9.84.D8.AA.D8.AE.D8.B5.D9.8A.D8.B5)
    *   [5.1 ربط المفاتيح](#.D8.B1.D8.A8.D8.B7_.D8.A7.D9.84.D9.85.D9.81.D8.A7.D8.AA.D9.8A.D8.AD)
    *   [5.2 تحديد الأوامر](#.D8.AA.D8.AD.D8.AF.D9.8A.D8.AF_.D8.A7.D9.84.D8.A3.D9.88.D8.A7.D9.85.D8.B1)
    *   [5.3 فتح الملفات باستخدام التطبيقات الافتراضية](#.D9.81.D8.AA.D8.AD_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A8.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_.D8.A7.D9.84.D8.AA.D8.B7.D8.A8.D9.8A.D9.82.D8.A7.D8.AA_.D8.A7.D9.84.D8.A7.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A.D8.A9)
        *   [5.3.1 استخدام sxiv لاستعراض الصور](#.D8.A7.D8.B3.D8.AA.D8.AE.D8.AF.D8.A7.D9.85_sxiv_.D9.84.D8.A7.D8.B3.D8.AA.D8.B9.D8.B1.D8.A7.D8.B6_.D8.A7.D9.84.D8.B5.D9.88.D8.B1)
*   [6 أوامر مفيدة](#.D8.A3.D9.88.D8.A7.D9.85.D8.B1_.D9.85.D9.81.D9.8A.D8.AF.D8.A9)
    *   [6.1 الأقراص الخارجية](#.D8.A7.D9.84.D8.A3.D9.82.D8.B1.D8.A7.D8.B5_.D8.A7.D9.84.D8.AE.D8.A7.D8.B1.D8.AC.D9.8A.D8.A9)
    *   [6.2 الأقراص على الشبكة](#.D8.A7.D9.84.D8.A3.D9.82.D8.B1.D8.A7.D8.B5_.D8.B9.D9.84.D9.89_.D8.A7.D9.84.D8.B4.D8.A8.D9.83.D8.A9)
    *   [6.3 أوامر متعلقة بالأرشفة](#.D8.A3.D9.88.D8.A7.D9.85.D8.B1_.D9.85.D8.AA.D8.B9.D9.84.D9.82.D8.A9_.D8.A8.D8.A7.D9.84.D8.A3.D8.B1.D8.B4.D9.81.D8.A9)
        *   [6.3.1 فك الضغط](#.D9.81.D9.83_.D8.A7.D9.84.D8.B6.D8.BA.D8.B7)
        *   [6.3.2 الضغط](#.D8.A7.D9.84.D8.B6.D8.BA.D8.B7)
    *   [6.4 ربط الصور](#.D8.B1.D8.A8.D8.B7_.D8.A7.D9.84.D8.B5.D9.88.D8.B1)
*   [7 مصادر من الإنترنت](#.D9.85.D8.B5.D8.A7.D8.AF.D8.B1_.D9.85.D9.86_.D8.A7.D9.84.D8.A5.D9.86.D8.AA.D8.B1.D9.86.D8.AA)

### التثبيت

يمكنك تثبيت [ranger](https://www.archlinux.org/packages/?name=ranger) من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories") باستعمال [pacman](/index.php/Pacman "Pacman"):

```
# pacman -S ranger

```

هناك أيضاً [ranger-git](https://aur.archlinux.org/packages.php?ID=35421) في مستودعات [AUR](/index.php/AUR "AUR").

إذا أردت أن تُعاين الملفات باستعمال "scope.sh" فقم بتثبيت:

*   [libcaca](https://www.archlinux.org/packages/?name=libcaca) لمعاينة الصور
*   [highlight](https://www.archlinux.org/packages/?name=highlight) لتلوين الكود بشكل مشابه لبرامج بيئة تطوير التطبيقات
*   [atool](https://www.archlinux.org/packages/?name=atool) لمعاينة الملفات المضغوطة
*   [lynx](https://www.archlinux.org/packages/?name=lynx), [w3m](https://www.archlinux.org/packages/?name=w3m), [elinks](https://www.archlinux.org/packages/?name=elinks) لمعاينة صفحات HTML
*   [poppler](https://www.archlinux.org/packages/?name=poppler) لمعاينة ملفات PDF
*   [transmission-show](https://www.archlinux.org/packages/?name=transmission-show) لمعاينة ملفات bit-torrent
*   [mediainfo](https://www.archlinux.org/packages/?name=mediainfo) أو [perl-image-exiftool](https://www.archlinux.org/packages/?name=perl-image-exiftool) لمعاينة معلومات ملفات الوسائط

## التشغيل

لبدأ رينجر قم بتشغيل أي برنامج طرفية مثل xterm واكتب الأمر `ranger` أو يمكنك استخدام الأمر:

```
xterm -e ranger

```

## مقارنة مع مديري ملفات آخرين

مقارنةً مع مديري الملفات ذوو الواجهة الرسومية والفأرة فإن كفاءة رينجر أكبر، لكن تبقى الواجهة الرسومية جذابة أكثر. لدى رينجر قسم واحد يحوي أعمدة متعددة للمجلدات المختلفة، وتستطيع أن ت عاين لمحتوى الملفات على الجانب الأيمن، ومقارنة مع مديري الملفات مزدوجي الأقسام فإن رينجر يعرض معلومات أكثر عن المجلدات والملفات، ويمكنك التنقل بين المجلدات بشكل سهل وسريع باستخدام لوحة المفاتيح أو الأوامر والمواقع المحفوظة، كما أن محتوى الملف أو المجلد يظهر بشكل تلقائي للمعاينة عند الوقوف على أحد الملفات أو المجلدات، ومن ميزات مدير الملفات رينجر أيضاً: العمل بأسلوب المحرر vi لربط المفاتيح، توفر الإشارات المرجعية، إمكانية الاختيار، إمكانية وضع وسوم، التبويبات المتعددة، سجل لحفظ الأوامر، القدرة على إنشاء وصلات، أوضاع تحكم متعددة، وعارض للمهمات. يوفر رينجر أيضاً أوامر قابلة للتخصيص ومفاتيح قابلة للربط حتى مع سكربتات خارجية. أقرب المنافسين لـ رينجر هو [Vifm](/index.php/Vifm "Vifm") الذي يتكون من قسمين مع ميزة المحرر vi السابقة لكنه يمتلك ميزات أقل بشكل عام.

## الوثائق

تستطيع فتح الكتيب الإرشادي لمدير الملفات رينجر بكتابة `?` يمكنك أيضاً فتح قائمة بالمفاتيح التي تم ربطها بأوامر معينة عن طريق كتابة `1?`، ويمكنك أيضاً كتابة `2?` لفتح قائمة الأوامر، و`3?` لقائمة الإعدادات.

## التخصيص

عند بدء تشغيل رينجر يقوم بإنشاء مجلد `~/.config/ranger/` ويمكنك نسخ ملفات التهيئة الافتراضية إلى هذا المجلد عن طريق الأمر:

 `ranger --copy-config=all` 

ومن ثم تستطيع تخصيصهم، من المفيد في هذه الحالة أن تكون ملماً بعض الشيء بلغة python.

*   `rc.conf` للتحكم بأوامر بدء التشغيل وربط المفاتيح
*   `commands.py` للتحكم بالأوامر التي يتم تنفيذها عند استخدام ":"
*   `rifle.conf` للتحكم بالتطبيقات التي يتم تشغيلها عند فتح أحد الملفات

يمكنك فتح الملفات باستخدام "l" أو "<Enter>". من أجل الملف `rc.conf` فإنك تحتاج فقط لأن تضيف التغييرات من الملف الافتراضي ﻷن كلا الملفين يتم تحميلهما، أما من أجل الملف `commands.py` فإذا لم تقم بإضافة الملف كاملاً فقم بوضع هذا السطر في أعلى الملف:

```
from ranger.api.commands import *

```

### ربط المفاتيح

قم باستخدام الملف `~/.config/ranger/rc.conf` لتعديل المفاتيح، حيث بإمكانك أيضاً أن تتعلم قواعد الكتابة والتعديل من نفس الملف، بالإضافة إلى أن هناك العديد من النماذج المعرفة مسبقاً.

المثال التالي يشرح كيفية استعمال "DD" لنقل الملفات المحددة إلى المجلد `~/.Trash/`، قم بوضع هذا الكود في `~/.config/ranger/rc.conf`:

```
# move to trash
map DD shell mv -t /home/myname/.config/ranger/Trash %s

```

### تحديد الأوامر

تكملة للمثال السابق فإن إضافة الأسطر التالية إلى `~/.config/ranger/commands.py` ستعمل على تعريف أمر لإفراغ مجلد المحذوفات `~/.Trash`:

```
class empty(Command):
    """:empty

    Empties the trash directory ~/.Trash
    """

    def execute(self):
        self.fm.run("rm -rf /home/myname/.Trash/{*,.[^.]*}")

```

لاستخدام الأمر قم بكتابة ":empty <Enter>" تستطيع استعمال المفتاح <tab> للإكمال التلقائي إذا أردت.

**تحذير:** لاحظ أن [^.] جزء أساسي من الأمر السابق، وبدونها سيتم حذف جميع الملفات والمجلدات من ..* وبالتالي مسح كل شيء في مجلد المنزل الخاص بك

### فتح الملفات باستخدام التطبيقات الافتراضية

قم بتعديل الملف `~/.config/ranger/rifle.conf` وبما أن الأسطر الأولى يتم تفيذها أولاً فيجب عليك وضع تعديلاتك في بداية الملف، على سبيل المثال السطر التالي سيجعل الملفات ذات الامتداد tex تُفتح باستخدام تطبيق kile.

```
ext tex = kile "$@"

```

#### استخدام sxiv لاستعراض الصور

من أجل استعراض الصور باستخدام [sxiv](/index.php/Sxiv "Sxiv") بعد أن قام رينجر بتشغيل عارض الصور الافتراضي عند فتح صورة معينة، استخدم [rifle_sxiv.sh script](http://git.savannah.gnu.org/cgit/ranger.git/tree/doc/examples/rifle_sxiv.sh) واتبع التعليمات الموجودة في التعليقات.

## أوامر مفيدة

### الأقراص الخارجية

من الممكن ربط الأقراص الخارجية بشكل تلقائي عن طريق [Udev](/index.php/Udev "Udev") أو عن طريق udev wrapper، الأقراص التي تم ربطها في `/media` تستطيع الدخول إليها بشكل سهل بالضغط على `gm` (go,media).

### الأقراص على الشبكة

### أوامر متعلقة بالأرشفة

هذه الأوامر تستخدم [atool](https://www.archlinux.org/packages/?name=atool) لتنفيذ أوامر الأرشفة.

#### فك الضغط

الأوامر التالية تنفذ عملية فك الضغط عن الأرشيف بنسخ (yy) ملف أو أكثر من ملفات الأرشيف ثم تنفيذ الأمر "استخرج هنا" ":extracthere" في المجلد المطلوب.

```
import os
from ranger.core.loader import CommandLoader

class extracthere(Command):
    def execute(self):
        """ Extract copied files to current directory """
        copied_files = tuple(self.fm.env.copy)

        if not copied_files:
            return

        def refresh(_):
            cwd = self.fm.env.get_directory(original_path)
            cwd.load_content()

        one_file = copied_files[0]
        cwd = self.fm.env.cwd
        original_path = cwd.path
        au_flags = ['-X', cwd.path]
        au_flags += self.line.split()[1:]
        au_flags += ['-e']

        self.fm.env.copy.clear()
        self.fm.env.cut = False
        if len(copied_files) == 1:
            descr = "extracting: " + os.path.basename(one_file.path)
        else:
            descr = "extracting files from: " + os.path.basename(one_file.dirname)
        obj = CommandLoader(args=['aunpack'] + au_flags \
                + [f.path for f in copied_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

```

#### الضغط

الأوامر التالية تُمكن المستخدم من ضغط عدة ملفات على المجلد الحالي عن طريق تحديدهم ومن ثم استدعاء الأمر ":compress <package name>" الذي يدعم اقتراح تسمية الأرشيف المضغوط وفقاً لاسم المجلد الحالي كما يدعم امتدادات وصيغ متعددة للضغط.

```
import os
from ranger.core.loader import CommandLoader

class compress(Command):
    def execute(self):
        """ Compress marked files to current directory """
        cwd = self.fm.env.cwd
        marked_files = cwd.get_selection()

        if not marked_files:
            return

        def refresh(_):
            cwd = self.fm.env.get_directory(original_path)
            cwd.load_content()

        original_path = cwd.path
        parts = self.line.split()
        au_flags = parts[1:]

        descr = "compressing files in: " + os.path.basename(parts[1])
        obj = CommandLoader(args=['apack'] + au_flags + \
                [os.path.relpath(f.path, cwd.path) for f in marked_files], descr=descr)

        obj.signal_bind('after', refresh)
        self.fm.loader.add(obj)

    def tab(self):
        """ Complete with current folder name """

        extension = ['.zip', '.tar.gz', '.rar', '.7z']
        return ['compress ' + os.path.basename(self.fm.env.cwd.path) + ext for ext in extension]

```

### ربط الصور

الأوامر التالية تفترض أنك تستخدم [cdemu](/index.php/Cdemu "Cdemu") لكي تربط الصور بالنظام (المقصود بالصور هي صور الأنظمة والبرامج ذوات الامتداد iso أو غيره، وليس صور jpg أو png أو gif وغيرها) و [autofs](/index.php/Autofs "Autofs") الذي يربط الأقراص الوهمية بمكان محدد ('/media/virtualrom' في هذه الحالة). **لا تنسى أن تغير مسار المجلد الذي سيتم ربط القرص فيه حسب إعدادات نظامك.**

لكي تربط صورة (أو عدة صور) بقرص وهمي من cdemu داخل رينجر فإنك تختار الصور ومن ثم تكتب ':mount' في الكونسول، قد تستغرق عملية الربط قليلاً من الوقت بحسب إعداداتك (بحسب إعداداتي استغرقت عملية الربط دقيقة واحدة)، فالأوامر تستخدم محملاً مخصصاً حيث أنها تنتظر المجلد لكي يتم ربطه ومن ثم تقوم بفتحه في الخلفية في التبويب التاسع.

```
import os, time
from ranger.core.loader import Loadable
from ranger.ext.signals import SignalDispatcher
from ranger.ext.shell_escape import *

class MountLoader(Loadable, SignalDispatcher):
    """
    Wait until a directory is mounted
    """
    def __init__(self, path):
        SignalDispatcher.__init__(self)
        descr = "Waiting for dir '" + path + "' to be mounted"
        Loadable.__init__(self, self.generate(), descr)
        self.path = path

    def generate(self):
        available = False
        while not available:
            try:
                if os.path.ismount(self.path):
                    available = True
            except:
                pass
            yield
            time.sleep(0.03)
        self.signal_emit('after')

class mount(Command):
    def execute(self):
        selected_files = self.fm.env.cwd.get_selection()

        if not selected_files:
            return

        space = ' '
        self.fm.execute_command("cdemu -b system unload 0")
        self.fm.execute_command("cdemu -b system load 0 " + \
                space.join([shell_escape(f.path) for f in selected_files]))

        mountpath = "/media/virtualrom/"

        def mount_finished(path):
            currenttab = self.fm.current_tab
            self.fm.tab_open(9, mountpath)
            self.fm.tab_open(currenttab)

        obj = MountLoader(mountpath)
        obj.signal_bind('after', mount_finished)
        self.fm.loader.add(obj)

```

## مصادر من الإنترنت

*   [ranger](http://nongnu.org/ranger) صفحة رينجر على الإنترنت.
*   [ranger mailing list](https://lists.nongnu.org/mailman/listinfo/ranger-users) قائمة رينجر البريدية
*   Arch Linux [forum thread](https://bbs.archlinux.org/viewtopic.php?id=93025) موضوع في منتديات أرش لينوكس
*   [GitHub-page](http://github.com/hut/ranger)
*   [DotShare.it](http://dotshare.it/category/fms/ranger/) تكوينات