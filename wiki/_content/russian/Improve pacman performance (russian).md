## Contents

*   [1 Увеличение скорости доступа к базе данных](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.B0_.D0.BA_.D0.B1.D0.B0.D0.B7.D0.B5_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85)
*   [2 Увеличение скорости загрузки](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8)
    *   [2.1 Использование wget](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_wget)
    *   [2.2 Использование aria2](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_aria2)
        *   [2.2.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
        *   [2.2.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [2.2.3 Подробнее об опциях](#.D0.9F.D0.BE.D0.B4.D1.80.D0.BE.D0.B1.D0.BD.D0.B5.D0.B5_.D0.BE.D0.B1_.D0.BE.D0.BF.D1.86.D0.B8.D1.8F.D1.85)
        *   [2.2.4 Дополнительные примечания](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.87.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [2.3 Использование powerpill-light](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_powerpill-light)
        *   [2.3.1 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.4 Использование airpac](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_airpac)
    *   [2.5 Скрипт зеркалирования - pacget (aria2)](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_-_pacget_.28aria2.29)
    *   [2.6 Использование других приложений](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
*   [3 Выбор самого быстрого зеркала](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D1.81.D0.B0.D0.BC.D0.BE.D0.B3.D0.BE_.D0.B1.D1.8B.D1.81.D1.82.D1.80.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
*   [4 Выбор локального зеркала](#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB.D0.B0)
*   [5 Использование rankmirrors](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_rankmirrors)
*   [6 Использование Reflector](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_Reflector)
*   [7 После смены зеркал](#.D0.9F.D0.BE.D1.81.D0.BB.D0.B5_.D1.81.D0.BC.D0.B5.D0.BD.D1.8B_.D0.B7.D0.B5.D1.80.D0.BA.D0.B0.D0.BB)
*   [8 Совместный доступ к пакетам по локальной сети](#.D0.A1.D0.BE.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BD.D1.8B.D0.B9_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF_.D0.BA_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0.D0.BC_.D0.BF.D0.BE_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B9_.D1.81.D0.B5.D1.82.D0.B8)

## Увеличение скорости доступа к базе данных

Pacman хранит всю информацию о пакетаx в коллекции маленьких файлов, один для каждого пакета. Увеличение скорости доступа к базе данных уменьшает время работы задач, связанных с базой данных, например, поиск пакетов и решение зависимостей пакета.

Самый безопасный и самый простой метод выполнить команду с правами root

```
pacman-optimize && sync

```

Будет выполнена попытка соединить все маленькие файлы в одном (физическом) местоположении на жестком диске так, чтобы головка жесткого диска не перемещалась по всему диску, обращаясь ко всем пакетам. Этот метод эффективен, но не наверняка. Это зависит от Вашей файловой системы, использования дискового пространства и фрагментации диска. В качестве более агрессивного варианта, перед оптимизацией базы данных, будет удаление из кэша всех неустановленных пакетов и неиспользуемых репозиториев:

```
# pacman -Sc && pacman-optimize

```

## Увеличение скорости загрузки

**Примечание:** Если у вас низкая скорость загрузки, убедитесь, что не используете зеркало ftp.archlinux.org ([новость с марта 2007 г.](https://www.archlinux.org/news/302/)), вместо него используйте другие зеркала из списка [зеркал](/index.php/Mirrors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Mirrors (Русский)").

Скорость Pacman'а при загрузке пакетов также можно улучшить, если использовать другое приложение для загрузки вместо встроенного в Pacman менеджера закачек.

В любом случае, прежде чем делать какие-либо изменения, убедитесь, что используете самый свежий Pacman.

```
pacman -Syu

```

### Использование wget

Если Вам нужны более мощные настройки прокси, нежели те, которые предоставляет встроенный менеджер закачек [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")'а - использование [wget](https://www.archlinux.org/packages/?name=wget) может быть более удобным.

Для того чтобы использовать `wget`, сначала установите его с помощью команды `pacman -S wget`, а затем отредактируйте `/etc/pacman.conf`, приведя в секции `[options]` строку **XferCommand =** к следующему виду:

```
XferCommand = /usr/bin/wget -c --passive-ftp -c %u

```

Вместо того чтобы размещать параметры `wget` в файле `/etc/pacman.conf`, Вы можете изменять непосредственно конфигурационный файл `wget`(общесистемный файл `/etc/wgetrc`, или пользовательские файлы `$HOME/.wgetrc`.

### Использование aria2

[aria2](/index.php/Aria2_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Aria2 (Русский)") - легковесная утилита загрузки с возможностью докачки и сегментированной HTTP/HTTPS и FTP загрузки. [aria2](http://aria2.sourceforge.net/) - одновременно поддерживает несколько HTTP/HTTPS и FTP подключений к зеркалам Arch, это означает, что может увеличиться скорости загрузки файлов и поиска пакетов.

**Примечание:** Включение aria2c в настройке XferCommand Pacman'а **не** приводит к параллельной закачке нескольких пакетов. Pacman вызывает XferCommand для одного пакета и ожидает завершения закачки перед вызовом для следующего. Для параллельной загрузки нескольких пакетов смотрите далее в разделе [powerpill-light](/index.php/Improve_pacman_performance#Using_powerpill-light "Improve pacman performance") section below.

#### Установка

Для загрузки и установки [aria2](https://www.archlinux.org/packages/?name=aria2) и зависимостей выполните:

```
# pacman -Syu aria2

```

#### Настройка

Найдите в файле `/etc/pacman.conf` секцию `[options]` и измените следующий параметр:

 `XferCommand = /usr/bin/aria2c --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 -t5 -d / -o %o %u` 

#### Подробнее об опциях

	`/usr/bin/aria2c`

	Полный путь к исполняемому файлу aria2.

	`--allow-overwrite=true`

	Перезапуск закачки если соответствующий файл не существует. (По умолчанию: false)

	`-c, --continue`

	Продолжить закачку частично загруженного файла если контрольный файл существует.

	`--file-allocation=none`

	Перед загрузкой заранее не выделять место под скачиваемый файл. (По умолчанию: prealloc) 

	`--log-level=error`

	Установить уровень ведения журнал - только ошибки. (По умолчанию: debug)

	`-m2, --max-tries=2`

	Предпринимать не более 2-х попыток для загрузки из зеркала выбранного файла. (По умолчанию: 5)

	`--max-connection-per-server=2`

	Устанавливать с зеркалом не более 2-х соединений на каждый файл. (По умолчанию: 1)

	`--max-file-not-found=5`

	Если в течении 5-ти попыток не будет получен ни один байт - отключать принудительную загрузку. (По умолчанию: 0)

	`--min-split-size=5M`

	Разбивать файл, только если его размер превышает 2;5MB = 10MB. (По умолчанию: 20M)

	`--no-conf`

	Запрет использования файла `aria2.conf` если он существует. (По умолчанию: `~/.aria2/aria2.conf`)

	`--remote-time=true`

	Использовать временные метки удаленного(-ых) файла(-ов) к локальному(-ым) файлу(-ам). (По умолчанию: false)

	`--summary-interval=60`

	Output download progress summary every 60 seconds. (По умолчанию: 60) 

	`-t5, --timeout=5`

	Установка 5-ти секундного тайм-аута для зеркала после установления соединения. (По умолчанию: 60)

	`-d, --dir`

	Директорию для загруженных файлов брать из настроек [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)").

	`-o, --output`

	Имя полученного файла из загруженного.

	`%o`

	Переменная предоставляющая локальные файлы согласно настройкам pacman.

	`%u`

	Переменная предоставляюща загруженные URL согласно настройкам pacman.

#### Дополнительные примечания

	 `--file-allocation=falloc`

	Рекомендуется к использованию с такими файловыми системами как ext4 (с поддержкой экстентов), btrfs или xfs, в связи с почти мгновенным выделением мета под большие (GB) файлы. Не стоит использовать с традиционными файловыим системами аналогичными ext3, в связи с тем, что времени на выделение затрачивается практически столько же, сколько на блокировку процессом aria2 и на переход к закачке.

	 `--summary-interval=0`

	Подавляет процесс загрузки основной выходной информации и может улучшить общую производительность. Журналирование будет вестись согласно значению установленному в опции `log-level`.

	 `XferCommand = /usr/bin/printf 'Downloading ' && echo %u | awk -F/ '{printf $NF}' && printf '...' && /usr/bin/aria2c -q --allow-overwrite=true -c --file-allocation=none --log-level=error -m2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=0 -t5 -d / -o %o %u && echo ' Complete!'`

	Использование команды XferCommand в таком виде не так полезно, но зато дает больше подробной и удобночитаемой информации.

### Использование powerpill-light

[pacman2aria2](http://xyne.archlinux.ca/projects/pacman2aria2/) предоставляет скрипт, называющийся [powerpill-light](https://aur.archlinux.org/packages/powerpill-light/), который можно использовать в качестве частичной замены [powerpill](/index.php/Powerpill_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Powerpill (Русский)"). И хотя это не полноценная обертка, как powerpill, но он поддерживает следующие возможности powerpill:

*   параллельную загрузку
*   сегментированную загрузку
*   поиск быстрых зеркал с помощью [Reflector](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)"), для увеличения скорости загрузки

Поэтому загрузка пакетов такая же быстрая, как и при использовании пакета [powerpill](https://aur.archlinux.org/packages/powerpill/).

Пакет pacman2aria2 можно установить из [AUR](https://aur.archlinux.org/packages.php?ID=47913) и из [репозитория Xyne's](http://xyne.archlinux.ca/repos/).

#### Использование

Запускайте powerpill-light, аналогично синхронизации с помощью pacman, но не используя "-S". К примеру, для обновления системы вместо "pacman -Su", выполните

```
 # powerpill-light -u

```

Для установки gnome, вместо "pacman -S gnome", выполните

```
 # powerpill-light gnome

```

### Использование airpac

Вкратце, [airpac](https://www.archlinux.org/packages/?name=airpac) является оболочкой [aria2c](https://www.archlinux.org/packages/?name=aria2c) для [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)"). И если [powerpill](https://aur.archlinux.org/packages/powerpill/) - это интерфейс над *pacman*, то *airpac* - это только загрузчик для него. Хотя, с другой стороны, поскольку *aria2c* только скачивает файлы, все, что касается непосредственно загрузки файлов, выполняется аналогично *powerpill*. Но через бэкенд нельзя загружать несколько файлов одновременно, так, как это делает *powerpill*.

По сути, *airpac* - это написанный на [Python](/index.php/Python_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Python (Русский)") скрипт [pacget](https://aur.archlinux.org/packages/pacget/). Основное же отличие *aria2c* заключается в обработке вывода. *airpac* отображает только самую минимальную информацию, т.е. прогресс загрузки, хотя прогрессбар в настоящее время и не используется (возможен в ближайшем будущем). Помимо этого, *airpac* кэширует базу данных файлов таким образом, чтобы не загружать ее при каждом обновлении базы пакетов. С другой стороны, поскольку *airpac* не понимает параметров *pacman*, будет нарушено `pacman -Syy`. В качестве обходного пути, для удаления кэшированных файлов `/var/lib/pacman/.airpac` можно выполнить `pacman -Sc`.

Конфигурационный файл - `/etc/airpac.conf`. На самом деле этот файл является конфигурационным для aria2c. Поэтому у пользователя есть возможность настроить airpac аналогично aria2c-у, без вмешательства в код airpac'а. Для получения дополнительной информации по настройкам - обратитесь к справочной документации aria2c.

По умолчанию airpac использует настройку *Server Performance Profile* из aria2c. Файл статистики расположен в `/var/lib/airpac.stats`. URI, по умолчанию, включено в *adaptive*.

Для использования измените в `/etc/pacman.conf`:

```
XferCommand = /usr/bin/airpac %u %o

```

### Скрипт зеркалирования - pacget (aria2)

Благодаря этому скрипту пользователи с широкополосным доступом могут значительно повысить скорость загрузки. В качестве зеркал для aria2, используются зеркала из `/etc/pacman.d/mirrorlist`. При этом aria2 загружает пакеты одновременно с нескольких зеркал, что дает хороший прирост в скорости загрузки пакетов.

**Примечание:** Вам понадобится добавить 'exec' перед /usr/bin/pacget в XferCommand. Это необходимо для того, чтоб при завершении pacget или aria2 (с id процесса pacget), также прекращал работу и pacman.

**Важно:** Использование зеркал которые не синхронизировались или не обновились может вызвать проблемы. Поэтому, для создания списка *быстрых* и *свежих* зеркал воспользуйтесь скриптом [(Русский)](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)"). Так же, ftp.archlinux.org допускает до двух IP. Вам нужно будет выбрать только один и указать IP адресс в `/etc/hosts`.
 `/usr/bin/pacget` 
```
#!/bin/bash

msg() {
  echo ""
  echo -e "   \033[1;34m->\033[1;0m \033[1;1m${1}\033[1;0m" >&2
}

error() {
  echo -e "\033[1;31m==> ERROR:\033[1;0m \033[1;1m$1\033[1;0m" >&2
}

CONF=/etc/pacget.conf
STATS=/etc/pacget.stats
ARIA2=$(which aria2c 2> /dev/null)

# ----- do some checks first -----
if [ ! -x "$ARIA2" ]; then
  error "aria2c was not found or isn't executable."
  exit 1
fi

if [ $# -ne 2 ]; then
  error "Incorrect number of arguments"
  exit 1
fi

filename=$(basename $1)
server=${1%/$filename}
arch=$(grep ^Architecture /etc/pacman.conf | cut -d '=' -f2 | sed 's/ //g')
if [[ $arch = "auto" ]]; then
  arch=$(uname -m)
fi
# Determine which repo is being used
repo=$(awk -F'/' '$(NF-2)~/^(community|core|extra|testing|comunity-testing|multilib)$/{print $(NF-2)}' <<< $server)
[ -z $repo ] && repo="custom"

# For db files, or when using a custom repo (which most likely doesn't have any mirror),
# use only the URL passed by pacman; Otherwise, extract the list of servers (from the include file of the repo) to download from
url=$1
if ! [[ $filename = *.db || $repo = "custom" ]]; then
  mirrorlist=$(awk -F' *= *' '$0~"^\\["r"\\]",/Include *= */{l=$2} END{print l}' r=$repo /etc/pacman.conf)
  if [ -n mirrorlist ]; then
    num_conn=$(grep ^split $CONF | cut -d'=' -f2)
    url=$(sed -r '/^Server *= */!d; s/Server *= *//; s/\$repo'"/$repo/"'; s/\$arch'"/$arch/; s/$/\/$filename/" $mirrorlist | head -n $(($num_conn *2)) )
  fi
fi

msg "Downloading $filename"
cd /var/cache/pacman/pkg/

touch $STATS

$ARIA2 --conf-path=$CONF --max-tries=1 --max-file-not-found=5 \
  --uri-selector=adaptive --server-stat-if=$STATS --server-stat-of=$STATS \
  --allow-overwrite=true --remote-time=true --log-level=error --summary-interval=0 \
  $url --out=${filename}.pacget && [ ! -f ${filename}.pacget.aria2 ] && mv ${filename}.pacget $2 && chmod 644 $2

exit $?

```
 `/etc/pacget.conf` 
```
# Файл логов
log=/var/log/pacget.log
# Количество серверов для загрузки
split=5
# Минимальный размер файла, который допускается дробить, т.е. загружать в несколько потоков (по умолчанию 20M)
min-split-size=1M
# Максимальная скорость загрузки (0 = без ограничений)
max-download-limit=0
# Минимальная скорость загрузки (0 = не важна)
lowest-speed-limit=0
# Время ожидания сервера
timeout=5
# 'none' или 'falloc'
file-allocation=none

```

Сохраните этот скрипт как /usr/bin/pacget.

```
# chmod 755 /usr/bin/pacget

```

И сделайте его исполняемым

В файле `/etc/pacman.conf`, секция [options], приведите параметр к следующему виду:

```
XferCommand = exec /usr/bin/pacget %u %o

```

**Примечание:** Если в вашем списке зеркал (/etc/pacman.d/*) сервер ftp.archlinux.org указан первым - то могут возникнуть проблемы связанные с тем, что зеркала не успевают синхронизироваться. Поэтому выберите зеркала которые уже синхронизировались, или которые вам больше подходят и переместите их в начало списка зеркал. Таким образом, даже если зеркала еще не успели синхронизироваться, закачка не будет вестись только с ftp.archlinux.org. Для облегчения поиска нужных серверов воспользуйтесь скриптом rankmirrors.

### Использование других приложений

C Pacman можно использовать и другие приложения для загрузки файлов. Вот некоторые приложения и связанные с ними настройки XferCommand:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`

## Выбор самого быстрого зеркала

При загрузке пакетов pacman использует зеркала в том порядке, в котором они записаны в `/etc/pacman.d/mirrorlist`. Однако может оказаться, что в начале списка расположены не самые быстрые зеркала.

**Примечание:** Написанное выше не касается [powerpill-light](/index.php/Improve_pacman_performance#Using_powerpill-light "Improve pacman performance"), поскольку пакеты скачиваются с нескольких зеркал одновременно, соответственно - повышается общая скорость закачки. Таким образом, скорость для каждого отдельного соединения уже не имеет такого значения, а для powerpill-light можно задать минимальную скорость подключения.

## Выбор локального зеркала

Проще всего отредактировать файл mirrorlist, поместив локальное зеркало в начало списка. pacman далее будет использовать это зеркало в качестве предпочитаемого.

Иначе, можно отредактировать pacman.conf, добавив локальное зеркало перед строкой, которая указывает на файл mirrorlist, т.е. там, где написано "add your preferred servers here". Это более безопасно, если все репозитории находятся на одном сервере.

## Использование rankmirrors

Для оценки качества связи и скорости доступа к зеркалам, которые использует pacman, можно воспользоваться [rankmirrors](/index.php/Mirrors_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.BE_.D1.81.D0.BA.D0.BE.D1.80.D0.BE.D1.81.D1.82.D0.B8 "Mirrors (Русский)").

## Использование Reflector

Для получения пользовательского списка зеркал, отсортированного по скорости загрузки, - воспользуйтесь [Reflector](/index.php/Reflector_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Reflector (Русский)").

## После смены зеркал

После смены зеркала необходимо обновить базу данных pacman. Для принудительной синхронизации зеркал, даже если было сообщение об актуальности базы данных, используйте спаренный параметр `y`.

```
# pacman -Syy

```

## Совместный доступ к пакетам по локальной сети

Если вам повезло и в вашей локальной сети имеется несколько компьютеров с Arch, то можно огранизовать совместный доступ с скачанным пакетам и, таким образом, значительно уменьшить время загрузки пакетов. Но имейте в виду, что нужно использовать пакеты соответствующей архитектуры (например только i686 или x86_64) иначе может возникнуть множество проблем.

Для получения дополнительной информации прочтите [Pacman tips#Network_shared_pacman_cache](/index.php/Pacman_tips#Network_shared_pacman_cache "Pacman tips").