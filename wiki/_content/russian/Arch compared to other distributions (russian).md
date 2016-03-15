Эта страница написана с целью показать сходства и различия между Arch и другими популярными дистрибутивами GNU/Linux. Этот вопрос задают очень часто, и хорошо было бы иметь стандартный ответ. Тем не менее, учтите: лучший способ сравнить дистрибутивы между собой — установить и попробовать самому. Текст ниже призван лишь дать достаточно информации, чтобы вы решили, подходит вам Arch или нет.

## Contents

*   [1 Source-based](#Source-based)
    *   [1.1 Arch и Gentoo](#Arch_.D0.B8_Gentoo)
    *   [1.2 Arch и Sorcerer/Lunar-linux/Source Mage](#Arch_.D0.B8_Sorcerer.2FLunar-linux.2FSource_Mage)
*   [2 Минималистичные](#.D0.9C.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D0.BB.D0.B8.D1.81.D1.82.D0.B8.D1.87.D0.BD.D1.8B.D0.B5)
    *   [2.1 Arch и Crux](#Arch_.D0.B8_Crux)
    *   [2.2 Arch и Rock](#Arch_.D0.B8_Rock)
*   [3 Arch и графические дистрибутивы](#Arch_.D0.B8_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D0.B8.D1.81.D1.82.D1.80.D0.B8.D0.B1.D1.83.D1.82.D0.B8.D0.B2.D1.8B)
    *   [3.1 Arch и Slackware](#Arch_.D0.B8_Slackware)
    *   [3.2 Arch и Debian](#Arch_.D0.B8_Debian)
    *   [3.3 Arch и Ubuntu](#Arch_.D0.B8_Ubuntu)
    *   [3.4 Arch и RPM-дистрибутивы](#Arch_.D0.B8_RPM-.D0.B4.D0.B8.D1.81.D1.82.D1.80.D0.B8.D0.B1.D1.83.D1.82.D0.B8.D0.B2.D1.8B)
        *   [3.4.1 Arch и Fedora](#Arch_.D0.B8_Fedora)
        *   [3.4.2 Arch и Mandriva](#Arch_.D0.B8_Mandriva)
        *   [3.4.3 Arch и SUSE](#Arch_.D0.B8_SUSE)
    *   [3.5 Arch и Frugalware](#Arch_.D0.B8_Frugalware)

## Source-based

Дистрибутивы, подразумевающие самостоятельную сборку пользователем пакетов, могут оптимизироваться под конкретное оборудование, переносимы и предоставляют наивысший контроль. Однако они отнимают значительное время на сборку пакетов. Arch предоставляет готовые пакеты, оптимизированные для i686 и x86_64, требуя меньше времени на установку пакетов и дистрибутива и облегчая поддержку. Не существует убедительного подтверждения, что source-based дистрибутивы работают быстрее, чем Arch.

### Arch и Gentoo

Оба эти дистрибутива основаны на системе *плавающих релизов*. Это приводит к тому, что новые версии пакетов почти сразу становятся доступными в репозиториях.

Gentoo имеет несколько больше пакетов и позволяет вам выбирать их версии. Arch позволяет как установку бинарных пакетов, так и сборку их из исходных кодов, и установка пакета, которого нет в репозитории, в Arch гораздо проще.

Пакеты в Gentoo собираются в соответствии с глобальными "USE"-флагами, тогда как система портов в Arch требует кастомизации каждого скрипта сборки по отдельности. PKGBUILD'ы создавать гораздо проще, чем ebuild'ы.

Arch поддерживает архитектуры i686 and x86_64, тогда как Gentoo официально поддерживает x86, PPC, SPARC, Alpha, AMD64, ARM, MIPS, HP/PA, S/390, sh, и Itanium.

### Arch и Sorcerer/Lunar-linux/Source Mage

Sorcerer/Lunar-linux/Sourcemage (SLS) — дистрибутивы, основанные на сборке из исходных кодов (т.н. source based), очень похожие на Gentoo. Они используют простой набор скриптов для создания описания процесса сборки пакета. В них используется глобальный конфигурационный файл для настройки компиляции пакетов, очень похожей на ABS в Arch. Утилиты в SLS совершают проверку зависимостей (включая опциональные) и слежение за пакетами (для удаления и обновления). Для семейства SLS не существует бинарных пакетов, однако в них легко откатиться на старую версию пакета.

Установка состоит в извлечении базовой системы (очень похожа на устновку Arch: оптимизация под i686, CLI и меню на ncurses, только базовые утилиты), после чего эту базовую систему можно пересобрать (опционально). Очевидно, что в процессе установки базовой системы не устанавливается никаких оконных сред и даже X-сервера. Но есть возможность легкой установки одного из нескольких серверов (xorg 6.8/7, xfree86).

SLS имеют очень сложную историю.

*   [Lunar Linux](http://lunar-linux.org/)

## Минималистичные

### Arch и Crux

Arch Linux изначально произошел от Crux. Джадд однажды описал различия: *"Я использовал Crux, прежде чем начать работу над Arch. Arch начинался из Crux. Затем я написал pacman и makepkg, которыми я заменил мои скрипты на bash (для начала я построил Arch из LFS). Вообще, это два отдельных дистрибутива, но технически они во многом схожи. У нас есть официальная поддержка зависимостей, например, однако Crux имеет сообщество, которое предоставляет другие преимущества. prt-get имеет зачатки контроля зависимостей. Crux имеет множество проблем, которые есть и у нас, это очень минималистичный набор пакетов, например."*

### Arch и Rock

Из [описания](http://rocklinux.net/wiki/About):

*"ROCK Linux — гибкий набор инструментов и деталей для создания дистрибутива Linux, то есть каркас для сборки собственного дистрибутива. ... Если вы не планируете собирать свой собственный дистрибутив, а просто заинтересованы в получении хорошего, универсального дистрибутива, то вам стоит обратить внимание на [Crystal ROCK](http://rocklinux.net/wiki/Crystal_ROCK)."*

Дистрибутив основан для того, чтобы быть инструментом. В сравнении с Arch; те же проблемы, связанные с требуемым временем для установки из исходников, и т.д. Похоже, что работает на многих типах процессоров таких как SPARC, ARM и т.д.

## Arch и графические дистрибутивы

Все "графические дистрибутивы" имеют множество сходств, и Arch очень отличается от любого из них. Arch ориентирован на использование командной строки. Arch — лучший дистрибутив, если вы действительно хотите изучить Linux. Графические дистрибутивы обычно имеют графические инсталляторы (вроде Anaconda в Fedora Core) и графические же утилиты для конфигурирования системы (вроде YaST в SUSE). Специфические различия между дистрибутивами описаны ниже.

### Arch и Slackware

Slackware и Arch — "простые" дистрибутивы. Оба используют систему инициализации в BSD-стиле. Arch предлагает намного более мощную систему управления пакетами (pacman), которая, в отличие от стандартных утилит Slackware, позволяет производить автоматическое обновление системы. Slackware более консервативен в своем релиз-цикле, предоставляя только стабильные пакеты. Arch значительно более либерален в этом плане. Arch заточен под i686, в то время как Slackware запускается на i486\. Arch очень хорош для тех пользователей Slackware, которые нуждаются в хорошем менеджере пакетов и более свежих версиях программ.

### Arch и Debian

Arch проще, чем Debian. В Arch'е меньше пакетов. Arch предлагает лучшую поддержку для сборки своих собственных пакетов. Arch более снисходителен к так называемым 'несвободным' ('non-free') пакетам. Arch оптимизирован для i686 и поэтому может потенциально работать быстрее, чем Debian. Пакеты Arch гораздо свежее, чем в Debian (current в Arch часто новее, чем Debian testing).

### Arch и Ubuntu

Arch имеет более простую иерархию, чем Ubuntu. Если вы любите компилировать собственные ядра, пробовать свежие программы из CVS или собирать программу из исходников, Arch вам подойдет больше. Если вы хотите быстрого развертывания системы и не хотите изучать ее внутренности, Ubuntu будет лучшим выбором. Вообще, разработчикам и энтузиастам Arch нравится больше, чем Ubuntu.

### Arch и RPM-дистрибутивы

RPM пакеты доступны во множестве мест, однако сторонние программы часто имеют проблемы с зависимостями, например, требуют более старые версии библиотек. Еще есть несоответствие между RPM, собранными для Red Hat, и RPM, собранными для Mandriva.

#### Arch и Fedora

Fedora - наследник дистрибутива Red Hat, являющийся в данное время одним из самых популярных дистрибутивов. Следовательно, он имеет большое сообщество и множество готовых пакетов, а также хорошую поддержку. Как и во всех RPM-дистрибутивах, управление пакетами доставляет немало проблем. Fedora включает в себя Yum в качестве фронтэнда к RPM, который самостоятельно скачивает пакеты и разрешает зависимости. Fedora всегда содержит множество инноваций и заработала славу интеграцией с SELinux и скомпилированными GCJ Java-программами (что лишает необходимости устанавливать Sun JRE). Fedora не пытается поддерживать mp3 из-за патентных проблем.

#### Arch и Mandriva

Mandriva (ранее Mandrake) - очень дружественный к пользователю дистрибутив, известный своим инсталлятором, который через некоторое время использования может начать разочаровывать. Основной проблемой является проблема с RPM, описанная ранее. Arch дает больше свободы действий и менее дружественен к пользователю. С ним вы по-настоящему научитесь использовать Linux.

#### Arch и SUSE

SUSE весь опутан настройщиком YaST, из которого можно сконфигурировать практически все. Arch не предоставляет вам ничего подобного (смотрите статью [Философия Arch](/index.php/%D0%A4%D0%B8%D0%BB%D0%BE%D1%81%D0%BE%D1%84%D0%B8%D1%8F_Arch "Философия Arch")). SUSE больше подходит для менее подготовленных пользователей и для тех, кто хочет, чтобы система работала сразу "из коробки", после минимальной настройки. SUSE не предоставляет поддержку mp3 сразу после установки, однако она может быть добавлена через YaST.

### Arch и Frugalware

Arch ориентирован на использование утилит командной строки (пользователь должен хотеть учиться). Frugalware — система, основанная на Slackware. Frugalware предоставляет лучшую поддержку различных языков. Также Frugalware поставляется с большим количеством документации. Frugalware претендует на то, чтобы быть быстрее, чем Arch. Оба дистрибутива используют pacman. Однако пакеты не очень-то совместимы.