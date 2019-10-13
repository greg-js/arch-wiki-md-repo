**Status de tradução:** Esse artigo é uma tradução de [Pkgfile](/index.php/Pkgfile "Pkgfile"). Data da última tradução: 2019-10-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Pkgfile&diff=0&oldid=581214) na versão em inglês.

Artigos relacionados

*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

**pkgfile** é uma ferramenta para pesquisar por arquivos de pacotes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

**Dica:** [pacman](https://www.archlinux.org/packages/?name=pacman) possui [uma funcionalidade similar embutida](/index.php/Pacman_(Portugu%C3%AAs)#Pesquisar_por_um_pacote_que_contenha_um_arquivo_específico "Pacman (Português)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Uso](#Uso)
*   [3 Comando não localizado](#Comando_não_localizado)
*   [4 Atualizações automáticas](#Atualizações_automáticas)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [pkgfile](https://www.archlinux.org/packages/?name=pkgfile). Alternativamente, instale a versão de desenvolvimento com o pacote [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/).

A base de dados do *pkgfile* pode então ser sincronizada com:

```
# pkgfile -u

```

## Uso

Para pesquisar por um pacote que contém o arquivo `makepkg`:

 `$ pkgfile makepkg`  `core/pacman` 

Para listar todos os arquivos fornecidos por [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring):

 `$ pkgfile -l archlinux-keyring` 
```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

Esse último é comparável com `pacman -Ql` (veja [pacman (Português)#Consultando base de dados de pacotes](/index.php/Pacman_(Portugu%C3%AAs)#Consultando_base_de_dados_de_pacotes "Pacman (Português)")), exceto que ela se aplica a pacotes remotos.

## Comando não localizado

Veja [Bash#Command not found](/index.php/Bash#Command_not_found "Bash"), [Zsh#The "command not found" handler](/index.php/Zsh#The_"command_not_found"_handler "Zsh") e [Fish#The "command not found" hook](/index.php/Fish#The_"command_not_found"_hook "Fish").

## Atualizações automáticas

**pkgfile** vem com um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") e [timer](/index.php/Systemd/Timers_(Portugu%C3%AAs) "Systemd/Timers (Português)") para sincronização automática da base de dados do pkgfile. Para ativar atualizações automáticas [habilite](/index.php/Habilite "Habilite") `pkgfile-update.timer`.

Por padrão, pkgfile será atualizado diariamente. Para alterar esse agendamento, [edite o arquivo unit](/index.php/Systemd_(Portugu%C3%AAs)#Editando_units_fornecidas "Systemd (Português)").