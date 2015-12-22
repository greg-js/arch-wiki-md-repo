# 1C Enterprise (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

**1C:Предприятие** - программный продукт компании «1С», предназначенный для автоматизации деятельности на предприятии.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Не видит HASP USB ключ](#.D0.9D.D0.B5_.D0.B2.D0.B8.D0.B4.D0.B8.D1.82_HASP_USB_.D0.BA.D0.BB.D1.8E.D1.87)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

1\. Скачиваем пакеты 1С Клиент и сервер актуальных версий.

2\. Распаковываем их всё в одну папку чтобы получить перечень пакетов, как в PKGBUILD ниже и переходим в эту директорию

3\. Создаём PKGBUILD фаил в директории с распаковаными пакетами со следующим содержимым

 `Пример файла PKGBUILD` 

```
# Maintainer: tsn <tsn@rimit.ru>;
pkgname=1c_enterprise83
_pkgname1c=1C_Enterprise83
if test "$CARCH" == x86_64; then
    _pkgarch1c=$CARCH		# Если собираем пакеты для 64 бит
else
    _pkgarch1c=('i386')		# Если собираем пакеты для 32 бит
fi
pkgver=8.3.6         # Поменяйте на вашу версию
pkgrel=2390          # Поменяйте на вашу версию
pkgdesc="1C 8.3 for Linux"
license=('custom')
arch=($CARCH)
options=('!strip')
depends=('libwebkit')
makedepends=('pkgextract')
url="www.1c.ru"
source=(
$_pkgname1c-client-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-client-nls-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-common-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-common-nls-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-server-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-server-nls-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-thin-client-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-thin-client-nls-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-ws-$pkgver-$pkgrel.$_pkgarch1c.rpm
$_pkgname1c-ws-nls-$pkgver-$pkgrel.$_pkgarch1c.rpm
)

md5sums=('28f1ea9c22bf493293d3edc7a5f54ef7'
         'f947dfd4927b0255fbe41fec5cdb4117'
         'b0b5f1606c5e8f51949a9d35ecf4ea5e'
         '7b4e5259228acd98f18955be397a8c78'
         'eaa186edc73086a5f2977eb39da4aaac'
         '718a2d2a8a0e998fcc2b4aafe7c58ac3'
         '6c69018ec2deabaf6df374b677b1e495'
         'badd3740e336686c6dc1528020d8d581'
         'da433f3f9d1beef5c0b7d0f276d40f58'
         '15f85758d76ee3a69f38291e6bdeb0a8')
package() {
   cd $pkgdir
   cp -r $srcdir/usr $pkgdir
   cp -r $srcdir/etc $pkgdir
   cp -r $srcdir/opt $pkgdir
}

```

**pkgver** - Версия технологической платформы. Измените на свою версию.

**pkgrel** - Номер сборки. Измените на свою версию.

4\. Для обновления контрольных сумм в файле _PKGBUILD_ для наших пакетов выполним:

```
$ updpkgsums

```

5\. Запускаем:

```
$ makepkg -s

```

Мы получили наш собраный пакет для установки "1С:Предприятие".

6\. Устанавливаем наш пакет:

```
# pacman -U 1c_enterprise83-8.3.6-2390-x86_64.pkg.tar.xz

```

## Запуск

Исполняемые файлы находятся в каталоге `/opt/1C/v8.3/_архитектура_платформы_/`.

## Решение проблем

### Не видит HASP USB ключ

Если система не видит лицензионный HASP-ключ, подключенный к компьютеру, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [aksusbd](https://aur.archlinux.org/packages/aksusbd/)<sup><small>AUR</small></sup> и [запустите](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D1%82%D0%B8%D1%82%D0%B5 "Запустите") службу `aksusbd`. После этого переподключите ключ к вашему копьютеру.

**Совет:** Проверить, что ключ виден в системе, можно в браузере, набрав в адресной строке `_ваш_IP_:1947`

## Смотрите также

*   [Кто соберет 1С Предприятие 8.3 для АУР ?](http://archlinux.org.ru/forum/topic/12594/)
*   [Yaourt (Русский)](/index.php/Yaourt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Yaourt (Русский)")

Retrieved from "[https://wiki.archlinux.org/index.php?title=1C_Enterprise_(Русский)&oldid=413094](https://wiki.archlinux.org/index.php?title=1C_Enterprise_(Русский)&oldid=413094)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Applications (Русский)](/index.php/Category:Applications_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Applications (Русский)")