[Neovim](https://neovim.io/) jest forkiem [Vim](/index.php/Vim "Vim") mającym na celu poprawę doświadczenia użytkownika, wtyczek i programów GUI.

## Contents

*   [1 Instalacja](#Instalacja)
*   [2 Konfiguracja](#Konfiguracja)
    *   [2.1 Przejście z vima](#Przej.C5.9Bcie_z_vima)
        *   [2.1.1 Ładowanie dodatków vima](#.C5.81adowanie_dodatk.C3.B3w_vima)
*   [3 Porady i wskazówki](#Porady_i_wskaz.C3.B3wki)
    *   [3.1 Zastępowanie vi i vim na neovim](#Zast.C4.99powanie_vi_i_vim_na_neovim)
    *   [3.2 Tworzenie linku symbolicznego init.vim do .vimrc](#Tworzenie_linku_symbolicznego_init.vim_do_.vimrc)
*   [4 Rozwiązywanie problemów](#Rozwi.C4.85zywanie_problem.C3.B3w)
    *   [4.1 Kursor nie jest przywracany do poprzedniego stanu po wyjściu](#Kursor_nie_jest_przywracany_do_poprzedniego_stanu_po_wyj.C5.9Bciu)
*   [5 Zobacz również](#Zobacz_r.C3.B3wnie.C5.BC)

## Instalacja

[Zainstaluj](https://wiki.archlinux.org/index.php/Help:Reading#Installation_of_packages) pakiet [neovim](https://www.archlinux.org/packages/?name=neovim) lub [neovim-git](https://aur.archlinux.org/packages/neovim-git/).

## Konfiguracja

### Przejście z vima

Neovim korzysta z `$XDG_CONFIG_HOME/nvim` zamiast z `~/.vim` jako swój głowny folder konfiguracyjny i `$XDG_CONFIG_HOME/nvim/init.vim` zamiast z `~/.vimrc` jako swój głowny plik konfiguracyjny.

Zobacz [nvim-from-vim](https://neovim.io/doc/user/nvim.html#nvim-from-vim) lub komende neovima `:help nvim-from-vim` żeby użyć swoją konfiguracje vima w neovimie.

#### Ładowanie dodatków vima

Jeśli chciałbyś użyć wtyczek, definicji składni lub innych dodatków które są zainstalowane dla vima, możesz dodać domyślną ścieżkę vima dla neovim poprzez dodanie jej do `rtp`. Na przykład możesz uruchomić w nvim następującą rzecz lub dodać ją do swojego pliku konfiguracji neovima:

```
set rtp^=/usr/share/vim/vimfiles/

```

## Porady i wskazówki

### Zastępowanie vi i vim na neovim

Ustawienie [wartości środowiska](https://wiki.archlinux.org/index.php/Environment_variables) `$VISUAL` i `$EDITOR` na nvim powinno być wystarczające w większości przypadków.

Niektóre programy mogą mieć mocno zakodowanego vi lub vima jako swój domyślny edytor tekstowy, żeby użyć neovima zamiast nich, zainstaluj [neovim-drop-in](https://aur.archlinux.org/packages/neovim-drop-in/).

### Tworzenie linku symbolicznego init.vim do .vimrc

Neovim jest w większości kompatybilny z standardowym vimem (lecz nie z vi), możesz stworzyć link symboliczny `nvim/init.vim` do swojego `.vimrc` żeby zachować starą konfiguracje:

```
$ ln -s ~/.vimrc ~/.config/nvim/init.vim

```

Jeżeli chcesz mieć kilka opcji tylko dla vima lub neovim, możesz użyć `if` w swoim pliku `.vimrc`:

```
if has('nvim')
    " Komendy dla neovima
else
    " Komendy dla vima
endif

```

## Rozwiązywanie problemów

### Kursor nie jest przywracany do poprzedniego stanu po wyjściu

Jeśli po wyjściu z neovima kursor nadal miga, zobacz rozwiązanie na GitHubie [neovim FAQ](https://github.com/neovim/neovim/wiki/FAQ#cursor-style-isnt-restored-after-exiting-nvim).

## Zobacz również

*   [Repozytorium na GitHubie](https://github.com/neovim/neovim)
*   [Wiki na GitHubie](https://github.com/neovim/neovim/wiki)