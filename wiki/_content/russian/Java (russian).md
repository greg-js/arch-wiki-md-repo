Ссылки по теме

*   [Java package guidelines](/index.php/Java_package_guidelines "Java package guidelines")

Из [Википедии](https://en.wikipedia.org/wiki/ru:Java "wikipedia:ru:Java"):

"*Java — объектно-ориентированный язык программирования, разработанный компанией Sun Microsystems (в последующем приобретенной компанией Oracle). Приложения Java обычно транслируются в специальный байт-код, поэтому они могут работать на любой виртуальной Java-машине вне зависимости от компьютерной архитектуры. Дата официального выпуска — 23 мая 1995 года.*"

Arch Linux официально поддерживает открытую реализацию [OpenJDK](http://openjdk.java.net/) версий 7 и 8\. Эти версии могут быть без проблем установлены одновременно, при этом переключение между ними производится с помощью специального скрипта `archlinux-java`. Несколько других реализаций доступны в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"), но они не поддерживаются официально.

## Contents

*   [1 Установка](#Установка)
    *   [1.1 Устаревание пакетов](#Устаревание_пакетов)
*   [2 Переключение между средами](#Переключение_между_средами)
    *   [2.1 Получение списка установленных совместимых сред Java](#Получение_списка_установленных_совместимых_сред_Java)
    *   [2.2 Установка среды Java по умолчанию](#Установка_среды_Java_по_умолчанию)
    *   [2.3 Сброс настроек среды Java по умолчанию](#Сброс_настроек_среды_Java_по_умолчанию)
    *   [2.4 Исправление настроек среды Java по умолчанию](#Исправление_настроек_среды_Java_по_умолчанию)
    *   [2.5 Запуск приложения с другой версией Java](#Запуск_приложения_с_другой_версией_Java)
*   [3 Требования к пакетам сред для поддержки archlinux-java](#Требования_к_пакетам_сред_для_поддержки_archlinux-java)
*   [4 Неподдерживаемые среды Java из AUR](#Неподдерживаемые_среды_Java_из_AUR)
    *   [4.1 Java SE](#Java_SE)
        *   [4.1.1 Java SE 6/7](#Java_SE_6/7)
    *   [4.2 Oracle JRockit](#Oracle_JRockit)
    *   [4.3 VMkit](#VMkit)
    *   [4.4 Parrot VM](#Parrot_VM)
*   [5 Решение проблем](#Решение_проблем)
    *   [5.1 MySQL](#MySQL)
    *   [5.2 Маскировка под другой оконный менеджер](#Маскировка_под_другой_оконный_менеджер)
    *   [5.3 Шрифты отображаются размыто](#Шрифты_отображаются_размыто)
    *   [5.4 В некоторых приложениях отсутствует текст](#В_некоторых_приложениях_отсутствует_текст)
    *   [5.5 Приложения не изменяют размер с WM, меню сразу закрывается](#Приложения_не_изменяют_размер_с_WM,_меню_сразу_закрывается)
*   [6 Советы и рекомендации](#Советы_и_рекомендации)
    *   [6.1 Улучшенное отображение шрифтов](#Улучшенное_отображение_шрифтов)
    *   [6.2 Оформление GTK](#Оформление_GTK)
    *   [6.3 Не-репарентинговые оконные менеджеры](#Не-репарентинговые_оконные_менеджеры)

## Установка

Следующие пакеты доступны в официальных репозиториях:

*   OpenJDK 7:

| Пакет | Примечание |
| [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) | Исполняющая среда (*JRE*) без графических инструментов – версия 7 |
| [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) | Полная версия исполняющей среды (*JRE*) – версия 7 |
| [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) | Пакет разработки (*JDK*) – версия 7 |
| [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) | Документация OpenJDK (javadoc) – версия 7 |
| [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src) | Исходные коды OpenJDK – версия 7 |

*   OpenJDK 8:

| Пакет | Примечание |
| [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) | Исполняющая среда (*JRE*) без графических инструментов – версия 8 |
| [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) | Полная версия исполняющей среды (*JRE*) – версия 8 |
| [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) | Пакет разработки (*JDK*) – версия 8 |
| [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) | Документация OpenJDK (javadoc) – версия 8 |
| [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src) | Исходные коды OpenJDK – версия 8 |

*   OpenJDK 9:

| Пакет | Примечание |
| [jre9-openjdk-headless](https://www.archlinux.org/packages/?name=jre9-openjdk-headless) | Исполняющая среда (*JRE*) без графических инструментов – версия 9 |
| [jre9-openjdk](https://www.archlinux.org/packages/?name=jre9-openjdk) | Полная версия исполняющей среды (*JRE*) – версия 9 |
| [jdk9-openjdk](https://www.archlinux.org/packages/?name=jdk9-openjdk) | Пакет разработки (*JDK*) – версия 9 |
| [openjdk9-doc](https://www.archlinux.org/packages/?name=openjdk9-doc) | Документация OpenJDK (javadoc) – версия 9 |
| [openjdk9-src](https://www.archlinux.org/packages/?name=openjdk9-src) | Исходные коды OpenJDK – версия 9 |

**Примечание:** JDK имеет зависимость от JRE, поэтому при установке JDK будет также установлена JRE.

**Примечание:** После установки вам может понадобиться обновить переменную окружения `$PATH`. Для этого отредактируйте файл `/etc/profile` или перезайдите в среду рабочего стола.

Общие для всех Java-пакетов пакеты [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) и [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) автоматически устанавливаются как зависимости и предоставляют файл настройки окружения `/etc/profile.d/jre.sh`. Этот файл содержит все переменные окружения, необходимые для работы Java-среды. Пакет [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) также предоставляет скрипт `archlinux-java`, который служит для установки Java-среды по умолчанию. Этот скрипт создает символические ссылки `/usr/lib/jvm/default` и `/usr/lib/jvm/default-runtime`, которые определяют текущую версию Java и текущую исполняемую среду (JVM) в `/usr/lib/jvm/java-${*мажорная_версия*}-${*имя_поставщика*`}. Для большинства исполняемых файлов среды Java создаются прямые ссылки в `/usr/bin`, остальные файлы доступны в `$PATH`.

**Важно:** Файл `/etc/profile.d/jdk.sh` больше не предоставляется ни одним из пакетов.

#### Устаревание пакетов

Хотя пакеты в Arch Linux могут иметь проприетарные версии пакетов в качестве зависимостей, открытая реализация имеет свою систему версий:

*   Пакеты [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk), [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) и [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) должны помечаться как устаревшие в зависимости от [версии *IcedTea*](http://icedtea.wildebeest.org/download/source) (например, `2.4.3`), а не их версии реализации от Oracle (например `u45` в выпуске `7.u45_2.4.3-1`).
*   Пакет [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web) должен помечаться как устаревший в зависимости от [версии *IcedTea Web*](http://icedtea.wildebeest.org/download/source) (например, `1.4.1`), и независимо от версии *IcedTea*.

## Переключение между средами

Для переключения между средами Java используется скрипт `archlinux-java`, который предоставляет следующие возможности:

```
archlinux-java *<COMMAND>*

COMMAND:
   status              Вывести список установленных сред Java
   get                 Вывести короткое имя среды Java, установленной по умолчанию
   set *имя_среды*   Установить среду *имя_среды* в качестве среды по умолчанию
   unset               Сбросить текущую установку среды Java по умолчанию
   fix                 Исправить нарушенную конфигурацию среды Java по умолчанию

```

### Получение списка установленных совместимых сред Java

```
$ archlinux-java status

```

Пример:

```
$ archlinux-java status
Available Java environments:
  java-7-openjdk (default)
  java-8-openjdk/jre

```

Обратите внимание на слово *(default)*, которым помечается текущая выбранная среда Java, в данном примере — `java-7-openjdk`. Запуск конкретного файла `java` и других исполняемых файлов среды зависит от этой настройки. Также обратите внимание, что в приведенном примере установлена только исполняющая среда (*JRE*) из состава OpenJDK 8.

### Установка среды Java по умолчанию

```
# archlinux-java set *имя_среды*

```

Пример:

```
# archlinux-java set java-8-openjdk/jre

```

**Совет:** Используйте команду `archlinux-java status` для отображения списка всех доступных сред Java.

Обратите внимание, что, если имя указано с ошибкой, скрипт не выполнит никаких действий. В примере из предыдущего раздела, установлен пакет [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), но не [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk), поэтому имя среды `java-8-openjdk` в данном случае неверно:

```
# archlinux-java set java-8-openjdk
'/usr/lib/jvm/java-8-openjdk' is not a valid Java environment path

```

### Сброс настроек среды Java по умолчанию

Обычно, нет необходимости сбрасывать установку среды Java по умолчанию. Если вы все-таки хотите это сделать, используйте команду `unset`, чтобы никакая среда более не использовалась:

```
# archlinux-java unset

```

### Исправление настроек среды Java по умолчанию

Если в качестве среды по умолчанию установлена некорректная среда Java, команда `archlinux-java fix` попробует это исправить. Обратите внимание, что если не была задана среда Java по умолчанию, команда попытается установить одну из доступных. Официально поддерживаемые пакеты "OpenJDK 7" и "OpenJDK 8" имеют при этом больший приоритет (в таком порядке), чем неофициальные версии из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

```
# archlinux-java fix

```

### Запуск приложения с другой версией Java

Если вы хотите запускать отдельное приложение с какой-нибудь другой установленной версией Java, не обязательно каждый раз перед этим устанавливать ее в качестве среды по умолчанию: вы можете использовать простой скрипт, который настроит окружение специально для запуска вашего приложения. Например, если по умолчанию используется jre7, а вы хотите использовать jre8:

```
#!/bin/sh

export PATH=/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH
exec */path/to/application*

```

## Требования к пакетам сред для поддержки `archlinux-java`

Этот раздел предназначается для тех, кто осуществляет сборку пакетов с альтернативными выпусками JVM для [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Чтобы пакет соответствовал принятой в Arch Linux схеме с использованием скрипта `archlinux-java`, он должен:

*   Помещать все файлы в `/usr/lib/jvm/java-${*номер_мажорной_версии*}-${*имя_поставщика*}` .
*   Убедиться, что все исполняемые файлы для которых пакетами [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) и [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/) создаются ссылки присутствуют собираемом пакете.
*   Предоставлять ссылки из `/usr/bin` к исполняемым файлам только если файлы ссылок не принадлежат пакетам [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) и [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/).
*   Имена man-страниц должны оканчиваться на `-${*номер мажорной версии*}-${*имя поставщика*`} для избежания конфликтов (пример смотрите в [списке файлов jre8-openjdk](https://www.archlinux.org/packages/extra/x86_64/jre8-openjdk/files/), где имена man-страниц оканчиваются на `-openjdk8`).
*   Не объявлять пакеты других сред Java, `java-runtime`, `java-runtime-headless` или `java-environment` как [конфликтующие](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#conflicts "PKGBUILD (Русский)"), а также в качестве [замещаемых](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#replaces "PKGBUILD (Русский)").
*   Использовать `archlinux-java` в целях установки, чтобы установить среду Java по умолчанию **если в данный момент уже не установлена подходящая среда** (то есть, пакеты не должны принудительно устанавливать какую-либо среду Java по умолчанию). Используйте [исходные коды официально поддерживаемого пакета исполняемой среды Java](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/java7-openjdk) в качестве примера.

Также, пожалуйста, имейте в виду, что:

*   Пакеты, которым нужна любая среда Java должны объявлять о зависимости к пакету `java-runtime`, `java-runtime-headless` или `java-environment`, как обычно.
*   Пакеты, которым нужна конкретная среда Java должны объявить о зависимости к соответствующему пакету.
*   Пакеты OpenJDK теперь объявляют о предоставлении функции `provides="java-runtime-openjdk=${pkgver}"`. Это позволяет сторонним пакетам объявлять о зависимости от OpenJDK без указания конкретной версии.

## Неподдерживаемые среды Java из AUR

**Важно:** Пакеты в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") могут не поддерживать `archlinux-java`.

### Java SE

Несколько пакетов в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") предоставляют реализации JDK и JRE от Oracle, из них основными являются [jre](https://aur.archlinux.org/packages/jre/) и [jdk](https://aur.archlinux.org/packages/jdk/).

#### Java SE 6/7

Предыдущие версии JRE и JDK доступны с пакетами [jre6](https://aur.archlinux.org/packages/jre6/)/[jre7](https://aur.archlinux.org/packages/jre7/) и [jdk6](https://aur.archlinux.org/packages/jdk6/)/[jdk7](https://aur.archlinux.org/packages/jdk7/) соответственно.

### Oracle JRockit

[JRockit](http://www.oracle.com/technetwork/middleware/jrockit/overview/index.html) — проприетарная реализация JVM с JIT от Oracle. Установку можно произвести через пакет [jrockit](https://aur.archlinux.org/packages/jrockit/).

### VMkit

[VMkit](http://vmkit.llvm.org/index.html) — основанный на LLVM фреймворк для виртуальных машин с JIT. В состав VMkit входит собственная JVM — J3\. J3 использует реализацию стандартной библиотеки Java GNU Classpath, но также может работать с реализациями от Apache.

### Parrot VM

[Parrot](http://www.parrot.org/) является виртуальной машиной, предоставляющей экспериментальную [поддержку Java](http://trac.parrot.org/parrot/wiki/Languages), которая реализуется двумя способами: либо посредством [транслятора байт-кода](http://code.google.com/p/parrot-jvm/), либо с помощью [компилятора Java с поддержкой формата Parrot](https://github.com/chrisdolan/perk). Пакет [parrot](https://aur.archlinux.org/packages/parrot/) доступен в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), а [parrot-git](https://aur.archlinux.org/packages/parrot-git/) — в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

## Решение проблем

### MySQL

По причине того факта, что JDBC-драйверы часто используют порт из URL для установки соединения с базой данных, это соединение считается удаленным (другими словами, MySQL не слушает на порту в соответствии с настройками по умолчанию), несмотря на то, что оно может быть на том же хосте. Таким образом, чтобы использовать JDBC и MySQL вам следует включить удаленный доступ к MySQL, следуя инструкциям на странице [MySQL#Grant remote access](/index.php/MySQL#Grant_remote_access "MySQL").

### Маскировка под другой оконный менеджер

Вы можете использовать [wmname](https://www.archlinux.org/packages/?name=wmname) [отсюда](http://tools.suckless.org/wmname) чтобы заставить JVM поверить, что используется какой-то другой оконный менеджер. Это должно решить проблемы с отображением графических приложений на Java, которые появляются в менеджерах вроде [Awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)") или [dwm](/index.php/Dwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dwm (Русский)").

```
$ wmname LG3D

```

После выполнения команды перезапустите Java-приложение.

Это работает, потому что в JVM содержится закодированный список не-репарентинговых оконных менеджеров. Что интересно, некоторые пользователи предпочитают маскировать свои менеджеры под `LG3D`, написанный [Sun, на Java](https://en.wikipedia.org/wiki/Project_Looking_Glass "wikipedia:Project Looking Glass"), однако также являющийся не-репарентинговым.

### Шрифты отображаются размыто

Даже после выполнения всех рекомендаций в разделе [#Улучшенное отображение шрифтов](#Улучшенное_отображение_шрифтов) некоторые шрифты все еще могут отображаться размыто. Если это так, попробуйте установить шрифты от Microsoft. Установите [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

### В некоторых приложениях отсутствует текст

Если в приложении совсем не отображаются никакие надписи, посмотрите советы в разделе [#Советы и рекомендации](#Советы_и_рекомендации), как предлагается в [FS#40871](https://bugs.archlinux.org/task/40871).

### Приложения не изменяют размер с WM, меню сразу закрывается

The standard Java GUI toolkit has a hard-coded list of "non-reparenting" window managers. If using one that is not on that list, there can be some problems with running some Java applications. One of the most common problems is "gray blobs", when the Java application renders as a plain gray box instead of rendering the GUI. Another one might be menus responding to your click, but closing immediately.

There are several things that may help:

*   For [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) or [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), append the line `export _JAVA_AWT_WM_NONREPARENTING=1` in `/etc/profile.d/jre.sh`. Then, source the file `/etc/profile.d/jre.sh` or log out and log back in.
*   For Oracle's JRE/JDK, use [SetWMName.](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-SetWMName.html) However, its effect may be canceled when also using `XMonad.Hooks.EwmhDesktops`. In this case, appending

```
 >> setWMName "LG3D"

```

to the `LogHook` may help.

See [[1]](http://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console) for more information.

## Советы и рекомендации

**Примечание:** Советы в этом разделе подходят всем приложениям, использующим внешнюю среду Java, установленную отдельно. Некоторые приложения поставляются со встроенной сборкой Java, либо используют нестандартные способы работы с графическим интерфейсом, отрисовки шрифтов и т. д. Поэтому, нет гарантий, что эти советы на самом деле сработают.

Поведением большинства приложений Java можно управлять, передавая переменные в исполняемую среду Java. Как предлагают [на форуме](https://bbs.archlinux.org/viewtopic.php?id=72892), сделать это можно добавлением указанной строки в ваш файл `~/.bashrc` (или `/etc/profile.d/jre.sh` для программ, при запуске которых среда не инициализируется из `~/.bashrc`, например, если программа запускается из Applications view в Gnome):

```
export _JAVA_OPTIONS="-D**<option 1>** -D**<option 2>**..."

```

Например, чтобы включить сглаживание шрифтов и оформление GTK по умолчанию:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'

```

### Улучшенное отображение шрифтов

Обе реализации Java, открытая и закрытая, имеют недостатки в реализации сглаживания шрифтов. Это может быть исправлено указанием следующих параметров:

`awt.useSystemAAFontSettings=on`, `swing.aatext=true`

Смотрите также [Шрифты в исполняемой среде Java](/index.php/Java_Runtime_Environment_fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Java Runtime Environment fonts (Русский)") для получения подробной информации.

### Оформление GTK

Если ваши Java-приложения выглядят отвратительно, вам, вероятно, сможет помочь смена оформления по умолчанию на тему GTK для компонентов Swing: `swing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

Некоторые упрямые приложения требуют использования кроссплатформенного оформления. В некоторых таких случаях, вам удастся заставить эти приложения использовать оформление GTK, установив следующий параметр:

`swing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

### Не-репарентинговые оконные менеджеры

Для не-репарентинговых оконных менеджеров следует установить следующую переменную окружения в файле `.xinitrc`:

```
export _JAVA_AWT_WM_NONREPARENTING=1

```