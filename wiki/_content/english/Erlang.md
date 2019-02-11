[Erlang](https://www.erlang.org/) is a programming language with the specific qualities of immutable data and distributed computing.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Usage](#Usage)
*   [3 Tips and tricks](#Tips_and_tricks)
    *   [3.1 Emacs mode](#Emacs_mode)

## Installation

[Install](/index.php/Install "Install") the [erlang](https://www.archlinux.org/packages/?name=erlang) package.

## Usage

For further documentation you can read [Erlang's docs](http://erlang.org/doc/getting_started/intro.html).

To activate the console, type in the command `erl`

Where you can enter commands like so:

```
   Erlang/OTP 21 [erts-10.1] [source] [64-bit] [smp:4:4] [ds:4:4:10] [async-threads:1] [hipe]
   Eshell V10.1  (abort with ^G)
   1> 1 + 2.
   3
   2> (2 + 3) * 4 / 5.
   4.0
   3>

```

## Tips and tricks

### Emacs mode

To set up the included [Emacs](/index.php/Emacs "Emacs") mode, `erlang-mode`, follow the [documentation](http://erlang.org/doc/apps/tools/erlang_mode_chapter.html#setup-on-unix) (the OTP path is `/usr/lib/erlang`).