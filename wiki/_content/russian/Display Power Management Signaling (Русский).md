**DPMS** (Display Power Management Signaling, сигналы управления энергопотреблением дисплеев) - это технология, позволяющая управлять питанием монитора, когда компьютер не используется.

## Настройка DPMS в X

Добавьте следующие строки в `/etc/X11/xorg.conf`: в секцию `Monitor`:

```
Option "DPMS" "true"

```

в секцию `ServerLayout`, измените, как считаете нужным время (в минутах):

```
Option "StandbyTime" "10"
Option "SuspendTime" "20"
Option "OffTime" "30" 

```

## Взаимодействие DPMS и xset

Можно выключать монитор, используя утилиту `xset`:

```
xset dpms force standby

```

устанавливает экран(ы) в режим ожидания,

```
xset dpms force suspend

```

переводит их в спящий режим и

```
xset dpms force off

```

выключает их немедленно. Если вы оставляете компьютер, вам не обязательно ждать, пока истечёт время ожидания, которое вы установили для выключения монитора. Просто сделайте это сразу, используя команду xset.

Также вы можете скопировать этот код в /usr/local/bin/display.sh:

```
#!/bin/bash
#
# Small script to set display into standby, suspend or off mode
# 20060301-Joffer
#

XSET=/usr/bin/xset

if [ $1 ]; then
        if [ $1 = "standby" ] || [ $1 = "suspend" ] || [ $1 = "off" ]; then
                $XSET dpms force $1
        else
                echo "Usage: $0 standby|suspend|off"
                exit
        fi
else
        echo "$0 usage: $0 standby|suspend|off"
        exit
fi

```

Сделайте его исполняемым (<tt>chmod +x /usr/local/bin/display.sh</tt>) и запустите: <tt>display.sh off</tt>. Для того чтобы последняя команда работала, необходимо добавить /usr/local/bin в переменную PATH, иначе вам придётся запускать скрипт с указанием полного пути:

```
# С /usr/local/bin в переменной PATH
display.sh suspend

# Без /usr/local/bin в переменной PATH
/usr/local/bin/display.sh standby

```

Этот маленький скрипт, возможно, может выглядеть лучше (если хотите, исправьте его), но свою работу он выполняет отлично.

## Смотрите также

*   [Спецификация DPMS](http://webpages.charter.net/dperr/dpms.htm)