**Netbeans** هو بيئة تطوير مدمجة IDE تُستخدم لتطوير تطبيقات بلغات Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, وغيرها من لغات البرمجة. برنامج NetBeans تمت كتابته بلغة java لذا فسوف يعمل على أي نظام يمكن تنصيب JVM عليه بما فيه Windows, Mac OS, Linux, و Solaris. حزمة JDK مطلوبة فقط إذا أردت تطوير برمجيات java بواسطة NetBeans لكنها غير مطلوبة في تطروير باقي اللغات.

## Contents

*   [1 تلميحات](#.D8.AA.D9.84.D9.85.D9.8A.D8.AD.D8.A7.D8.AA)
    *   [1.1 إزالة التعرج في خطوط NetBeans](#.D8.A5.D8.B2.D8.A7.D9.84.D8.A9_.D8.A7.D9.84.D8.AA.D8.B9.D8.B1.D8.AC_.D9.81.D9.8A_.D8.AE.D8.B7.D9.88.D8.B7_NetBeans)
        *   [1.1.1 Netbeans فقط](#Netbeans_.D9.81.D9.82.D8.B7)
        *   [1.1.2 Java بشكل عام](#Java_.D8.A8.D8.B4.D9.83.D9.84_.D8.B9.D8.A7.D9.85)
    *   [1.2 GTK look and feel](#GTK_look_and_feel)
*   [2 إستكشاف الأخطاء و إصلاحها](#.D8.A5.D8.B3.D8.AA.D9.83.D8.B4.D8.A7.D9.81_.D8.A7.D9.84.D8.A3.D8.AE.D8.B7.D8.A7.D8.A1_.D9.88_.D8.A5.D8.B5.D9.84.D8.A7.D8.AD.D9.87.D8.A7)
    *   [2.1 OpenJDK vs Sun's JDK](#OpenJDK_vs_Sun.27s_JDK)
    *   [2.2 Glassfish خادم - Can`t download Glassfish server I/O Exception](#Glassfish_.D8.AE.D8.A7.D8.AF.D9.85_-_Can.60t_download_Glassfish_server_I.2FO_Exception)
    *   [2.3 Netbeans لا يبدأ بعد تشغيله لأول مرة](#Netbeans_.D9.84.D8.A7_.D9.8A.D8.A8.D8.AF.D8.A3_.D8.A8.D8.B9.D8.AF_.D8.AA.D8.B4.D8.BA.D9.8A.D9.84.D9.87_.D9.84.D8.A3.D9.88.D9.84_.D9.85.D8.B1.D8.A9)

## تلميحات

**Note:** ملف الإعدادات netbeans.conf العام `/usr/share/netbeans/etc/netbeans.conf` ستتم إعادة ضبطه عند التحديثات. لذا قم بوضع التعديلات في الإعدادت في الملف المحلي الخاص بك `~/.netbeans/<ver>/etc/netbeans.conf` (ربما تحتاج الى إنشاء مجلد etc وملف .conf).

*   الإعدادات في ملف netbeans.conf المحلي ستقوم بأخد محل الإعدادات في الملف العام
*   خيارات التي تُمرر في سطر الأوامر ستقوم بحل محل الإعدادات في ملفي الإعدادات الخاص و العام

### إزالة التعرج في خطوط NetBeans

#### Netbeans فقط

قم بإضافة `-J-Dswing.aatext=TRUE -J-Dawt.useSystemAAFontSettings=on` الى سطر 'netbeans_default_options' في ملف netbeans.conf الخاص بك.

#### Java بشكل عام

قم بمراجعة [Java#Better font rendering](/index.php/Java#Better_font_rendering "Java").

### GTK look and feel

لتغيير Netbeans look and feel الى GTK قم بإضافة `--laf com.sun.java.swing.plaf.gtk.GTKLookAndFeel` الى السطر الخاص بخيارات NetBeans ‘netbeans_default_options’ في ملف `/usr/share/netbeans/etc/netbeans.conf`

## إستكشاف الأخطاء و إصلاحها

### OpenJDK vs Sun's JDK

Netbeans 7.0-1 لا يعمل بشكل دائم مع OpenJDK، بعض المشاكل التي تم التبليغ عنها :

*   البدء - في بعض الحالات لا يقوم NetBeans بالعمل .
*   التنصيب - ملف .sh الذي يأتي مع مُنصب NetBeans يفشل في البدء
*   JavaFX لا تعمل بشكل صحيح (راجع [FS#29843](https://bugs.archlinux.org/task/29843)).

### Glassfish خادم - Can`t download Glassfish server I/O Exception

إذا حاولت إضافة خادم Glassfish جديد، قد لا تتمكن من تحميل الخادم. NetBeans يُعيد الخطأ :

```
I/O Exception: [http://java.net/download/glassgish/3.0.1/release/glassfish-3.0.1-ml.zip](http://java.net/download/glassgish/3.0.1/release/glassfish-3.0.1-ml.zip)

```

الحل هو :

*   تحميل النسخة المفتوحة المصدر من خادم GlassFish من الموقع الرسمي : [http://download.java.net/glassfish/3.0.1/release/glassfish-3.0.1-ml.zip](http://download.java.net/glassfish/3.0.1/release/glassfish-3.0.1-ml.zip)
*   قم بفك ضغط ملف zip في أي مجلد تريد

### Netbeans لا يبدأ بعد تشغيله لأول مرة

إذا حصلت على رسالة كالرسالة التالية عندما تقوم بتشغيل NetBeans من الطرفية :

 `# netbeans -h` 
```
 Exception in thread "main" java.lang.UnsatisfiedLinkError: /usr/lib/jvm/java-6-openjdk/jre/lib/i386/libsplashscreen.so: libgif.so.4: cannot open shared object file: No such file or directory

```

يكون لديك خيارين

*   يمكنك بدء NetBeans مُستخدمًا الخيار -nosplash :

```
# netbeans --nosplash

```

*   أو قم بتنصيب الحزمة الناقصة ([libungif](https://www.archlinux.org/packages/?name=libungif)), ومن ثم سيعمل NetBeans كالمعتاد.