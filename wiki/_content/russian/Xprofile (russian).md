Файлы xprofile, ~/.xprofile и /etc/xprofile позволяют выполнять команды при старте сессии пользователя X, до старта [Оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)").

Файл xprofile похож по стилю на [xinitrc](/index.php/Xinitrc "Xinitrc").

## Совместимость

Файлы xprofile автоматически выполняются следующими экранными менеджерами:

*   [GDM](/index.php/GDM "GDM") - `/etc/gdm/Xsession`
*   [KDM](/index.php/KDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDM (Русский)") - `/usr/share/config/kdm/Xsession`
*   [LightDM](/index.php/LightDM "LightDM") - `/etc/lightdm/Xsession`
*   [LXDM](/index.php/LXDM "LXDM") - `/etc/lxdm/Xsession`
*   [SDDM](/index.php/SDDM "SDDM") - `/usr/share/sddm/scripts/Xsession`

### Выполнение xprofile со стартом xinit

Можно выполнить xprofile, если сессия начинается со старта одной из следующих программ:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDM (Русский)")
*   [SLiM](/index.php/SLiM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SLiM (Русский)")
*   Любой другой [Экранный менеджер](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)") который использует `~/.xsession` или `~/.xinitrc`

Любой запуск `~/.xinitrc` (обычно копируется из `/etc/X11/xinit/xinitrc` если он не существует) выполняется прямым или косвенным образом. Поэтому надо добавить следующие строки в файлы:

 `~/.xinitrc и /etc/X11/xinit/xinitrc` 
```
#!/bin/sh

# Убедитесь, что эти строки перед командой 'exec', иначе не будет работать.
[ -f /etc/xprofile ] && source /etc/xprofile
[ -f ~/.xprofile ] && source ~/.xprofile

```

## Конфигурация

Сначала, создайте файл `~/.xprofile`, если он не существует. Далее, добавьте программы, которые буду запускаться при старте сессии. Для примера будут использоваться [tint2](/index.php/Tint2_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tint2 (Русский)") и [nm-applet](/index.php/NetworkManager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NetworkManager (Русский)"):

 `~/.xprofile` 
```
tint2 &
nm-applet &

```