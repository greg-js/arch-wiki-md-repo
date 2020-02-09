Ссылки по теме

*   [Java Package Guidelines](/index.php/Java_Package_Guidelines "Java Package Guidelines")
*   [Шрифты окружения Java Runtime](/index.php/%D0%A8%D1%80%D0%B8%D1%84%D1%82%D1%8B_%D0%BE%D0%BA%D1%80%D1%83%D0%B6%D0%B5%D0%BD%D0%B8%D1%8F_Java_Runtime "Шрифты окружения Java Runtime")

Из [Википедии](https://en.wikipedia.org/wiki/ru:Java "wikipedia:ru:Java"):

	Java — строго типизированный объектно-ориентированный язык программирования, разработанный компанией Sun Microsystems (в последующем приобретённой компанией Oracle). Разработка ведётся сообществом, организованным через Java Community Process, язык и основные реализующие его технологии распространяются по лицензии GPL. Права на торговую марку принадлежат корпорации Oracle.

Arch Linux официально поддерживает [OpenJDK](https://en.wikipedia.org/wiki/ru:OpenJDK "wikipedia:ru:OpenJDK"), свободную реализацию Java SE, версий 7, 8, 10, 11 и 13\. Эти версии можно без проблем установить одновременно, а также переключаться между ними с помощью скрипта `archlinux-java`. Несколько других реализаций доступны в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"), но они не поддерживаются официально.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
    *   [1.1 OpenJDK](#OpenJDK)
    *   [1.2 OpenJFX](#OpenJFX)
    *   [1.3 Другие реализации](#Другие_реализации)
    *   [1.4 Инструменты для разработки](#Инструменты_для_разработки)
        *   [1.4.1 Декомпиляторы](#Декомпиляторы)
*   [2 Переключение между средами](#Переключение_между_средами)
    *   [2.1 Получение списка установленных совместимых сред Java](#Получение_списка_установленных_совместимых_сред_Java)
    *   [2.2 Установка среды Java по умолчанию](#Установка_среды_Java_по_умолчанию)
    *   [2.3 Удаление метки по умолчанию](#Удаление_метки_по_умолчанию)
    *   [2.4 Исправление конфигурации Java](#Исправление_конфигурации_Java)
    *   [2.5 Запуск приложений с окружением не установленным по умолчанию](#Запуск_приложений_с_окружением_не_установленным_по_умолчанию)
*   [3 Требования к пакетам сред для поддержки archlinux-java](#Требования_к_пакетам_сред_для_поддержки_archlinux-java)
*   [4 Решение проблем](#Решение_проблем)
    *   [4.1 Не подключается MySQL](#Не_подключается_MySQL)
    *   [4.2 Не запускается IntelliJ IDEA](#Не_запускается_IntelliJ_IDEA)
    *   [4.3 Ошибки отрисовки приложений Java](#Ошибки_отрисовки_приложений_Java)
    *   [4.4 Неразборчивый шрифт в приложениях Java](#Неразборчивый_шрифт_в_приложениях_Java)
    *   [4.5 В некоторых приложениях отсутствует текст](#В_некоторых_приложениях_отсутствует_текст)
    *   [4.6 Система зависает при дебаггинге](#Система_зависает_при_дебаггинге)
    *   [4.7 Конструктор JavaFX MediaPlayer вылетает с ошибкой](#Конструктор_JavaFX_MediaPlayer_вылетает_с_ошибкой)
    *   [4.8 В приложениях Java не открываются внешние ссылки](#В_приложениях_Java_не_открываются_внешние_ссылки)
    *   [4.9 Ошибка инициализации QuantumRenderer: no suitable pipeline found](#Ошибка_инициализации_QuantumRenderer:_no_suitable_pipeline_found)
*   [5 Советы и рекомендации](#Советы_и_рекомендации)
    *   [5.1 Улучшенное отображение шрифтов](#Улучшенное_отображение_шрифтов)
    *   [5.2 Удаление сообщения Picked up _JAVA_OPTIONS](#Удаление_сообщения_Picked_up_JAVA_OPTIONS)
    *   [5.3 Оформление GTK](#Оформление_GTK)
    *   [5.4 Ускорение отрисовки 2D](#Ускорение_отрисовки_2D)

## Установка

**Примечание:**

*   Официально поддерживается только [OpenJDK](#OpenJDK).
*   После установки окружение Java должно быть определено в переменной `$PATH`, что можно сделать с помощью команды `source` или повторного входа в среду рабочего стола.

Существуют два главных пакета, которые являются зависимыми: [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) (содержит основные файлы для Java Runtime Environment — JRE) и [java-environment-common](https://www.archlinux.org/packages/?name=java-environment-common) (содержит основные файлы для Java Development Kit — JDK). Переменная окружения `$PATH` в файле `/etc/profile.d/jre.sh` указывает на каталог `/usr/lib/jvm/default/bin`, заданный скриптом `archlinux-java`. Ссылки `/usr/lib/jvm/default` и `/usr/lib/jvm/default-runtime` следует менять только при помощи скрипта `archlinux-java`. Эти ссылки ведут на выбранное рабочее окружение Java в `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}` или JRE — `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME}/jre`.

Большинство исполняемых файлов Java находятся в `/usr/bin`, остальные доступны через `$PATH`. Скрипт `/etc/profile.d/jdk.sh` больше не предоставляется ни одним из пакетов.

### OpenJDK

[OpenJDK](https://en.wikipedia.org/wiki/ru:OpenJDK "wikipedia:ru:OpenJDK") — свободная реализация [Java Platform, Standard Edition](https://en.wikipedia.org/wiki/ru:Java_Platform,_Standard_Edition "wikipedia:ru:Java Platform, Standard Edition") (Java SE).

	Headless JRE

	минимальная среда выполнения для Java; не поддерживает GUI.

	Full JRE

	полная среда выполнения, поддерживающая GUI и зависящая от *headless JRE*.

	JDK

	[Java Development Kit](https://en.wikipedia.org/wiki/ru:Java_Development_Kit "wikipedia:ru:Java Development Kit"); необходим для разработки Java-приложений и зависит от *full JRE*.

| Версия | Headless JRE | Full JRE | JDK | Документация | Исходный код |
| [OpenJDK 13](https://openjdk.java.net/projects/jdk/13/) | [jre-openjdk-headless](https://www.archlinux.org/packages/?name=jre-openjdk-headless) | [jre-openjdk](https://www.archlinux.org/packages/?name=jre-openjdk) | [jdk-openjdk](https://www.archlinux.org/packages/?name=jdk-openjdk) | [openjdk-doc](https://www.archlinux.org/packages/?name=openjdk-doc) | [openjdk-src](https://www.archlinux.org/packages/?name=openjdk-src) |
| [OpenJDK 11](https://openjdk.java.net/projects/jdk/11/) | [jre11-openjdk-headless](https://www.archlinux.org/packages/?name=jre11-openjdk-headless) | [jre11-openjdk](https://www.archlinux.org/packages/?name=jre11-openjdk) | [jdk11-openjdk](https://www.archlinux.org/packages/?name=jdk11-openjdk) | [openjdk11-doc](https://www.archlinux.org/packages/?name=openjdk11-doc) | [openjdk11-src](https://www.archlinux.org/packages/?name=openjdk11-src) |
| [OpenJDK 10](https://openjdk.java.net/projects/jdk/10/) | [jre10-openjdk-headless](https://www.archlinux.org/packages/?name=jre10-openjdk-headless) | [jre10-openjdk](https://www.archlinux.org/packages/?name=jre10-openjdk) | [jdk10-openjdk](https://www.archlinux.org/packages/?name=jdk10-openjdk) | [openjdk10-doc](https://www.archlinux.org/packages/?name=openjdk10-doc) | [openjdk10-src](https://www.archlinux.org/packages/?name=openjdk10-src) |
| [OpenJDK 8](https://openjdk.java.net/projects/jdk8/) | [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) | [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) | [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) | [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) | [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src) |
| [OpenJDK 7](https://openjdk.java.net/projects/jdk7/) | [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) | [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) | [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) | [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) | [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src) |

**OpenJDK GA** — свежая сборка OpenJDK General-Availability Release от Oracle.

	[https://jdk.java.net](https://jdk.java.net) || [java-openjdk-bin](https://aur.archlinux.org/packages/java-openjdk-bin/)

**OpenJDK EA** — свежая сборка OpenJDK Early-Access от Oracle.

	[https://jdk.java.net](https://jdk.java.net) || [java-openjdk-ea-bin](https://aur.archlinux.org/packages/java-openjdk-ea-bin/)

**IcedTea-Web** — Java Web Start и устаревший плагин Java для браузеров.

	[https://icedtea.classpath.org/wiki/IcedTea-Web](https://icedtea.classpath.org/wiki/IcedTea-Web) || [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web)

### OpenJFX

[OpenJFX](https://wiki.openjdk.java.net/display/OpenJFX) — свободная реализация [JavaFX](https://en.wikipedia.org/wiki/ru:JavaFX "wikipedia:ru:JavaFX"). Данный пакет включён в Java SE (реализация JRE и JDK от Oracle) и относится лишь к пользователям свободной реализации Java (OpenJDK).

| Версия | Runtime и Developement Kit | Документация | Исходный код |
| [OpenJFX 13](https://wiki.openjdk.java.net/display/OpenJFX/Main) | [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx) | [java-openjfx-doc](https://www.archlinux.org/packages/?name=java-openjfx-doc) | [java-openjfx-src](https://www.archlinux.org/packages/?name=java-openjfx-src) |
| [OpenJFX 11](https://wiki.openjdk.java.net/display/OpenJFX/Main) | [java11-openjfx](https://www.archlinux.org/packages/?name=java11-openjfx) | [java11-openjfx-doc](https://www.archlinux.org/packages/?name=java11-openjfx-doc) | [java11-openjfx-src](https://www.archlinux.org/packages/?name=java11-openjfx-src) |
| [OpenJFX 8](https://wiki.openjdk.java.net/display/OpenJFX/Main) | [java8-openjfx](https://www.archlinux.org/packages/?name=java8-openjfx) | [java8-openjfx-doc](https://www.archlinux.org/packages/?name=java8-openjfx-doc) | [java8-openjfx-src](https://www.archlinux.org/packages/?name=java8-openjfx-src) |

**OpenJFX GA** — свежая сборка OpenJFX General-Availability Release от Gluon.

	[https://openjfx.io/](https://openjfx.io/) || [java-openjfx-bin](https://aur.archlinux.org/packages/java-openjfx-bin/)

**OpenJFX EA** — свежая сборка OpenJFX Early-Access от Gluon.

	[https://openjfx.io/](https://openjfx.io/) || [java-openjfx-ea-bin](https://aur.archlinux.org/packages/java-openjfx-ea-bin/)

### Другие реализации

**Java SE** — реализация JRE и JDK от Oracle.

	[https://www.oracle.com/technetwork/java/javase/downloads/index.html](https://www.oracle.com/technetwork/java/javase/downloads/index.html) || [jre](https://aur.archlinux.org/packages/jre/) [jre9](https://aur.archlinux.org/packages/jre9/) [jre8](https://aur.archlinux.org/packages/jre8/) [jre7](https://aur.archlinux.org/packages/jre7/) [jre6](https://aur.archlinux.org/packages/jre6/) [jdk](https://aur.archlinux.org/packages/jdk/) [jdk9](https://aur.archlinux.org/packages/jdk9/) [jdk8](https://aur.archlinux.org/packages/jdk8/) [jdk7](https://aur.archlinux.org/packages/jdk7/) [jdk6](https://aur.archlinux.org/packages/jdk6/) [jdk5](https://aur.archlinux.org/packages/jdk5/) [jdk-devel](https://aur.archlinux.org/packages/jdk-devel/)

**OpenJ9** — JRE от Eclipse, созданная при участии IBM.

	[https://www.eclipse.org/openj9/](https://www.eclipse.org/openj9/) || [jdk-openj9-bin](https://aur.archlinux.org/packages/jdk-openj9-bin/) [jdk13-openj9-bin](https://aur.archlinux.org/packages/jdk13-openj9-bin/) [jdk12-openj9-bin](https://aur.archlinux.org/packages/jdk12-openj9-bin/) [jdk11-openj9-bin](https://aur.archlinux.org/packages/jdk11-openj9-bin/) [jdk10-openjdk-openj9-bin](https://aur.archlinux.org/packages/jdk10-openjdk-openj9-bin/) [jdk9-openj9-bin](https://aur.archlinux.org/packages/jdk9-openj9-bin/) [jdk8-openj9-bin](https://aur.archlinux.org/packages/jdk8-openj9-bin/)

**IBM J9** — реализация восьмой редакции JRE от IBM.

	[https://developer.ibm.com/javasdk/](https://developer.ibm.com/javasdk/) || [jdk8-j9-bin](https://aur.archlinux.org/packages/jdk8-j9-bin/) [jdk7-j9-bin](https://aur.archlinux.org/packages/jdk7-j9-bin/) [jdk7r1-j9-bin](https://aur.archlinux.org/packages/jdk7r1-j9-bin/)

**Parrot VM** — виртуальная машина с экспериментальной поддержкой [языков](http://trac.parrot.org/parrot/wiki/) Java при помощи двух методов — [Java VM bytecode translator](https://code.google.com/p/parrot-jvm/) или [Java compiler targeting the Parrot VM](https://github.com/chrisdolan/perk).

	[http://www.parrot.org/](http://www.parrot.org/) || [parrot](https://aur.archlinux.org/packages/parrot/)

**Примечание:** 32-битные версии Java SE имеют префикс `bin32-`, например, [bin32-jre](https://aur.archlinux.org/packages/bin32-jre/) и [bin32-jdk](https://aur.archlinux.org/packages/bin32-jdk/). Они используют [java32-runtime-common](https://aur.archlinux.org/packages/java32-runtime-common/), работая с [java-runtime-common](https://www.archlinux.org/packages/?name=java-runtime-common) вместе с суффиксом `32`, например, `java32`. То же самое происходит и с [java32-environment-common](https://aur.archlinux.org/packages/java32-environment-common/), который используется только 32-битными пакетами JDK.

### Инструменты для разработки

См. [List of applications#Integrated development environments](/index.php/List_of_applications#Integrated_development_environments "List of applications") для получения списка IDE (в частности, секцию "Java IDEs").

Чтобы усложнить процесс реверс-инжиниринга, можно воспользоваться обфускатором [proguard](https://aur.archlinux.org/packages/proguard/).

#### Декомпиляторы

*   **Bytecode Viewer** — пакет для [обратного инжиниринга](https://en.wikipedia.org/wiki/ru:%D0%9E%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%B0%D1%8F_%D1%80%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B0 "wikipedia:ru:Обратная разработка") Java-приложений, включающий в себя декомпилятор, редактор и дебаггер.

	[https://bytecodeviewer.com](https://bytecodeviewer.com) || [bytecode-viewer](https://aur.archlinux.org/packages/bytecode-viewer/)

*   **CFR** — декомпилятор Java, поддерживающий также новые возможности Java 9 и выше.

	[https://www.benf.org/other/cfr/](https://www.benf.org/other/cfr/) || [cfr](https://aur.archlinux.org/packages/cfr/)

*   **Fernflower** — аналитический декомпилятор Java-приложений, разработанный для [IntelliJ IDEA](/index.php/IntelliJ_IDEA "IntelliJ IDEA").

	[https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine](https://github.com/JetBrains/intellij-community/tree/master/plugins/java-decompiler/engine) || [fernflower-git](https://aur.archlinux.org/packages/fernflower-git/)

*   **[JAD](https://en.wikipedia.org/wiki/JAD_(software) "wikipedia:JAD (software)")** — неподдерживаемый декомпилятор Java.

	[https://varaneckas.com/jad](https://varaneckas.com/jad) || [jad](https://www.archlinux.org/packages/?name=jad)

*   **JD-Core-java** — обёртка над [JD Decompiler](https://en.wikipedia.org/wiki/JD_Decompiler "wikipedia:JD Decompiler").

	[https://github.com/nviennot/jd-core-java](https://github.com/nviennot/jd-core-java) || [jd-core-java](https://aur.archlinux.org/packages/jd-core-java/)

*   **Krakatau** — декомпилятор, ассемблер и дизассемблер для Java.

	[https://github.com/Storyyeller/Krakatau](https://github.com/Storyyeller/Krakatau) || [krakatau-git](https://aur.archlinux.org/packages/krakatau-git/)

*   **Procyon decompiler** — экспериментальный декомпилятор Java, разработанный под влиянием ILSpy и Mono.Cecil.

	[https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler](https://bitbucket.org/mstrobel/procyon/wiki/Java%20Decompiler) || [procyon-decompiler](https://aur.archlinux.org/packages/procyon-decompiler/), GUI: [luyten](https://aur.archlinux.org/packages/luyten/)

## Переключение между средами

Для переключения используется скрипт `archlinux-java`

```
archlinux-java <COMMAND>

COMMAND:
       status          список установленных окружений Java и их статус
       get             короткое название текущего окружения Java
       set <JAVA_ENV>  устанавливает окружение <JAVA_ENV> по умолчанию
       unset           удаляет метку `по умолчанию` с окружения Java
       fix             исправляет ошибки конфигурации Java

```

### Получение списка установленных совместимых сред Java

```
$ archlinux-java status

Available Java environments:
  java-7-openjdk (default)
  java-8-openjdk/jre

```

Метка `(default)` как раз и подписывает окружение, установленное по умолчанию. Выполнение `java` или других команд будет ссылаться на эту версию. Отметка `/jre` означает, что установлен только JRE.

### Установка среды Java по умолчанию

```
# archlinux-java set java-8-openjdk/jre

```

**Совет:** Используйте команду `archlinux-java status` для отображения списка всех доступных сред Java.

**Примечание:** Использование названия неустановленного или несуществующего окружения Java ведёт к ошибке `is not a valid Java environment path`.

```
# archlinux-java set java-8-openjdk
'/usr/lib/jvm/java-8-openjdk' is not a valid Java environment path

```

### Удаление метки `по умолчанию`

Нет особой необходимости специально удалять метку, так как при работе с пакетами это происходит автоматически. Если необходимость всё же есть, используется команда `unset`.

```
# archlinux-java unset

```

### Исправление конфигурации Java

Если на какое-нибудь окружене Java задана неверная ссылка, команда `fix` попытается найти и исправить ошибку. Если окружение по умолчанию не задано, эта команда его установит на самый свежий доступный.

```
# archlinux-java fix

```

### Запуск приложений с окружением не установленным по умолчанию

Для таких случаев стоит написать скрипт. В примере ниже используется `java-8-openjdk/jre`

```
#!/bin/sh

export PATH="/usr/lib/jvm/java-8-openjdk/jre/bin/:$PATH"
exec /path/to/application "$@"

```

## Требования к пакетам сред для поддержки `archlinux-java`

**Примечание:** Информация применима и к `archlinux32-java`, при отличии, что в названиях пакетов используется верное наименование с `32` (см. [выше](#Другие_реализации)).

Этот раздел предназначен для тех, кто хочет распространять свои пакеты JVM в [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Arch User Repository") и использовать для управления `archlinux-java`. Пакеты должны соответствовать всем пунктам ниже:

*   все файлы пакета располагаются по адресу `/usr/lib/jvm/java-${JAVA_MAJOR_VERSION}-${VENDOR_NAME`}
*   все исполняемые файлы для [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) и [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/) имеют соответствующие ссылки
*   исполняемые файл, не принадлежащие к [java-runtime-common](https://www.archlinux.org/packages/extra/any/java-runtime-common/files/) и [java-environment-common](https://www.archlinux.org/packages/extra/any/java-environment-common/files/), имеют ссылки из `/usr/bin`
*   суффиксы [манов](https://wiki.archlinux.org/index.php/man_page_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:man page") такие: `-${VENDOR_NAME}${JAVA_MAJOR_VERSION`}; например, смотри [jre8-openjdk](https://www.archlinux.org/packages/extra/x86_64/jre8-openjdk/files/), где они имеют суффиксы `-openjdk8`
*   не используется ни [PKGBUILD conflicts](https://wiki.archlinux.org/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#conflicts "ru:PKGBUILD"), ни [PKGBUILD replaces](https://wiki.archlinux.org/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#replaces "ru:PKGBUILD") с другими JDK, `java-runtime`, {ic|java-runtime-headless}} или `java-environment`
*   используется скрипт `archlinux-java`, чтобы устанавливать окружение по умолчанию, если ни одно другое окружение не задано — то есть **не перезаписывается** значение по умолчанию

Стоит принять во внимание и эти советы:

*   пакеты, которым нужно окружение Java должны объявить зависимости `java-runtime`, {ic|java-runtime-headless}} или `java-environment`
*   пакеты, которым нужно определённое окружение Java должны объявить зависимости с необходимым суффиксом
*   пакеты OpenJDK объявляют `provides="java-runtime-openjdk=${pkgver}"`, что позволяет стороннему пакету объявлять зависимость от OpenJDK **без указания версии**

## Решение проблем

### Не подключается MySQL

В связи с тем, что драйверы JDBC часто используют порт в URI для установления соединения с базой данных, он считается «удаленным» (т. е. MySQL не прослушивает порт в соответствии с его настройками по умолчанию), несмотря на то, что, возможно, они работают на одном хосте. Таким образом, чтобы использовать JDBC и MySQL, вы должны разрешить удаленный доступ к MySQL, следуя инструкциям в статье [MySQL](https://wiki.archlinux.org/index.php/MySQL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Включение_удалённого_доступа "ru:MySQL").

### Не запускается IntelliJ IDEA

Если IntelliJ IDEA вылетает с ошибкой `The selected directory is not a valid home for JDK`, придётся установить другую JDK или использовать IntelliJ IDEA с JetBrains Runtime.

### Ошибки отрисовки приложений Java

В оконных менеджерах [Awesome](https://wiki.archlinux.org/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Awesome"), [Dwm](https://wiki.archlinux.org/index.php/Dwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Dwm") и [Ratpoison](/index.php/Ratpoison "Ratpoison") возникают ошибки отрисовки GUI в Java, появляются серые окна, приложения не изменяют размер, меню мгновенно закрываются. Для того, чтобы JVM думала, что используется оконный менеджер, отличный от установленного, используется [wmname](https://www.archlinux.org/packages/?name=wmname). Задайте поддельное название оконного менеджера, например, `compiz` или `LG3D`

```
$ wmname compiz

```

После выполнения команды нужно перезапустить приложение Java. Такое поведение обосновано тем, что в JVM прямо установлены известные оконные менеджеры, которые используют подход *non-re-parenting*.

Если установка поддельного оконного менеджера не применима, есть несколько советов:

*   для [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) и [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk), добавьте строчку `export _JAVA_AWT_WM_NONREPARENTING=1` в `/etc/profile.d/jre.sh`, затем выполните его или перезайдите
*   для свежих JVM работает добавление `export AWT_TOOLKIT=MToolkit` в `~/.xinitrc` перед командой запуска оконного менеджера
*   для пакетов Oracle можно использовать [SetWMName](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Using_SetWMName), однако, положительный эффект может быть сброшен при использовании пакета `XMonad.Hooks.EwmhDesktops` в приложении. В этом случае может помочь добавление строчки `>> setWMName "LG3D"` к `LogHook`.

Смотри также [Problems with Java applications, Applet java console](https://wiki.haskell.org/Xmonad/Frequently_asked_questions#Problems_with_Java_applications.2C_Applet_java_console) на Haskell.org.

### Неразборчивый шрифт в приложениях Java

Некоторые шрифты не читаются, поэтому следует установить другие, читаемые шрифты, например, [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts/).

### В некоторых приложениях отсутствует текст

Далее в разделе [#Улучшенное отображение шрифтов](#Улучшенное_отображение_шрифтов) приводятся параметры; см. также [FS#40871](https://bugs.archlinux.org/task/40871).

### Система зависает при дебаггинге

Используйте параметр JVM `-Dsun.awt.disablegrab=true`. Смотри также [страницу бага](https://bugs.java.com/bugdatabase/view_bug.do?bug_id=6714678) в JDK 6.

### Конструктор JavaFX MediaPlayer вылетает с ошибкой

При создании экземпляра класса `MediaPlayer` может появиться такая ошибка:

```
... (i.e. FXMLLoader construction exceptions) ...
Caused by: MediaException: UNKNOWN : com.sun.media.jfxmedia.MediaException: Could not create player! : com.sun.media.jfxmedia.MediaException: Could not create player!
 at javafx.scene.media.MediaException.exceptionToMediaException(MediaException.java:146)
 at javafx.scene.media.MediaPlayer.init(MediaPlayer.java:511)
 at javafx.scene.media.MediaPlayer.<init>(MediaPlayer.java:414)
 at <constructor call>
...

```

это связано с несовеместимостью JavaFX и [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg) из репозитория, поэтому следует установить [ffmpeg-compat-55](https://aur.archlinux.org/packages/ffmpeg-compat-55/). См. также [обсуждение](https://www.reddit.com/r/archlinux/comments/70o8o6) на Reddit.

### В приложениях Java не открываются внешние ссылки

Установите [gvfs](https://www.archlinux.org/packages/?name=gvfs); в приложении требуется реализовать метод `Desktop.Action.BROWSE`. См. также [обсуждение](https://bugs.launchpad.net/ubuntu/+source/openjdk-8/+bug/1574879/comments/2) на Launchpad.

### Ошибка инициализации `QuantumRenderer`: `no suitable pipeline found`

Либо отсутствует GTK2 — установите [gtk2](https://www.archlinux.org/packages/?name=gtk2), либо отсутствует OpenJFX — установите [java-openjfx](https://www.archlinux.org/packages/?name=java-openjfx).

## Советы и рекомендации

**Примечание:** Предложения в этом разделе применимы ко всем приложениям, использующим явно установленную (внешнюю) среду выполнения Java. Некоторые приложения связаны с собственной средой выполнения или используют собственную механику для графического интерфейса пользователя, рендеринга шрифтов и т. д., поэтому ни один из нижеприведённых советов не будет работать гарантированно.

Поведение большинства приложений Java можно контролировать, предоставляя предопределённые переменные для среды выполнения Java. Для этого нужно добавлять строчки в `~/.bashrc` или `/etc/profile.d/jre.sh`.

```
export _JAVA_OPTIONS="-D**<option 1>** -D**<option 2>**..."

```

Например, предопределённое использование сглаженных шрифтов и GTK:

```
export _JAVA_OPTIONS='-Dawt.useSystemAAFontSettings=on -Dswing.aatext=true -Dswing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel'

```

### Улучшенное отображение шрифтов

Установите параметры JVM `-Dawt.useSystemAAFontSettings=on`, `-Dswing.aatext=true`. См. статью [Java Runtime Environment fonts](https://wiki.archlinux.org/index.php/Java_Runtime_Environment_fonts_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:Java Runtime Environment fonts")

### Удаление сообщения `Picked up _JAVA_OPTIONS`

При установке какого-либо параметра JVM появялестя сообщение вида `Picked up _JAVA_OPTIONS=...`. Чтобы избавиться от сообщения, используйте команды ниже

```
_SILENT_JAVA_OPTIONS="$_JAVA_OPTIONS"
unset _JAVA_OPTIONS
alias java='java "$_SILENT_JAVA_OPTIONS"'

```

### Оформление GTK

Установите параметры JVM `swing.defaultlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`. Некоторые приложения используют кроссплатформенный вид `Metal`; чтобы переопределить его, используйте параметр JVM `swing.crossplatformlaf=com.sun.java.swing.plaf.gtk.GTKLookAndFeel`.

	Поддержка GTK 3

В версиях, предшествующих Java 9 использовался вид GTK 2\. Эта несовместимость между версиями GTK может нарушить работу приложений, использующих плагины Java с графическим интерфейсом, поскольку смешивание GTK 2 и GTK 3 в одном и том же процессе не поддерживается (например, LibreOffice 5.0). Начиная с Java 9 можно выбрать GTK `2`, `2.2` или `3`, но по умолчанию используется GTK 2; чтобы задать приоритет используйте параметр JVM `jdk.gtk.version=3`.

### Ускорение отрисовки 2D

Если доступно использование [OpenGL](https://wiki.archlinux.org/index.php/OpenGL_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ru:OpenGL"), его можно включить в приложениях Java, задав переменную окружения

```
export _JAVA_OPTIONS='-Dsun.java2d.opengl=true'

```

**Примечание:** Включение этого параметра может привести к неправильной работе пользовательского интерфейса таких программ, как все IDE от JetBrains, из-за чего они частично отрисовывают окна, всплывающие окна и панели инструментов.