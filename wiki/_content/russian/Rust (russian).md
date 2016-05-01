**Состояние перевода:** На этой странице представлен перевод статьи [Rust](/index.php/Rust "Rust"). Дата последней синхронизации: 25 мая 2015‎‎. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Rust&diff=0&oldid=374538).

[Rust](http://rust-lang.org/) - это язык программирования, который работает невероятно быстро, предотвращает ошибки на стадии компиляции, и позволяет писать безопасные многопоточные программы.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Проверка после установки](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
*   [2 Кросс-компиляция](#.D0.9A.D1.80.D0.BE.D1.81.D1.81-.D0.BA.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D1.8F.D1.86.D0.B8.D1.8F)
    *   [2.1 Windows](#Windows)
*   [3 Cargo](#Cargo)
    *   [3.1 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [4 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Для [установки](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") последней стабильной версии Rust, нужно [установить](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") пакет [rust](https://www.archlinux.org/packages/?name=rust) из [официального репозитория](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Если вы хотите собрать из исходных кодов стабильную, бета, или ночную версию Rust, то посетите [страницу загрузки Rust](http://www.rust-lang.org/install.html). Также можете использовать пакет [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) в [AUR](/index.php/AUR "AUR") для сборки ночной версии Rust (уже включает в себе систему сборки Cargo).

### Проверка после установки

Давайте убедимся, что Rust установился корректно, написав простую программу:

 `~/hello.rs` 
```
 fn main() {
     println!("Hello, World!");
 }

```

Затем скомпилируйте её с помощью `rustc`, введя это:

 `$ rustc hello.rs && ./hello` 
```
Hello, World!

```

## Кросс-компиляция

### Windows

В этом разделе, `$ARCH` будет целевой архитектурой (`x86_64` или `i686`).

1.  [Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)") [mingw-w64-gcc](https://www.archlinux.org/packages/?name=mingw-w64-gcc) и [wine](https://www.archlinux.org/packages/?name=wine)
2.  Add a binfmt definition for windows executables either manually or by installing [binfmt-wine](https://aur.archlinux.org/packages/binfmt-wine/) from the [AUR](/index.php/AUR "AUR").
3.  Install a copy of rust's standard library for windows in your rustlib directory (`/usr/local/lib/rustlib` if you're using [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) and `/usr/lib/rustlib` if you're using the official [rust](https://www.archlinux.org/packages/?name=rust) package). The easiest way to do this is to download the rust installer for windows for your target architecture, install it under wine (`wine start my-rust-installer.msi`) and copy `$INSTALL_DIR/bin/rustlib/$ARCH-pc-windows-gnu` into your rustlib directory.
4.  Finally, tell cargo where to find the MinGW-w64 gcc/ar by adding the following to your cargo config:

 `~/.cargo/config` 
```
[target.$ARCH-pc-windows-gnu]
linker = "/usr/bin/$ARCH-w64-mingw32-gcc"
ar = "/usr/$ARCH-w64-mingw32/bin/ar"

```

Finally, you can cross compile for windows by passing the `--target $ARCH-pc-windows-gnu` to cargo:

```
$ # Сборка
$ cargo build --release --target "$ARCH-pc-windows-gnu"
$ # Запуск unit-тестов через wine
$ cargo test --target "$ARCH-pc-windows-gnu"

```

## Cargo

[Cargo](https://crates.io/) - это система сборки и менеджер пакетов для Rust. Его можно установить через [AUR](/index.php/AUR "AUR") пакет [cargo-bin](https://aur.archlinux.org/packages/cargo-bin/).

Cargo помогает работать с зависимостями вашего проекта, скачивая из своего [хранилища](https://crates.io/) или стороннего [Git](/index.php/Git "Git") репозитория.

### Использование

Создадим новый проект с помощью Cargo:

 `$ cargo new hello_world --bin` 
**Note:** Cargo использует файл [манифеста](http://doc.crates.io/manifest.html) `Cargo.toml`, который содержит метаданные, необходимые Cargo для сборки вашего проекта. `Cargo.toml` 
```
[package]
name = "hello_world"
version = "0.1.0"
authors = ["Your Name <you@example.com>"]
```

## Смотрите также

*   [Официальный сайт языка программирования Rust (англ.)](http://rust-lang.org/)
*   [Статья в Wikipedia](https://ru.wikipedia.org/wiki/Rust_(язык_программирования))
*   [Примеры с небольшими описаниями (англ.)](http://rustbyexample.com/)
*   [Подборка материалов по изучению Rust (англ.)](https://github.com/ctjhoa/rust-learning)
*   [Хранилище Cargo библиотек (crates)](https://crates.io/)
*   [Перевод официальной книги по Rust](http://kgv.github.io/rust_book_ru)