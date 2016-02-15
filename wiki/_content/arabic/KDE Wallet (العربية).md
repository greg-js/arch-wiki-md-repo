[مدير محفظة كدي](http://utils.kde.org/projects/kwalletmanager/) أداة لإدارة كلمات المرور على نظام كدي لديك. استخدام نظام محفظة كدي الفرعي لا يسمح لك بإبقاء أسرارك فقط بل وأيضًا الوصول إلى كلمات المرور لأيِّ تطبيق يتكامل مع محفظة كدي وإدارتها.

## استخدام محفظة كدي لتخزين مفاتيح ssh

ثبّت Ksshaskpass من مستودع المجتمع:

```
pacman -S ksshaskpass

```

أنشئ الملف:

```
~/.kde4/Autostart/ssh-add.sh

```

أضف المحتويات هذه:

```
#!/bin/sh
ssh-add </dev/null

```

اجعل الملف قابلًا للتنفيذ ونفّذه:

```
chmod +x ~/.kde4/Autostart/ssh-add.sh
~/.kde4/Autostart/ssh-add.sh

```

قد تحتاج أيضًا إلى تنفيذ أمر source على السكرِبت الذي يضبط متغيّر البيئة `SSH_ASKPASS`:

```
. /etc/profile.d/ksshaskpass.sh

```

سيسألك عن كلمة المرور ويزيل فكّ مفاتيح ssh خاصتك.

قد تحتاج إلى الذهاب إلى إعدادات النظام > إدارة النظام > بدء التشغيل والإطفاء > البدء التلقائي > أضف سكربت.

## محفظة كدي لِفَيَرْفُكس

لا توجد إضافة لجعل فَيَرْفُكس يخزّن كلمات المرور في محفظة كدي.

[http://kde-apps.org/content/show.php/Firefox+addon+for+kwallet?content=116886](http://kde-apps.org/content/show.php/Firefox+addon+for+kwallet?content=116886)

## محفظة كدي لِكروميوم

لِكروميوم تكامل مع محفظة كدي مضمّن

لتمكينه عليك تنفيذ كروميوم بإضافة --password-store=kwallet أو --password-store=detect.

يفترض أن يكون الأمر الثاني هو الافتراضي لكنه لا يعمل للكاتب، لذا إن كان لا يعمل معك أيضًا، استدعِ المتصفّح بِـ:

 `chromium --password-store=kwallet`