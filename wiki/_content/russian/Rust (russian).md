**Состояние перевода:** На этой странице представлен перевод статьи [Rust](/index.php/Rust "Rust"). Дата последней синхронизации: 4 декабря 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Rust&diff=0&oldid=458391).

[Википедия](https://en.wikipedia.org/wiki/Rust_(programming_language) "wikipedia:Rust (programming language)"):

	*[Rust](https://www.rust-lang.org/) — мультипарадигмальный компилируемый язык программирования общего назначения, спонсируемый Mozilla Research, поддерживающий функциональное программирование, модель акторов и процедурное программирование.*

	*Внимание языка сосредоточено на трёх задачах: безопасность, скорость и параллелизм. Он сопоставим по скорости и возможностям с C++, однако, даёт большую безопасность при работе с памятью, что обеспечивается механизмами ограничения.*

## Contents

*   [1 Rust Core Library](#Rust_Core_Library)
*   [2 Стандартная библиотека Rust](#Стандартная_библиотека_Rust)
*   [3 Цикл выпуска](#Цикл_выпуска)
*   [4 Установка](#Установка)
    *   [4.1 Из репозитория](#Из_репозитория)
    *   [4.2 С помощью Rustup](#С_помощью_Rustup)
    *   [4.3 Проверка после установки](#Проверка_после_установки)
*   [5 Кросс-компиляция](#Кросс-компиляция)
    *   [5.1 С помощью rustup](#С_помощью_rustup_2)
    *   [5.2 Windows](#Windows)
    *   [5.3 Неофициальные пакеты](#Неофициальные_пакеты)
*   [6 Cargo](#Cargo)
    *   [6.1 Использование](#Использование)
*   [7 Поддержка в IDE](#Поддержка_в_IDE)
    *   [7.1 Инструменты](#Инструменты)
        *   [7.1.1 Racer](#Racer)
        *   [7.1.2 Clippy](#Clippy)
    *   [7.2 Редакторы](#Редакторы)
        *   [7.2.1 Atom](#Atom)
        *   [7.2.2 IntelliJ IDEA](#IntelliJ_IDEA)
        *   [7.2.3 Visual Studio Code](#Visual_Studio_Code)
        *   [7.2.4 Vim](#Vim)
        *   [7.2.5 Emacs](#Emacs)
        *   [7.2.6 Kate](#Kate)
*   [8 Смотрите также](#Смотрите_также)

### Rust Core Library

[Rust Core Library](https://doc.rust-lang.org/core/) — свободная от зависимостей основа стандартной библиотеки Rust. It interfaces directly with LLVM primitives, which allows Rust to be platform and hardware-agnostic. It is this integration with LLVM allows Rust to obtain greater performance than equivalent C applications compiled with Clang, making Rust software designed with libcore lower level than C. Developers looking to target software for embedded platforms may forego the standard library with `#[nostd]` to exclusively use the no-batteries-included core library for smaller binary sizes and improved performance. However, using `#[nostd]` limits the amount of software support that you can get from the larger Rust community as a majority of libraries require the standard library.

### Стандартная библиотека Rust

[Стандартная библиотека Rust](https://doc.rust-lang.org/std/index.html) предоставляет удобные абстракции высокого уровня, с помощью которых создаётся большинство переносимых программ на Rust. Например, она содержит типы `Vec`, `Iterator`, `Option`, `Result` и `String`; огромное число методов для примитивов языка; много стандартных макросов; поддержка ввода-вывода и многопоточности; использование кучи (heap) с помощью `Box`; и многие другие высокоуровневые возможности, не доступные в libcore.

### Цикл выпуска

Rust следует шестинедельному циклу выпуска, похожему на цикл выпуска Firefox. С каждым новым выпуском ядро и стандартные библиотеки улучшаются для поддержки большего числа платформ, повышения производительности и стабилизации новых возможностей для использования со стабильной версией Rust.

## Установка

### Из репозитория

Для установки последней стабильной версии Rust из официальных репозиториев Arch Linux, [установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D1%8C "Установить") пакет [rust](https://www.archlinux.org/packages/?name=rust). Он установит компилятор rustc. Также вы можете поставить [cargo](https://www.archlinux.org/packages/?name=cargo).

### С помощью Rustup

Официальный и рекомендумемый способ установки Rust для разработки ПО — с помощью инструмента [Rustup](https://www.rustup.rs/), написанного на Rust.

Преимуществом использования Rustup вместо обычной устаноки Rust из репозитория является возможность установки нескольких toolchains (stable, beta, nightly) для нескольких целевых платформ (windows, mac, android) и архитектур (x86, x86_64, arm).

Есть два способа установки rustup: официально поддерживаемый разработчиками Rust и поддерживаемый Arch Linux.

1.  Скачайте скрипт установки с помощью `curl -f https://sh.rustup.rs > rust.sh`, просмотрите его: `vim ./rust.sh` и запустите: `./rust.sh` для установки. Для обновления rustup в будущем запускайте `rustup self update`.
2.  Также пакет [rustup](https://www.archlinux.org/packages/?name=rustup) доступен в официальных репозиториях Arch Linux. Обратите внимание, что при установке с помощью этого пакета обновление с помощью `rustup self update` работать **не** будет, и для обновления rustup следует обновлять этот пакет с помощью pacman.

Теперь нужно установить сам Rust. По умолчанию будет установлена стабильная версия для вашей архитектуры.

**Note:** Добавьте $HOME/.cargo/bin в переменную окружения PATH перед выполнением команды rustup.

```
$ rustup default stable

```

Проверим версию Rust с помощью `rustc -V` :

 `$ rustc -V ` 
```
rustc 1.13.0 (2c6933acc 2016-11-07)

```

Если вы хотите использовать nightly, выполните:

```
$ rustup install nightly
$ rustup default nightly

```
 `$ rustc -V ` 
```
rustc 1.15.0-nightly (c80c31a50 2016-12-02)

```

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

### С помощью rustup

Использовать кросс-компиляцию с rustup очень легко. Он поддерживает очень много целевых платформ. Полный их список можно увидеть с помощью команды `rustup target list`.

Например, если вы хотите использовать stable Rust для Windows с компилятором GNU, сделайте следующее:

```
$ rustup install stable-x86_64-pc-windows-gnu

```

Эта команда установит только rust и инструменты для вашей целевой платформы, и для кросс-компиляции нужно сделать ещё несколько вещей.

### Windows

В этом разделе `$ARCH` будет целевой архитектурой (`x86_64` или `i686`).

1.  [Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_определенных_пакетов "Pacman (Русский)") [mingw-w64-gcc](https://aur.archlinux.org/packages/mingw-w64-gcc/) и [wine](https://www.archlinux.org/packages/?name=wine)
2.  Добавьте определение binfmt для исполняемых файлов Windows вручную или из [binfmt-wine](https://aur.archlinux.org/packages/binfmt-wine/).
3.  Если вы используете rustup, достаточно просто выполнить команды `rustup install stable-$ARCH-pc-windows-gnu` и `rustup target add $ARCH-pc-windows-gnu` для установки Rust и стандартной библиотеки для вашей архитектуры. Если вы не используете rustup, поставьте стандартную библиотеку Rust для Windows в вашем каталоге rustlib (`/usr/local/lib/rustlib` если у вас [rust-nightly-bin](https://aur.archlinux.org/packages/rust-nightly-bin/) или `/usr/lib/rustlib` если вы используете пакет [rust](https://www.archlinux.org/packages/?name=rust)). Простейший путь для этого — скачать установщик Rust под Windows для нужной вам архитектуры, установить с помощью Wine (`wine start my-rust-installer.msi`) и скопировать `$INSTALL_DIR/lib/rustlib/$ARCH-pc-windows-gnu` в ваш каталог rustlib.
4.  Подскажите cargo, где искать MinGW-w64 gcc/ar добавлением следующих параметров в `~/.cargo/config` (создайте файл, если он отсутствует):

 `~/.cargo/config` 
```
[target.$ARCH-pc-windows-gnu]
linker = "/usr/bin/$ARCH-w64-mingw32-gcc"
ar = "/usr/$ARCH-w64-mingw32/bin/ar"

```

Теперь вы можете выполнять кросс-компиляцию для Windows, указывая дополнительный аргумент `--target $ARCH-pc-windows-gnu` при вызове cargo:

```
$ # Сборка
$ cargo build --release --target "$ARCH-pc-windows-gnu"
$ # Запуск unit-тестов через wine
$ cargo test --target "$ARCH-pc-windows-gnu"

```

### Неофициальные пакеты

[Неофициальный репозиторий archlinuxcn](/index.php/Unofficial_user_repositories#archlinuxcn "Unofficial user repositories") содержит rust-nightly и стандартную библиотеку Rust для i686, ARM, ARMv7, Windows 32 и 64, и вы можете просто установить то, что вам нужно, и использовать кросс-компиляцию. Тем не менее вам нужно найти ARM toolchain самостоятельно. Для Windows 32bit вам нужно получить libgcc_s_dw2-1.dll для сборки и запуска.

## Cargo

[Cargo](https://crates.io/), систему сборки и менеджер пакетов для Rust, можно установить с помощью пакета [cargo](https://www.archlinux.org/packages/?name=cargo). Nightly доступен в AUR: [cargo-nightly-bin](https://aur.archlinux.org/packages/cargo-nightly-bin/). Если у вас [rustup](https://www.archlinux.org/packages/?name=rustup), то он уже содержит в себе cargo.

Cargo помогает работать с зависимостями вашего проекта, скачивая их из своего [хранилища](https://crates.io/) или стороннего [Git](/index.php/Git "Git") репозитория. Также он позволяет убедиться, что вы всегда будете получать повторяемые сборки. Рекомендуем прочитать [официальное руководство](http://doc.crates.io/guide.html).

### Использование

Для создания нового проекта с помощью Cargo:

 `$ cargo new hello_world --bin` 

Эта команда создаст директорию с файлом `Cargo.toml` по умолчанию и настроит сборку в исполняемый файл (потому что мы добавили `--bin`; иначе будет собираться библиотека).

**Note:** Cargo использует файл [манифеста](http://doc.crates.io/manifest.html) `Cargo.toml`, который содержит метаданные, необходимые Cargo для сборки вашего проекта. `Cargo.toml` 
```
[package]
name = "hello_world"
version = "0.1.0"
authors = ["Ваше Имя <you@example.com>"]
```

## Поддержка в IDE

### Инструменты

#### Racer

Движок автозаполнения [Racer](https://github.com/phildawes/racer) является лучшим способом получения поддержки автозаполнения на данный момент, однако для этого требуется также установить копию исходного кода Rust, которую вы можете получить одним из нескольких способов:

*   С помощью rustup: `rustup component add rust-src`
*   Из AUR: [rust-src](https://aur.archlinux.org/packages/rust-src/) или [rust-nightly-src](https://aur.archlinux.org/packages/rust-nightly-src/), в этом случае вы должны установить переменную окружения `RUST_SRC_PATH`.

После установки исходного кода вы можете использовать `Cargo` для установки racer или получить его из репозиториев ([rust-racer](https://www.archlinux.org/packages/?name=rust-racer)).

```
$ cargo install racer

```

#### Clippy

[Clippy](https://github.com/Manishearth/rust-clippy) использует поддержку плагинов компилятора в Nightly-сборках Rust, чтобы обеспечить большое количество дополнительных проверок для обнаружения и предупреждения о более широком разнообразии ошибок и неидиоматическом Rust. Поскольку для работы требуется поддержка плагинов компилятора, clippy не будет работать при компиляции с помощью стабильной версии компилятора Rust.

```
$ cargo +nightly install clippy

```

### Редакторы

#### Atom

[Atom](/index.php/Atom "Atom") поддерживает программирование на Rust, когда установлены оба следующих модуля: [language-rust](https://atom.io/packages/language-rust) и [linter-rust](https://atom.io/packages/linter-rust).

#### IntelliJ IDEA

В [IntelliJ IDEA](https://www.jetbrains.com/idea/) имеется [Rust plugin](https://github.com/intellij-rust/intellij-rust). Этот плагин также работает с CLion. При настройке toolchain используйте rustup для загрузки исходников (`rustup component add rust-src`), а затем выберите `~/.rustup/toolchains/<your toolchain>/bin` в качестве расположения toolchain.

#### Visual Studio Code

В [Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code") поддержка Rust может быть получена через официальное [kalitaalexey.vscode-rust](https://marketplace.visualstudio.com/items?itemName=kalitaalexey.vscode-rust) дополнение.

#### Vim

В [Vim](/index.php/Vim "Vim") поддержка Rust может быть получена через официальный [rust.vim](https://github.com/rust-lang/rust.vim) плагин.

#### Emacs

В [Emacs](/index.php/Emacs "Emacs") поддержка Rust может быть получена через официальный [rust-mode](https://github.com/rust-lang/rust-mode) плагин или [emacs-rust-mode](https://aur.archlinux.org/packages/emacs-rust-mode/) пакет.

#### Kate

В Kate поддержка Rust может быть получена через официальный [kate](https://github.com/rust-lang/kate-config) плагин. Он устанавливается по-умолчанию пакетом [kate](https://www.archlinux.org/packages/?name=kate), требует установки [racer](https://aur.archlinux.org/packages/racer/) и ручной активации.

## Смотрите также

*   [Официальный сайт языка программирования Rust (англ.)](https://www.rust-lang.org/)
*   [Документация Rust (англ.)](https://www.rust-lang.org/documentation.html)
*   [Официальная Книга (англ.)](https://doc.rust-lang.org/stable/book/)
*   [Перевод Книги на русский язык](https://rurust.github.io/rust_book_ru/)
*   [Обзор API стандартной библиотеки (англ.)](https://doc.rust-lang.org/std/)
*   [Rust на примерах (англ.)](https://doc.rust-lang.org/stable/rust-by-example/)
*   [Rust на примерах (частичный перевод на русский язык)](https://rurust.github.io/rust-by-example-ru/)
*   [Подборка материалов по изучению Rust](https://github.com/ctjhoa/rust-learning)
*   [Библиотеки (крейты, crates), доступные через Cargo](https://crates.io/)
*   [Новостная рассылка This Week in Rust (англ.)](https://this-week-in-rust.org/)
*   [Блог языка программирования Rust (англ.)](https://blog.rust-lang.org/)
*   [Форум пользователей Rust (англ.)](https://users.rust-lang.org/)
*   [The Rust Internals Forum (англ.)](https://internals.rust-lang.org/)
*   [Список библиотек и ресурсов Awesome Rust: A curated list of Rust libraries and resources (англ.)](https://rust.libhunt.com/)
*   [Статья в Википедии](https://en.wikipedia.org/wiki/ru:Rust_(%D1%8F%D0%B7%D1%8B%D0%BA_%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D1%8F) "wikipedia:ru:Rust (язык программирования)")
*   [Русскоязычный сайт о Rust](https://rustycrate.ru/)
*   [Русскоязычный форум](https://forum.rustycrate.ru/)