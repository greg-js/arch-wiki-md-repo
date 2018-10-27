**Состояние перевода:** На этой странице представлен перевод статьи [Getting and installing Arch](/index.php/Getting_and_installing_Arch "Getting and installing Arch"). Дата последней синхронизации: 15 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Getting_and_installing_Arch&diff=0&oldid=482030).

Этот раздел содержит статьи про релизы Arch Linux и информацию о том, как скачать и установить Arch Linux.

Установочные образы и их [GnuPG](/index.php/GnuPG_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GnuPG (Русский)") подписи можно получить на странице [Загрузок](https://archlinux.org/download/).

## Проверка подписи

Перед использованием рекомендуется проверить подпись образа, особенно при загрузке из "HTTP-зеркала", где загрузка может быть подвержена перехвату для [обслуживания вредоносных образов](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

В системе с установленным [GnuPG](/index.php/GnuPG_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GnuPG (Русский)") сделайте это, загрузив *PGP-подпись* (под *Контрольные суммы*) в каталог ISO, и [проверьте](/index.php/GnuPG#Verify_a_signature "GnuPG") это с помощью `gpg --keyserver-options auto-key-retrieve --verify archlinux-<версия>-x86_64.iso.sig`.

Альтернативно, запустите `pacman-key -v archlinux-<версия>-x86_64.iso.sig` из существующей установки Arch Linux.

**Примечание:**

*   Подписью можно манипулировать, если она загружается с зеркального сайта, а не из [archlinux.org](https://archlinux.org/download/) как указано выше. В этом случае следует убедиться, что открытый ключ, который используется для расшифровки подписи, подписывается другим, заслуживающим доверия ключом. Команда `gpg` выводит отпечаток открытого ключа.
*   Еще один способ проверки подлинности подписи - убедиться, что отпечаток открытого ключа идентичен ключевому отпечатку файла [Arch Linux developer](https://www.archlinux.org/people/developers/), который подписал ISO-файл. Смотрите [Википедия:Криптосистема_с_открытым_ключом](https://en.wikipedia.org/wiki/ru:%D0%9A%D1%80%D0%B8%D0%BF%D1%82%D0%BE%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0_%D1%81_%D0%BE%D1%82%D0%BA%D1%80%D1%8B%D1%82%D1%8B%D0%BC_%D0%BA%D0%BB%D1%8E%D1%87%D0%BE%D0%BC "w:ru:Криптосистема с открытым ключом") для получения дополнительной информации о процессе открытого ключа для аутентификации ключей.

## Способы установки

В таблице ниже представлен обзор распространенных способов загрузки установочного носителя. Поскольку процесс установки извлекает пакеты из удаленного репозитория, эти способы требуют подключения к Интернету. Если у вас его нет, смотрите статью [Установка пакетов без доступа к интернету](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%BF%D0%B0%D0%BA%D0%B5%D1%82%D0%BE%D0%B2_%D0%B1%D0%B5%D0%B7_%D0%B4%D0%BE%D1%81%D1%82%D1%83%D0%BF%D0%B0_%D0%BA_%D0%B8%D0%BD%D1%82%D0%B5%D1%80%D0%BD%D0%B5%D1%82%D1%83 "Установка пакетов без доступа к интернету") и раздел [Archiso (Русский)#Установка без подключения к Интернету](/index.php/Archiso_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA_.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82.D1.83 "Archiso (Русский)").

**Примечание:**

*   Указание текущего загрузочного устройства на диск, содержащий установочный носитель Arch, обычно достигается нажатием клавиши во время фазы [POST](https://en.wikipedia.org/wiki/ru:POST_(%D0%B0%D0%BF%D0%BF%D0%B0%D1%80%D0%B0%D1%82%D0%BD%D0%BE%D0%B5_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5) "w:ru:POST (аппаратное обеспечение)"), как показано на заставке. Подробнее смотрите в руководстве вашей материнской платы.
*   Когда появится меню Arch, выберите *Boot Arch Linux* и нажмите `Enter`, чтобы войти в окружение установки.
*   Смотрите [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) список [параметров загрузки](/index.php/Kernel_parameters_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Kernel parameters (Русский)"), и [packages.both](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) список включенных пакетов.

| Способ | Статьи | Условия |
| Запись образа на флэш-накопитель или оптический диск, затем загрузка с него. | 

*   [Установочный образ на USB-накопителе](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BE%D1%87%D0%BD%D1%8B%D0%B9_%D0%BE%D0%B1%D1%80%D0%B0%D0%B7_%D0%BD%D0%B0_USB-%D0%BD%D0%B0%D0%BA%D0%BE%D0%BF%D0%B8%D1%82%D0%B5%D0%BB%D0%B5 "Установочный образ на USB-накопителе")
*   [Оптический привод#Запись](/index.php/%D0%9E%D0%BF%D1%82%D0%B8%D1%87%D0%B5%D1%81%D0%BA%D0%B8%D0%B9_%D0%BF%D1%80%D0%B8%D0%B2%D0%BE%D0%B4#.D0.97.D0.B0.D0.BF.D0.B8.D1.81.D1.8C "Оптический привод")

 | 

*   Установка на одну, или несколько машин в большинстве
*   Приобретение непосредственно загрузочной системы

 |
| Монтирование образа на сервере и загрузка его по сети у клиентов. | 

*   [PXE (Русский)](/index.php/PXE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PXE (Русский)")
*   [Бездисковая система](/index.php/%D0%91%D0%B5%D0%B7%D0%B4%D0%B8%D1%81%D0%BA%D0%BE%D0%B2%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "Бездисковая система")

 | 

*   Модель клиент-сервер
*   Подключение к сети (1Гбит+)

 |
| Монтирование образа в запущенной системе Linux и установка Arch из окружения chroot. | 

*   [Установка Arch из другого дистрибутива](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_Arch_%D0%B8%D0%B7_%D0%B4%D1%80%D1%83%D0%B3%D0%BE%D0%B3%D0%BE_%D0%B4%D0%B8%D1%81%D1%82%D1%80%D0%B8%D0%B1%D1%83%D1%82%D0%B8%D0%B2%D0%B0 "Установка Arch из другого дистрибутива")
*   [Установка по SSH](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%BF%D0%BE_SSH "Установка по SSH")

 | 

*   Замена существующей системы с уменьшенным временем простоя
*   Установка на локальном компьютере, либо на удаленном через [VNC](/index.php/Vncserver_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vncserver (Русский)") или [SSH](/index.php/SSH_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "SSH (Русский)")

 |
| Настройка виртуальной машины и установка Arch в качестве гостевой системы. | 

*   [Категория:Монитор виртуальных машин](/index.php/Category:Hypervisors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Hypervisors (Русский)")
*   [Moving an existing install into (or out of) a virtual machine](/index.php/Moving_an_existing_install_into_(or_out_of)_a_virtual_machine "Moving an existing install into (or out of) a virtual machine")

 | 

*   Операционная система, совместимая с программным обеспечением для виртуализации
*   Приобретение изолированной системы для обучения, тестирования или отладки

 |
| Установка Arch рядом с установленной Windows. | 

*   [Двойная загрузка: Windows и Arch](/index.php/%D0%94%D0%B2%D0%BE%D0%B9%D0%BD%D0%B0%D1%8F_%D0%B7%D0%B0%D0%B3%D1%80%D1%83%D0%B7%D0%BA%D0%B0:_Windows_%D0%B8_Arch "Двойная загрузка: Windows и Arch")

 | 

*   Машина, совместно используемая пользователями Windows
*   Позволяет легко сделать заводской сброс на устройствах с предустановленной Windows

 |
| Установка Arch в подсистему Linux на Windows. | 

*   [Установка на WSL](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%BD%D0%B0_WSL "Установка на WSL")

 | 

*   Машина под управлением Windows 10 Fall Creators Update или позже
*   Нет графического интерфейса, за исключением доступа к сети

 |

## Смотрите также

*   [README.transfer](https://projects.archlinux.org/archiso.git/tree/docs/README.transfer)
*   [README.altbootmethods](https://projects.archlinux.org/archiso.git/tree/docs/README.altbootmethods)