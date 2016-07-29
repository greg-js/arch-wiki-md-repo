**[Package creation guidelines](/index.php/Creating_packages "Creating packages")**

* * *

[CLR](/index.php/CLR_package_guidelines "CLR package guidelines") – [Cross](/index.php/Cross-compiling_tools_package_guidelines "Cross-compiling tools package guidelines") – [Eclipse](/index.php/Eclipse_plugin_package_guidelines "Eclipse plugin package guidelines") – [Free Pascal](/index.php/Free_Pascal_package_guidelines "Free Pascal package guidelines") – [GNOME](/index.php/GNOME_package_guidelines "GNOME package guidelines") – [Go](/index.php/Go_package_guidelines "Go package guidelines") – [Haskell](/index.php/Haskell_package_guidelines "Haskell package guidelines") – [Java](/index.php/Java_package_guidelines "Java package guidelines") – [KDE](/index.php/KDE_package_guidelines "KDE package guidelines") – [Kernel](/index.php/Kernel_module_package_guidelines "Kernel module package guidelines") – [Lisp](/index.php/Lisp_package_guidelines "Lisp package guidelines") – [MinGW](/index.php/MinGW_package_guidelines "MinGW package guidelines") – [Node.js](/index.php/Node.js_package_guidelines "Node.js package guidelines") – [Nonfree](/index.php/Nonfree_applications_package_guidelines "Nonfree applications package guidelines") – [OCaml](/index.php/OCaml_package_guidelines "OCaml package guidelines") – [Perl](/index.php/Perl_package_guidelines "Perl package guidelines") – [PHP](/index.php/PHP_package_guidelines "PHP package guidelines") – [Python](/index.php/Python_package_guidelines "Python package guidelines") – [Ruby](/index.php/Ruby_Gem_package_guidelines "Ruby Gem package guidelines") – [VCS](/index.php/VCS_package_guidelines "VCS package guidelines") – [Web](/index.php/Web_application_package_guidelines "Web application package guidelines") – [Wine](/index.php/Wine_package_guidelines "Wine package guidelines")

Этот документ определяет стандарты для создания пакетов Common Language Runtime (.NET) для Arch Linux. На текущий момент только [Mono](/index.php/Mono "Mono") способен обеспечить эффективный и работоспособный запуск CLR в смешанных системах. Будьте внимательны - большинство CLR программ разработанных в среде Microsoft .NET могут не запустится в Mono, так как содержат платформозависимые .NET-факторы: вызовы P/Invoke и Microsoft DRM API (цифровые средства защиты авторских прав). Однако, в связке с [Wine](/index.php/Wine "Wine") (версия 1.5.6 и выше), у Вас есть некоторая вероятность запустить ваше приложение. Для получения информации смотрите [Wine PKGBUILD Guidelines](/index.php/Wine_PKGBUILD_Guidelines "Wine PKGBUILD Guidelines").

## Contents

*   [1 Подготовка к сборке пакетов](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [1.1 Подписанные сборки](#.D0.9F.D0.BE.D0.B4.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.81.D0.B1.D0.BE.D1.80.D0.BA.D0.B8)
*   [2 Примеры PKGBUILDs](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_PKGBUILDs)
    *   [2.1 xbuild](#xbuild)
        *   [2.1.1 Неподписанные DLL](#.D0.9D.D0.B5.D0.BF.D0.BE.D0.B4.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_DLL)
    *   [2.2 NAnt](#NAnt)
    *   [2.3 Prebuild](#Prebuild)

## Подготовка к сборке пакетов

*   Всегда добавляйте [mono](https://www.archlinux.org/packages/?name=mono) в `depends`
*   Всегда выставляйте `arch` в `any`. Mono не поддерживает сборку (запуск) 64-битных приложений.
*   Всегда добавляйте `!strip` в `options`
*   Если Вы собираете библиотеку (DLL), которая будет установлена в Mono's global assembly cache (GAC), добавте GAS в зависимости (к пакету) .
*   Если приложение/библиотека поставляется с отладочной базой данных (program debug database file, Foo.dll.pdb), переконвертируйте её: `pdb2mdb Foo.dll`
*   Если Вы собираете приложение (EXE), убедитесь в том, что добавили скрипт для запуска в `/usr/bin`. Пример скрипта:

```
#!/bin/sh
mono foo.exe $@

```

### Подписанные сборки

Если пакет будет установлен в GAC, убедитесь, что у Вас есть ключ для подписи. Если нет, то сгенерируйте его: `sn -k 1024 Foo.snk`. Затем Вам нужно дизасембелировать пакет: `monodis Foo.dll --output=Foo.il`. После чего соберать снова, но уже с подписью: `ilasm /dll /key:Foo.snk Foo.il`

## Примеры PKGBUILDs

### xbuild

#### Неподписанные DLL

```
# Maintainer: yourname <yourmail>
pkgname=foo
pkgver=1.0
pkgrel=1
pkgdesc="Fantabulous library for .Net"
arch=('any')
url="http://www.foo.bar"
license=('GPL')
depends=('mono')
options=('!strip')
source=("http://www.foo.bar/foobar.tar.gz")
md5sums=('4736ac4f34fd9a41fa0197eac23bbc24')

build() {
  cd "${srcdir}/foobar"

  xbuild Foo.sln

  # if the package is unsigned, do the following:
  cd "/bin/x86/Debug"
  monodis Foo.dll --output=Foo.il
  sn -k 1024 Foo.snk
  ilasm /dll /key:Foo.snk Foo.il
}

package() {
  cd "${srcdir}/foobar/bin/x86/Debug"

  install -Dm644 Foo.dll "$pkgdir/usr/lib/foobar/Foo.dll"
  install -Dm644 Foo.dll.mdb "$pkgdir/usr/lib/foobar/Foo.dll.mdb"

  # Register assembly into Mono's GAC
  gacutil -i Foo.dll -root "$pkgdir/usr/lib"
}

```

### NAnt

### Prebuild