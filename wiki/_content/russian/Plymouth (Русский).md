[Plymouth](http://fedoraproject.org/wiki/Releases/FeatureBetterStartup) — это проект из Fedora, обеспечивающий загрузку системы без бегущих надписей (логов) на экране. Он базируется на [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") (KMS, установка разрешения и глубины цвета на уровне ядра) для обеспечения родного разрешения экрана на раннем этапе загрузки, после чего отображает привлекательный загрузочный экран вплоть до этапа выбора пользователя.

## Contents

*   [1 Подготовка](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [3.1 Включение Plymouth в Initcpio](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_Plymouth_.D0.B2_Initcpio)
    *   [3.2 Командная строка ядра](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.B0.D1.8F_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B0_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [3.3 Изменение темы](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BC.D1.8B)
*   [4 Устранение неполадок](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.BF.D0.BE.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA)
    *   [4.1 Маленькие черные квадраты](#.D0.9C.D0.B0.D0.BB.D0.B5.D0.BD.D1.8C.D0.BA.D0.B8.D0.B5_.D1.87.D0.B5.D1.80.D0.BD.D1.8B.D0.B5_.D0.BA.D0.B2.D0.B0.D0.B4.D1.80.D0.B0.D1.82.D1.8B)
    *   [4.2 Выключение <-- Все еще проблема?](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.3C--_.D0.92.D1.81.D0.B5_.D0.B5.D1.89.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0.3F)
*   [5 Также смотри](#.D0.A2.D0.B0.D0.BA.D0.B6.D0.B5_.D1.81.D0.BC.D0.BE.D1.82.D1.80.D0.B8)

## Подготовка

**Важно:** Plymouth в настоящее время находится в активной разработке и может содержать ошибки.

Plymouth главным образом использует KMS для обработки графики. Если вы знаете что это такое и уже настроили, смело переходите к [Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0).

В противном случае у вас есть два варианта:

1.  Установить и настроить KMS: пожалуйста, обратитесь к инструкциям для видеокарт [ATI](/index.php/ATI#AMD.2FAti_cards_and_KernelModeSetting_.28KMS.29 "ATI"), [Intel](/index.php/Intel#KMS_.28Kernel_Mode_Setting.29 "Intel") или [Nvidia](/index.php/Nouveau#KMS "Nouveau"). Все они требуют редактирования/пересборки ядра. Это будет описано позже в этой статье, поэтому редактирование образа ядра пока может быть пропущено.
2.  Несмотря на то, что использование KMS предпочтительно, Plymouth может работать без них. Если у вас нет возможности использовать KMS, то вам понадобится [framebuffer](/index.php/Framebuffer#Framebuffer_Resolution "Framebuffer"). Рекомендуется использовать драйвер Uvesafb, так как он поддерживает разрешения широкоформатных дисплеев.

Если у вас не настроены ни KMS ни framebuffer, то Plymouth вернется в текстовый режим.

## Установка

Plymouth пока недоступен в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и должен быть установлен из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

Стабильная версия называется [plymouth](https://aur.archlinux.org/packages/plymouth/), последний стабильный релиз был в июле 2012 года [[1]](http://www.freedesktop.org/software/plymouth/releases/?C=M;O=D), но можно использовать версию [plymouth-git](https://aur.archlinux.org/packages/plymouth-git/).

## Конфигурация

### Включение Plymouth в Initcpio

Добавьте Plymouth в HOOKS в [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). Он обязательно **должен** быть добавлен *после* **base**, **udev** и **autodetect**:

 `/etc/mkinitcpio.conf`  `HOOKS="base udev autodetect [...] plymouth"` 
**Важно:** Если используется [шифрование жестких дисков](/index.php/System_Encryption_with_LUKS_for_dm-crypt "System Encryption with LUKS for dm-crypt") с **encrypt** hook, *необходимо* заменить его на **plymouth-encrypt** чтобы получить доступ к запросу пароля TTY.

Для более раннего запуска KMS надо добавить модуль [radeon](/index.php/Radeon "Radeon") (для видеокарт radeon), [i915](/index.php/Intel "Intel") (для видеокарт Intel) или [nouveau](/index.php/Nouveau "Nouveau") (для видеокарт nvidia) в строку MODULES в `/etc/mkinitcpio.conf`:

 `/etc/mkinitcpio.conf` 
```
MODULES="i915"
**или**
MODULES="radeon"
**или**
MODULES="nouveau"
```

Переконфигурация образа ядра (см. статью [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") для более детальной информации):

 `# mkinitcpio -p [имя вашего ядра]` 

### Командная строка ядра

Неоходимо установить **quiet splash** режим ядра в параметрах командной линии загрузчика. Ниже пример для [Grub2](/index.php/Grub2 "Grub2") и `/boot/grub/grub.cfg` (для [GRUB](/index.php/GRUB "GRUB") и [LILO](/index.php/LILO "LILO") шаблон аналогичен):

```
linux /boot/vmlinuz-linux root=/dev/... ro quiet splash

```

Можно заставить KMS принудительно запускаться раньше добавив "*radeon.modeset=1*" (для видеокарт radeon) or "*i915.modeset=1*" (для видеокарт Intel) в опции ядра:

```
linux /boot/vmlinuz-linux root=/dev/... radeon.modeset=1

```

```
linux /boot/vmlinuz-linux root=/dev/... i915.modeset=1

```

Так же можно отредактировать файл `/etc/default/grub` и добавить опции ядра в строке *GRUB_CMDLINE_LINUX_DEFAULT=""*. Чтобы сгенерировать `grub.cfg` выполните:

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

### Изменение темы

Plymouth имеет на выбор темы:

1.  Fade-in: "Простая тема с затухающими и разгорающимися мерцающими звездами"
2.  Glow: "Производственная тема, показывающая процесс загрузки в виде круговой диаграммы"
3.  Script: "Пример скрипта" (Несмотря на описание выглядит очень симпатичной темой Arch)
4.  Solar: "Космическая тема, голубая звезда с протуберанцами" and
5.  Spinfinity: "Простая тема показывающая вращающийся знак бесконечности в центре экрана"
6.  *(Text: "Текстовый режим с трехцветной полосой прогресса")*
7.  *(Details: "Резервная тема с подробностями загрузки")*

Список установленных тем можно вызвать командой:

```
plymouth-set-default-theme -l

```

Для просмотра тем без перезагрузки. Нажать Ctrl+Alt+F2 для переключения консоли, войти как root и набрать:

```
plymouthd
plymouth --show-splash

```

Для выхода из просмотра нажать Ctrl+Alt+F2 снова и набрать:

```
plymouth --quit

```

Установить желаемую тему можно утилитой **plymouth-set-default-theme**, например:

```
# plymouth-set-default-theme spinfinity

```

Соберите образ ядра:

```
# mkinitcpio -p [name of your kernel preset]

```

Перезагрузитесь.

## Устранение неполадок

### Маленькие черные квадраты

По каким-то причинам после выполнения команды выйти, Plymouth может оставить черные квадраты вверху экрана видимые поверх всех окон. Два подтвержденных случая, это ноутбук с видеокартой ATI при использовании KMS, и десктоп с видеокартой nVidia использующий framebuffer. Источником проблемы является опция `--retain-splash` , которая требуется для максимально плавного отображения в процессе загрузки. Обходным путем является принудительное закрытие Plymouth *после* логина, когда опция `--retain-splash`более не требуется.

Нужно отредактировать `~/.xinitrc` и добавить следующую линию **перед** линией запускающей менеджер окружения рабочего стола (подобной "exec openbox-session") чтобы выключить Plymouth:

```
sudo /bin/plymouth quit &

```

**Обратите внимание:** Отсутствие `--retain-splash` и дополнительный знак `&` требуются чтобы xinitrc мог продолжать запуск графического окружения и оставить Plymouth выключаться в фоновом режиме.

**Важно:** Если не вставить это **перед** строкой запуска сессии рабочего стола (к примеру "exec startxfce4") **приведет** в результате к **незапускаемой** сессии.

Чтобы получить разрешение на принудительное отключение Plymouth без пароля, нужно отредактировать `/etc/sudoers`:

```
$ su
# EDITOR=nano visudo

```

и добавить:

```
*Ваш_Логин*      ALL=(ALL) NOPASSWD: /bin/plymouth

```

После этого необходимо перезагрузиться.

### Выключение `<-- Все еще проблема?`

Если имеется проблема с выключением Power Off, к примеру компьютер перезагружается вместо выключения, причиной может быть или KMS или Plymouth. Если причина в Plymouth, то необходимо или запустить "plymouth --mode ..." в случае перезагрузки или halt или отредактировать `/etc/rc.d/functions.d/plymouth.functions` и закомментировать следующий блок:

```
if [ "$0" == "/etc/rc.shutdown" ]; then
...
fi

```

## Также смотри

[Обсуждение на форуме](https://bbs.archlinux.org/viewtopic.php?id=81406)