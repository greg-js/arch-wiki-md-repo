[Allegro](https://liballeg.org/) is, as their website states,

	a cross-platform library mainly aimed at video game and multimedia programming. It handles common, low-level tasks such as creating windows, accepting user input, loading data, drawing images, playing sounds, etc. and generally abstracting away the underlying platform. However, Allegro is not a game engine: you are free to design and structure your program as you like.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Use](#Use)
*   [3 Troubleshooting](#Troubleshooting)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [allegro](https://www.archlinux.org/packages/?name=allegro) package.

For the development version, install the [allegro-git](https://aur.archlinux.org/packages/allegro-git/) package.

There is also a package for the legacy version of Allegro, [allegro4](https://www.archlinux.org/packages/?name=allegro4), which you can use for source which it requires.

**Note:** Allegro 5 is not backwards compatible with Allegro 4\. Developing new applications using Allegro 4 is discouraged.

## Use

Once installed, include the necessary base header into necessary source files:

 `main.c`  `#include <allegro5/allegro5.h>` 

If your main function is inside a C++ file, then it must have this signature: `int main(int argc, char **argv)`

## Troubleshooting

*   A common first mistake is to forget to link against the Allegro libraries. For an overview, use `pkg-config --list-all` .

*   Another trap for young players is to forget to include and initialise the necessary modules. Each module is a header, which needs to be included in the source file. Make sure you initialised it with the correct command and linked against the module, see above. For the exact details, refer to the manual.

## See also

*   [Allegro documentation](https://liballeg.org/api.html) files and reference manual
*   [Allegro new Wiki](https://github.com/liballeg/allegro_wiki/wiki)
*   [Old Wiki, which is slowly migrating to one linked right above](https://wiki.allegro.cc/)
*   [Allegro community network](https://www.allegro.cc/about)