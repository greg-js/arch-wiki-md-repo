Related articles

*   [xinitrc](/index.php/Xinitrc "Xinitrc")

Файлы xprofile, `~/.xprofile` и `/etc/xprofile`, позволяют выполнять команды при старте сессии пользователя X. До старта [оконного менеджера](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)").

Файл xprofile схож по стилю с [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)").

## Совместимость

Следующие экранные менеджеры имеют встроенную поддержку xprofile:

*   [GDM](/index.php/GDM "GDM") - `/etc/gdm/Xsession`
*   KDM - `/usr/share/config/kdm/Xsession`
*   [LightDM](/index.php/LightDM "LightDM") - `/etc/lightdm/Xsession`
*   [LXDM](/index.php/LXDM "LXDM") - `/etc/lxdm/Xsession`
*   [SDDM](/index.php/SDDM "SDDM") - `/usr/share/sddm/scripts/Xsession`

### Выполнение команд из xprofile со стартом xinit

Следующие программы автоматически выполнят команды из xprofile при старте сеанса:

*   `startx`
*   `xinit`
*   [XDM](/index.php/XDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "XDM (Русский)")
*   [SLiM](/index.php/SLiM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SLiM (Русский)")
*   Любой другой [экранный менеджер](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)"), использующий `~/.xsession` или `~/.xinitrc`

Все запуски происходят прямым или косвенным образом из `~/.xinitrc` или `/etc/X11/xinit/xinitrc`, если первый не существует. Поэтому все требуемые команды xprofile должны располагаться именно там.

 `~/.xinitrc и /etc/X11/xinit/xinitrc` 
```
#!/bin/sh

# Убедитесь в том, что эти строчки перед первой командой 'exec', иначе ничего не сработает
[ -f /etc/xprofile ] && source /etc/xprofile
[ -f ~/.xprofile ] && source ~/.xprofile

...

```

## Конфигурация

Во-первых, создайте файл `~/.xprofile`, если его не существует. Затем добавьте соответствующие команды для программ, требующих запуск при старте сессии. Смотрите ниже:

 `~/.xprofile` 
```
tint2 &
nm-applet &

```