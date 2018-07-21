Ссылки по теме

*   [Unreal Tournament 4 (Русский)](/index.php/Unreal_Tournament_4_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Unreal Tournament 4 (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Unreal Engine 4](/index.php/Unreal_Engine_4 "Unreal Engine 4"). Дата последней синхронизации: 24 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Unreal_Engine_4&diff=0&oldid=482795).

Unreal Engine 4 - последняя версия движка для видеоигр, созданная Epic Games

Содержимое этой статьи было первоначально написано на [этой странице](https://wiki.unrealengine.com/Building_On_Linux) и адаптировано специально для Arch Linux.

## Contents

*   [1 Минимальные требования](#.D0.9C.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.82.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.1 Установка из AUR](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_AUR)
    *   [2.2 Установка из исходного кода](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B8.D0.B7_.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BA.D0.BE.D0.B4.D0.B0)
        *   [2.2.1 Получение](#.D0.9F.D0.BE.D0.BB.D1.83.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
        *   [2.2.2 Компиляция](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F)
*   [3 Исправление проблем](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Проблемы с компиляцией](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BA.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D0.B5.D0.B9)
    *   [3.2 Проблемы во время выполнения](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B2.D0.BE_.D0.B2.D1.80.D0.B5.D0.BC.D1.8F_.D0.B2.D1.8B.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.3 Проблемы с проектом кода на C++](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BF.D1.80.D0.BE.D0.B5.D0.BA.D1.82.D0.BE.D0.BC_.D0.BA.D0.BE.D0.B4.D0.B0_.D0.BD.D0.B0_C.2B.2B)
    *   [3.4 Отключение всплывающих подсказок](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D1.81.D0.BF.D0.BB.D1.8B.D0.B2.D0.B0.D1.8E.D1.89.D0.B8.D1.85_.D0.BF.D0.BE.D0.B4.D1.81.D0.BA.D0.B0.D0.B7.D0.BE.D0.BA)
    *   [3.5 Случайное зависание под KDE](#.D0.A1.D0.BB.D1.83.D1.87.D0.B0.D0.B9.D0.BD.D0.BE.D0.B5_.D0.B7.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B4_KDE)
    *   [3.6 Пустой огромный квадрат в Blueprint](#.D0.9F.D1.83.D1.81.D1.82.D0.BE.D0.B9_.D0.BE.D0.B3.D1.80.D0.BE.D0.BC.D0.BD.D1.8B.D0.B9_.D0.BA.D0.B2.D0.B0.D0.B4.D1.80.D0.B0.D1.82_.D0.B2_Blueprint)
*   [4 Дополнительный контент](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BD.D1.82)
    *   [4.1 Стартовый контент](#.D0.A1.D1.82.D0.B0.D1.80.D1.82.D0.BE.D0.B2.D1.8B.D0.B9_.D0.BA.D0.BE.D0.BD.D1.82.D0.B5.D0.BD.D1.82)
    *   [4.2 Приложения marketplace](#.D0.9F.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_marketplace)

## Минимальные требования

*   Intel или Amd CPU@2.5GHz Quad Core **64 бит**
*   GPU: NVIDIA GeForce GTX 470 или AMD Radeon 6870 HD series
*   RAM: 8 GB

## Установка

### Установка из AUR

Unreal Engine 4 доступен в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)") как пакет [unreal-engine](https://aur.archlinux.org/packages/unreal-engine/).

Пакет весит 22 ГБ после установки, поэтому для сборки требуется около 100 ГБ свободного места. Существует около 7 ГБ исходных файлов для загрузки, а компиляция может занять несколько часов.

Поскольку репозиторий является приватным, вы можете [настроить SSH-ключ](https://help.github.com/articles/generating-an-ssh-key/), чтобы ваша учетная запись GitHub использовалась для загрузки источника.

Так-же рекомендуется увеличить размер папки tmp (исходный размер 7.8), либо сменить каталог сборки.

Для уменьшения размера загрузки, вы можете [скачать релиз как tar.gz](https://github.com/EpicGames/UnrealEngine/releases) после входа в github.com, а затем использовать этот файл в качестве источника в PKGBUILD.

### Установка из исходного кода

#### Получение

Сначала зарегистрируйтесь на [UnrealEngine.com](https://www.unrealengine.com/) и перечислите свою учетную запись GitHub в свою учетную запись Epic Games. После регистрации вы сможете [просмотреть исходный код](https://github.com/EpicGames/UnrealEngine).

#### Компиляция

Для компиляции вручную смотрите [официальные инструкции по сборке на Linux](https://wiki.unrealengine.com/Building_On_Linux#Building).

## Исправление проблем

### Проблемы с компиляцией

Если компиляция не удалась, попробуйте собрать редактор с помощью профиля Debug:

```
$ make UE4Editor-Linux-Debug

```

### Проблемы во время выполнения

Если редактор не запускается из меню, или что-то не работает правильно, запустите его в консоли и проверьте вывод на наличие ошибок.

```
$ cd /opt/unreal-engine/Engine/Binaries/Linux/
$ ./UE4Editor

```

### Проблемы с проектом кода на C++

После создания проекта кода новый проект открывается в текстовом редакторе, а не в UE4Editor, как это должно быть. После повторного запуска редактора новый проект появляется и может быть открыт, но при первом запуске для компиляции требуется около получаса, и поскольку это происходит в фоновом режиме (без GUI), это может показаться недействительным. Использование ЦП должно показывать, что оно все еще компилируется, и вы можете запустить редактор с консоли, чтобы увидеть прогресс.

### Отключение всплывающих подсказок

Наведение указателя мыши на всплывающие подсказки UE4 может оказаться очень медленной процедурой. Их можно отключить, добавив

 `Engine/Config/ConsoleVariables.ini`  `Slate.AllowToolTips=0` 

### Случайное зависание под KDE

Отключите содержимое индексного файла в параметрах поиска файлов KDE.

### Пустой огромный квадрат в Blueprint

Если вы используете мультимониторную конфигурацию и переместили blueprint на второй экран, и при вызове контекстного меню (ПКМ в blueprint) у вас проявляется данный баг, то откройте Edit Preferences -> User interface и поставьте галочку напротив Enable Window Animation и перезапустите UnrealEngine.

## Дополнительный контент

### Стартовый контент

Проект StarterContent установлен в /opt/unreal-engine/Samples/StarterContent/StarterContent.uproject, вы можете перейти к нему с панели запуска.

### Приложения marketplace

Лаунчер с Unreal Marketplace недоступен для Linux еще [[1]](https://forums.unrealengine.com/showthread.php?52166-Unreal-launcher-for-linux), поэтому приложения, такие как проект ContentExamples, не могут быть установлены из Linux[[2]](https://answers.unrealengine.com/questions/301869/download-content-from-marketplace-on-linux.html).

Приложения marketplace можно загрузить с помощью [лаунчера](https://www.unrealengine.com/download) в Windows (в Mac также может работать), они хранятся в:

```
   /Program Files (x86)/Epic Games/Launcher/VaultCache/

```