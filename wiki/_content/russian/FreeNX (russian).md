## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Сервер](#.D0.A1.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
        *   [2.1.1 Ключи](#.D0.9A.D0.BB.D1.8E.D1.87.D0.B8)
        *   [2.1.2 Запуск сервера](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80.D0.B0)
    *   [2.2 Клиент](#.D0.9A.D0.BB.D0.B8.D0.B5.D0.BD.D1.82)
        *   [2.2.1 Arch Linux](#Arch_Linux)
        *   [2.2.2 Windows](#Windows)
        *   [2.2.3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_2)
*   [3 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
    *   [3.1 Горячие клавиши](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
    *   [3.2 Выход из полноэкранного режима](#.D0.92.D1.8B.D1.85.D0.BE.D0.B4_.D0.B8.D0.B7_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0)
    *   [3.3 Советы по возобновлению](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.BF.D0.BE_.D0.B2.D0.BE.D0.B7.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8E)
    *   [3.4 Правка DPI настроек](#.D0.9F.D1.80.D0.B0.D0.B2.D0.BA.D0.B0_DPI_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
*   [4 Настройка менеджеров рабочего стола KDE или Gnome](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.BE.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0_KDE_.D0.B8.D0.BB.D0.B8_Gnome)
    *   [4.1 Alternative fix](#Alternative_fix)
*   [5 Problems](#Problems)
    *   [5.1 Отладка проблем](#.D0.9E.D1.82.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.2 Авторизация OK, соединение пропадает](#.D0.90.D0.B2.D1.82.D0.BE.D1.80.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_OK.2C_.D1.81.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.BF.D0.B0.D0.B4.D0.B0.D0.B5.D1.82)
    *   [5.3 Key changes](#Key_changes)
    *   [5.4 Xorg 7](#Xorg_7)
    *   [5.5 Wrong password / No connection possible](#Wrong_password_.2F_No_connection_possible)
        *   [5.5.1 NX Crashes on session startup](#NX_Crashes_on_session_startup)
    *   [5.6 NX logo then blank screen](#NX_logo_then_blank_screen)
    *   [5.7 GDM/XDM Session Menu Error with non-KDE or Gnome Desktop Managers (more common with non-Arch Linux users)](#GDM.2FXDM_Session_Menu_Error_with_non-KDE_or_Gnome_Desktop_Managers_.28more_common_with_non-Arch_Linux_users.29)

## Установка

Пакет разделён на две части:

*   freenx (сервер)
*   nxclient (клиент)

## Настройка

### Сервер

Открытая реализация сервера находится в пакете 'freenx'.

*   Чтобы разрешить вход на сервер, добавьте 'sshd' в список демонов в /etc/rc.conf.

Основной конфигурационный файл - /opt/NX/etc/node.conf. Если вы используете KDE или Gnome, то вам нет необходимости править этот файл, установки по умолчанию вам подходят. Если у вас другой оконный менеджер, такой как Fluxbox/Openbox или Xfce, вам может понадобиться слегка отредактировать этот файл (смотрите ниже).

#### Ключи

Ключи используются для аутентификации клиентов сервером. По умолчанию во время установки генерируется новый набор случайных ключей, один для сервера и один для клиентов. Вам понадобится скопировать этот клиентский ключ на каждую клиентскую машину (с Windows или Linux).

Клиентский ключ находится в файле /opt/NX/home/nx/.ssh/client.id_dsa.key.

Также вы можете использовать ключ по умолчанию, предоставляемый компанией NoMachine со всеми клиентами. В этом случае вам не нужно копировать сгенерированный ключ на каждую клиентскую машину. Чтобы сервер принимал дефолтный клиентский ключ, запустите

```
/opt/NX/bin/nxsetup --install --setup-nomachine-key --clean --purge

```

Пересоздать случайные ключи:

*   /opt/NX/bin/nxsetup --install --clean --purge

Перенести ключи на другой сервер freenx:

*   директория /opt/NX/home/nx/.ssh содержит файлы ключей

```
 -rw------- 1 nx root  697  9\. Okt 12:55 authorized_keys
 -rw------- 1 nx root  668  9\. Okt 11:48 client.id_dsa.key
 -rw------- 1 nx root  609  9\. Okt 12:55 server.id_dsa.pub.key

```

*   Сохраните эти файлы
*   Добавьте эти файла на новый сервер. Им нужны те же самые права доступа, имена, группа и директория!

```
 # cp authorized_keys client.id_dsa.key server.id_dsa.pub.key /opt/NX/home/nx/.ssh/
 # chmod 600 /opt/NX/home/nx/.ssh/*
 # chown nx /opt/NX/home/nx/.ssh/*
 # chgrp root /opt/NX/home/nx/.ssh/*

```

*   Пересоздайте файл known_hosts:

```
 # echo -n 127.0.0.1 > /opt/NX/home/nx/.ssh/known_hosts
 # cat /etc/ssh/ssh_host_rsa_key.pub >> /opt/NX/home/nx/.ssh/known_hosts
 # chmod 633 /opt/NX/home/nx/.ssh/known_hosts
 # chown nx /opt/NX/home/nx/.ssh/known_hosts
 # chgrp root /opt/NX/home/nx/.ssh/known_hosts

```

#### Запуск сервера

После установки для запуска сервера не надо делать ничего вручную, он уже запущен. Единственная служба, которая необходима для соединения - sshd.

В действительности, если вы проверите список процессов (`ps aux`), вы не увидите запущенного nxserver. Причина в том, что nxserver действительно стартует только при входе в sshd специального пользователя 'nx'. В качестве оболочки (shell) для этого пользователя указан nxserver, так же, как для обычных пользователей указан bash.

### Клиент

#### Arch Linux

Загрузите клиент с помощью pacman:

```
pacman -S nxclient

```

#### Windows

Загрузите клиент с сайта компании Nomachine: [http://www.nomachine.com](http://www.nomachine.com)

Замечание: Nomachine собирается удалить старые клиенты с сайта, так что если ваша установка работает, сохраните её в надёжное место. :)

#### Настройка

Как упомянуто выше, клиент должен содержать правильный ключ для доступа к серверу. Если вы используете сгенерированные вами во время установки ключи, вам необходимо скопировать клиентский ключ в следующее месторасположение:

*   Windows: `<yourinstalldironwindows>/share/keys/client.id_dsa.key`
*   Arch Linux: `/opt/NX/share/keys/client.id_dsa.key`

После помещения ключей вам возможно придётся импортировать их с помощью nxclient GUI. В конфигурационном диалоге нажмите кнопку 'Key...' и импортируйте новый клиентский ключ.

## Запуск

### Горячие клавиши

```
CTR+ALT+F          Переключить полноэкранный режим. 
CTRL+ALT+T         Показать диалог завершения или приостановления сессии.
CTRL+ALT+M         Максимизировать или минимизировать окно.
CTRL+ALT+Mouse     Drags the viewport, so you can view different portions 
                   of the desktop. 
CTRL+ALT+Arrows 
or                 Moves the viewport by an incremental amount of pixels. 
CTRL+ALT+Keypad 
CTRL+ALT+S         It will activate "screen-scraping" mode, so all the GetImage
                   originated by the clients will be forwarded to the real
                   display. This should make happy those who love taking
                   screenshots ;-). By pressing the sequence again, nxagent
                   will revert to the usual "fast" mode.
CTRL+ALT+E         Ленивое кодирование изображений.
CTRL+ALT+Shift+ESC Экстренный выход и закрытие окна.

```

### Выход из полноэкранного режима

Существует магический пиксель в верхнем правом углу, где обычно находится панель работы с окошкой в nx-приложениях в полноэкранном режиме. Кликните по нему правой кнопкой мыши и в приложении в этом углу появится панель управления.

### Советы по возобновлению

*   Возобновление - это немного экспериментов, и "падения" после восстановления сессии могут показать какие приложения успешно восстанавливаются, а какие нет.
*   Восстановления между сессиями Linux и Windows не работают.
*   Если восстановление неудачно, то подождите немного, не нажимайте кнопку Cancel/Отмена иначе сессии останутся открытыми и будут в холостую занимать оперативную память на сервере. Чтобы завершить сессию, используйте программу Session Admin для убийства нужного процесса.

### Правка DPI настроек

Если Вы хотите себе одинаковые размеры шрифтов и dpi во всех Ваших клиентских сессиях, поправьте файл для Х-сервера под названием "Xft.dpi". К примеру, добавленная строка "Xft.dpi: 100" в "~/.Xresources" сделает на десктопе 100dpi.

## Настройка менеджеров рабочего стола KDE или Gnome

Перед тем как делать что-нибудь из этого раздела, убедитесь, что сервер работает и подключения к нему разрешены. Далее будут решения проблем связанных с NXClient.

Вот простой пример подключения к сессиям Gnome и KDE, однако,процесс подключения к другим оконными менеджерам, типа fluxbox, xfce и whatever несколько отличается.

Выберите "custom" и используйте команду "startx", далее появится один из двух результатов: на пустом экране после лого !М или клиентская часть сообщит об ошибке, связанной с Х-сервером. Если команда "startx" не сработала, то используйте другую команду для запуска вашего оконного менеджера.

#### Alternative fix

A simple fix without resorting to the above seems to involve a simple edit to the config file. This should work for fluxbox/openbox/xfce or any other window manager that uses the **.xinitrc** startup file in a call to **startx**.

Simply edit the config file (as root):

```
/opt/NX/etc/node.conf

```

and change

```
#USER_X_STARTUP_SCRIPT=.Xclients

```

to

```
USER_X_STARTUP_SCRIPT=.xinitrc

```

Remember to remove the # symbol from the start of the line.

Then in the client under configuration settings, choose **Custom** as the desktop, and click on settings:

*   In the first group select - **`Run the default X client Script on server`**
*   In the second group select - **`New virtual desktop`**

## Problems

### Отладка проблем

Редактируйте конфиг nxserver :

```
 vi /opt/NX/etc/node.conf

```

Измените:

```
 #SESSION_LOG_CLEAN=1

```

на

```
 SESSION_LOG_CLEAN=0

```

Тогда вы сможете смотреть/отлаживать лог файл

```
 $HOME/.nx/T-C-<hostname>-<display>-<session-id>

```

Для удачных соединений:

```
 $HOME/.nx/F-C-<hostname>-<display>-<session-id>

```

Для неудачных.

### Авторизация OK, соединение пропадает

Если вы пытаетесь startkde

```
 vi /opt/NX/etc/node.conf

```

Ищите:

```
 COMMAND_START_KDE=startkde

```

Замените на:

```
 COMMAND_START_KDE=/opt/kde/bin/startkde

```

### Key changes

Change the key in GUI setup to new generated key.

### Xorg 7

Be aware that you have to remove the /usr/X11R6 directory, else strange things can happen.

### Wrong password / No connection possible

*   If you get always wrong password or no connection after authentication was done and you are sure that you typed it correct, check that your server can connect to itself using localhost by ssh and that it is not blocked either by /etc/hosts.deny or not allowed by /etc/hosts.allow.

*   If you messed up your key files, create new ones or fix the old ones, it's probably caused by a wrong known_hosts file.

#### NX Crashes on session startup

If your NX Client shows the NX logo then disappears with a Connection Problem dialog afterwards.

Then it could be due to missing fonts. Mostly applies if you have installed Arch Linux base and then installed freenx after without the whole X11 set.

Solution until FreeNX Dependencies is fixed is to install xorg-fonts-misc on your NX Server (pacman -S xorg-fonts-misc) and your NX should work.

Note: This does not apply to freenx 0.6.1-3 and above, fix has been incorporated in it and following versions.

### NX logo then blank screen

If you see the NX logo (!M) then a blank screen.

This problem can be solved by running a login manager- The problem is that X11 is not started, and it appears that "startx" or similar do not work from the freenx client. Follow these instructions to setup a login manager and load it at startup: [Display manager](/index.php/Display_manager "Display manager")

Blind: If this does not resolve your issues, be aware that freenx and bash_completion do not play well together. I only got things to work after removing bash_completion from the .bashrc.

### GDM/XDM Session Menu Error with non-KDE or Gnome Desktop Managers (more common with non-Arch Linux users)

Problem: A session menu comes up talking about "chooseSessionListWidget." A window manager never loads.

Fix :

Double check to see if ~/.xinitrc is executable.

```
 ls -la ~/ | grep .xinitrc

```

If the file is not executable, simply

```
 chmod +x ~/.xinitrc

```

Keep in mind this command should be executed along with pertinent instructions on this page about "Setting up non-KDE or Gnome desktop managers"