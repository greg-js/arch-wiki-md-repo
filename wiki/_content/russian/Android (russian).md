В этой статье я постараюсь описать установку android-sdk под arch linux, включая особенности x64 систем.

## Contents

*   [1 Подготовка.](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0.)
*   [2 Установка android-sdk](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_android-sdk)
    *   [2.1 Установка через yaourt.](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_yaourt.)
        *   [2.1.1 Настройка Netbeans](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Netbeans)
    *   [2.2 Установка через Eclipse](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.87.D0.B5.D1.80.D0.B5.D0.B7_Eclipse)
*   [3 Прописать PATH](#.D0.9F.D1.80.D0.BE.D0.BF.D0.B8.D1.81.D0.B0.D1.82.D1.8C_PATH)

## Подготовка.

Для работы нам понадобится [yaourt](/index.php/Yaourt "Yaourt")

Также проследите, что бы в /etc/pacman.conf были сняты комментарии с следующих строк:

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Желательно обновить систему:

```
yaourt -Syu

```

ну или хотя бы синхронизировать репозитории

```
yaourt -Sy

```

## Установка android-sdk

Тут есть три пути:

*   установить через систему управления пакетами arch linux yaourt.
*   установить через Eclipse.
*   поставить вручную.

Последний вариант рассматривать не буду.

**Примечание:** android-sdk существует только в варианте x86, в принципе это не проблема для x64, нужно только установить 32-х разрядные версии библиотек. Обратите на это внимание если выберите второй или третий вариант установки, иначе все установится, но работать не будет.

### Установка через yaourt.

```
# yaourt -S android-sdk

```

Преимуществом данного метода является то, что yaourt сам проследит и доставит все необходимые зависимости и про библиотеки можно не беспокоиться.

Если ставили из под root, могут возникнуть трудности с доступом к папкам sdk, для устранения:

```
# chown -Rv <имя вашего пользователя> /opt/android-sdk

```

**Примечание:** На данный момент установлены только базовые компоненты android-sdk, о чем сказано в /opt/android-sdk/SDK Readme.txt

Для установки всех компонентов:

```
# cd /opt/android-sdk
#./tools/android

```

#### Настройка Netbeans

Если вы пользуетесь IDE Netbeans, загрузите [nbandroid](http://www.nbandroid.org):

```
Tools -> Plugins -> Settings

```

Добавьте URL: [http://nbandroid.org/release72/updates/updates.xml](http://nbandroid.org/release72/updates/updates.xml)

Затем перейдите в **Available Plugins** и установите плагины **Android** и **Android Test Runner** для вашей версии IDE. После установки перейдите:

```
Tools -> Options -> Miscellaneous -> Android

```

и выберите путь Android SDK (обычно /opt/android-sdk). Доустановить необходимые пакеты и создать AVD можно в:

```
Tools -> Android SDK and AVD manager

```

Готово!

### Установка через Eclipse

Установка Eclipse:

```
#pacman -S eclipse

```

Устанавливаем все необходимые библиотеки:

```
# yaourt  -S lib32-alsa-lib lib32-openal lib32-libstdc++5 lib32-libxv lib32-ncurses lib32-sdl lib32-zlib swt

```

Этот пункт не пройдет если вы не убрали комментарий с [multilib] в /etc/pacman.conf

Запускаем Eclipse.

```
# eclipse

```

Далее идем в

**Help => Install New Software => Add**

**Name: Indigo**

**Location: [http://download.eclipse.org/releases/indigo/](http://download.eclipse.org/releases/indigo/)**

Немного подождем, затем в последней категории:

**Web, XML, Java EE and OSGi Enterprise Development**

выбираем последний пункт

**WST Server Adapters**

Ну и устанавливаем выбранный компонент.

Теперь опять идем в

**Help => Install New Software => Add**

**Name: ADT plugin**

**Location: [https://dl-ssl.google.com/android/eclipse/](https://dl-ssl.google.com/android/eclipse/)**

**Select All**

и заканчиваем установку.

На панели Eclipse запускаем "Opens the Android SDK Manager" устанавливаем Tools и нужную нам версию платформы android.

## Прописать PATH

В не зависимости от того каким путем Вы установили android-sdk, желательно прописать PATH в .bashrc или .bash_profile В моем случае это:

```
PATH=$PATH:/home/anton/android/android-sdk/tools:/home/anton/android/android-sdk/platform-tools

```

Вот и все, приятной работы!