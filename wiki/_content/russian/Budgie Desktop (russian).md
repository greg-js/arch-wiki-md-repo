Budgie написанный с нуля рабочий стол, который используется по умолчанию в Операционной Системе Solus. К тому же, более современный дизайн Budgie может имитировать внешний вид рабочего стола GNOME 2.

Сейчас Budgie находится в стадии разработки, так что могут появляться ошибки и добавляться новые возможности.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Help:%D0%A7%D1%82%D0%B5%D0%BD%D0%B8%D0%B5#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Help:Чтение") последний стабильный пакет [budgie-desktop](https://aur.archlinux.org/packages/budgie-desktop/) или текущую разрабатываемую версию [budgie-desktop-git](https://aur.archlinux.org/packages/budgie-desktop-git/). Также рекомендуется установить необязательные зависимости, чтобы получить более полную рабочую среду. Также рекомендуется установить группу [gnome](https://www.archlinux.org/groups/x86_64/gnome/), которая содержит приложения для стандартной работы GNOME.

### Запуск

Выберите сессию *Budgie Desktop* [Экранного менеджера](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер"), или измените [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") добавив Budgie Desktop:

 `~/.xinitrc` 
```
export XDG_CURRENT_DESKTOP=Budgie:GNOME
exec budgie-desktop

```

## Использование

Вы можете видеть уведомления сообщений, устанавливать громкость, и изменять внешний вид рабочего стола при поомщи боковой панели, под названием "Raven". Доступ к ней осуществляется нажатием `Super+N` или щелчком по Апплету Индикатора Состояния.

## Смотрите также

*   [Официальный сайт проекта Solus (Англ.)](https://solus-project.com/)
*   [Официальный git-репозиторий для разработки Solus (Англ.)](https://git.solus-project.com/)
*   [Build status for Solus projects](https://build.solus-project.com/)