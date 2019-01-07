**Состояние перевода:** На этой странице представлен перевод статьи [Dynamic Kernel Module Support](/index.php/Dynamic_Kernel_Module_Support "Dynamic Kernel Module Support"). Дата последней синхронизации: 6 января 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Dynamic_Kernel_Module_Support&diff=0&oldid=555532).

Из [Википедии](https://en.wikipedia.org/wiki/ru:Dynamic_Kernel_Module_Support "wikipedia:ru:Dynamic Kernel Module Support"):

	Dynamic Kernel Module Support (DKMS) — это фреймворк, который используется для генерации тех модулей ядра Linux, которые в общем случае не включены в дерево исходного кода. DKMS позволяет драйверам устройств автоматически пересобираться, когда ядро уже установлено.

Это означает, что пользователь может не ждать, пока какая-то компания, проект или сопроводитель пакета выпустит новую версию модуля. После введения [Pacman#Hooks](/index.php/Pacman#Hooks "Pacman") пересборка модулей осуществляется автоматически во время обновления ядра.

## Contents

*   [1 Установка](#Установка)
*   [2 Обновления](#Обновления)
*   [3 Использование](#Использование)
    *   [3.1 Список модулей](#Список_модулей)
    *   [3.2 Пересборка модулей](#Пересборка_модулей)
    *   [3.3 Удаление модулей](#Удаление_модулей)
*   [4 Создание DKMS пакета](#Создание_DKMS_пакета)
    *   [4.1 Название пакета](#Название_пакета)
    *   [4.2 Зависимости](#Зависимости)
    *   [4.3 Построение директории для исходных файлов](#Построение_директории_для_исходных_файлов)
    *   [4.4 Применение патчей](#Применение_патчей)
    *   [4.5 Автоматическая загрузка модуля в .install](#Автоматическая_загрузка_модуля_в_.install)
    *   [4.6 Вывод namcap](#Вывод_namcap)
    *   [4.7 Пример](#Пример)
        *   [4.7.1 PKGBUILD](#PKGBUILD)
        *   [4.7.2 dkms.conf](#dkms.conf)
        *   [4.7.3 .install](#.install)
*   [5 Смотрите также](#Смотрите_также)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [dkms](https://www.archlinux.org/packages/?name=dkms) и заголовочные файлы ядра ([linux-headers](https://www.archlinux.org/packages/?name=linux-headers) для ядра по умолчанию — [linux](https://www.archlinux.org/packages/?name=linux)).

Значительное число модулей, не включенных в ядро, имеют DKMS вариант; некоторые из них размещаются в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), но большинство из них можно найти только в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

## Обновления

Обычно пересборка модулей DKMS во время обновления ядра выполняется бесшовно, но что-то может пойти не так. Следует обратить особое внимание на вывод [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")! Это, в частности, относится к тем системам, которым требуется модуль DKMS для успешной загрузки и/или если вы используете DKMS с ядром не из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Для того, чтобы следовать изменениям в ядре, исправить ошибки или добавить необходимый функционал, подумайте об обновлении соответствующего пакета DKMS перед перезагрузкой.

## Использование

Использование DKMS вручную.

Автозавершение по `Tab` будет доступно после выполнения команды:

```
# source /usr/share/bash-completion/completions/dkms

```

### Список модулей

Чтобы увидеть текущее состояние модулей, версий и ядер внутри дерева, выполните:

```
# dkms status

```

### Пересборка модулей

Пересборка всех модулей для текущего ядра:

```
# dkms autoinstall

```

или для конкретного ядра:

```
# dkms autoinstall -k 3.16.4-1-ARCH

```

Сборка *конкретного* модуля для текущего ядра:

```
# dkms install -m nvidia -v 334.21

```

или просто:

```
# dkms install nvidia/334.21

```

Сборка модуля для *всех* ядер:

```
# dkms install nvidia/334.21 --all

```

### Удаление модулей

Удаление модуля (старые автоматически не удаляются):

```
# dkms remove -m nvidia -v 331.49 --all

```

или просто:

```
# dkms remove nvidia/331.49 --all

```

Если пакет [dkms](https://www.archlinux.org/packages/?name=dkms) удален, то теряется информация о предыдущих файлах сборки модуля. В этом случае, перейдите в директорию `/usr/lib/modules/KERNELVERSION-ARCH` и удалите все файлы и папки, которые больше не используются.

## Создание DKMS пакета

Здесь приведены некоторые рекомендации, которым необходимо следовать при создании пакета DKMS.

### Название пакета

Пакеты DKMS обозначают приписыванием "*-dkms*" к исходному названию пакета.

Переменная `$_pkgname` часто используется после `$pkgname`, чтобы описать название пакета без "*-dkms*" (например, `_pkgname=${pkgname%-*}`). Это полезно для того, чтобы сохранялось сходство между исходным PKGBUILD пакета и его DKMS вариантом.

### Зависимости

Зависимости должны наследоваться от оригинального пакета с добавлением [dkms](https://www.archlinux.org/packages/?name=dkms) и удалением [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (так как он указан в пакете dkms как *необязательный*).

### Построение директории для исходных файлов

Сборка исходных файлов должна происходить в (сборочная директория по умолчанию):

```
/usr/src/*PACKAGE_NAME*-*PACKAGE_VERSION*

```

В директории, где хранятся пакеты, конфигуратор DKMS говорит DKMS, как построить модуль (`dkms.conf`), включая переменные `PACKAGE_NAME` и `PACKAGE_VERSION`.

*   `PACKAGE_NAME` - имя проекта (обычно `$_pkgname` или `$_pkgbase`).
*   `PACKAGE_VERSION` - по соглашению это также должно быть `$pkgver`.

### Применение патчей

К исходным файлам можно применить патчи непосредственно в PKGBUILD или через `dkms.conf`.

### Автоматическая загрузка модуля в .install

Загрузку и выгрузку модулей следует оставить пользователю. Учитывая то, что может произойти сбой модуля при загрузке.

Кроме того, вам не нужно каждый раз запускать `depmod`, чтобы обновить зависимости модуля ядра. Pacman автоматически вызывает `dkms install` и `dkms remove`, как хуки. `dkms install` гарантирует, что `depmod` будет запущен по окончании процесса. `dkms install` зависит от `dkms build` (чтобы собрать исходники для текущего ядра), который, в свою очередь, зависит от `dkms add` (чтобы создать символическую ссылку на `/var/lib/dkms/<package>/<version>/source` в `/usr/src/<package>`).

### Вывод namcap

Использование [namcap](/index.php/Namcap "Namcap") (инструмент, который пытается проверить распространенные ошибки и нестандартные решения в пакете) это хорошая практика, следует хоть раз проверить *любой* пакет с помощью этого инструмента; однако, он еще не был обновлен для использования со специфичными пакетами DKMS.

Например, DKMS по умолчанию использует `/usr/src/`, но Namcap считает что это нестандартная директория, это немного противоречит [ссылке](https://en.wikipedia.org/wiki/ru:Filesystem_Hierarchy_Standard "wikipedia:ru:Filesystem Hierarchy Standard").

### Пример

Вот пример пакета, который редактирует `dkms.conf` в соответствии с именем пакета и его версии.

#### PKGBUILD

 `PKGBUILD` 
```
# Maintainer: foo <foo(at)gmail(dot)com>
# Contributor: bar <bar(at)gmai(dot)com>

_pkgbase=amazing
pkgname=amazing-dkms
pkgver=1
pkgrel=1
pkgdesc="The Amazing kernel modules (DKMS)"
arch=('i686' 'x86_64')
url="[https://www.amazing.com/](https://www.amazing.com/)"
license=('GPL2')
depends=('dkms')
conflicts=("${_pkgbase}")
install=${pkgname}.install
source=("${url}/files/tarball.tar.gz"
        'dkms.conf'
        'linux-3.14.patch')
md5sums=(*use 'updpkgsums'*)

build() {
  cd ${_pkgbase}-${pkgver}

  # Patch
  patch -p1 -i "${srcdir}"/linux-3.14.patch

}

package() {
  # Install
  msg2 "Starting make install..."
  make DESTDIR="${pkgdir}" install

  # Copy dkms.conf
  install -Dm644 dkms.conf "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

  # Set name and version
  sed -e "s/@_PKGBASE@/${_pkgbase}/" \
      -e "s/@PKGVER@/${pkgver}/" \
      -i "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/dkms.conf

  # Copy sources (including Makefile)
  cp -r ${_pkgbase}/* "${pkgdir}"/usr/src/${_pkgbase}-${pkgver}/
}
```

#### dkms.conf

 `dkms.conf` 
```
PACKAGE_NAME="@_PKGBASE@"
PACKAGE_VERSION="@PKGVER@"
MAKE[0]="make --uname_r=$kernelver"
CLEAN="make clean"
BUILT_MODULE_NAME[0]="@_PKGBASE@"
DEST_MODULE_LOCATION[0]="/kernel/drivers/misc"
AUTOINSTALL="yes"
```

#### .install

Теперь в *pacman* есть хуки DKMS, поэтому вам не нужно указывать конфигурацию, специфичную для DKMS, в вашем файле `.install`. `dkms install` и `dkms remove` будут вызываны автоматически.

## Смотрите также

*   [Linux Journal: Exploring Dynamic Kernel Module Support](http://www.linuxjournal.com/article/6896)