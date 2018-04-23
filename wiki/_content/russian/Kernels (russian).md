Ссылки по теме

*   [Модули ядра](/index.php/%D0%9C%D0%BE%D0%B4%D1%83%D0%BB%D0%B8_%D1%8F%D0%B4%D1%80%D0%B0 "Модули ядра")
*   [Compile kernel module](/index.php/Compile_kernel_module "Compile kernel module")
*   [Kernel Panics](/index.php/Kernel_Panics "Kernel Panics")
*   [Linux-ck (Русский)](/index.php/Linux-ck_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Linux-ck (Русский)")
*   [sysctl](/index.php/Sysctl "Sysctl")

**Состояние перевода:** На этой странице представлен перевод статьи [Kernels](/index.php/Kernels "Kernels"). Дата последней синхронизации: 29 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Kernels&diff=0&oldid=428531).

Из [Wikipedia](https://ru.wikipedia.org/wiki/Ядро_операционной_системы):

	Ядро́ — центральная часть операционной системы (ОС), обеспечивающая приложениям координированный доступ к ресурсам компьютера, таким как процессорное время, память, внешнее аппаратное обеспечение, внешнее устройство ввода и вывода информации. Также обычно ядро предоставляет сервисы файловой системы и сетевых протоколов.

Существуют различные альтернативные доступные ядра Arch Linux в дополнение к основным Linux ядрам. В этой статье перечислены некоторые из вариантов имеющихся в репозиториях, с кратким описанием каждого из них. Существует также описание патчей, которые могут быть применены к ядру. Статья заканчивается обзором пользовательской компиляции ядра со ссылками на различные методы.

## Contents

*   [1 Предварительно скомпилированные ядра](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B2.D0.B0.D1.80.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE_.D1.81.D0.BA.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [1.1 Официальные пакеты](#.D0.9E.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
    *   [1.2 Неофициальные пользовательские репозитории с готовыми, собранными ядрами Linux](#.D0.9D.D0.B5.D0.BE.D1.84.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B5_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B8_.D1.81_.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D1.8B.D0.BC.D0.B8.2C_.D1.81.D0.BE.D0.B1.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.BC.D0.B8_.D1.8F.D0.B4.D1.80.D0.B0.D0.BC.D0.B8_Linux)
    *   [1.3 AUR пакеты](#AUR_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D1.8B)
*   [2 Патчи и наборы патчей (патчсеты)](#.D0.9F.D0.B0.D1.82.D1.87.D0.B8_.D0.B8_.D0.BD.D0.B0.D0.B1.D0.BE.D1.80.D1.8B_.D0.BF.D0.B0.D1.82.D1.87.D0.B5.D0.B9_.28.D0.BF.D0.B0.D1.82.D1.87.D1.81.D0.B5.D1.82.D1.8B.29)
    *   [2.1 Как установить](#.D0.9A.D0.B0.D0.BA_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C)
    *   [2.2 Основные патчи и патчсеты](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D1.82.D1.87.D0.B8_.D0.B8_.D0.BF.D0.B0.D1.82.D1.87.D1.81.D0.B5.D1.82.D1.8B)
        *   [2.2.1 -ck](#-ck)
        *   [2.2.2 -rt](#-rt)
        *   [2.2.3 -bld](#-bld)
        *   [2.2.4 -grsecurity](#-grsecurity)
        *   [2.2.5 Tiny-Патчи](#Tiny-.D0.9F.D0.B0.D1.82.D1.87.D0.B8)
        *   [2.2.6 -pf](#-pf)
    *   [2.3 Индивидуальные патчи](#.D0.98.D0.BD.D0.B4.D0.B8.D0.B2.D0.B8.D0.B4.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D0.B0.D1.82.D1.87.D0.B8)
        *   [2.3.1 Reiser4](#Reiser4)
        *   [2.3.2 fbsplash](#fbsplash)
*   [3 Компиляция ядра](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [3.1 Используя Arch Build System (ABS)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8F_Arch_Build_System_.28ABS.29)
    *   [3.2 Традиционный метод](#.D0.A2.D1.80.D0.B0.D0.B4.D0.B8.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D0.B9_.D0.BC.D0.B5.D1.82.D0.BE.D0.B4)
    *   [3.3 Пропиетарный NVIDIA драйвер](#.D0.9F.D1.80.D0.BE.D0.BF.D0.B8.D0.B5.D1.82.D0.B0.D1.80.D0.BD.D1.8B.D0.B9_NVIDIA_.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)
    *   [4.1 Тесты и обзоры](#.D0.A2.D0.B5.D1.81.D1.82.D1.8B_.D0.B8_.D0.BE.D0.B1.D0.B7.D0.BE.D1.80.D1.8B)

## Предварительно скомпилированные ядра

### Официальные пакеты

	[linux](https://www.archlinux.org/packages/?name=linux)

	Linux ядро и модули из репозитория [core]. Ванильное ядро с [некоторыми патчами](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux).

	[linux-lts](https://www.archlinux.org/packages/?name=linux-lts)

	Версия ядра Linux и модулей с долгосрочной поддержкой (LTS - Long Term Support) из репозитория [core].

	[linux-grsec](https://www.archlinux.org/packages/?name=linux-grsec)

	Linux ядро и модули с [Grsecurity Patchset](/index.php/Grsecurity_Patchset "Grsecurity Patchset") и PaX патчами для повышения безопасности.

	[linux-zen](https://www.archlinux.org/packages/?name=linux-zen)

	[ZEN-ядро](https://github.com/zen-kernel/zen-kernel) результат совместной работы проекта Zen-kernel.

Для создания этого ядра берётся свежее стабильное официальное ядро Linux. И вносятся изменения проектом Zen-kernel (планировщик CPU BFS, BFQ-планировщик (I/O) ввода-вывода, Aufs, Unionfs, Reiser4, TuxOnIce, PHC и многие другие), которые улучшают отзывчивость и производительность системы.

### Неофициальные пользовательские репозитории с готовыми, собранными ядрами Linux

Рекомендуется посмотреть[этот раздел](/index.php/Unofficial_user_repositories "Unofficial user repositories")

### AUR пакеты

	[linux-aufs_friendly](https://aur.archlinux.org/packages/linux-aufs_friendly/)

	AUFS-совместимое ядро Linux и модули, полезно при использовании [Docker](/index.php/Docker_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Docker (Русский)")

	[linux-apparmor](https://aur.archlinux.org/packages/linux-apparmor/)

	Linux ядро с включенными возможностями [AppArmor](/index.php/AppArmor "AppArmor")

	[linux-bfs](https://aur.archlinux.org/packages/linux-bfs/)

	Ядро Linux и модули с [Brain Fuck Scheduler](https://en.wikipedia.org/wiki/ru:Brain_Fuck_Scheduler "wikipedia:ru:Brain Fuck Scheduler") (BFS) - созданное Коном Коливасом (Con Kolivas) для PC с меньшим, чем 4096 ядрами, и BFQ I/O планировщиком в качестве дополнительного

	[linux-chromebook](https://aur.archlinux.org/packages/linux-chromebook/)

	Ядро Linux с добавлением аппаратной поддержки [chromebook](/index.php/Chromebook "Chromebook")

[Linux-ck](https://aur.archlinux.org/packages/Linux-ck/)

	Ядро Linux, доступное в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"), которое позволяет пользователям запускать [ядро с набором патчей Кона Коливаса](https://en.wikipedia.org/wiki/Linux-ck_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "wikipedia:Linux-ck (Русский)"), включая "Brain Fuck Scheduler" (BFS)

	Эти патчи предназначены для улучшения отклика системы с особым упором на PC, подходят для любого PC

	[linux-eee-ck](https://aur.archlinux.org/packages/linux-eee-ck/)

	Ядро Linux и модули для Asus Eee PC 701, собранные с ck1-патчами Кона Коливаса (Con Kolivas)

	[linux-fbcondecor](https://aur.archlinux.org/packages/linux-fbcondecor/)

	Ядро Linux и модули с [fbcondecor поддержкой](/index.php/Fbsplash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fbsplash (Русский)").

	[linux-git](https://aur.archlinux.org/packages/linux-git/)

	Ядро Linux и модули собранное с [Linus Torvalds' Git репозитория](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git).

	[linux-ice](https://aur.archlinux.org/packages/linux-ice/)

	Ядро Linux и модули с gentoo-sources патчами и [TuxOnIce](/index.php/TuxOnIce "TuxOnIce") поддержкой.

	[linux-libre](https://aur.archlinux.org/packages/linux-libre/), [linux-libre-lts](https://aur.archlinux.org/packages/linux-libre-lts/), [linux-libre-grsec](https://aur.archlinux.org/packages/linux-libre-grsec/), [linux-libre-rt](https://aur.archlinux.org/packages/linux-libre-rt/), [linux-libre-xen](https://aur.archlinux.org/packages/linux-libre-xen/)

	Ядро Linux с "binary blobs".

	[linux-lqx](https://aur.archlinux.org/packages/linux-lqx/)

	[Liquorix](http://liquorix.net) - ядро, построенное с использованием Debian-конфигурации и ZEN-патчей. Предназначено для рабочего стола, мультимедийных, игровых и рабочих станций, часто используется в качестве замены ядра Debian Linux

Damentz, - сопровождающий набор патчей Liquorix, является также разработчиком для набора патчей ZEN

	[linux-lts34](https://aur.archlinux.org/packages/linux-lts34/)

	Ядро Linux 3.4 с долгосрочной поддержкой (LTS - Long Term Support).

	[linux-lts310](https://aur.archlinux.org/packages/linux-lts310/)

	Ядро Linux 3.10 с долгосрочной поддержкой (LTS - Long Term Support).

	[linux-lts312](https://aur.archlinux.org/packages/linux-lts312/)

	Ядро Linux 3.12 с долгосрочной поддержкой (LTS - Long Term Support).

	[linux-mainline](https://aur.archlinux.org/packages/linux-mainline/)

	Ядро Linux-mainline.

	[linux-mptcp](https://aur.archlinux.org/packages/linux-mptcp/)

	Ядро Linux и модули с поддержкой [Multipath TCP](http://multipath-tcp.org/)

	[kernel-netbook](https://aur.archlinux.org/packages/kernel-netbook/)

	Статичное ядро для нетбуков с Intel Atom N270/N280/N450/N550, таких как Eee PC, с добавлением внешней прошивки ([broadcom-wl](https://www.archlinux.org/packages/?name=broadcom-wl)) и наборами патчей (BFS + TuxOnIce + BFQ опцией); только для Intel GPU

	[linux-pax](https://aur.archlinux.org/packages/linux-pax/)

	Ядро Linux и модули с [PaX](/index.php/PaX "PaX") патчами для повышенной безопасности.

	[linux-pf](https://aur.archlinux.org/packages/linux-pf/)

	Ядро Linux и модули с pf-патчами ядра [-ck патчи (BFS included), TuxOnIce, BFQ] и aufs3.

Это ядро также доступно (уже собранное)[из неофициального пользовательского репозитория](/index.php/Unofficial_user_repositories#Linux-pf "Unofficial user repositories").

	[linux-tresor](https://aur.archlinux.org/packages/linux-tresor/)/[linux-lts-tresor](https://aur.archlinux.org/packages/linux-lts-tresor/)

	Текущее/LTS Linux ядро и модули со встроенным [патчем TRESOR](https://www1.informatik.uni-erlangen.de/tresor)

	[linux-vfio](https://aur.archlinux.org/packages/linux-vfio/)/[linux-vfio-lts](https://aur.archlinux.org/packages/linux-vfio-lts/)

	Ядро Linux и несколько патчей написанных Алексом Уильямсон (Alex Williamson) (переопределяющих acs и i915) предоставляющих возможность сделать PCI Passthrough с KVM на некоторых машинах.

Используется для хранения ключей шифрования AES не в ОЗУ, а в регистрах CPU, [подробнее тут](http://www.opennet.ru/tips/2617_tresor_aes_crypt_cpu_cryptsetup_dmcrypt.shtml).

## Патчи и наборы патчей (патчсеты)

Есть много причин, чтобы пропатчить ядро, основные из них для работы или для поддержки не-магистральных функций, таких как поддержка файловой системы Reiser4\. Другие причины могут включать в себя забаву и посмотреть, как это делается и какие улучшения при этом появляются.

Однако, важно отметить, что лучшим способом увеличить скорость работы вашей системы будет сконфигурированное ядро именно для вашей системы, особенно под конкретную архитектуру и тип процессора. По этой причине использовать заранее упакованные версии пользовательских ядер с общими настройками архитектуры не рекомендуется, или не стоит. Еще одним приемуществом является то, что вы можете уменьшить размер вашего ядра (и, следовательно время сборки). Для этого не включая поддержку тех модулей, которыми вы не пользуетесь. Например вы можете убрать поддержку bluetooth, video4linux, 1000Mbit ethernet и т.д. Т.е. убрать тот ненужный для вас функционал и/или поддержку того оборудования которого у вас нет. Хотя эта статья не о конфигурации ядра, тем не менее рекомендуется в качестве первого шага, основы, чтобы понять какой набор патчей использовать.

Конфигурационные файлы для пакетов ядра Arch можно использовать в качестве отправной точки. Они находятся в Arch исходных файлов пакета, например[[1]](https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/linux) связано с [linux](https://www.archlinux.org/packages/?name=linux). Файл конфигурации вашего текущего ядра также всегда доступны в файловой системе в `/proc/config.gz`.

### Как установить

Процесс установки пользовательских пакетов ядра опирается на систему сборки Arch (ABS). Если вы не собирали какие-либо пользовательские пакеты самостоятельно, вы можете обратиться к следующим статьям: [Arch Build System (Русский)](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") и [Creating packages (Русский)](/index.php/Creating_packages_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Creating packages (Русский)").

Если вы не патчили или настраивали ядро ранее, то это не так сложно, и есть много PKGBUILD’ов на форуме для отдельных пакетов. Тем не менее, мы советуем вам начать с нуля, с некоторым исследованием преимуществах каждого набора патчей, а не просто произвольной выборки из всего множества. Таким образом, вы узнаете гораздо больше о том, что вы делаете, а не просто выберите ядро при запуске, а потом будите гадать, что же там изменилось.

Смотрите [#Compilation](#Compilation).

**Примечание:** Не забудьте изменить параметры загрузки в загрузчике [GRUB](/index.php/GRUB "GRUB"), чтобы использовать новое ядро.

### Основные патчи и патчсеты

Прежде всего важно отметить, что патчи и патчсеты разработаны различными людьми. Некоторые из этих людей на самом деле участвует в производстве ядра Linux. Но есть и любители, которые могут поменять функции ядра надежности и стабильности в лучшую/худшую сторону.

Стоит также отметить, что некоторые патчи строятся на старых версиях ядра и (или) патчах (которые могут или не могут быть отражены в названии патча). Патчсеты (и обновления ядра) часто и зачастую не идут в ногу со временем. Так что не стоит сходить с ума, если это не ваше хобби.

Вы можете воспользоваться поиском Google для поиска других видов патчей.

**Примечание:** Этот раздел **только для ознакомления** - никаких гарантий о надёжности или стабильности на этой странице.

#### -ck

[Linux-ck](/index.php/Linux-ck "Linux-ck") содержит патчи, предназначенные для улучшения отклика системы с особым упором на рабочем столе, подходят для любой нагрузки. Патчи создаются и поддерживаются Коном Коливасом (Con Kolivas). Его сайт [http://users.on.net/~ckolivas/kernel/](http://users.on.net/~ckolivas/kernel/). Кон поддерживает полный набор патчей, но также обеспечивает одиночные патчи, так что вы можете добавить только те, которые Вы предпочитаете.

-ck можно найти на [http://ck.kolivas.org/patches/4.0/](http://ck.kolivas.org/patches/4.0/)

#### -rt

Это набор патчей поддерживается небольшой группой разработчиков ядра, во главе с Инго Молнар (Ingo Molnar). Позволяет превратить обычный Linux в ОС реального времени. Главное применение такой системы – промышленные и встроенные системы, но на обычном компьютере она тоже может быть интересна. Например тем, кто часто занимается обработкой звука и видео или постоянно грузит систему какими-нибудь ресурсоемкими вычислениями. Также есть положительный эффект от применения этого ядра на highload-серверах.

Патч на [https://www.kernel.org/pub/linux/kernel/projects/rt/](https://www.kernel.org/pub/linux/kernel/projects/rt/)

#### -bld

**Важно:** Этот патч находится в разработке.

[BLD](https://code.google.com/p/bld/) (Barbershop Load Distribution) лучше всего описывается как O(1) техника сортировки процессов. Это реализация альтернативного алгоритма планирования задач. BLD ограничивается решением задачи по корректному распределению нагрузки путем отслеживания не всех привязанных к CPU очередей, а только наиболее и наименее загруженных очередей выполнения (rq, runqueue). BLD не пытается балансировать нагрузку на систему в контексте отслеживания бездействующих idle-процессов, а акцентирует внимание на распределении всей нагрузки между имеющимися процессорами наиболее простым путём с минимальным числом усложнений. Главным достоинством BLD является сам подход, показывающий что достаточно простыми методами можно добиться равномерного распределения нагрузки, не заботясь особенно о том сколько CPU используется в системе и соответственно без лавинообразного падения производительности на накладные расходы при увеличении числа CPU (BLD обеспечивает уровень производительности O(i), где i - число CPU).

По материалам [этой новости](http://www.opennet.ru/opennews/art.shtml?num=33070%7C)

#### -grsecurity

[Grsecurity](/index.php/Grsecurity "Grsecurity") Из [[2]](https://ru.wikipedia.org/wiki/Grsecurity) Это проект для Linux, который включает в себя некоторые улучшения связанные с безопасностью, включая принудительный контроль доступа, рандомизацию ключевых локальных и сетевых информативных данных, ограничения /proc и chroot() jail, контроль сетевых сокетов, контроль возможностей, и добавочные функции аудита. Типичной областью применения являются web-сервера и системы, которые принимают удалённые соединения из сомнительных мест, такие как сервера, которые обеспечивают shell-доступ для пользователей. Патч grsecurity выпущен под GPL, является свободным ПО и включает в себя набор патчей PaX. Создатель и ведущий разработчик grsecurity — Brad Spengler aka. Spender.

Grsecurity патчи можно посмотреть на [https://grsecurity.net](https://grsecurity.net)

#### Tiny-Патчи

Цель[Linux Tiny](http://elinux.org/Linux_Tiny) использование минимального дискового пространства и оперативной памяти, а также облегчение труда маломощных компьютеров. Целевые пользователи являются разработчиками встраиваемых систем и пользователями маломощных или устаревших машин, таких как 386/

Патч-релизы против господствующего Linux ядра были прекращены. Разработчики решили сосредоточиться на нескольких патчах и попытках поставить их в официальное ядро.

#### -pf

[linux-pf](https://aur.archlinux.org/packages/linux-pf/) Это набор патчей, поверх официального ядра, обеспечивающих повышенную отзывчивость системы, предоставляющих альтернативную подсистему гибернации (более быстрая, по сравнению с основной), а также уменьшают использование памяти с помощью техники объединения одинаковых страниц. Набор патчей включает в себя: планировщик процессов BFS от Кона Коливаса (Con Kolivas) с дополнительными исправлениями от Альфреда Чена (Alfred Chen), планировщик ввода-вывода BFQ Паоло Валенте (Paolo Valente), Арианны Аванзини (Arianna Avanzini) и Мауро Маринони (Mauro Marinoni), подсистема гибернации TuxOnIce от Найджела Каннингема (Nigel Cunningham), реализация техники слияния одинаковых страниц в памяти UKSM от Най Ся (Nai Xia), патч от Graysky, расширяющий список процессоров для оптимизации ядра компилятором.

Смотрите [linux-pf](/index.php/Linux-pf "Linux-pf") для большей информации.

### Индивидуальные патчи

Эти патчи могут быть просто включены в любую сборку ванильного ядра или включены (возможно, с какой-то крупной тонкой настройки) в другой набор патчей.

#### Reiser4

[Reiser4](/index.php/Reiser4 "Reiser4")

#### fbsplash

[fbsplash](/index.php/Fbsplash "Fbsplash")

## Компиляция ядра

Arch Linux предусматривает несколько методов компиляции ядра.

### Используя Arch Build System (ABS)

Используя [ABS](/index.php/Arch_Build_System_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch Build System (Русский)") воспользуетесь высоким качеством существующих [linux](https://www.archlinux.org/packages/?name=linux) [PKGBUILD](/index.php/PKGBUILD_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PKGBUILD (Русский)") и преимущества [менеджера пакетов Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). PKGBUILD структурирован таким образом, что вы можете остановить сборку после получения исходного кода, и сконфигурировать ядро.

Смотрите [Kernels/Arch Build System](/index.php/Kernels/Arch_Build_System "Kernels/Arch Build System").

### Традиционный метод

Это загрузка архива с исходным кодом, распаковка, и компиляция. После компиляции доступны два способа установки: традиционный ручной метод, или[Makepkg](/index.php/Makepkg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Makepkg (Русский)") + [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)").

Преимуществом установки традиционным методом является то, что вы не привязаны к какому-либо дистрибутиву.

Смотрите [Kernels/Compilation/Traditional](/index.php/Kernels/Compilation/Traditional "Kernels/Compilation/Traditional").

### Пропиетарный NVIDIA драйвер

Смотрите[NVIDIA#Alternate install: custom kernel](/index.php/NVIDIA#Alternate_install:_custom_kernel "NVIDIA") инструкцию по использованию пропиетарного драйвера NVIDIA с патченным ядром.

## Смотрите также

*   [O'Reilly - Linux Kernel in a Nutshell](http://www.kroah.com/lkn/) (свободная электронная книга)

### Тесты и обзоры

*   [Есть ли польза от кастомных ядер](http://habrahabr.ru/post/131263/)
*   [Тест планировщика ввода/вывода BFQ](http://www.youtube.com/watch?v=J-e7LnJblm8)
*   [бенчмарки BFQ](http://algogroup.unimore.it/people/paolo/disk_sched/results.php)