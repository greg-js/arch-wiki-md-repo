Ссылки по теме

*   [ArchWiki:IRC](/index.php/ArchWiki:IRC "ArchWiki:IRC")
*   [International communities](/index.php/International_communities "International communities")
*   [phrik](/index.php/Phrik "Phrik")

**Состояние перевода:** На этой странице представлен перевод статьи [Arch IRC channels](/index.php/Arch_IRC_channels "Arch IRC channels"). Дата последней синхронизации: 2 июня 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Arch_IRC_channels&diff=0&oldid=566394).

Вам потребуется [IRC-клиент](/index.php/List_of_applications/Internet_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#IRC "List of applications/Internet (Русский)") для использования [IRC](https://en.wikipedia.org/wiki/ru:IRC включает в себя клиент [Irssi](/index.php/Irssi "Irssi").

Пожалуйста, ознакомьтесь с [Кодексом поведения](/index.php/Code_of_conduct_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Code of conduct (Русский)") и [Code of conduct#IRC](/index.php/Code_of_conduct#IRC "Code of conduct") перед вступлением в какие-либо официальные каналы. Также см. [Глоссарий](/index.php/%D0%93%D0%BB%D0%BE%D1%81%D1%81%D0%B0%D1%80%D0%B8%D0%B9 "Глоссарий") и [IRC Jargon](http://www.ircbeginner.com/ircinfo/abbreviations.html) для ознакомления с распространёнными терминами IRC.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Основные каналы](#Основные_каналы)
    *   [1.1 Регистрация](#Регистрация)
    *   [1.2 Операторы каналов](#Операторы_каналов)
*   [2 Другие каналы](#Другие_каналы)
*   [3 Международные IRC-каналы](#Международные_IRC-каналы)

## Основные каналы

**Примечание:**

*   Различные веб-клиенты и шлюзы могут иногда блокироваться из-за злоупотребления. Если вы столкнулись с такой проблемой, используйте "*надёжный*" IRC-клиент или попросите одного из операторов разблокировать вас (`+e`).
*   Канал [#archlinux-offtopic](https://alyp.tk/stats/aotstats.html) собирает статистику. Если вы хотели бы навсегда отказаться от участия в ней, обратитесь к *jp/alyptik*.

Эта секция рассказывает о [#archlinux](ircs://chat.freenode.net/archlinux), основном [IRC](https://en.wikipedia.org/wiki/ru:IRC "wikipedia:ru:IRC")-канале поддержки Arch Linux, а также [#archlinux-offtopic](ircs://chat.freenode.net/archlinux-offtopic), основном канале Arch Linux для общения. Оба канала доступны в сети [Freenode](https://freenode.net/).

Основная тема канала **#archlinux** — поддержка и обсуждение Arch Linux.

### Регистрация

Каналам **#archlinux** и **#archlinux-offtopic** заданы режимы `+r` и `+q $~a`, чтобы уменьшить количество спама. Это означает, что необходимо пройти идентификацию `NickServ` перед вступлением в эти каналы и отправкой сообщений соответственно. Если же вы не зарегистрированы и не прошли идентификацию, вы будете перенаправлены в **#archlinux-unregistered**.

См. [freenode FAQ](https://freenode.net/kb/answer/registration) и `NickServ help` при подключении к *chat.freenode.net*, чтобы зарегистрироваться с помощью NickServ:

```
/query NickServ HELP REGISTER
/query NickServ HELP IDENTIFY

```

**Примечание:**

*   Воспользуйтесь `/quote NickServ <command>` или `/msg NickServ <command>`, если `/query` не работает в вашем клиенте.
*   Некоторые IRC-клиенты сталкиваются с состоянием гонки (race condition), когда они автоматически пытаются присоединиться к каналу перед прохождением идентификации NickServ. Данная проблема исправляется включением SASL — см. документацию вашего IRC-клиента или [страницу о SASL](https://freenode.net/kb/answer/sasl) на freenode для получения необходимых инструкций.
*   Введите `/msg ChanServ ACCESS #archlinux LIST`, чтобы получить список людей, которые могут помочь. Также можно присоединиться к **#freenode** и спросить там.

### Операторы каналов

Операторы Arch участвуют как в **#archlinux**, так и в **#archlinux-offtopic**. См. полный список ниже или выполните `/msg phrik listops` на freenode.

Не стесняйтесь использовать `/query` или `/msg`, если вам нужна помощь оператора. Здесь представлен список операторов по состоянию на 1 ноября 2018:

*   alad
*   amcrae
*   falconindy
*   gehidore / man
*   grawity
*   heftig
*   jelle
*   MrElendig / Mion
*   Namarrgon
*   pid1
*   tigrmesh / tigr
*   vodik
*   wonder / ioni

## Другие каналы

Размер нашего сообщества привёл к созданию нескольких IRC каналов. Используйте команду `/query alis list *archlinux*`, чтобы получить список всех каналов на freenode, которые содержат "archlinux" в своём названии.

| Канал | Описание |
| [#archlinux64](ircs://chat.freenode.net/archlinux64) | Канал обсуждения x86_64, в основном на английском. |
| [#archlinux-aur](ircs://chat.freenode.net/archlinux-aur) | Общее обсуждение [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). |
| [#archlinux-aurweb](ircs://chat.freenode.net/archlinux-aurweb) | Обсуждение разработки [aurweb](https://projects.archlinux.org/aurweb.git/). |
| [#archlinux-bugs](ircs://chat.freenode.net/archlinux-bugs) | Обсуждение ошибок (багов). |
| [#archlinux-classroom](ircs://chat.freenode.net/archlinux-classroom) | Проект по разработке и проведению занятий для сообщества Arch Linux. |
| [#archlinux-devops](ircs://chat.freenode.net/archlinux-devops) | Обсуждение внутренней инфраструктуры Arch Linux и DevOps. |
| [#archlinux-multilib](ircs://chat.freenode.net/archlinux-multilib) | Обсуждение проекта Arch Linux Multilib и пакетирования. |
| [#archlinux-newbie](ircs://chat.freenode.net/archlinux-newbie) | Здесь вы можете поучиться, попробовать новые вещи и попросить о помощи, не опасаясь насмешек. |
| [#archlinux-pacman](ircs://chat.freenode.net/archlinux-pacman) | Разработка и обсуждение [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). |
| [#archlinux-projects](ircs://chat.freenode.net/archlinux-projects) | Обсуждение разработки проектов (mkinitcpio, abs, dbscripts, devtools и т.д.). |
| [#archlinux-reproducible](ircs://chat.freenode.net/archlinux-reproducible) | Обсуждение повторяемых сборок. |
| [#archlinux-security](ircs://chat.freenode.net/archlinux-security) | Обсуждение проблем безопасности в пакетах Arch. |
| [#archlinux-wiki](ircs://chat.freenode.net/archlinux-wiki) | Обсуждение [ArchWiki](/index.php/ArchWiki:About_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki:About (Русский)"), статей и [Форумов Arch Linux](https://bbs.archlinux.org/). |
| [#archlinux-women](ircs://chat.freenode.net/archlinux-women) | Обсуждение гендерного равенства, в основном на английском. |
| [#archlinux-proaudio](ircs://chat.freenode.net/archlinux-proaudio) | Обсуждение [Arch Linux Pro Audio](/index.php/Professional_audio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Professional audio (Русский)"). Также существует неофициальный #archaudio. |

## Международные IRC-каналы

Международные обсуждения доступны на следующих каналах, также расположенных в IRC сети **[irc.freenode.net](irc://irc.freenode.net)**, если не указано иное:

| Канал | Обсуждение |
| [#archlinux-za](ircs://chat.freenode.net/archlinux-za) | Обсуждение (африкаанс, английский) |
| [#archlinux-br](ircs://chat.freenode.net/archlinux-br) | Обсуждение (бразильский) |
| [#archlinux-cn](ircs://chat.freenode.net/archlinux-cn) | Обсуждение (китайский); также на **[irc.oftc.net#arch-cn](irc://irc.oftc.net/arch-cn)** |
| [#archlinux-cr](ircs://chat.freenode.net/archlinux-cr) | Обсуждение (Коста-Рика) |
| [#archlinux.cz](ircs://chat.freenode.net/archlinux.cz) | Обсуждение (чешский) |
| [#archlinux.dk](ircs://chat.freenode.net/archlinux.dk) | Обсуждение (датский) |
| [#archlinux.fi](ircs://chat.freenode.net/archlinux.fi) | Обсуждение (финский) |
| [#archlinux-fr](ircs://chat.freenode.net/archlinux-fr) | Обсуждение (французский) |
| [#archlinux-gaelic](ircs://chat.freenode.net/archlinux-gaelic) | Обсуждение (гэльский) |
| [#archlinux.de](ircs://chat.freenode.net/archlinux.de) | Обсуждение (немецкий) |
| [#archlinux-greece](ircs://chat.freenode.net/archlinux-greece) | Обсуждение (греческий) |
| [#archlinux-il](ircs://chat.freenode.net/archlinux-il) | Обсуждение (иврит) |
| [#archlinux.hu](ircs://chat.freenode.net/archlinux.hu) | Обсуждение (венгерский) |
| [#archlinux-it](ircs://chat.freenode.net/archlinux-it) | Обсуждение (итальянский); также на **[irc.azzurra.org#archlinux](irc://irc.azzurra.org/archlinux)** |
| [#archlinux-nordics](ircs://chat.freenode.net/archlinux-nordics) | Обсуждение (датский, финский, норвежский и шведский) |
| [#archlinux-kr](ircs://chat.freenode.net/archlinux-kr) | Обсуждение (корейский) |
| [#archlinux-ir](ircs://chat.freenode.net/archlinux-ir) | Обсуждение (персидский) |
| [#archlinux.org.pl](ircs://chat.freenode.net/archlinux.org.pl) | Обсуждение (польский) |
| [#archlinux-pt](ircs://chat.freenode.net/archlinux-pt) | Обсуждение (португальский) |
| [#archlinux.ro](ircs://chat.freenode.net/archlinux.ro) | Обсуждение (румынский) |
| [#archlinux-tg](ircs://chat.freenode.net/archlinux-tg) | Обсуждение (русский); мост между IRC и Телеграм-группой [Arch Linux RU](https://t.me/ArchLinuxChatRU) |
| [#archlinux-ru](ircs://chat.freenode.net/archlinux-ru) | Обсуждение (русский); также на **[irc.mibbit.net#archlinux-ru](irc://irc.mibbit.net/archlinux-ru)** |
| [#archlinux-rs](ircs://chat.freenode.net/archlinux-rs) | Обсуждение (сербский) |
| [#archlinux-es](ircs://chat.freenode.net/archlinux-es) | Обсуждение (испанский) |
| [#archlinux.se](ircs://chat.freenode.net/archlinux.se) | Обсуждение (шведский) |
| [#archlinux-tr](ircs://chat.freenode.net/archlinux-tr) | Discussion (турецкий) |
| [#archlinux-ve](ircs://chat.freenode.net/archlinux-ve) | Обсуждение (Венесуэла) |
| [#archlinuxvn](ircs://chat.freenode.net/archlinuxvn) | Обсуждение (вьетнамский, Tiếng Việt) |