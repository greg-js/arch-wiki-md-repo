**Состояние перевода:** На этой странице представлен перевод статьи [General troubleshooting](/index.php/General_troubleshooting "General troubleshooting"). Дата последней синхронизации: 23 октября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=General_troubleshooting&diff=0&oldid=406300).

General troubleshooting - Устранение общих неполадок в системе. Эта статья дает советы по устранению общих проблем. Для решения проблем, связанных с конкретной программой, посетите соответствующую страницу Wiki.

## Contents

*   [1 Внимание к деталям](#.D0.92.D0.BD.D0.B8.D0.BC.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA_.D0.B4.D0.B5.D1.82.D0.B0.D0.BB.D1.8F.D0.BC)
*   [2 Вопросы / перечень](#.D0.92.D0.BE.D0.BF.D1.80.D0.BE.D1.81.D1.8B_.2F_.D0.BF.D0.B5.D1.80.D0.B5.D1.87.D0.B5.D0.BD.D1.8C)
*   [3 Более конкретно](#.D0.91.D0.BE.D0.BB.D0.B5.D0.B5_.D0.BA.D0.BE.D0.BD.D0.BA.D1.80.D0.B5.D1.82.D0.BD.D0.BE)
*   [4 Дополнительная поддержка](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BF.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0)
*   [5 Разрешения сессии](#.D0.A0.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D0.B5.D1.81.D1.81.D0.B8.D0.B8)
*   [6 Проблемы загрузки](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
*   [7 Файл: не может быть найден файл!](#.D0.A4.D0.B0.D0.B9.D0.BB:_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B6.D0.B5.D1.82_.D0.B1.D1.8B.D1.82.D1.8C_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD_.D1.84.D0.B0.D0.B9.D0.BB.21)
*   [8 Fuser](#Fuser)
*   [9 Почему я не могу записывать на NTFS разделы?](#.D0.9F.D0.BE.D1.87.D0.B5.D0.BC.D1.83_.D1.8F_.D0.BD.D0.B5_.D0.BC.D0.BE.D0.B3.D1.83_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D1.8B.D0.B2.D0.B0.D1.82.D1.8C_.D0.BD.D0.B0_NTFS_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D1.8B.3F)
*   [10 Проверка орфографии помечает весь мой текст как с ошибками!](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BE.D1.80.D1.84.D0.BE.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D0.B8_.D0.BF.D0.BE.D0.BC.D0.B5.D1.87.D0.B0.D0.B5.D1.82_.D0.B2.D0.B5.D1.81.D1.8C_.D0.BC.D0.BE.D0.B9_.D1.82.D0.B5.D0.BA.D1.81.D1.82_.D0.BA.D0.B0.D0.BA_.D1.81_.D0.BE.D1.88.D0.B8.D0.B1.D0.BA.D0.B0.D0.BC.D0.B8.21)
*   [11 Проблемы с GTK-приложениями](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_GTK-.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8)
*   [12 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Внимание к деталям

Для того чтобы решить проблему *абсолютно необходимо* твёрдо понимать конкретные функции системы. Как это работает, и что нужно для запуска без ошибок? Если вы не можете ответить на эти вопросы, то настоятельно рекомендуется к рассмотрению [Archwiki](/index.php/Table_of_contents_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Table of contents (Русский)") статьи, для функций с которыми у вас проблемы. После того, как вы почувствуете, что поняли систему, вам будет проще с решением точечных проблем.

## Вопросы / перечень

Для вас ниже приведён ряд вопросов , когда дело обстоит с неисправной системой. Под каждым вопросом есть замечания, объясняющие, как вы должны ответить на каждый вопрос, и несколько лёгких способов, о том как собрать данные вывода, и какие инструменты могут быть использованы для обзора логов и журналов.

1.  В чем проблема(ы)?

    	Будьте *как можно точнее*. Это поможет вам не запутаться и/или не отвлекаться при поиске конкретной информации.

2.  Есть ли сообщения об ошибках? (какие-нибудь)

    	Скопируйте и вставьте *полный вывод*, который содержит **сообщения об ошибках** связанных с вашим вопросом в отдельный файл, например `$HOME/issue.log`. Как пример, направьте вывод следующей команды [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") в файл `$HOME/issue.log`:

    	 `$ mkinitcpio -p linux >> $HOME/issue.log` 

3.  Можете ли вы воспроизвести проблему?

    	Если да, то предоставьте для этого *точные* **шаг-за-шагом** инструкции/команды.

4.  Что было изменено с момента работы системы без ошибок, до момента когда вы впервые столкнулись с проблемой?

    	Если это произошло сразу после обновления, то смотрите список **всех пакетов, которые были обновлены**. Включая *номера версий*, а также вставьте весь журнал обновления [pacman](/index.php/Pacman "Pacman").log (`/var/log/pacman.log`). Кроме того, примите к сведению статус *любого* сервиса(ов) необходимого(ых) для работы неисправной программы, с помощью инструментов [systemd](/index.php/Systemd "Systemd")'а systemctl. Например, чтобы направить вывод из следующих [systemd](/index.php/Systemd#Basic_systemctl_usage "Systemd") команд в `$HOME/issue.log`:

    	 `$ systemctl status dhcpcd@eth0.service >> $HOME/issue.log` 

    **Обратите внимание:** Использование `**>>**` не перезапишет существующий текст в `$HOME/issue.log`.

## Более конкретно

При попытке решить проблему, **никогда** не подходите к ней как:

*Приложение X не работает.*

Напротив, посмотрите на проблему в полном объеме:

*Приложение X даёт Y ошибку(и) при выполнении Z при условии A и B*.

Например: LibreOffice(X) не даёт навести курсор(Y) при выборе меню(Z) в xmonad(A).

## Дополнительная поддержка

Вся информация перед вами. Вы должны иметь хорошее представление о том, что происходит с системой. Теперь можете начать работать над исправлениями.

Если вам нужна дополнительная поддержка, обратитесь на [[форум](http://archlinux.org.ru/forum/%7CРусскоязычный)].

## Разрешения сессии

**Обратите внимание:** Вы должны использовать [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") в качестве системы инициализации работы локальных сеансов, - которая необходима для разрешения polkit и ACL для различных устройств (смотрите `/usr/lib/udev/rules.d/70-uaccess.rules` и [[1]](http://enotty.pipebreaker.pl/2012/05/23/linux-automatic-user-acl-management/))

Во-первых, убедитесь, что у вас есть действующий локальный сеанс X:

```
$ loginctl show-session $XDG_SESSION_ID

```

Должны получить на выходе `Remote=no` и `Active=yes`. Если это не так, убедитесь, что X работает на томже tty, где и произошел вход. Это нужно чтобы сохранить сеанс logind. Который обрабатывается по умолчанию `/etc/X11/xinit/xserverrc`.

Сессия D-Bus также должна быть запущена вместе с X. Смотрите больше информации по [D-Bus#Starting the user session](/index.php/D-Bus#Starting_the_user_session "D-Bus").

Основные [polkit](/index.php/Polkit "Polkit") действия не требуют дальнейшей настройки. Некоторые действия polkit требуют дальнейшей проверки подлинности, даже при местной сессии. Для этой работы агент аутентификации polkit должен быть запущен. Смотрите больше информации по [polkit#Authentication agents](/index.php/Polkit#Authentication_agents "Polkit").

## Проблемы загрузки

Смотрите [Boot debugging](/index.php/Boot_debugging "Boot debugging").

## Файл: не может быть найден файл!

*Пример:* После обычного ежедневного обновления, или после установки пакета, вы получаете следующее сообщение об ошибке:

```
# file: could not find ... (не может быть найден такой-то файл)!

```

Это, скорее всего, оставит систему поломанной. И любые попытки сделать пересборку/переустановку пакета(ов) ничего не дадут. Кроме того, любые попытки, чтобы попытаться пересобрать [initramfs](/index.php/Initramfs "Initramfs") приведут в дальнейшем к ошибке:

```
# mkinitcpio -p linux
==> Building image from preset: 'default'
 -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux.img
file: could not find any magic files!
==> ERROR: invalid kernel specifier: `/boot/vmlinuz-linux'
==> Building image from preset: 'fallback'
 -> -k /boot/vmlinuz-linux -c /etc/mkinitcpio.conf -g /boot/initramfs-linux-fallback.img -S autodetect
file: could not find any magic files!
@==> ERROR: invalid kernel specifier: `/boot/vmlinuz-linux'

```

Установленное ранее приложение поместило файл настроек в пределах `/etc/ld.so.conf.d/` или оно внесло изменения в `/etc/ld.so.conf`, которые в настоящий момент недействительны.

1.  Загрузитесь с установочного носителя Arch Linux Live CD.
2.  Смонтируйте корневой раздел (`**/**`) в `/mnt` и воспользуйтесь [arch-chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_arch-chroot "Change root (Русский)"), [chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Change root (Русский)") в вашей системе.

**Обратите внимание:** [arch-chroot](/index.php/Change_root_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_arch-chroot "Change root (Русский)") leaves mounting the `/boot` partition up to the user.

1.  Исследуйте `/etc/ld.so.conf` и удалите любые найденные неверные строки.
2.  Исследуйте файлы расположенные в каталоге `/etc/ld.so.conf.d/` и удалите все неверные файлы.
3.  Пересоберите [initramfs](/index.php/Mkinitcpio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0 "Mkinitcpio (Русский)").

```
# mkinitcpio -p linux

```

1.  Перезагрузитесь обратно в установленную систему.
2.  После загрузки, установите пакет который привёл систему в нерабочее состояние:

```
# pacman -S <пакет>

```

## Fuser

*fuser* это утилита командной строки для обнаружения процессов, использующих ресурсы, такие как файлы, файловые системы и порты TCP/UDP.

*fuser* находится в пакете [psmisc](https://www.archlinux.org/packages/?name=psmisc), который уже должен быть установлен как часть группы [base](https://www.archlinux.org/groups/x86_64/base/).

## Почему я не могу записывать на NTFS разделы?

В чистой системе вы можете только читать из файловой системы NTFS. Если хотите записывать, установите пакет [ntfs-3g](https://www.archlinux.org/packages/?name=ntfs-3g).

## Проверка орфографии помечает весь мой текст как с ошибками!

Вы установили [aspell](https://www.archlinux.org/packages/?name=aspell) словарь? Воспользуйтесь `pacman -Ss aspell` чтобы увидеть доступные словари для скачивания.

Если после установки словарей проблема не решена, то скорее всего это проблема с `enchant`. Проверьте известные файлы словарей:

 `$ aspell dicts` 
```
ru
ru_RU
... и т.д.
```

Если соответствующий словарь языка в списке, добавьте его в `/usr/share/enchant/enchant.ordering`. Из приведенного выше примера, сделайте так:

```
ru_RU:aspell

```

## Проблемы с GTK-приложениями

Если у вас наблюдаются следующие (или другие) симптомы :

*   Чёрная рамка вокруг приложений GTK
*   Двойная тень (см. раздел [клиентские декорации](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82.D1.81.D0.BA.D0.B8.D0.B5_.D0.B4.D0.B5.D0.BA.D0.BE.D1.80.D0.B0.D1.86.D0.B8.D0.B8 "GTK+ (Русский)"), для решения)
*   Различные темы приложений между GTK+ 2 и GTK+ 3
*   Не соответствует цвет фона в строке заголовка (TitleBar)
*   Неправильный фокус событий в тайловых оконных менеджерах

Смотрите раздел [решение проблем с GTK+](/index.php/GTK%2B_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC "GTK+ (Русский)")

## Смотрите также

*   [IRC Collaborative Debugging](/index.php/IRC_Collaborative_Debugging "IRC Collaborative Debugging")
*   [Step-by-step debugging guide](/index.php/Step-by-step_debugging_guide "Step-by-step debugging guide")
*   [Fix the Most Common Problems](http://www.maximumpc.com/article/features/linux_troubleshooting_guide_fix_most_common_problems)
*   [A how-to in troubleshooting for newcomers](https://www.reddit.com/r/archlinux/comments/tjjwr/archlinux_a_howto_in_troubleshooting_for_newcomers/)