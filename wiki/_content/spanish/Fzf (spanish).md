**Estado de la traducción**
Este artículo es una traducción de [Fzf](/index.php/Fzf "Fzf"), revisada por última vez el **2018-11-04**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Fzf&diff=0&oldid=553024) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

[fzf](https://github.com/junegunn/fzf) es un buscador difuso de línea de comandos de propósito general.

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
    *   [2.1 Shells](#Shells)
        *   [2.1.1 bash](#bash)
        *   [2.1.2 zsh](#zsh)
        *   [2.1.3 fish](#fish)
    *   [2.2 Vim](#Vim)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [fzf](https://www.archlinux.org/packages/?name=fzf). La versión de desarrollo es [fzf-git](https://aur.archlinux.org/packages/fzf-git/).

## Configuración

### Shells

Opcionalmente, [fzf keybindings](https://github.com/junegunn/fzf/wiki/Configuring-shell-key-bindings) y la terminación están disponibles para los distintos shells:

*   `<CTRL+T>` lista de archivos+carpetas en el directorio actual (por ejemplo, `git commit <CTRL+T>`, seleccione algunos archivos usando `<TAB>`, y finalmente `<Intro>`)
*   `<CTRL+R>` historial de búsqueda de comandos de shell
*   `<ALT+C>` directorio de cambio difuso

#### [bash](/index.php/Bash "Bash")

[Cargue](/index.php/Help:Reading_(Espa%C3%B1ol)#Cargar_fuentes "Help:Reading (Español)") los archivos deseados de su `.bashrc`:

*   `/usr/share/fzf/key-bindings.bash`
*   `/usr/share/fzf/completion.bash`

#### [zsh](/index.php/Zsh "Zsh")

[Cargue](/index.php/Help:Reading_(Espa%C3%B1ol)#Cargar_fuentes "Help:Reading (Español)") los archivos deseados de su `.zshrc`:

*   `/usr/share/fzf/key-bindings.zsh`
*   `/usr/share/fzf/completion.zsh`

#### [fish](/index.php/Fish "Fish")

Para fish, los keybindings se encuentran en:

*   `/usr/share/fish/functions/fzf_key_bindings.fish`

fish cargará de esta manera por defecto, pero los enlaces tienen que ser habilitados manualmente:

 `~/.config/fish/functions/fish_user_key_bindings.fish` 
```
function fish_user_key_bindings
	fzf_key_bindings
end

```

la terminación de fzf en fish se puede activar con funciones personalizadas: [https://github.com/junegunn/fzf/wiki/Examples-(fish)](https://github.com/junegunn/fzf/wiki/Examples-(fish))

### Vim

El plugin básico [Vim](/index.php/Vim_(Espa%C3%B1ol) "Vim (Español)") ya está incluido dentro del paquete e instalado en el directorio global de plugins de Vim. Por lo tanto, no es necesario añadir nada a su `.vimrc` para poder usarlo. Pero sólo proporciona el comando FZF. Hay un plugin de Vim adicional hecho por el autor de fzf que define algunas funciones de conveniencia, véase [https://github.com/junegunn/fzf.vim](https://github.com/junegunn/fzf.vim).