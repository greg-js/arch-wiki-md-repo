Budgie is the default desktop of Solus Operating System, written from scratch. Besides a more modern design, Budgie can emulate the look and feel of the GNOME 2 desktop.

At this time Budgie is heavily under development, so you can expect minor bugs and new features to be added as time goes on.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Install](/index.php/Install "Install") the [budgie-desktop](https://aur.archlinux.org/packages/budgie-desktop/) package for the latest stable or [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/) for current git master. It's recommended to install its optional dependencies also to get a more complete desktop environment. It's recommended also to install the [gnome](https://www.archlinux.org/groups/x86_64/gnome/) group, which contains applications required for the standard GNOME experience.

### Запуск

Choose *Budgie Desktop* session from a [display manager](/index.php/Display_manager "Display manager") of choice, or modify [xinitrc](/index.php/Xinitrc "Xinitrc") to include Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Использование

You can see the notification messages, set volume, and modify the look and feel of the desktop with the sidebar called "Raven". It can be accessed with `Super+N` key or by clicking on the Status Indicator applet.

## Смотрите также

*   [Официальный сайт проекта Solus (Англ.)](https://solus-project.com/)
*   [Official git repositories for Solus development](https://git.solus-project.com/)
*   [Build status for Solus projects](https://build.solus-project.com/)