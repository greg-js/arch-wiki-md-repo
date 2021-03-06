Эта статья содержит только советы по запуску игр и соответствующие советы по настройке системы. Список популярных игр для GNU/Linux можно найти на [Common Applications/Games](/index.php/Common_Applications/Games "Common Applications/Games") и [Netbook Games](/index.php/Netbook_Games "Netbook Games").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Игровые Среды](#Игровые_Среды)
*   [2 Получение игр](#Получение_игр)
    *   [2.1 Родные](#Родные)
    *   [2.2 Wine](#Wine)
    *   [2.3 Flash](#Flash)
    *   [2.4 Java](#Java)
*   [3 Запуск игр в Arch](#Запуск_игр_в_Arch)
    *   [3.1 Мульти-экранные настройки](#Мульти-экранные_настройки)
    *   [3.2 Захват клавиатуры](#Захват_клавиатуры)
    *   [3.3 Запуск игр в отдельном X сервере](#Запуск_игр_в_отдельном_X_сервере)
    *   [3.4 Настройка мыши](#Настройка_мыши)
    *   [3.5 Фильтры HRTF с OpenAL](#Фильтры_HRTF_с_OpenAL)
*   [4 Смотрите также](#Смотрите_также)

## Игровые Среды

Для игр в Linux существует множество окружений:

*   Родное – игры написанные под Linux (как правило бесплатные и с открытым исходным кодом).
*   Браузер – таким играм требуется браузер и, чаще всего, подключение к интернету.
    *   Plugin-based – для игры понадобится установка дополнительного плагина.
        *   [Java](/index.php/Java "Java") Webstart – для легкой установки кросс-платформенных игр.
        *   [Flash](/index.php/Flash "Flash") – часто встречающиеся в интернете игры.
        *   Unity – специализированное дополнение для браузера, в настоящее время корректно работает только в Google Chrome. Большинство игр – коммерческие.
    *   **HTML 5** – игры, использующие технологии Canvas и WebGL и работающие во всех современных браузерах, однако на слабых компьютерах будут **очень** медленными.
*   Специализированные окружения (програмные эмуляторы) – сначала требуется установка эмулятора, затем можно будет искать игры (большинство из них защищены авторским правом!)
    *   [Wine](/index.php/Wine "Wine") – позволяет запускать множество игр под Windows.
    *   [Crossover Games](http://www.codeweavers.com/) - участники команды Codeweavers являются основными разработчиками Wine. Использование Crossover Games, в сравнении с другими способами, в некоторых случаях позволяет проще и быстрее устанавливать и использовать игры. Crossover это коммерческий продукт, у которого имеется [форум](http://www.codeweavers.com/support/forums/) и активно участвующие в жизни сообщества разработчики.
    *   [DOSBox](/index.php/DOSBox "DOSBox") – для игр под DOS.
    *   [scummvm](https://www.archlinux.org/packages/?name=scummvm) – для множества устаревших приключенческих игр.
*   Аппаратные эмуляторы – эмулируют не програмную среду, а устройство в целом. Относительно авторских прав то же самое.

## Получение игр

### Родные

Большое колличество доступно в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") или в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Инсталяторы некоторых игр можно найти у [Loki](/index.php?title=Loki&action=edit&redlink=1 "Loki (page does not exist)"). Хорошим источником игр можно считать [Desura](/index.php?title=Desura&action=edit&redlink=1 "Desura (page does not exist)") (если заботитесь о безопасности или имеется множество багов).

### Wine

*   [Wine AppDB](http://appdb.winehq.org/) это централизованный источних данных о работающих в Wine играх.
*   Смотрите также [Category:Wine](/index.php?title=Category:Wine&action=edit&redlink=1 "Category:Wine (page does not exist)").

### Flash

Существует несколько больших порталов для flash-игр, среди них:

*   [https://armorgames.com/](https://armorgames.com/)
*   [https://www.kongregate.com/](https://www.kongregate.com/)
*   [https://www.newgrounds.com/](https://www.newgrounds.com/)

### Java

*   Множество маленьких игр, некоторые менее 4kb (дизайн некоторых игр – настоящий шедевр) можно найти перейдя по адресу [http://www.java4k.com](http://www.java4k.com).
*   [https://www.pogo.com/](https://www.pogo.com/) – крупнейший портал казуальных Java-игр
*   [The Java Game Tome](http://www.javagametome.com/) - огромная база данных, в основном по казуальным играм.

## Запуск игр в Arch

Некоторым играм, или типам игр, может потребоваться специальная настройка для запуска. В основном в Arch Linux игры будут работать прямо из коробки, а возможно, и с более высокой производительностью чем в других дистрибутивах (благодаря оптимизациям при компиляции). Тем не менее могут потребоваться некоторые настройки или скрипты для достижения желаемого эффекта.

### Мульти-экранные настройки

Использование мульти-экранных настроек может вызвать проблемы с полноэкранными играми. В таких случаях, одно из решений - [запускать другой Х-сервер](#Starting_games_in_a_seperate_X_server). В качестве другого решения можно воспользоваться советами из [статьи об NVIDIA](/index.php/NVIDIA#Gaming_using_TwinView "NVIDIA") (может быть полезна и не только пользователям NVIDIA).

### Захват клавиатуры

Некоторые игры захватывают клавиатуру и не позволяют переключаться между окнами (комбинация `Alt+Tab`). Для того, чтобы можно было пользоваться сочитаниями клавиш совместно с SDL играми, загрузите [sdl-nokeyboardgrab](https://aur.archlinux.org/packages/sdl-nokeyboardgrab/). Также можно предотвратить захват клавиатуры на уровне X11, для этого воспользуйтесь пакетом [libx11-nokeyboardgrab](https://aur.archlinux.org/packages/libx11-nokeyboardgrab/).

**Примечание:** Как извествно, SDL не всегда могут перехватывать системный ввод. В этом случае, возможно, придется подождать несколько секунд

### Запуск игр в отдельном X сервере

Как упоминалось ранее, иногда может возникнуть необходимость запуска отдельного Х сервера. Отдельный X сервер дает некоторые преимущества, например более высокую производительность, возможность перехода в игру по клавишам CTRL-ALT-F7 / CTRL-ALT-F8, не требуется завершать основную сессию X-ов (она продолжает работать) в случае конфликта игры с видеодрайвером. Для запуска отдельного X сервера (для примера возьмем [Nexuiz](http://alientrap.org/nexuiz/)) достаточно выполнить следующее:

```
xinit /usr/bin/nexuiz-glx -- :1

```

Можно дополнительно создать конфигурациооный файл для X-ов:

```
xinit /usr/bin/nexuiz-glx -- :1 -xf86config xorg-game.conf 

```

Если ваша основная конфигурация поддерживает технологию NVIDIA Twinview, то для ЗD игр, аналогичных Nexuiz, будет доступна возможность использования нескольких мониторов. Отдельный Х-сервер нежелательно использовать в конфигурациях, в которых рекомендуется отключать второй экран.

Скрипт запуска игры в Openbox, из вашего домашнего каталога или из /usr/local/bin, будет выглядеть следующим образом:

```
$ cat ~/game.sh
if [ $# -ge 1 ]; then
  game="`which $1`"
  openbox="`which openbox`"
  tmpgame="/tmp/tmpgame.sh"
  DISPLAY=:1.0
  echo -e "${openbox} &
${game}" > ${tmpgame}
  echo "starting ${game}"
  xinit ${tmpgame} -- :1 -xf86config xorg-game.conf || exit 1
else
  echo "not a valid argument"
fi

```

После выполнения chmod +x запустить скрипт можно следующей командой:

```
$ ~/game.sh nexuiz-glx

```

### Настройка мыши

Для игр, требующих точность при перемещении мыши, можно настроить скорость ее реакции. Для получения дополнительной информации обратитесь [сюда](/index.php/Mouse_polling_rate "Mouse polling rate").

### Фильтры HRTF с OpenAL

Можно подключить фильтры HRTF в играх поддерживающих OpenAL. Для включения отредактируйте файл `/etc/openal/alsoft.conf` (или, если файл отсутствует, скопируйте файл примера) и замените:

```
#hrtf = false

```

на

```
hrtf = true

```

## Смотрите также

*   [LinuxGames](http://www.linuxgames.com/) - Новости об играх для linux
*   [Free Gamer](http://freegamer.blogspot.com/) - Блог об играх с открытым исходным котод
*   [FreeGameDev](http://forum.freegamedev.net/) - Сообщество разработчиков свободных/открытых игр
*   [Libregamewiki](http://libregamewiki.org/) - wiki свободных игр
*   [SIG/Games](https://fedoraproject.org/wiki/SIGs/Games#Gaming_News_sites) - Новостной сайт об играх в OS/Linux и списки в Fedora wiki
*   [live.linux-gamers](http://live.linux-gamers.net) - Основанный на Arch игровой live-дистрибутив
*   [Games on Linux](http://www.gamesonlinux.com) - Коммерческие игры для Linux
*   [Игры для Linux Q&A](https://unixgames.ru) - Сервис вопросов и ответов по играм для Linux (и другим UNIX-like ОС)