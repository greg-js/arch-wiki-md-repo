Artigos relacionados

*   [Mirrors](/index.php/Mirrors "Mirrors")
*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")

Para métodos gerais para melhorar a flexibilidade das dicas fornecidas ou do *pacman* em si, veja [Core utilities](/index.php/Core_utilities "Core utilities") e [Bash](/index.php/Bash "Bash").

## Contents

*   [1 Manutenção](#Manuten.C3.A7.C3.A3o)
    *   [1.1 Listando pacotes](#Listando_pacotes)
        *   [1.1.1 Com tamanho](#Com_tamanho)
        *   [1.1.2 Por data](#Por_data)
        *   [1.1.3 Que não estejam em um grupo ou repositório especificado](#Que_n.C3.A3o_estejam_em_um_grupo_ou_reposit.C3.B3rio_especificado)
        *   [1.1.4 Pacotes de desenvolvimento](#Pacotes_de_desenvolvimento)
    *   [1.2 Listando arquivos pertencentes a um pacote com tamanho](#Listando_arquivos_pertencentes_a_um_pacote_com_tamanho)
    *   [1.3 Identificar arquivos que pertençam a nenhum pacote](#Identificar_arquivos_que_perten.C3.A7am_a_nenhum_pacote)
    *   [1.4 Removendo pacotes não usados (órfãos)](#Removendo_pacotes_n.C3.A3o_usados_.28.C3.B3rf.C3.A3os.29)
    *   [1.5 Removendo tudo exceto o grupo base](#Removendo_tudo_exceto_o_grupo_base)
    *   [1.6 Obtendo a lista de dependências de vários pacotes](#Obtendo_a_lista_de_depend.C3.AAncias_de_v.C3.A1rios_pacotes)
    *   [1.7 Listando arquivos backup modificados](#Listando_arquivos_backup_modificados)
    *   [1.8 Fazer backup da base de dados do pacman](#Fazer_backup_da_base_de_dados_do_pacman)
    *   [1.9 Verificar changelogs facilmente](#Verificar_changelogs_facilmente)
*   [2 Instalação e recuperação](#Instala.C3.A7.C3.A3o_e_recupera.C3.A7.C3.A3o)
    *   [2.1 Instalando pacotes a partir de um CD/DVD ou pendrive](#Instalando_pacotes_a_partir_de_um_CD.2FDVD_ou_pendrive)
    *   [2.2 Repositório local personalizado](#Reposit.C3.B3rio_local_personalizado)
    *   [2.3 Cache do pacman compartilhado na rede](#Cache_do_pacman_compartilhado_na_rede)
        *   [2.3.1 Cache de somente leitura](#Cache_de_somente_leitura)
        *   [2.3.2 Cache somente leitura distribuído](#Cache_somente_leitura_distribu.C3.ADdo)
        *   [2.3.3 Cache de leitura-escrita](#Cache_de_leitura-escrita)
        *   [2.3.4 Duas vias com rsync](#Duas_vias_com_rsync)
        *   [2.3.5 Cache dinâmico de proxy reverso usando nginx](#Cache_din.C3.A2mico_de_proxy_reverso_usando_nginx)
        *   [2.3.6 Sincronizar cache de pacotes do pacman usando programas de sincronização](#Sincronizar_cache_de_pacotes_do_pacman_usando_programas_de_sincroniza.C3.A7.C3.A3o)
        *   [2.3.7 Prevenção de purgas de cache indesejadas](#Preven.C3.A7.C3.A3o_de_purgas_de_cache_indesejadas)
    *   [2.4 Recriar um pacote do sistema de arquivos](#Recriar_um_pacote_do_sistema_de_arquivos)
    *   [2.5 Lista de pacotes instalados](#Lista_de_pacotes_instalados)
    *   [2.6 Listando todos os arquivos alterados de pacotes](#Listando_todos_os_arquivos_alterados_de_pacotes)
    *   [2.7 Reinstalando todos pacotes](#Reinstalando_todos_pacotes)
    *   [2.8 Restaurar a base de dados local do pacman](#Restaurar_a_base_de_dados_local_do_pacman)
    *   [2.9 Recuperando um pendrive a partir de uma instalação existente](#Recuperando_um_pendrive_a_partir_de_uma_instala.C3.A7.C3.A3o_existente)
    *   [2.10 Vendo um único arquivo dentro de um arquivo .pkg](#Vendo_um_.C3.BAnico_arquivo_dentro_de_um_arquivo_.pkg)
    *   [2.11 Localizar aplicativos que usam bibliotecas de pacotes mais antigos](#Localizar_aplicativos_que_usam_bibliotecas_de_pacotes_mais_antigos)
*   [3 Desempenho](#Desempenho)
    *   [3.1 Velocidades de acesso da base de dados](#Velocidades_de_acesso_da_base_de_dados)
    *   [3.2 Velocidades de download](#Velocidades_de_download)
        *   [3.2.1 Powerpill](#Powerpill)
        *   [3.2.2 wget](#wget)
        *   [3.2.3 aria2](#aria2)
        *   [3.2.4 Outros aplicativos](#Outros_aplicativos)
*   [4 Utilitários](#Utilit.C3.A1rios)
    *   [4.1 Front-ends gráficos](#Front-ends_gr.C3.A1ficos)

## Manutenção

**Nota:** Em vez de usar *comm* (que requer entradas ordenadas com *sort*) na seção abaixo, você também pode usar `grep -Fxf` ou `grep -Fxvf`.

Veja também [Manutenção do sistema](/index.php/Manuten%C3%A7%C3%A3o_do_sistema "Manutenção do sistema").

### Listando pacotes

Você pode querer obter a lista de pacotes instalados com sua versão, o que é útil ao relatar erros ou discutir pacotes instalados.

*   Listar todos os pacotes instalados explicitamente: `pacman -Qe`.
*   Listar todos pacotes nativos (ou seja, presente na base de dados de sincronização) instalados explicitamente que não são dependências diretas ou opcional: `pacman -Qent`.
*   Listar todos os pacotes externos (geralmente baixados e instalados manualmente): `pacman -Qm`.
*   Listar todos os pacotes nativos (instalados a partir de base(s) de dados de sincronização): `pacman -Qn`.
*   Listar pacotes por expressão regular: `pacman -Qs *regex*`.
*   Listar pacotes por expressão regular com formato de saída personalizada: `expac -s "%-30n %v" *regex*` (precisa de [expac](https://www.archlinux.org/packages/?name=expac)).

#### Com tamanho

Para obter uma lista de pacotes instalados ordenados por tamanho, que pode ser útil para liberar espaço em seu disco rígido:

*   Instale [expac](https://www.archlinux.org/packages/?name=expac) e execute `expac -H M '%m\t%n' | sort -h`.
*   Execute [pacgraph](https://www.archlinux.org/packages/?name=pacgraph) com a opção `-c`.

Para listas o tamanho baixado de vários pacotes (deixe `*pacotes*` em branco para listar todos os pacotes):

```
$ expac -S -H M '%k\t%n' *pacotes*

```

Para listar pacotes instalados explicitamente que não estejam em [base](https://www.archlinux.org/groups/x86_64/base/) nem [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/) com tamanho e descrição:

```
$ expac -H M "%011m\t%-20n\t%10d" $(comm -23 <(pacman -Qqen | sort) <(pacman -Qqg base base-devel | sort)) | sort -n

```

#### Por data

Para listar os últimos 20 pacotes instalados com [expac](https://www.archlinux.org/packages/?name=expac), execute:

```
$ expac --timefmt='%Y-%m-%d %T' '%l\t%n' | sort | tail -n 20

```

ou com segundos desde o *epoch* (1970-01-01 UTC):

```
$ expac --timefmt=%s '%l\t%n' | sort -n | tail -n 20

```

#### Que não estejam em um grupo ou repositório especificado

**Nota:** Para obter uma lista de pacotes instalados como dependências, mas não mais exigidos para qualquer pacote instalado, veja [#Removendo pacotes não usados (órfãos)](#Removendo_pacotes_n.C3.A3o_usados_.28.C3.B3rf.C3.A3os.29).

Listar os pacotes instalados explicitamente que não estejam no grupo [base](https://www.archlinux.org/groups/x86_64/base/) nem no [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/):

```
$ comm -23 <(pacman -Qeq | sort) <(pacman -Qgq base base-devel | sort)

```

Listar todos os pacotes instalados não necessários para outros pacotes, e que não estejam no grupo [base](https://www.archlinux.org/groups/x86_64/base/) nem no [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/):

```
$ comm -23 <(pacman -Qqt | sort) <(pacman -Sqg base base-devel | sort)

```

Mesmo que o acima, mas com descrições:

```
$ expac -HM '%-20n\t%10d' $(comm -23 <(pacman -Qqt | sort) <(pacman -Qqg base base-devel | sort))

```

Listar todos os pacotes instalados que *não* estão no repositório especificado *nome_repo*

```
$ comm -23 <(pacman -Qtq | sort) <(pacman -Slq *nome_repo* | sort)

```

Listar todos os pacotes instalados que estão no repositório *nome_repo*:

```
$ comm -12 <(pacman -Qtq | sort) <(pacman -Slq *nome_repo* | sort)

```

#### Pacotes de desenvolvimento

Para listar todos os pacotes de desenvolvimento/instáveis, execute:

```
$ pacman -Qq | awk '/^.+(-cvs|-svn|-git|-hg|-bzr|-darcs)$/'

```

### Listando arquivos pertencentes a um pacote com tamanho

This one might come in handy if you have found that a specific package uses a huge amount of space and you want to find out which files make up the most of that.

```
$ pacman -Qlq *package* | grep -v '/$' | xargs du -h | sort -h

```

### Identificar arquivos que pertençam a nenhum pacote

If your system has stray files not owned by any package (a common case if you do not [use the package manager to install software](/index.php/Enhance_system_stability#Use_the_package_manager_to_install_software "Enhance system stability")), you may want to find such files in order to clean them up. The general process for doing so is:

1.  Create a sorted list of the files you want to check ownership of: `$ find /etc /opt /usr | sort > all_files.txt` 
2.  Create a sorted list of the files tracked by *pacman* (and remove the trailing slashes from directories): `$ pacman -Qlq | sed 's|/$||' | sort > owned_files.txt` 
3.  Find lines in the first list that are not in the second: `$ comm -23 all_files.txt owned_files.txt` 

This process is tricky in practice because many important files are not part of any package (e.g. files generated at runtime, custom configs) and so will be included in the final output, making it difficult to pick out the files that can be safely deleted.

**Tip:** The [lostfiles](https://aur.archlinux.org/packages/lostfiles/) script performs similar steps, but also includes an extensive blacklist to remove common false positives from the output. [aconfmgr](https://github.com/CyberShadow/aconfmgr) ([aconfmgr-git](https://aur.archlinux.org/packages/aconfmgr-git/)) also allows tracking orphaned files using a configuration script.

### Removendo pacotes não usados (órfãos)

For recursively removing orphans and their configuration files:

```
# pacman -Rns $(pacman -Qtdq)

```

If no orphans were found *pacman* outputs `error: no targets specified`. This is expected as no arguments were passed to `pacman -Rns`.

**Note:** The arguments `-Qt` list only true orphans. To include packages which are *optionally* required by another package, pass the `-t` flag twice (*i.e.*, `-Qtt`).

### Removendo tudo exceto o grupo base

If it is ever necessary to remove all packages except the base group, try this one-liner:

```
# pacman -R $(comm -23 <(pacman -Qq | sort) <((for i in $(pacman -Qqg base); do pactree -ul "$i"; done) | sort -u))

```

The one-liner was originally devised in [this discussion](https://bbs.archlinux.org/viewtopic.php?id=130176), and later improved in this article.

### Obtendo a lista de dependências de vários pacotes

Dependencies are alphabetically sorted and doubles are removed.

**Note:** To only show the tree of local installed packages, use `pacman -Qi`.

```
$ pacman -Si *packages* | awk -F'[:<=>]' '/^Depends/ {print $2}' | xargs -n1 | sort -u

```

Alternatively, with [expac](https://www.archlinux.org/packages/?name=expac):

```
$ expac -l '
' %E -S *packages* | sort -u

```

### Listando arquivos backup modificados

If you want to backup your system configuration files you could copy all files in `/etc/`, but usually you are only interested in the files that you have changed. Modified [backup files](/index.php/Pacnew_and_Pacsave_files#Package_backup_files "Pacnew and Pacsave files") can be viewed with the following command:

```
# pacman -Qii | awk '/^MODIFIED/ {print $2}'

```

Running this command with root permissions will ensure that files readable only by root (such as `/etc/sudoers`) are included in the output.

**Tip:** See [#Listing all changed files from packages](#Listing_all_changed_files_from_packages) to list all changed files *pacman* knows, not only backup files.

### Fazer backup da base de dados do pacman

The following command can be used to back up the local *pacman* database:

```
$ tar -cjf pacman_database.tar.bz2 /var/lib/pacman/local

```

Store the backup *pacman* database file on one or more offline media, such as a USB stick, external hard drive, or CD-R.

The database can be restored by moving the `pacman_database.tar.bz2` file into the `/` directory and executing the following command:

```
# tar -xjvf pacman_database.tar.bz2

```

**Note:** If the *pacman* database files are corrupted, and there is no backup file available, there exists some hope of rebuilding the *pacman* database. Consult [#Restore pacman's local database](#Restore_pacman.27s_local_database).

**Tip:** The [pakbak-git](https://aur.archlinux.org/packages/pakbak-git/) package provides a script and a [systemd](/index.php/Systemd "Systemd") service to automate the task. Configuration is possible in `/etc/pakbak.conf`.

### Verificar changelogs facilmente

When maintainers update packages, commits are often commented in a useful fashion. Users can quickly check these from the command line by installing [pacolog](https://aur.archlinux.org/packages/pacolog/). This utility lists recent commit messages for packages from the official repositories or the AUR, by using `pacolog <package>`.

## Instalação e recuperação

Alternative ways of getting and restoring packages.

### Instalando pacotes a partir de um CD/DVD ou pendrive

To download packages, or groups of packages:

```
# cd ~/Packages
# pacman -Syw base base-devel grub-bios xorg gimp --cachedir .
# repo-add ./custom.db.tar.gz ./*

```

Then you can burn the "Packages" folder to a CD/DVD or transfer it to a USB stick, external HDD, etc.

To install:

**1.** Mount the media:

```
# mkdir /mnt/repo
# mount /dev/sr0 /mnt/repo    #For a CD/DVD.
# mount /dev/sdxY /mnt/repo   #For a USB stick.

```

**2.** Edit `pacman.conf` and add this repository *before* the other ones (e.g. extra, core, etc.). This is important. Do not just uncomment the one on the bottom. This way it ensures that the files from the CD/DVD/USB take precedence over those in the standard repositories:

 `/etc/pacman.conf` 
```
[custom]
SigLevel = PackageRequired
Server = file:///mnt/repo/Packages
```

**3.** Finally, synchronize the *pacman* database to be able to use the new repository:

```
# pacman -Syu

```

### Repositório local personalizado

Use the *repo-add* script included with *pacman* to generate a database for a personal repository. Use `repo-add --help` for more details on its usage. To add a new package to the database, or to replace the old version of an existing package in the database, run:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/package-1.0-1-x86_64.pkg.tar.xz*

```

**Note:** A package database is a tar file, optionally compressed. Valid extensions are *.db* or *.files* followed by an archive extension of *.tar*, *.tar.gz*, *.tar.bz2*, *.tar.xz*, or *.tar.Z*. The file does not need to exist, but all parent directories must exist.

The database and the packages do not need to be in the same directory when using *repo-add*, but keep in mind that when using *pacman* with that database, they should be together. Storing all the built packages to be included in the repository in one directory also allows to use shell glob expansion to add or update multiple packages at once:

```
$ repo-add */path/to/repo.db.tar.gz /path/to/*.pkg.tar.xz*

```

**Warning:** *repo-add* adds the entries into the database in the same order as passed on the command line. If multiple versions of the same package are involved, care must be taken to ensure that the correct version is added last. In particular, note that lexical order used by the shell depends on the locale and differs from the [vercmp](https://www.archlinux.org/pacman/vercmp.8.html) ordering used by *pacman*.

*repo-remove* is used to remove packages from the package database, except that only package names are specified on the command line.

```
$ repo-remove */path/to/repo.db.tar.gz pkgname*

```

Once the local repository database has been created, add the repository to `pacman.conf` for each system that is to use the repository. An example of a custom repository is in `pacman.conf`. The repository's name is the database filename with the file extension omitted. In the case of the example above the repository's name would simply be *repo*. Reference the repository's location using a `file://` url, or via FTP using [ftp://localhost/path/to/directory](ftp://localhost/path/to/directory).

If willing, add the custom repository to the [list of unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories"), so that the community can benefit from it.

### Cache do pacman compartilhado na rede

If you happen to run several Arch boxes on your LAN, you can share packages so that you can greatly decrease your download times. Keep in mind you should not share between different architectures (i.e. i686 and x86_64) or you will run into problems.

#### Cache de somente leitura

If you are looking for a quick and dirty solution, you can simply run a standalone webserver which other computers can use as a first mirror: `darkhttpd /var/cache/pacman/pkg`. Just add this server at the top of your mirror list. Be aware that you might get a lot of 404 errors, due to cache misses, depending on what you do, but *pacman* will try the next (real) mirrors when that happens.

#### Cache somente leitura distribuído

There are Arch-specific tools for automatically discovering other computers on your network offering a package cache. Try [pacserve](/index.php/Pacserve "Pacserve"), [pkgdistcache](https://aur.archlinux.org/packages/pkgdistcache/), or [paclan](https://aur.archlinux.org/packages/paclan/). pkgdistcache uses Avahi instead of plain UDP which may work better in certain home networks that route instead of bridge between WiFi and Ethernet.

Historically, there was [PkgD](https://bbs.archlinux.org/viewtopic.php?id=64391) and [multipkg](https://github.com/toofishes/multipkg), but they are no longer maintained.

#### Cache de leitura-escrita

In order to share packages between multiple computers, simply share `/var/cache/pacman/` using any network-based mount protocol. This section shows how to use [shfs](/index.php/Shfs "Shfs") or [SSHFS](/index.php/SSHFS "SSHFS") to share a package cache plus the related library-directories between multiple computers on the same local network. Keep in mind that a network shared cache can be slow depending on the file-system choice, among other factors.

First, install any network-supporting filesystem packages: [shfs-utils](https://www.archlinux.org/packages/?name=shfs-utils), [sshfs](https://www.archlinux.org/packages/?name=sshfs), [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs), [samba](https://www.archlinux.org/packages/?name=samba) or [nfs-utils](https://www.archlinux.org/packages/?name=nfs-utils).

**Tip:**

*   To use *sshfs* or *shfs*, consider reading [Using SSH Keys](/index.php/Using_SSH_Keys "Using SSH Keys").
*   By default, *smbfs* does not serve filenames that contain colons, which results in the client downloading the offending package afresh. To prevent this, use the `mapchars` mount option on the client.

Then, to share the actual packages, mount `/var/cache/pacman/pkg` from the server to `/var/cache/pacman/pkg` on every client machine.

**Note:** Do not make `/var/cache/pacman/pkg` or any of its ancestors (e.g., `/var`) a symlink. *Pacman* expects these to be directories. When *pacman* re-installs or upgrades itself, it will remove the symlinks and create empty directories instead. However during the transaction *pacman* relies on some files residing there, hence breaking the update process. Refer to [FS#50298](https://bugs.archlinux.org/task/50298) for further details.

#### Duas vias com rsync

Another approach in a local environment is [rsync](/index.php/Rsync "Rsync"). Choose a server for caching and enable the [Rsync#rsync daemon](/index.php/Rsync#rsync_daemon "Rsync"). On clients synchronize two-way with this share via rsync protocol. Filenames that contain colons are no problem for the rsync protocol.

Draft example for a client, using `uname -m` within the share name ensures an architecture dependedant sync:

```
 # rsync rsync://server/share_$(uname -m)/ /var/cache/pacman/pkg/ ...
 # pacman ...
 # paccache ...
 # rsync /var/cache/pacman/pkg/ rsync://server/share_$(uname -m)/  ...

```

#### Cache dinâmico de proxy reverso usando nginx

[nginx](/index.php/Nginx "Nginx") can be used to proxy requests to official upstream mirrors and cache the results to local disk. All subsequent requests for that file will be served directly from the local cache, minimizing the amount of internet traffic needed to update a large number of servers with minimal effort.

**Warning:** This method has a limitation. You must use mirrors that use the same relative path to package files and you must configure your cache to use that same path. In this example, we are using mirrors that use the relative path `/archlinux/$repo/os/$arch` and our cache's `Server` setting in `mirrorlist` is configured similarly.

In this example, we will run the cache server on `http://cache.domain.local:8080/` and storing the packages in `/srv/http/pacman-cache/`.

Create the directory for the cache and adjust the permissions so nginx can write files to it:

```
 # mkdir /srv/http/pacman-cache
 # chown http:http /srv/http/pacman-cache

```

Next, configure nginx as the [dynamic cache](https://gist.github.com/anonymous/97ec4148f643de925e433bed3dc7ee7d) (read the comments for an explanation of the commands).

Finally, update your other Arch Linux servers to use this new cache by adding the following line to the `mirrorlist` file:

 `/etc/pacman.d/mirrorlist` 
```
Server = http://cache.domain.local:8080/archlinux/$repo/os/$arch
...

```

**Note:** You will need to create a method to clear old packages, as this directory will continue to grow over time. `paccache` (which is included with *pacman*) can be used to automate this using retention criteria of your choosing. For example, `find /srv/http/pacman-cache/ -type d -exec paccache -v -r -k 2 -c {} \;` will keep the last 2 versions of packages in your cache directory.

#### Sincronizar cache de pacotes do pacman usando programas de sincronização

Use [Resilio Sync](/index.php/Resilio_Sync "Resilio Sync") or [Syncthing](/index.php/Syncthing "Syncthing") to synchronize the *pacman* cache folders (i.e. `/var/cache/pacman/pkg`).

#### Prevenção de purgas de cache indesejadas

By default, `pacman -Sc` removes package tarballs from the cache that correspond to packages that are not installed on the machine the command was issued on. Because *pacman* cannot predict what packages are installed on all machines that share the cache, it will end up deleting files that should not be.

To clean up the cache so that only *outdated* tarballs are deleted, add this entry in the `[options]` section of `/etc/pacman.conf`:

```
CleanMethod = KeepCurrent

```

### Recriar um pacote do sistema de arquivos

To recreate a package from the file system, use *bacman* (included with *pacman*). Files from the system are taken as they are, hence any modifications will be present in the assembled package. Distributing the recreated package is therefore discouraged; see [ABS](/index.php/ABS "ABS") and [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine") for alternatives.

**Tip:** *bacman* honours the `PACKAGER`, `PKGDEST` and `PKGEXT` options from `makepkg.conf`. Custom options for the compression tools can be configured by exporting the relevant environment variable, for example `XZ_OPT="-T 0"` will enable parallel compression for *xz*.

An alternative tool would be [fakepkg](https://aur.archlinux.org/packages/fakepkg/). It supports parallelization and can handle multiple input packages in one command, which *bacman* both does not support.

### Lista de pacotes instalados

Keeping a list of explicitly installed packages can be useful to speed up installation on a new system:

```
$ pacman -Qqe > pkglist.txt

```

**Note:** If you used `-Qqet`, when reinstalling the list all the non-top-level packages would be set as dependencies.

To install packages from the list backup, run:

```
# pacman -S - < pkglist.txt

```

**Tip:**

*   To skip already installed packages, use `--needed`.
*   Use `comm -13 <(pacman -Qqdt | sort) <(pacman -Qqdtt | sort) > optdeplist.txt` to also create a list of the installed optional dependencies which can be reinstalled with `--asdeps`.

In case the list includes foreign packages, such as [AUR](/index.php/AUR "AUR") packages, remove them first:

```
# pacman -S $(comm -12 <(pacman -Slq | sort) <(sort pkglist.txt))

```

To remove all the packages on your system that are not mentioned in the list:

```
# pacman -Rsu $(comm -23 <(pacman -Qq | sort) <(sort pkglist.txt))

```

**Tip:** These tasks can be automated. See [bacpac](https://aur.archlinux.org/packages/bacpac/), [packup](https://aur.archlinux.org/packages/packup/), [pacmanity](https://aur.archlinux.org/packages/pacmanity/), and [pug](https://aur.archlinux.org/packages/pug/) for examples.

### Listando todos os arquivos alterados de pacotes

If you are suspecting file corruption (e.g. by software/hardware failure), but are unsure if files were got corrupted, you might want to compare with the hash sums in the packages. This can be done with [pacutils](https://www.archlinux.org/packages/?name=pacutils):

```
# paccheck --md5sum --quiet

```

For recovery of the database see [#Restore pacman's local database](#Restore_pacman.27s_local_database). The `mtree` files can also be [extracted as `.MTREE` from the respective package files](#Viewing_a_single_file_inside_a_.pkg_file).

**Note:** This should **not** be used as is when suspecting malicious changes! In this case security precautions such as using a live medium and an independent source for the hash sums are advised.

### Reinstalando todos pacotes

To reinstall all native packages, use:

```
# pacman -Qnq | pacman -S -

```

Foreign (AUR) packages must be reinstalled separately; you can list them with `pacman -Qmq`.

*Pacman* preserves the [installation reason](/index.php/Installation_reason "Installation reason") by default.

### Restaurar a base de dados local do pacman

See [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database").

### Recuperando um pendrive a partir de uma instalação existente

If you have Arch installed on a USB key and manage to mess it up (e.g. removing it while it is still being written to), then it is possible to re-install all the packages and hopefully get it back up and working again (assuming USB key is mounted in `/newarch`)

```
# pacman -S $(pacman -Qq --dbpath /newarch/var/lib/pacman) --root /newarch --dbpath /newarch/var/lib/pacman

```

### Vendo um único arquivo dentro de um arquivo .pkg

For example, if you want to see the contents of `/etc/systemd/logind.conf` supplied within the [systemd](https://www.archlinux.org/packages/?name=systemd) package:

```
$ tar -xOf /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz etc/systemd/logind.conf

```

Or you can use [vim](https://www.archlinux.org/packages/?name=vim) to browse the archive:

```
$ vim /var/cache/pacman/pkg/systemd-204-3-x86_64.pkg.tar.xz

```

### Localizar aplicativos que usam bibliotecas de pacotes mais antigos

Even if you installed a package the existing long-running programs (like daemons and servers) still keep using code from old package libraries. And it is a bad idea to let these programs running if the old library contains a security bug.

Here is a way how to find all the programs that use old packages code:

```
# lsof +c 0 | grep -w DEL | awk '1 { print $1 ": " $NF }' | sort -u

```

It will print running program name and old library that was removed or replaced with newer content.

## Desempenho

### Velocidades de acesso da base de dados

*Pacman* stores all package information in a collection of small files, one for each package. Improving database access speeds reduces the time taken in database-related tasks, e.g. searching packages and resolving package dependencies. The safest and easiest method is to run as root:

```
# pacman-optimize

```

This will attempt to put all the small files together in one (physical) location on the hard disk so that the hard disk head does not have to move so much when accessing all the data. This method is safe, but is not foolproof: it depends on your filesystem, disk usage and empty space fragmentation. Another, more aggressive, option would be to first remove uninstalled packages from cache and to remove unused repositories before database optimization:

```
# pacman -Sc && pacman-optimize

```

### Velocidades de download

**Note:** If your download speeds have been reduced to a crawl, ensure you are using one of the many [mirrors](/index.php/Mirrors "Mirrors") and not ftp.archlinux.org, which is [throttled since March 2007](https://www.archlinux.org/news/302/).

When downloading packages *pacman* uses the mirrors in the order they are in `/etc/pacman.d/mirrorlist`. The mirror which is at the top of the list by default however may not be the fastest for you. To select a faster mirror, see [Mirrors](/index.php/Mirrors "Mirrors").

*Pacman*'s speed in downloading packages can also be improved by using a different application to download packages, instead of *pacman*'s built-in file downloader.

In all cases, make sure you have the latest *pacman* before doing any modifications.

```
# pacman -Syu

```

#### Powerpill

[Powerpill](/index.php/Powerpill "Powerpill") is a *pacman* wrapper that uses parallel and segmented downloading to try to speed up downloads for *pacman*.

#### wget

This is also very handy if you need more powerful proxy settings than *pacman*'s built-in capabilities.

To use `wget`, first [install](/index.php/Install "Install") the [wget](https://www.archlinux.org/packages/?name=wget) package then modify `/etc/pacman.conf` by uncommenting the following line in the `[options]` section:

```
XferCommand = /usr/bin/wget -c -q --show-progress --passive-ftp -O %o %u

```

Instead of uncommenting the `wget` parameters in `/etc/pacman.conf`, you can also modify the `wget` configuration file directly (the system-wide file is `/etc/wgetrc`, per user files are `$HOME/.wgetrc`.

#### aria2

[aria2](/index.php/Aria2 "Aria2") is a lightweight download utility with support for resumable and segmented HTTP/HTTPS and FTP downloads. aria2 allows for multiple and simultaneous HTTP/HTTPS and FTP connections to an Arch mirror, which should result in an increase in download speeds for both file and package retrieval.

**Note:** Using aria2c in *pacman*'s XferCommand will **not** result in parallel downloads of multiple packages. *Pacman* invokes the XferCommand with a single package at a time and waits for it to complete before invoking the next. To download multiple packages in parallel, see [Powerpill](/index.php/Powerpill "Powerpill").

Install [aria2](https://www.archlinux.org/packages/?name=aria2), then edit `/etc/pacman.conf` by adding the following line to the `[options]` section:

```
XferCommand = /usr/bin/aria2c --allow-overwrite=true --continue=true --file-allocation=none --log-level=error --max-tries=2 --max-connection-per-server=2 --max-file-not-found=5 --min-split-size=5M --no-conf --remote-time=true --summary-interval=60 --timeout=5 --dir=/ --out %o %u

```

**Tip:** [This alternative configuration for using *pacman* with aria2](https://bbs.archlinux.org/viewtopic.php?pid=1491879#p1491879) tries to simplify configuration and adds more configuration options.

See [OPTIONS](http://aria2.sourceforge.net/manual/en/html/aria2c.html#options) in [aria2c(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/aria2c.1) for used aria2c options.

*   `-d, --dir` :The directory to store the downloaded file(s) as specified by *pacman*.
*   `-o, --out`: The output file name(s) of the downloaded file(s).
*   `%o`: Variable which represents the local filename(s) as specified by *pacman*.
*   `%u`: Variable which represents the download URL as specified by *pacman*.

#### Outros aplicativos

There are other downloading applications that you can use with *pacman*. Here they are, and their associated XferCommand settings:

*   `snarf`: `XferCommand = /usr/bin/snarf -N %u`
*   `lftp`: `XferCommand = /usr/bin/lftp -c pget %u`
*   `axel`: `XferCommand = /usr/bin/axel -n 2 -v -a -o %o %u`
*   `hget`: `XferCommand = /usr/bin/hget %u -n 2 -skip-tls false` (please read the [documentation on the Github project page](https://github.com/huydx/hget) for more info)

## Utilitários

*   **Lostfiles** — Script that identifies files not owned by any package.

	[https://github.com/graysky2/lostfiles](https://github.com/graysky2/lostfiles) || [lostfiles](https://aur.archlinux.org/packages/lostfiles/)

*   **Pacmatic** — *Pacman* wrapper to check Arch News before upgrading, avoid partial upgrades, and warn about configuration file changes.

	[http://kmkeen.com/pacmatic](http://kmkeen.com/pacmatic) || [pacmatic](https://www.archlinux.org/packages/?name=pacmatic)

*   **pacutils** — Helper library for libalpm based programs.

	[https://github.com/andrewgregory/pacutils](https://github.com/andrewgregory/pacutils) || [pacutils](https://www.archlinux.org/packages/?name=pacutils)

*   **[pkgfile](/index.php/Pkgfile "Pkgfile")** — Tool that finds what package owns a file.

	[http://github.com/falconindy/pkgfile](http://github.com/falconindy/pkgfile) || [pkgfile](https://www.archlinux.org/packages/?name=pkgfile)

*   **pkgtools** — Collection of scripts for Arch Linux packages.

	[https://github.com/Daenyth/pkgtools](https://github.com/Daenyth/pkgtools) || [pkgtools](https://aur.archlinux.org/packages/pkgtools/)

*   **repoctl** — Tool to help manage local repositories.

	[https://github.com/cassava/repoctl](https://github.com/cassava/repoctl) || [repoctl](https://aur.archlinux.org/packages/repoctl/)

*   **repose** — An Arch Linux repository building tool.

	[https://github.com/vodik/repose](https://github.com/vodik/repose) || [repose](https://www.archlinux.org/packages/?name=repose)

*   **[snap-pac](/index.php/Snapper#Wrapping_pacman_transactions_in_snapshots "Snapper")** — Make *pacman* automatically use snapper to create pre/post snapshots like openSUSE's YaST.

	[https://github.com/wesbarnett/snap-pac](https://github.com/wesbarnett/snap-pac) || [snap-pac](https://www.archlinux.org/packages/?name=snap-pac)

### Front-ends gráficos

**Warning:** Some front-ends such as [octopi](https://aur.archlinux.org/packages/octopi/) [[1]](https://github.com/aarnt/octopi/issues/134#issuecomment-142099266) perform [partial upgrades](/index.php/Partial_upgrade "Partial upgrade") periodically.

*   **Arch-Update** — Update indicator for Gnome-Shell.

	[https://github.com/RaphaelRochet/arch-update](https://github.com/RaphaelRochet/arch-update) || [gnome-shell-extension-arch-update](https://aur.archlinux.org/packages/gnome-shell-extension-arch-update/)

*   **Arch-Update-Notifier** — Update indicator for KDE.

	[https://github.com/I-Dream-in-Code/kde-arch-update-plasmoid](https://github.com/I-Dream-in-Code/kde-arch-update-plasmoid) || [plasma5-applets-kde-arch-update-notifier-git](https://aur.archlinux.org/packages/plasma5-applets-kde-arch-update-notifier-git/)

*   **Discover** — A collection of package management tools for KDE, using PackageKit.

	[https://projects.kde.org/projects/kde/workspace/discover](https://projects.kde.org/projects/kde/workspace/discover) || [discover](https://www.archlinux.org/packages/?name=discover)

*   **GNOME packagekit** — GTK based package management tool

	[http://www.freedesktop.org/software/PackageKit/](http://www.freedesktop.org/software/PackageKit/) || [gnome-packagekit](https://www.archlinux.org/packages/?name=gnome-packagekit)

*   **GNOME Software** — Gnome Software App. (Curated selection for GNOME)

	[https://wiki.gnome.org/Apps/Software](https://wiki.gnome.org/Apps/Software) || [gnome-software](https://www.archlinux.org/packages/?name=gnome-software)

*   **kalu** — A small application that will add an icon to your systray and sit there, regularly checking if there's anything new for you to upgrade.

	[https://jjacky.com/kalu/](https://jjacky.com/kalu/) || [kalu](https://aur.archlinux.org/packages/kalu/)

*   **pamac** — A DBus daemon and Gtk3 frontend for libalpm written in Vala.

	[https://github.com/manjaro/pamac/](https://github.com/manjaro/pamac/) || [pamac-aur](https://aur.archlinux.org/packages/pamac-aur/)

*   **pcurses** — Package management in a curses frontend

	[https://github.com/schuay/pcurses](https://github.com/schuay/pcurses) || [pcurses](https://www.archlinux.org/packages/?name=pcurses)

*   **tkPacman** — Depends only on Tcl/Tk and X11, and interacts with the package database via the CLI of *pacman*.

	[http://sourceforge.net/projects/tkpacman](http://sourceforge.net/projects/tkpacman) || [tkpacman](https://aur.archlinux.org/packages/tkpacman/)