Eclipse - это проект с открытым исходным кодом, цель которого - создание универсальной платформы для разработчиков. Eclipse широко известна своей кросс-платформенной интегрированной средой разработки (ИСР, IDE).

Eclipse IDE написана, в основном, на Java. Однако, она также может использоваться для разработки на многих языках, включая Java, C/C++, PHP и Perl. IDE также обеспечивает поддержку subversion (см. ниже) и управление задачами (посредством встроенного списка TODO или пакет Eclipse-mylyn).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка Eclipse](#Установка_Eclipse)
*   [2 Плагины](#Плагины)
    *   [2.1 C/C++](#C/C++)
        *   [2.1.1 Eclipse CDT](#Eclipse_CDT)
    *   [2.2 perl](#perl)
        *   [2.2.1 EPIC](#EPIC)
    *   [2.3 PHP](#PHP)
        *   [2.3.1 Eclipse PDT](#Eclipse_PDT)
        *   [2.3.2 PHPEclipse](#PHPEclipse)
    *   [2.4 Python](#Python)
        *   [2.4.1 PyDev](#PyDev)
    *   [2.5 Веб-разработка (HTML, CSS, JavaScript...)](#Веб-разработка_(HTML,_CSS,_JavaScript...))
        *   [2.5.1 Aptana Studio](#Aptana_Studio)
    *   [2.6 Subversion](#Subversion)
        *   [2.6.1 Subclipse](#Subclipse)
        *   [2.6.2 Eclipse Subversive](#Eclipse_Subversive)
    *   [2.7 Git](#Git)
        *   [2.7.1 EGit](#EGit)
    *   [2.8 Mercurial support](#Mercurial_support)
        *   [2.8.1 MercurialEclipse](#MercurialEclipse)
    *   [2.9 LaTeX support](#LaTeX_support)
        *   [2.9.1 TeXlipse](#TeXlipse)
*   [3 Настройка Eclipse](#Настройка_Eclipse)
    *   [3.1 Включение обновлений](#Включение_обновлений)
*   [4 Интеграция с javadoc](#Интеграция_с_javadoc)
    *   [4.1 Онлайн Версия](#Онлайн_Версия)
    *   [4.2 Оффлайн Версия](#Оффлайн_Версия)

## Установка Eclipse

Установить Eclipse SDK в Arch Linux очень просто:

```
# pacman -S eclipse

```

Это базовый пакет, с ним вы можете приступать к разработке на Java.

## Плагины

Плагины позволяют значительно расширить возможности среды и приспособить её под конкретные задачи. Установить плагины для Eclipse можно двумя способами:

*   Использовать [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") для установки тех плагинов, которые присутствуют в репозиториях Arch (в статье [Eclipse plugin package guidelines](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") есть дополнительная информация);
*   Воспользоваться менеджером плагинов Eclipse, который скачает и установит плагины прямо из их собственных репозиториев. В этом случае вам понадобится найти необходимый репозиторий на сайте разработчиков плагина, затем перейти в меню *Help -> Install New Software...*, ввести адрес репозитория в поле *Work with*, выбрать нужный плагин из списка и следовать дальнейшим укаазаниям установщика.

**Важно:**

*   При установке плагинов с помощью менеджера плагинов Eclipse, лучше запускать Eclipse от root: тогда плагины установятся в `/usr/share/eclipse/plugins/`. если же проводить эту операцию от имени пользователя, плагины будут сохранены в подпапку `~/.eclipse/`, зависимую от версии. Таким образом, после обновления Eclipse они больше не будут работать.
*   Не запускайте Eclipse от root для повседневной работы.

Ниже расположен список плагинов, добавляющих поддержку различных языков и технологий.

### C/C++

#### Eclipse CDT

*   Страница проекта: [http://www.eclipse.org/cdt/](http://www.eclipse.org/cdt/)
*   Пакет из [extra]: [eclipse-cdt](https://www.archlinux.org/packages/?name=eclipse-cdt)

### perl

#### EPIC

*   Страница проекта: [http://www.epic-ide.org/](http://www.epic-ide.org/)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-epic](https://aur.archlinux.org/packages/eclipse-epic/)

### PHP

#### Eclipse PDT

*   Страница проекта: [http://www.eclipse.org/pdt/](http://www.eclipse.org/pdt/)
*   Инструкции по установке плагина для Eclipse: [http://wiki.eclipse.org/PDT/Installation](http://wiki.eclipse.org/PDT/Installation)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-pdt](https://aur.archlinux.org/packages/eclipse-pdt/)

#### PHPEclipse

*   Страница проекта: [http://www.phpeclipse.com/](http://www.phpeclipse.com/)
*   Пакет из [community]: [eclipse-phpeclipse](https://aur.archlinux.org/packages/eclipse-phpeclipse/)

### Python

#### PyDev

*   Страница проекта: [http://pydev.org/](http://pydev.org/)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-pydev](https://aur.archlinux.org/packages/eclipse-pydev/)

### Веб-разработка (HTML, CSS, JavaScript...)

#### Aptana Studio

*   Страница проекта: [http://www.aptana.org/](http://www.aptana.org/)
*   Плагин для Eclipse устанавливается через менеджер плагинов
*   Может работать в качестве отдельного приложения. Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

### Subversion

#### Subclipse

*   Страница проекта: [http://subclipse.tigris.org/](http://subclipse.tigris.org/)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-subclipse](https://aur.archlinux.org/packages/eclipse-subclipse/)
*   [Как использовать Subversion вместе с Eclipse](http://www-128.ibm.com/developerworks/opensource/library/os-ecl-subversion/)

#### Eclipse Subversive

*   Страница проекта: [http://www.eclipse.org/subversive/](http://www.eclipse.org/subversive/)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-subversive](https://aur.archlinux.org/packages/eclipse-subversive/)

### [Git](/index.php/Git "Git")

#### EGit

*   Страница проекта: [http://www.eclipse.org/egit](http://www.eclipse.org/egit)
*   Ссылка на репозиторий: [http://download.eclipse.org/egit/updates](http://download.eclipse.org/egit/updates)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-egit](https://aur.archlinux.org/packages/eclipse-egit/)

### [Mercurial](/index.php/Mercurial "Mercurial") support

#### MercurialEclipse

*   Страница проекта: [http://code.google.com/a/eclipselabs.org/p/mercurialeclipse/](http://code.google.com/a/eclipselabs.org/p/mercurialeclipse/)
*   Ссылка на репозиторий: [http://mercurialeclipse.eclipselabs.org.codespot.com/hg.wiki/update_site/stable](http://mercurialeclipse.eclipselabs.org.codespot.com/hg.wiki/update_site/stable)
*   Пакет из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"): [eclipse-mercurial](https://aur.archlinux.org/packages/eclipse-mercurial/)

### [LaTeX](/index.php/LaTeX "LaTeX") support

#### TeXlipse

*   Страница проекта: [http://texlipse.sourceforge.net/](http://texlipse.sourceforge.net/)
*   Ссылка на репозиторий: [http://texlipse.sourceforge.net](http://texlipse.sourceforge.net)

## Настройка Eclipse

После установки Eclipse с помощью pacman, вам наверняка захочется немного его настроить.

### Включение обновлений

Пока что ваш Eclipse не знает, где брать обновления.

**Tip:** На сайте Eclipse вы можете найти несколько адресов, которые вы можете добавить в **Window -> Preferences -> Install/Update -> Available Software Sites -> Add...**

Вы можете попробовать этот адрес:

```
[http://download.eclipse.org/releases/maintenance](http://download.eclipse.org/releases/maintenance)

```

Однако, если у вас установлен Eclipse 3.6.x (Helios), используйте этот:

```
[http://download.eclipse.org/releases/helios](http://download.eclipse.org/releases/helios)

```

а добавленные автоматически могут быть активированы в меню *Available Software Sites*.

После этих операций вы можете обновлять и дополнять Eclipse в меню **Help**.

## Интеграция с javadoc

Позволяет видеть элементы API при наведении курсора мыши на стандартные методы Java.

### Онлайн Версия

Если у вас постоянное соединение с интернетом, вы можете использовать онлайн-документацию, предоставляемую Sun:

1.  Откройте **Window/Preferences**, а затем **Java/Installed JREs**
2.  Один из пунктов имеет имя **java** и тип **Standard VM**. Выделите его и нажмите **Edit**
3.  Выберите `/opt/java/jre/lib/rt.jar` под **JRE system libraries:**, и щёлкните **Javadoc Location...**
4.  Введите [http://java.sun.com/javase/6/docs/api/](http://java.sun.com/javase/6/docs/api/) в текстовом поле **Javadoc location path:**
5.  Готово!

### Оффлайн Версия

Если у вас нет соединения с Интернетом или вам не хотелось бы постоянно расходовать трафик на документацию, вы можете сохранить её на ваш жёсткий диск.

1.  Откройте в своём любимом браузере [http://java.sun.com/javase/downloads/index.jsp](http://java.sun.com/javase/downloads/index.jsp)
2.  Найдите **Java SE 6 Documentation** и щёлкните по ссылке загрузки.
3.  Следуя инструкциям, загрузите `jdk-6-doc.zip` на ваш жёсткий диск (например, в `/home/docs/jdk-6-doc.zip`).

1.  Откройте **Window/Preferences**, а затем **Java/Installed JREs**
2.  Один из пунктов имеет имя **java** и тип **Standard VM**. Выделите его и нажмите **Edit**
3.  Выберите `/opt/java/jre/lib/rt.jar` под **JRE system libraries:**, и щёлкните **Javadoc Location...**
4.  Выберите пункт **Javadoc in archive**
5.  Введите путь к ранее скачанному `jdk-6-doc.zip` (например, `/home/docs/jdk-6-doc.zip`) в текстовом поле **Archive path:**
6.  Готово!