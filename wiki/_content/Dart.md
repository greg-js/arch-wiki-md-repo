# Dart

From the language's [home page](http://dartlang.org):

NaN

## Contents

*   [1 Installation](#Installation)
*   [2 Example](#Example)
*   [3 Dart Editor](#Dart_Editor)
*   [4 Dart Vim Syntax](#Dart_Vim_Syntax)

## Installation

The latest version of Dart is available in the [official repositories](/index.php/Official_repositories "Official repositories") as [dart](https://www.archlinux.org/packages/?name=dart). The bleeding edge version of Dart is available in the [AUR](/index.php/AUR "AUR") as [dart-trunk](https://aur.archlinux.org/packages/dart-trunk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dart-trunk)]</sup>.

## Example

Place the following code in a temporary file named hello.dart:

```
void main() {
  print("Hello Arch User!");
}

```

Now, run the following in the same directory as hello.dart:

```
$ dart hello.dart

```

You should get the following output:

```
Hello Arch User!

```

## Dart Editor

Dart has its own editor, based on Eclipse, and it is available in the AUR as [dart-editor](https://aur.archlinux.org/packages/dart-editor/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dart-editor)]</sup> or [dart-editor-dev](https://aur.archlinux.org/packages/dart-editor-dev/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dart-editor-dev)]</sup> for the development version.

## Dart Vim Syntax

[vim-dart-plugin](https://aur.archlinux.org/packages/vim-dart-plugin/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/vim-dart-plugin)]</sup> provides a Vim plugin that supports the Dart language's syntax and provides highlighting for the language.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dart&oldid=392049](https://wiki.archlinux.org/index.php?title=Dart&oldid=392049)"