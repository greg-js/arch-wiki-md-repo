[نيمو](https://github.com/linuxmint/nemo) هو مدير ملفات سطح المكتب [Cinnamon](/index.php/Cinnamon "Cinnamon")

## Contents

*   [1 التثبيت](#.D8.A7.D9.84.D8.AA.D8.AB.D8.A8.D9.8A.D8.AA)
    *   [1.1 جعل نيمو مدير الملفات الافتراضي](#.D8.AC.D8.B9.D9.84_.D9.86.D9.8A.D9.85.D9.88_.D9.85.D8.AF.D9.8A.D8.B1_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA_.D8.A7.D9.84.D8.A7.D9.81.D8.AA.D8.B1.D8.A7.D8.B6.D9.8A)
*   [2 التهيئة](#.D8.A7.D9.84.D8.AA.D9.87.D9.8A.D8.A6.D8.A9)
    *   [2.1 إظهار أو إخفاء أيقونات سطح المكتب](#.D8.A5.D8.B8.D9.87.D8.A7.D8.B1_.D8.A3.D9.88_.D8.A5.D8.AE.D9.81.D8.A7.D8.A1_.D8.A3.D9.8A.D9.82.D9.88.D9.86.D8.A7.D8.AA_.D8.B3.D8.B7.D8.AD_.D8.A7.D9.84.D9.85.D9.83.D8.AA.D8.A8)
*   [3 الإضافات](#.D8.A7.D9.84.D8.A5.D8.B6.D8.A7.D9.81.D8.A7.D8.AA)
*   [4 إجراءات نيمو](#.D8.A5.D8.AC.D8.B1.D8.A7.D8.A1.D8.A7.D8.AA_.D9.86.D9.8A.D9.85.D9.88)
    *   [4.1 Clam Scan](#Clam_Scan)
    *   [4.2 نقل الملفات](#.D9.86.D9.82.D9.84_.D8.A7.D9.84.D9.85.D9.84.D9.81.D8.A7.D8.AA)

## التثبيت

قم [بتثبيت](/index.php/Pacman "Pacman") [nemo](https://www.archlinux.org/packages/?name=nemo) من [المستودعات الرسمية](/index.php/Official_repositories "Official repositories")

### جعل نيمو مدير الملفات الافتراضي

للتغيير من نُوتيلُس إلى نيمو:

 `/usr/share/applications/nautilus.desktop` 
```
[...]
#Exec=nautilus %U
Exec=nemo %U
[...]
```

## التهيئة

### إظهار أو إخفاء أيقونات سطح المكتب

```
# false to hide ; true to show
dconf write /org/nemo/desktop/show-desktop-icons false

```

## [الإضافات](https://github.com/linuxmint/nemo-extensions)

*   **Nemo fileroller** — دمج برنامج File Roller مع نيمو.

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-fileroller](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-fileroller) || [nemo-fileroller](https://www.archlinux.org/packages/?name=nemo-fileroller)

*   **RabbitVCS Nemo** — دمج RabbitVCS مع نيمو.

	[http://www.rabbitvcs.org](http://www.rabbitvcs.org) || [rabbitvcs-nemo](https://aur.archlinux.org/packages/rabbitvcs-nemo/)

*   **Python2 Nemo** — ارتباطات Python لواجهة برمجة إضافات نيمو.

	[https://github.com/linuxmint/nemo-extensions/tree/master/nemo-python](https://github.com/linuxmint/nemo-extensions/tree/master/nemo-python) || [python2-nemo](https://aur.archlinux.org/packages/python2-nemo/)

## إجراءات نيمو

تُمَكن المستخدم من إضافة عناصر جديدة إلى قائمة نيمو. الملف الموجود في `/usr/share/nemo/actions/sample.nemo_action` يحتوي على أمثلة على إجراءات نيمو. الأماكن التي توضع فيها ملفات الإجراءات المعدلة:

*   `$HOME/.local/share/nemo/actions/`
*   `/usr/share/nemo/actions/`

انتبه إلى نهاية اسم الملف الذي تريد إضافته، يجب أن يحافظ على النهاية `.nemo_action`.

### Clam Scan

 `$HOME/.local/share/nemo/actions/clamscan.nemo_action` 
```
[Nemo Action]
Name=Clam Scan
Comment=Clam Scan

Exec=gnome-terminal -x sh -c "clamscan -r %F | less"

Icon-Name=bug-buddy

Selection=Any

Extensions=dir;exe;dll;zip;gz;7z;rar;
```

### نقل الملفات

ترجمة للكود:

 `$HOME/.local/share/nemo/actions/archive.nemo_action` 
```
[Nemo Action]
Active=true

#الاسم الذي سيعرض في القائمة، تحديد المكان مدعوم من قبل مواصفات سطح المكتب القياسي
#استعمل %N كمعطى (اختياري) لعرض اسم الملف في التصنيف
#إذا تم اختيار عدة أسماء فسيتم اختيار الاسم الأول بطريقة اعتباطية
#استعمال المعطيات سيكون غير فعال في حالة اختيار عدة أسماء أو في حالة اختيار Any بدون تعيين أو في حالة عدم اختيار أي اسم None(سيتم التعامل معها حرفياً)
# **** مطلوب ****

Name=Archive %N

#عندما يكون تحديد المكان مدعوم (سيظهر في شريط الحالة)
# بإمكانك استعمال %N في حقل الاسم، وبنفس الشروط السابقة المطبقة على %N

Comment=Archiving %N will add .archive to the object.

#الذي تريد تنفيذه ضعه داخل < > لكي يبقى داخل مجلد الإجراءات
#استعمل %U كمعطى عندما تريد إدراج قائمة روابط، واستعمل %F لإدراج قائمة ملفات
# **** مطلوب ****
#

Exec=<archive.py %F>

#لتحديد الفئة: [S]ingle أو [M]ultiple أو Any أو None، (نقرة في الخلفية)
#القيمة الافتراضية ستكون وحيد Single في حال تم ترك الحقل فارغاً

Selection=S

#الإضافات التي سيتم عرضها - عبارة عن مصفوفة أو جدول يوضع في نهايته فاصلة منقوطة ;
#استعمل "dir" لاختيار دليل أو مسار و "none" لعدم اختيار إضافة
# استعمل "any" لوحدها منتهية بفاصلة منقوطة لاختيار أي ملف
#الإضافات غير حساسة لحالة الأحرف، jpg تطابق JPG أو jPg أو jpg ... إلخ
# **** مطلوب ****

Extensions=any;
```

الكود الأصلي:

 `$HOME/.local/share/nemo/actions/archive.nemo_action` 
```
[Nemo Action]
Active=true

# The name to show in the menu, locale supported with standard desktop spec.
# Use %N as an (optional) token to display the simple filename in the label.
# If multiple are selected, then the arbitrary first selected name will be used.
# Token is inactive for selection type of Multiple, None and Any (it will be treated literally)
# **** REQUIRED ****

Name=Archive %N

# Tool tip, locale supported (Appears in the status bar)
# %N can be used as with the Name field, same rules apply

Comment=Archiving %N will add .archive to the object.

# What to run.  Enclose in < > to run an executable that resides in the actions folder.
# Use %U as a token where to insert a URL list, use %F as a token to insert a file list
# **** REQUIRED ****
#Exec=gedit %F

Exec=<archive.py %F>

# What type selection: [S]ingle, [M]ultiple, Any, or None (background click)
# Defaults to Single if this field is missing

Selection=S

# What extensions to display on - this is an array, end with a semicolon
# Use "dir" for directory selection and "none" for no extension
# Use "any" by itself, semi-colon-terminated, for any file type
# Extensions are NOT case sensitive.  jpg will match JPG, jPg, jpg, etc..
# **** REQUIRED ****

Extensions=any;
```
 `$HOME/.local/share/nemo/actions/archive.py` 
```
#! /usr/bin/python2 -OOt

import sys
import os
import shutil

filename = sys.argv[0]
print "Running " + filename
print "With the following arguments:"
for arg in sys.argv:
    if filename == arg:
        continue
    else:
        print arg
        #os.rename('%s','%s.archive') % (arg,arg)
        shutil.move(arg, arg+".archive")
```