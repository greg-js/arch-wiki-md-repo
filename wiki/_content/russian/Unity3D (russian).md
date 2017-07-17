**Состояние перевода:** На этой странице представлен перевод статьи [Unity3D](/index.php/Unity3D "Unity3D"). Дата последней синхронизации: 13 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Unity3D&diff=0&oldid=481838).

Из [Unity - игровой движок, инструменты и многоплатформенность](https://unity3d.com/unity):

	*Редактор Unity — это общее место для творчества художников, дизайнеров, разработчиков и многих других. Редактор доступен для Windows, Mac, Linux; в него входят инструменты для создания 2D- и 3D-сцен, режим мгновенного тестирования для ускорения работы и проверки версий, а также мощная система анимации.*

Не путать с Canonical's [Unity](/index.php/Unity "Unity").

**Примечание:** Редактор для Linux в настоящее время является экспериментальным. Пожалуйста, сообщайте обо всех ошибках на [форуме Unity](http://forum.unity3d.com/forums/linux-editor-support-feedback-experimental.93/)!

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Android Remote](#Android_Remote)
    *   [2.1 Подготовка компьютера](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BC.D0.BF.D1.8C.D1.8E.D1.82.D0.B5.D1.80.D0.B0)
        *   [2.1.1 Установка пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.1.2 Настройка редактора](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.80.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.BE.D1.80.D0.B0)
    *   [2.2 Подготовка Android](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_Android)
    *   [2.3 Проверка](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0)
*   [3 Исправление проблем](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Unity падает при первом запуске до/при входа(е) в систему](#Unity_.D0.BF.D0.B0.D0.B4.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.BF.D0.B5.D1.80.D0.B2.D0.BE.D0.BC_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B5_.D0.B4.D0.BE.2F.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0.28.D0.B5.29_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [3.2 Unity падает при попытке загрузить проект](#Unity_.D0.BF.D0.B0.D0.B4.D0.B0.D0.B5.D1.82_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BF.D1.8B.D1.82.D0.BA.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.B8.D1.82.D1.8C_.D0.BF.D1.80.D0.BE.D0.B5.D0.BA.D1.82)
    *   [3.3 Unity падает, если отсутствует ~/.config/user-dirs.dirs](#Unity_.D0.BF.D0.B0.D0.B4.D0.B0.D0.B5.D1.82.2C_.D0.B5.D1.81.D0.BB.D0.B8_.D0.BE.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.7E.2F.config.2Fuser-dirs.dirs)

## Установка

**Важно:** Пакет Unity - **огромный**. Для успешной установки вам понадобится около 8 ГБ свободного места для сборки пакета и еще 3.5 ГБ для его установки.

Просто установите [AUR](/index.php/AUR "AUR") пакет [unity-editor](https://aur.archlinux.org/packages/unity-editor/) или [unity-editor-beta](https://aur.archlinux.org/packages/unity-editor-beta/) для бета-версии.

## Android Remote

[Unity Remote](http://docs.unity3d.com/Manual/UnityRemote5.html) - приложение для Android, которое позволяет получить хорошее представление о том, как ваша игра действительно выглядит и обрабатывается на целевом Android устройстве. Это достигается благодаря отправки визуального вывода из редактора на экран устройства, а при этом входные данные с устройства отправляются обратно в запущенный проект в Unity.

### Подготовка компьютера

#### Установка пакетов

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [android-udev](https://www.archlinux.org/packages/?name=android-udev), который обеспечит правильные правила [udev](/index.php/Udev_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Udev (Русский)") для вашего устройства.

Установите пакет [android-sdk](https://aur.archlinux.org/packages/android-sdk/) и один из пакетов из группы [java-environment](https://www.archlinux.org/packages/?name=java-environment), предпочтительно JDK7, хотя сообщается, что он должен работать с OpenJDK тоже.

#### Настройка редактора

Откройте редактор, перейдите к *Edit -> Preferences* и установите правильные пути к Android SDK и JDK.

**Совет:**

*   Android SDK обычно находится в `/opt/android-sdk`.
*   Местоположение JDK зависит от используемой вами версии, если вы хотите использовать значение установленное по умолчанию, тогда смотрите его в `/usr/lib/jvm/default`.

Перейдите в *Edit -> Project Settings -> Editor* и установите `Unity Remote Device` на `любое устройство Android`.

Дополнительную информацию можно найти в [документации Unity](http://docs.unity3d.com/Manual/android-sdksetup.html).

### Подготовка Android

Установите [Unity Remote 5](https://play.google.com/store/apps/details?id=com.unity3d.genericremote) из Play Маркета. Также вы можете загрузить и собрать его самостоятельно из Asset Store.

Также [рекомендуется](http://www.howtogeek.com/192732/android-usb-connections-explained-mtp-ptp-and-usb-mass-storage/)[[1]](http://last24.info/read/2014/10/31/7/8174) установить Android-устройство в режим PTP.

**Примечание:** Не забудьте включить “USB-отладку” на вашем устройстве. Перейдите в раздел *Настройки -> Для разработчиков*, затем включите USB-отладку. Начиная с Android Jelly Bean 4.2 раздел "Для разработчиков" скрыт по умолчанию. Чтобы показать его, нажмите *Найстройки -> Об устройстве -> Номер сборки* несколько раз. Затем вы сможете получить доступ к параметрам *Настройки -> Для разработчиков*.

Для получения дополнительной информации смотрите [документацию Unity](http://docs.unity3d.com/Manual/UnityRemote5.html).

### Проверка

Если у вас открыт Unity, закройте его.

Подключите телефон к компьютеру и запустите Unity Remote.

Откройте редактор и нажмите кнопку воспроизведения. Теперь вы должны увидеть, как ваша игра передается на ваше Android-устройство.

Если он не работает или у вас есть вопросы, смотрите [документацию Unity](http://docs.unity3d.com/Manual/UnityRemote5.html).

## Исправление проблем

### Unity падает при первом запуске до/при входа(е) в систему

Это редкая ошибка, когда конфигурация Unity создается неправильно. Вы можете попробовать выполнить сброс:

 `$ rm -rf ~/.config/unity3d/{*.prefs,*.log,Preferences} ` 

### Unity падает при попытке загрузить проект

Пользователи [сообщают](http://forum.unity3d.com/threads/unity-on-arch-manjaro-linux.350315/page-3#post-2271637), что отключение `GTK_IM_MODULE` предотвращает сбой.

### Unity падает, если отсутствует ~/.config/user-dirs.dirs

Посмотрите, как сгенерировать файлы xdg здесь: [Каталоги пользователей XDG](/index.php/XDG_user_directories "XDG user directories")