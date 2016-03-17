Из [Википедии](https://en.wikipedia.org/wiki/ru:Dynamic_Kernel_Module_Support "wikipedia:ru:Dynamic Kernel Module Support"):

	**Dynamic Kernel Module Support**(**DKMS**) — это фреймворк, который используется для генерации тех модулей ядра Linux, которые в общем случае не включены в дерево исходного кода. DKMS позволяет драйверам устройств автоматически пересобираться, когда ядро уже установлено.

## Contents

*   [1 Преимущества и недостатки](#.D0.9F.D1.80.D0.B5.D0.B8.D0.BC.D1.83.D1.89.D0.B5.D1.81.D1.82.D0.B2.D0.B0_.D0.B8_.D0.BD.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D1.82.D0.BA.D0.B8)
*   [2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [3 Обновления](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
*   [4 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [4.1 Список модулей](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
    *   [4.2 Пересборка модулей](#.D0.9F.D0.B5.D1.80.D0.B5.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
    *   [4.3 Удаление модулей](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
*   [5 Создание DKMS пакета](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_DKMS_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0)
    *   [5.1 Название пакета](#.D0.9D.D0.B0.D0.B7.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0)
    *   [5.2 Зависимости](#.D0.97.D0.B0.D0.B2.D0.B8.D1.81.D0.B8.D0.BC.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.3 Построение директории для исходных файлов](#.D0.9F.D0.BE.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B8_.D0.B4.D0.BB.D1.8F_.D0.B8.D1.81.D1.85.D0.BE.D0.B4.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2)
    *   [5.4 Применение патчей](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D1.82.D1.87.D0.B5.D0.B9)
    *   [5.5 Автоматическая загрузка модуля в .install](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D1.8F_.D0.B2_.install)
    *   [5.6 Вывод namcap](#.D0.92.D1.8B.D0.B2.D0.BE.D0.B4_namcap)
    *   [5.7 Пример](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80)
        *   [5.7.1 PKGBUILD](#PKGBUILD)
        *   [5.7.2 dkms.conf](#dkms.conf)
        *   [5.7.3 .install](#.install)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Преимущества и недостатки

*Преимуществом* использования DKMS является то, что модули можно будет пересобрать после обновления ядра. Это означает, что пользователь может не ждать, пока какая-то компания, проект или сопроводитель пакета выпустит новую версию модуля.

*Недостатком* использования DKMS является то, что DKMS портит базу данных Pacman. Проблема в том, что конечные модули больше не принадлежат какому-то пакету, поэтому Pacman не может их отследить. Однако, теоретически такая поддержка может быть добавлена с помощью перехватчиков (хуков) (смотрите: [FS#2985](https://bugs.archlinux.org/task/2985)).

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [dkms](https://www.archlinux.org/packages/?name=dkms).

Значительное число модулей, не включенных в ядро, имеют DKMS вариант; некоторые из них размещаются в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), но большинство из них можно найти только в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"). Ниже перечислены пакеты, которые имеют DKMS версию:

*   [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst"): [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/)
*   [NVIDIA](/index.php/NVIDIA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "NVIDIA (Русский)"):
    *   [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms)
    *   [nvidia-304xx-dkms](https://www.archlinux.org/packages/?name=nvidia-304xx-dkms)
    *   [nvidia-173xx-dkms](https://aur.archlinux.org/packages/nvidia-173xx-dkms/)
    *   [nvidia-96xx-dkms](https://aur.archlinux.org/packages/nvidia-96xx-dkms/)
*   [VirtualBox](/index.php/VirtualBox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VirtualBox (Русский)"), раздел [VirtualBox#Хосты, работающие со сторонним ядром](/index.php/VirtualBox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A5.D0.BE.D1.81.D1.82.D1.8B.2C_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.89.D0.B8.D0.B5_.D1.81.D0.BE_.D1.81.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.BD.D0.B8.D0.BC_.D1.8F.D0.B4.D1.80.D0.BE.D0.BC "VirtualBox (Русский)")
*   [VMware](/index.php/VMware_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "VMware (Русский)"), раздел [VMware#Using DKMS to manage the modules](/index.php/VMware#Using_DKMS_to_manage_the_modules "VMware")

## Обновления

Модули способны пересобираться через значительное количество обновления ядра, но время от времени нужно обновлять соответствующий пакет до перезагрузки. Это требуется для того, чтобы следовать изменениям в ядре, исправить ошибки или добавить необходимый функционал.

## Использование

Использование DKMS вручную.

Автозавершение по `Tab` будет доступно после выполнения команды:

```
# source /usr/share/bash-completion/completions/dkms

```

### Список модулей

Чтобы увидеть текущее состояние модулей, версий и ядер внутри дерева, выполните:

```
$ dkms status

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

Если пакет [dkms](https://www.archlinux.org/packages/?name=dkms) удален, то теряется информация о предыдущих файлах сборки модуля. В этом случае, перейдите в директорию `/usr/lib/modules/KERNELVERSION-ARCH` и удалите файлы и/или папки, которые больше не используются.

## Создание DKMS пакета

Здесь приведены некоторые рекомендации, которым необходимо следовать при создании пакета DKMS.

### Название пакета

Пакеты DKMS обозначают приписыванием "*-dkms*" к исходному названию пакета.

Переменная `$_pkgname` часто используется после `$pkgname`, чтобы описать название пакета без "*-dkms*" (например, `_pkgname=${pkgname%-*}`). Это полезно для того, чтобы сохранялось сходство между исходным PKGBUILD пакета и его DKMS вариантом.

### Зависимости

Зависимости должны наследоваться от оригинального пакета с добавлением [dkms](https://www.archlinux.org/packages/?name=dkms) и удалением [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) (так как он указан в пакете dkms как *необязательный*).

### Построение директории для исходных файлов

Сборка исходных файлов должна происходить в (сборочная директория DKMS по умолчанию):

```
/usr/src/*PACKAGE_NAME*-*PACKAGE_VERSION*

```

В директории, где хранятся пакеты, конфигуратор DKMS говорит DKMS как построить модуль (`dkms.conf`), включая переменные `PACKAGE_NAME` и `PACKAGE_VERSION`.

*   `PACKAGE_NAME` - имя проекта (обычно `$_pkgname` или `$_pkgbase`).
*   `PACKAGE_VERSION` - по соглашению это также должно быть `$pkgver`.

### Применение патчей

К исходным файлам можно применить патчи непосредственно в PKGBUILD или через `dkms.conf`.

### Автоматическая загрузка модуля в .install

Загрузку и выгрузку модулей следует оставить пользователю. Учитывая тот факт, что может произойти сбой модуля при загрузке.

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

  # Build
  msg2 "Starting ./configure..."
  ./configure

  msg2 "Starting make..."
  make
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

Вместо `depmod` теперь можно использовать `dkms install` (это зависит от `dkms build`, который зависит от `dkms add`):

 `amazing-dkms.install` 
```
# old version (without -$pkgrel): ${1%%-*}
# new version (without -$pkgrel): ${2%%-*}

post_install() {
    dkms install *amazing*/${1%%-*}
}

pre_upgrade() {
    pre_remove ${2%%-*}
}

post_upgrade() {
    post_install ${1%%-*}
}

pre_remove() {
    dkms remove *amazing*/${1%%-*} --all
}

```

**Совет:** Чтобы держать DKMS пакеты ближе к их не DKMS версиям: избегайте загромождения файлов при помощи специфичными для DKMS вещами (например, номера версий, которые нуждаются в обновлении).

## Смотрите также

*   [Linux Journal: Exploring Dynamic Kernel Module Support](http://www.linuxjournal.com/article/6896)