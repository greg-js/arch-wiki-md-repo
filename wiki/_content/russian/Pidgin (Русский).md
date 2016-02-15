**Состояние перевода:** На этой странице представлен перевод статьи [Pidgin](/index.php/Pidgin "Pidgin"). Дата последней синхронизации: 2015-07-29\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Pidgin&diff=0&oldid=382084).

С домашней страницы [проекта](http://www.pidgin.im/):

	_Pidgin - это простой в использовании свободный чат клиент, используемый миллионами. Подключение к AIM, MSN, Yahoo и другим чат сетям в одном флаконе._

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Проверка правописания](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D1.80.D0.B0.D0.B2.D0.BE.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F)
*   [3 Исправление звука](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B2.D1.83.D0.BA.D0.B0)
*   [4 Ошибка веб браузера](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.B2.D0.B5.D0.B1_.D0.B1.D1.80.D0.B0.D1.83.D0.B7.D0.B5.D1.80.D0.B0)
*   [5 Ошибка кодировки QIP](#.D0.9E.D1.88.D0.B8.D0.B1.D0.BA.D0.B0_.D0.BA.D0.BE.D0.B4.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B8_QIP)
*   [6 ICQ](#ICQ)
*   [7 IRC](#IRC)
*   [8 Xfire](#Xfire)
*   [9 Web QQ](#Web_QQ)
*   [10 Facebook XMPP](#Facebook_XMPP)
*   [11 Конфиденциальность](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B4.D0.B5.D0.BD.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [11.1 Pidgin-OTR](#Pidgin-OTR)
    *   [11.2 Pidgin-Encryption](#Pidgin-Encryption)
    *   [11.3 Pidgin-GPG](#Pidgin-GPG)
*   [12 Sametime протокол](#Sametime_.D0.BF.D1.80.D0.BE.D1.82.D0.BE.D0.BA.D0.BE.D0.BB)
*   [13 SIP/Simple protocol for Live Communications Server 2003/2005/2007](#SIP.2FSimple_protocol_for_Live_Communications_Server_2003.2F2005.2F2007)
*   [14 Другие пакеты](#.D0.94.D1.80.D1.83.D0.B3.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
*   [15 Плагин Skype](#.D0.9F.D0.BB.D0.B0.D0.B3.D0.B8.D0.BD_Skype)
*   [16 Автоматический выход перед гибернацией](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4_.D0.B3.D0.B8.D0.B1.D0.B5.D1.80.D0.BD.D0.B0.D1.86.D0.B8.D0.B5.D0.B9)
*   [17 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [17.1 Установка Pidgin после установки Carrier](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Pidgin_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_Carrier)
*   [18 Импорт истории Kopete в Pidgin](#.D0.98.D0.BC.D0.BF.D0.BE.D1.80.D1.82_.D0.B8.D1.81.D1.82.D0.BE.D1.80.D0.B8.D0.B8_Kopete_.D0.B2_Pidgin)
*   [19 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [pidgin](https://www.archlinux.org/packages/?name=pidgin). Также есть варианты:

*   **Pidgin Light** — Лёгкая версия Pidgin без GStreamer, Tcl/Tk, XScreenSaver, поддержки видео/голоса.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

Вы также можете установить дополнительные плагины из [purple-plugin-pack](https://www.archlinux.org/packages/?name=purple-plugin-pack).

## Проверка правописания

Aspell будет установлен как зависимость, но для предотвращения отображения текста как некорректный вам нужно установить aspell словарь, например [aspell-ru](https://www.archlinux.org/packages/?name=aspell-ru). Чтобы посмотреть список доступных языков, воспользуйтесь командой `pacman -Ss aspell`.

Если проверка правописания не работает, попробуйте запустить aspell отдельно, чтобы проверить что он установлен корректно и не выдаёт полезное сообщения об ошибке.

```
$ echo center | aspell -a

```

**Обратите внимание:** Плагин **switch spell**-входит в состав пакета [purple-plugin-pack](https://www.archlinux.org/packages/?name=purple-plugin-pack). Он позволяет переключатся между разными языками.

## Исправление звука

Для того чтобы звук заработал, необходимо установить пакет [gstreamer0.10-good](https://www.archlinux.org/packages/?name=gstreamer0.10-good). Альтарнативно, на вкладке настроек "Звуки" можно задать метод 'команда' и использовать одну из следующих команд.

После настройки [ALSA](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)"):

```
$ aplay %s

```

Если используется [OSS](/index.php/OSS "OSS"):

```
$ ossplay %s

```

И для [PulseAudio](/index.php/PulseAudio_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PulseAudio (Русский)"):

```
$ paplay %s

```

## Ошибка веб браузера

Если при клике по ссылке Pidgin генерирует ошибку про попытку использования 'sensible-browser' для открытия ссылки, попробуйте отредактировать `~/.purple/prefs.xml`. Найдите в файле строку, содержащую 'sensible-browser' и измените её на такую:

```
<pref name='command' type='path' value='firefox'/>

```

В этом примере предполагается, что вы используете [Firefox](/index.php/Firefox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Firefox (Русский)").

## Ошибка кодировки QIP

Еще одна ошибка кодировки символов, возникающая при взаимодействии Pidgin и QIP, которая, в особенности, касается чешского языка, но также есть и другие подверженные языки. Есть два возможных решения. Лучшее решение состоит в том, чтобы обновиться с QIP до QIP 2012 или QIP Infimum, второе решение - установить и включить плагин с помощью пакета [pidgin-qip-decoder](https://aur.archlinux.org/packages/pidgin-qip-decoder/).

## ICQ

Вы можете изменить кодировку для ICQ аккаунта, если кодировка в **Информация о собеседнике** некорректна:

```
Уч. записи > _ваш ICQ аккаунт_ > Редактировать аккаунт > вкладка Дополнительно

```

Выберите `Кодирование: CP1251` (для кириллицы).

## IRC

Это небольшая инструкция по подключению к Freenode. Она должна работать и для других IRC сетей, если вы впишите номер порта и другие специфичные настройки.

Перейдите в _Уч. записи > Управление учётными записями > Добавить_. Заполните/выберите следующие опции:

```
Протокол: IRC
Имя пользователя: _ваше имя пользователя_

```

Теперь перейдите в _Собеседники > Новое мгновенное сообщение_ (или нажмите `Ctrl+m`), введите 'freenode.net' в текстовое поле и _имяпользователя_@irc.freenode.net, затем нажмите 'Ok'. Введите:

```
/join #archlinux

```

Канал приведён в качестве примера.

Для регистрации вашего ника, введите:

```
/msg nickserv register _пароль_ _email-адрес_

```

Следуйте инструкциям в регистрационном письме. Для дальнейшей помощи введите:

```
/msg nickserv help
/msg nickserv help _command_

```

Последним шагом будет добавление вашего канала в 'Собеседники': перейдите в _Собеседники > Присоединиться к чату_, введите необходимый канал в тектовое поле Канал, например (#archlinux).

## Xfire

Просто установите [pidgin-gfire](https://www.archlinux.org/packages/?name=pidgin-gfire) и затем добавьте новый аккаунт, выбрав xfire в качестве протокола.

## Web QQ

Просто установите [pidgin-lwqq](https://www.archlinux.org/packages/?name=pidgin-lwqq) и затем добавьте новый аккаунт, выбрав webQQ в качестве протокола. QQ - это проприетарный чат протокол/IM сервис, в основном используемый в Азии, особенно в Китае.

## Facebook XMPP

Facebook XMPP был отключён 30 апреля 2015\. Смотрите [[1]](https://developers.facebook.com/docs/chat?_fb_noscript=1) Альтернативой является использование ThirdPartyPlugin, который использует Facebook IM, смотрите [[2]](https://github.com/jgeboski/purple-facebook)

## Конфиденциальность

В Pidgin есть некоторые настройки конфиденциальности по умолчанию. Например, вам не может написать любой землянин; только люди из ваших контактов или из выбранного списка. Для изменения этих настроек перейдите в меню

```
Средства > Конфиденциальность

```

### Pidgin-OTR

Это плагин, предоставляющий возможность Off-The-Record (OTR) переписки в Pidgin. OTR - это криптографический протокол, который шифрует ваши мгновенные сообщения.

Сначала вы должны установить [pidgin-otr](https://www.archlinux.org/packages/?name=pidgin-otr) из официальных репозиториев. После того как это будет сделано, OTR будет добавлен в Pidgin.

1.  Для включения OTR, запустите Pidgin, и перейдите в _Средства_ > _Модули_ или нажмите `Ctrl+u`. Прокрутите вниз до записи "Off-The-Record Messaging". Если относящийся к ней чекбокс не отмечен, отметьте его.
2.  Далее, выделите строку с плагином и нажмите кнопку "Настроить модуль" внизу окна. Выберите аккаунт, для которого вы хотите создать ключ, затем нажмите "Создать". Теперь у вас есть только что сгенерированный приватный ключ. Если вы не понимаете что делают другие опции, оставьте их как есть, поскольку опции по умолчанию будут нормально работать.
3.  Следующим шагом вы должны связаться с собеседником, который тоже установил OTR. В окне этого чата должна появиться новая иконка справа сверху от текстового поля ввода. Нажмите на неё и выберите "Начать приватную беседу". Теперь начнётся 'Неподтверждённая' сессия. Неподтверждённые сессии зашифрованы, но не подтверждены, то есть вы начали приватную беседу с кем-то, кто использует аккаунт вашего собеседника с установленным OTR, но может являться не вашим собеседником. Инструкции по верификации собеседника выходят за рамки данного раздела, однако они могут быть добавлены в дальнейшем.

### Pidgin-Encryption

[pidgin-encryption](https://www.archlinux.org/packages/?name=pidgin-encryption) прозрачно для вас шифрует ваши мгновенные сообщения с помощью RSA шифрования. Легко в использовании и очень безопасно.

Вы можете включить его таким же образом, как и Pidgin-OTR.

Теперь вы можете открыть окно беседы и там должна появиться иконка рядом с меню. Нажмите её для включения или выключения шифрования. Если вы хотите, чтобы шифрование включалось автоматически, нажмите правой клавишей мыши на имени собеседника (в вашем контакт листе) и выберите Включить Автоматическое шифрование Да. Теперь, когда будет открываться новое окно диалога с этим собеседником, шифрование включится автоматически.

### Pidgin-GPG

Pidgin-GPG прозрачно для вас шифрует разговоры, используя GPG, используя все преимущества и возможности предсуществующего WoT.

Плагин доступен в AUR как [pidgin-gpg](https://aur.archlinux.org/packages/pidgin-gpg/). Включается так же, как описано выше для предыдущих плагинов.

## Sametime протокол

Поддержка протокола Sametime появится после установки двух пакетов из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"):

*   [meanwhile](https://aur.archlinux.org/packages/meanwhile/)
*   [libpurple-meanwhile](https://aur.archlinux.org/packages/libpurple-meanwhile/)

Раньше приходилось пересобирать Pidgin, убрав флаг компиляции `--disable-meanwhile`, теперь этого не требуется. После установки этих двух пакетов протокол 'Sametime' будет доступен при создании учётной записи.

## SIP/Simple protocol for Live Communications Server 2003/2005/2007

Установите плагин [pidgin-sipe](https://www.archlinux.org/packages/?name=pidgin-sipe) из [официальных репозиториев](/index.php/%D0%9E%D1%84%D0%B8%D1%86%D0%B8%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D1%80%D0%B5%D0%BF%D0%BE%D0%B7%D0%B8%D1%82%D0%BE%D1%80%D0%B8%D0%B8 "Официальные репозитории").

## Другие пакеты

В репозиториях Arch Linux есть и другие пакеты, связанные с Pidgin. Здесь представлены самые популярные:

*   [pidgin-libnotify](https://www.archlinux.org/packages/?name=pidgin-libnotify) - поддержка [libnotify](https://www.archlinux.org/packages/?name=libnotify) для того, чтобы уведомления соответствовали системной теме
*   [guifications](https://www.archlinux.org/packages/?name=guifications) - всплывающие уведомления в стиле Toaster
*   [microblog-purple](https://aur.archlinux.org/packages/microblog-purple/) - плагин [libpurple](https://www.archlinux.org/packages/?name=libpurple) для поддержки сервисов микроблогов типа twitter
*   [pidgin-latex](https://aur.archlinux.org/packages/pidgin-latex/) - небольшой latex-плагин для Рidgin. Разместите между `$$` математическое выражение, и оно будет обработано (получатель тоже должен установить этот плагин)

## Плагин Skype

Установите пакет [skype4pidgin-git](https://aur.archlinux.org/packages/skype4pidgin-git/) или [purple-skypeweb-git](https://aur.archlinux.org/packages/purple-skypeweb-git/).

## Автоматический выход перед гибернацией

Если вы отправляете ваш компьютер спать, собеседникам будет казаться, что вы всё ещё онлайн около 15 минут. Для предотвращения потери сообщений, вам нужно установить статус в оффлайн перед тем как отправить компьютер в сон или гибернировать. Ваш статусное сообщение не изменится.

Для автоматизации этого, создайте новый systemd юнит `pidgin-suspend` в `/etc/systemd/system` Возьмите следующую заготовку и замените _myuser_ на вашего пользователя.

```
[Unit]
Description=Suspend Pidgin
Before=sleep.target
StopWhenUnneeded=yes

[Service]
Type=oneshot
User=_myuser_
RemainAfterExit=yes
Environment=DISPLAY=:0
ExecStart=-/usr/bin/purple-remote setstatus?status=offline
ExecStop=-/usr/bin/purple-remote setstatus?status=available

[Install]
WantedBy=sleep.target

```

Если вы используете [pm-utils](/index.php/Pm-utils_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pm-utils (Русский)"), то вы вместо этого можете создать файл `00pidgin` в `/etc/pm/sleep.d/`.

```
#!/bin/sh
#
# 00pidgin: set offline/online status

case "$1" in
    hibernate|suspend)
        DISPLAY=:0 su -c 'purple-remote setstatus?status=offline' ''%myuser''
    ;;
    thaw|resume)
        DISPLAY=:0 su -c 'purple-remote setstatus?status=available' ''%myuser''
    ;;
    *) exit $NA
    ;;
esac

```

## Решение проблем

### Установка Pidgin после установки Carrier

Если вы перед этим устанавливали [carrier](https://aur.archlinux.org/packages/carrier/) (также известный как [FunPidgin](http://funpidgin.sourceforge.net/)), следуйте следующим инструкциям _до_ установки Pidgin:

*   Выйдите из Carrier
*   Удалите директорию `~/.purple`.

**Важно:** Это сотрёт все ваши настройки пользователя для всех программ, которые используют libpurple, например Pidgin, Carrier и так далее.

```
rm -r ~/.purple

```

*   Деинсталлируйте **carrier** и **libpurple**.
*   Установите **pidgin** и **libpurple**.

## Импорт истории Kopete в Pidgin

*   Установите [xalan-c](https://www.archlinux.org/packages/?name=xalan-c) и создайте `~/bin/history_import_kopete2pidgin.sh` со следующим содержимым:

```
#!/bin/sh

KOPETE_DIR=~/.kde4/share/apps/kopete/logs
PIDGIN_DIR=~/.purple/logs
CURRENT_DIR=~/bin

cd

if [ ! -d $KOPETE_DIR ];then
    echo "Kopete log directory not found"
    exit 1;
fi

if [ ! -d $PIDGIN_DIR ];then
    echo "Pidgin log directory not found"
    exit 2;
fi

for KOPETE_PROTODIR in $(ls $KOPETE_DIR); do
    PIDGIN_PROTODIR=$(echo $KOPETE_PROTODIR | sed 's/Protocol//' | tr [:upper:] [:lower:])
    for accnum in $(ls $KOPETE_DIR/$KOPETE_PROTODIR); do
        echo "Account number: $accnum"
        for num in $(ls $KOPETE_DIR/$KOPETE_PROTODIR/$accnum); do
            FILENAME=$(Xalan $KOPETE_DIR/$KOPETE_PROTODIR/$accnum/$num $CURRENT_DIR/history_import_kopete2pidgin_filename.xslt)
            if [ $? = 0 ]; then
                echo "$KOPETE_DIR/$KOPETE_PROTODIR/$accnum/$num"
                echo " -> $PIDGIN_DIR/$PIDGIN_PROTODIR/$FILENAME"
                mkdir -p $(dirname $PIDGIN_DIR/$PIDGIN_PROTODIR/$FILENAME)
                Xalan -o $PIDGIN_DIR/$PIDGIN_PROTODIR/$FILENAME $KOPETE_DIR/$KOPETE_PROTODIR/$accnum/$num $CURRENT_DIR/history_import_kopete2pidgin.xslt
            fi
        done
    done
done

```

*   Сделайте файл `~/bin/history_import_kopete2pidgin.sh` исполняемым:

```
chmod +x ~/bin/history_import_kopete2pidgin.sh

```

*   Создайте файл `~/bin/history_import_kopete2pidgin.xslt` со следующим содержимым:

```
<?xml version="1.0"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="text" indent="no" />

    <xsl:template match="kopete-history">
        <xsl:apply-templates select="msg"/>
    </xsl:template>

    <xsl:template match="msg">
        <xsl:text>(</xsl:text>
        <xsl:value-of select="translate(substring-after(@time,' '),':',',')"/>
        <xsl:text>) </xsl:text>
        <xsl:value-of select="@nick"/>
        <xsl:if test="not(@nick) or @nick = _">_
            <xsl:value-of select="@from"/>
        </xsl:if>
        <xsl:text>: </xsl:text>
        <xsl:value-of select="."/>
		<xsl:text>
</xsl:text>
    </xsl:template>
</xsl:stylesheet>
</nowiki>
```

*   Создайте файл `~/bin/history_import_kopete2pidgin_filename.xslt` со следующим содержимым:

```
<?xml version="1.0"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
    <xsl:output method="text" indent="no" />

    <xsl:template match="kopete-history">
        <xsl:value-of select="head/contact[@type = 'myself']/@contactId"/>
        <xsl:text>/</xsl:text>
        <xsl:value-of select="head/contact[not(@type)]/@contactId"/>
        <xsl:text>/</xsl:text>
        <xsl:value-of select="head/date/@year"/>
        <xsl:text>-</xsl:text>
        <xsl:if test="head/date/@month &lt; 10">0</xsl:if>
        <xsl:value-of select="head/date/@month"/>
        <xsl:text>-</xsl:text>
        <xsl:if test="string-length(substring-before(msg[1]/@time,' ')) &lt; 2">0</xsl:if>
        <xsl:value-of select="translate(msg[1]/@time,' :','.')"/>
        <xsl:text>+0200EET.txt</xsl:text>
    </xsl:template>
</xsl:stylesheet>
```

*   Выполните следующую команду в shell:

```
~/bin/history_import_kopete2pidgin.sh

```

## Смотрите также

*   [Pidgin homepage](http://pidgin.im)
*   [History import Kopete to Pidgin](http://lukav.com/wordpress/2008/03/30/history-import-kopete-to-pidgin)