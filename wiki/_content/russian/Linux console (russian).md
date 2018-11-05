**Состояние перевода:** На этой странице представлен перевод статьи [Linux console](/index.php/Linux_console "Linux console"). Дата последней синхронизации: 28 сентября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Linux_console&diff=0&oldid=544394).

Related articles

*   [Консоль Linux/Настройка клавиатуры](/index.php/%D0%9A%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C_Linux/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B "Консоль Linux/Настройка клавиатуры")
*   [Taking a screenshot (Русский)#Виртуальная консоль](/index.php/Taking_a_screenshot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C "Taking a screenshot (Русский)")
*   [Color output in console](/index.php/Color_output_in_console "Color output in console")
*   [getty](/index.php/Getty "Getty")

Согласно [Википедии](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"):

	**Консоль Linux** - системная консоль, реализованная в [ядре Linux](/index.php/Kernel_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Kernel (Русский)"). Консоль Linux предоставляет возможность для ядра и других процессов отправлять текстовый вывод пользователю и получать текстовый ввод от пользователя. Пользователь обычно вводит текст с помощью клавиатуры и получает вывод на мониторе. Ядро Linux поддерживает виртуальные консоли - логически раздельные консоли, но которые используют одну и ту же физическую клавиатуру и экран.

Эта статься объясняет основы консоли Linux и как настроить отображение шрифтов в ней. Настройка клавиатуры описана в подстранице [Консоль Linux/Настройка клавиатуры](/index.php/%D0%9A%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D1%8C_Linux/%D0%9D%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B "Консоль Linux/Настройка клавиатуры").

## Contents

*   [1 Реализация](#.D0.A0.D0.B5.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
    *   [1.1 Виртуальная консоль](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)
    *   [1.2 Текстовый режим](#.D0.A2.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC)
    *   [1.3 Фреймбуфер консоли](#.D0.A4.D1.80.D0.B5.D0.B9.D0.BC.D0.B1.D1.83.D1.84.D0.B5.D1.80_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D0.B8)
*   [2 Сочетание клавиш](#.D0.A1.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
*   [3 Шрифты](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B)
    *   [3.1 Предосмотр и временные изменения](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.B8_.D0.B2.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.2 Постоянные настройки](#.D0.9F.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Реализация

The console, unlike most services that interact directly with users, is implemented in the kernel. This contrasts with terminal emulation software, such as [Xterm](/index.php/Xterm "Xterm"), which is implemented in user space as a normal application. The console has always been part of released Linux kernels, but has undergone changes in its history, most notably the transition to using the [framebuffer](https://en.wikipedia.org/wiki/Linux_framebuffer "wikipedia:Linux framebuffer") and support for [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode").

Despite many improvements in the console, its full backward compatibility with legacy hardware means it is limited compared to a graphical terminal emulator.

### Виртуальная консоль

The console is presented to the user as a series of [virtual consoles](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console"). These give the impression that several independent terminals are running concurrently; each virtual console can be logged in with different users, run its own shell and have its own font settings. The virtual consoles each use a device `/dev/ttyX`, and you can switch between them by pressing `Alt+F*x*` (where `*x*` is equal to the virtual console number, beginning with 1). The device `/dev/console` is automatically mapped to the active virtual console.

See also [chvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/chvt.1), [openvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/openvt.1) and [deallocvt(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/deallocvt.1).

### Текстовый режим

Since Linux originally began as a kernel for PC hardware, the console was developed using standard IBM [CGA/EGA/VGA](https://en.wikipedia.org/wiki/VGA "wikipedia:VGA") graphics, which all PCs supported at the time. The graphics operated in VGA text mode, which provides a simple 80x25 character display with 16 colours. This legacy mode is similar the capabilities of dedicated text terminals, such as the [DEC VT100](https://en.wikipedia.org/wiki/VT100 "wikipedia:VT100") series. It is still possible to boot in text mode if the system hardware supports it, but almost all modern distributions (including Arch Linux) use the framebuffer console instead.

### Фреймбуфер консоли

As Linux was ported to other non-PC architectures, a better solution was required, since other architectures do not use VGA-compatible graphics adapters, and may not support text modes at all. The framebuffer console was implemented to provide a standard console across all platforms, and so presents the same VGA-style interface regardless of the underlying graphics hardware. As such, the Linux console is not a terminal emulator, but a terminal in its own right. It uses the terminal type `linux`, and is largely compatible with VT100.

## Сочетание клавиш

| Сочетание клавиш | Описание |
| `Ctrl+Alt+Del` | Перезагрузка компьютера (указано символической ссылкой `/usr/lib/systemd/system/ctrl-alt-del.target`) |
| `Alt+F1`, `F2`, `F3`, ... | Переключение на *n*-ную виртуальную консоль |
| `Alt+ ←` | Переключение на предыдущую виртуальную консоль |
| `Alt+ →` | Переключение на следующую виртуальную консоль |
| `Scroll Lock` | Когда клавиша Scroll Lock включена, ввод/вывод заблокирован |
| `Shift+PgUp`/`PgDown` | Прокрутка буфера консоли вверх/вниз |
| `Ctrl+c` | Завершение текущей задачи |
| `Ctrl+d` | Вставить EOF (символ конца файла) |
| `Ctrl+z` | Остановить текущую задачу |

Для получения дополнительной информации смотрите [console_codes(4)](https://jlk.fjfi.cvut.cz/arch/manpages/man/console_codes.4).

## Шрифты

**Note:** This section is about the [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console"). For alternative console solutions offering more features (full Unicode fonts, modern graphics adapters etc.), see [fbterm](/index.php/Fbterm "Fbterm"), [KMSCON](/index.php/KMSCON "KMSCON") or similar projects.

By default, the [virtual console](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") uses the kernel built-in font with a [CP437](https://en.wikipedia.org/wiki/CP437 "wikipedia:CP437") character set, but this can be easily changed.

The [Linux console](https://en.wikipedia.org/wiki/Linux_console "wikipedia:Linux console") uses UTF-8 encoding by default, but because the standard VGA-compatible framebuffer is used, a console font is limited to either a standard 256, or 512 glyphs. If the font has more than 256 glyphs, the number of colours is reduced from 16 to 8\. In order to assign correct symbol to be displayed to the given Unicode value, a special translation map, often called *unimap*, is needed. Nowadays most of the console fonts have the *unimap* built-in; historically, it had to be loaded separately.

The [kbd](https://www.archlinux.org/packages/?name=kbd) package provides tools to change virtual console font and font mapping. Available fonts are saved in the `/usr/share/kbd/consolefonts/` directory, those ending with *.psfu* or *.psfu.gz* have a Unicode translation map built-in.

Keymaps, the connection between the key pressed and the character used by the computer, are found in the subdirectories of `/usr/share/kbd/keymaps/`, see [/Keyboard configuration](/index.php?title=Linux_console_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Keyboard_configuration&action=edit&redlink=1 "Linux console (Русский)/Keyboard configuration (page does not exist)") for details.

**Note:** Replacing the font can cause issues with programs that expect a standard VGA-style font, such as those using line drawing graphics.

**Tip:** For European based languages written in Latin/Greek letters you can use `eurlatgr` font, it includes a broad range of Latin/Greek letter variations as well as special characters [[2]](https://lists.altlinux.org/pipermail/kbd/2014-February/000439.html).

### Предосмотр и временные изменения

**Совет:** Доступна организованная библиотека изображений для предосмотра: [Скриншоты шрифтов консоли Linux](http://alexandre.deverteuil.net/pages/consolefonts/).

```
$ showconsolefont

```

показывает таблицу глифов или букв шрифта.

`setfont` временно меняет шрифт, если передать имя шрифта (из `/usr/share/kbd/consolefonts/`), например

```
$ setfont lat2-16 -m 8859-2

```

Таким образом, чтобы иметь маленький шрифт **8x8**, с установленным шрифтом, как показано ниже, используйте, например:

```
$ setfont -h8 /usr/share/kbd/consolefonts/drdos8x8.psfu.gz

```

Имена шрифтов чувствительны к регистру. `setfont` без параметра устанавливает шрифт по умолчанию в консоли.

**Совет:** Все команды, изменяющие шрифт, могут быть напечатаны "вслепую".

**Примечание:** *setfont* работает только на используемой консоли. Любые другие консоли, активные или неактивные, остаются незатронутыми.

### Постоянные настройки

The `FONT` variable in `/etc/vconsole.conf` is used to set the font at boot, persistently for all consoles. See [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5) for details.

For displaying characters such as *Č, ž, đ, š* or *Ł, ę, ą, ś* using the font `lat2-16.psfu.gz`:

 `/etc/vconsole.conf` 
```
...
FONT=lat2-16
FONT_MAP=8859-2
```

It means that second part of ISO/IEC 8859 characters are used with size 16\. You can change font size using other values (e.g. `lat2-08`). For the regions determined by 8859 specification, look at the [Wikipedia:ISO/IEC 8859#The parts of ISO/IEC 8859](https://en.wikipedia.org/wiki/ISO/IEC_8859#The_parts_of_ISO.2FIEC_8859 "wikipedia:ISO/IEC 8859").

To use the specified font in early userspace, use the `consolefont` hook in `/etc/mkinitcpio.conf`. See [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") for more information.

If the fonts seems to not change on boot, or change only temporarily, it is most likely that they got reset when graphics driver was initialized and console was switched to framebuffer. To avoid this, load your graphics driver earlier. See for example [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"), [[3]](https://bbs.archlinux.org/viewtopic.php?id=145765) or other ways to setup your framebuffer before `/etc/vconsole.conf` is applied.

## Смотрите также

*   [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting")
*   [The TTY demystified – Linus Åkesson](https://www.linusakesson.net/programming/tty/)