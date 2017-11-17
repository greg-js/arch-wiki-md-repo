Artigos relacionados

*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")

**pkgfile** é uma ferramenta para pesquisar por arquivos de pacotes nos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

**Dica:** [pacman](https://www.archlinux.org/packages/?name=pacman) possui [uma funcionalidade similar embutida](/index.php/Pacman_(Portugu%C3%AAs)#Pesquisar_por_um_pacote_que_contenha_um_arquivo_espec.C3.ADfico "Pacman (Português)").

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Uso](#Uso)
*   [3 Comando não localizado](#Comando_n.C3.A3o_localizado)
*   [4 Atualizações automáticas](#Atualiza.C3.A7.C3.B5es_autom.C3.A1ticas)

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

Veja [Bash#Command not found](/index.php/Bash#Command_not_found "Bash") e [Zsh#The "command not found" hook](/index.php/Zsh#The_.22command_not_found.22_hook "Zsh").

## Atualizações automáticas

**pkgfile** vem com um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") e [timer](/index.php/Systemd/Timers "Systemd/Timers") para sincronização automática da base de dados do pkgfile. Para ativar atualizações automáticas [habilite](/index.php/Habilite "Habilite") `pkgfile-update.timer`.

Por padrão, pkgfile será atualizado diariamente. Para alterar esse agendamento, [edite o arquivo unit](/index.php/Systemd_(Portugu%C3%AAs)#Editando_units_fornecidas "Systemd (Português)").