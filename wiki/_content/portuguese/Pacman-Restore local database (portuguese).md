**Status de tradução:** Esse artigo é uma tradução de [Pacman/Restore local database](/index.php/Pacman/Restore_local_database "Pacman/Restore local database"). Data da última tradução: 2018-11-05\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Pacman/Restore_local_database&diff=0&oldid=553241) na versão em inglês.

Sinais de que o pacman precisa de uma restauração da base de dados local:

*   `pacman -Q` fornece absolutamente nenhuma saída e `pacman -Syu` relata erroneamente que o sistema está atualizado.
*   Ao tentar instalar um pacote usando `pacman -S *pacote*` e ele emite uma lista de dependências já satisfeitas.

Muito provavelmente, a base de dados de softwares instalados do pacman, `/var/lib/pacman/local`, foi corrompida ou excluída. Embora este seja um problema sério, ele pode ser restaurado seguindo as instruções abaixo.

Primeiramente, certifique-se de que o arquivo de registro de logs do pacman está presente:

```
$ ls /var/log/pacman.log

```

Se não existe, *não* é possível continuar com este método. Você pode usar o [script de detecção de pacotes do Xyne](https://bbs.archlinux.org/viewtopic.php?pid=670876) para recriar a base de dados. Caso contrário, a solução provável é reinstalar todo o sistema.

## Gerando a lista de recuperação de pacotes

**Atenção:** Se por algum motivo o seu cache do [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou destino de pacotes do [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)") contenham pacotes de outras arquiteturas, remova-os antes de continuar.

[Instale](/index.php/Instale "Instale") o pacote [pacutils](https://www.archlinux.org/packages/?name=pacutils) para obter *paclog*.

Crie um script de filtro de logs e torne-o executável:

 `pacrecover` 
```
#!/bin/bash -e

. /etc/makepkg.conf

PKGCACHE=$((grep -m 1 '^CacheDir' /etc/pacman.conf || echo 'CacheDir = /var/cache/pacman/pkg') | sed 's/CacheDir = //')

pkgdirs=("$@" "$PKGDEST" "$PKGCACHE")

while read -r -a parampart; do
  pkgname="${parampart[0]}-${parampart[1]}-*.pkg.tar.xz"
  for pkgdir in ${pkgdirs[@]}; do
    pkgpath="$pkgdir"/$pkgname
    [ -f $pkgpath ] && { echo $pkgpath; break; };
  done || echo ${parampart[0]} 1>&2
done

```

Execute o script (opcionalmente, passando diretórios adicionais com pacotes como parâmetros):

```
 $ paclog --pkglist /var/log/pacman.log | ./pacrecover >files.list 2>pkglist.orig

```

Desta forma, serão criados dois arquivos: `files.list` com arquivos de pacote, ainda presentes na máquina e `pkglist.orig`, pacotes os quais devem ser baixados. A operação posterior pode resultar em incompatibilidade entre arquivos de versões mais antigas do pacote, ainda presentes na máquina e arquivos, encontrados na nova versão. Essas incompatibilidades terão de ser corrigidas manualmente.

Aqui está uma maneira de restringir automaticamente a segunda lista de pacotes disponíveis em um repositório:

```
$ { cat pkglist.orig; pacman -Slq; } | sort | uniq -d > pkglist

```

**Nota:** Se isso falhar com `falha ao iniciar a biblioteca alpm`, verifique se `/var/lib/pacman/local/ALPM_DB_VERSION` existe - se não existir, execute `pacman-db-upgrade` como root seguido por `pacman -Sy` e, então, **tente novamente o comando anterior**.

Verifique se algum pacote importante do *base* está em falta e adicione-o à lista:

```
$ comm -23 <(pacman -Sgq base | sort) pkglist.orig >> pkglist

```

Proceda assim que o conteúdo de ambas listas seja satisfatório, já que elas serão usadas para restaurar a base de dados de pacotes instalados do pacman; `/var/lib/pacman/local/`.

## Efetuando a recuperação

Defina uma função de bash para fins de recuperação:

```
 recovery-pacman() {
    sudo pacman "$@"  \
    --log /dev/null   \
    --noscriptlet     \
    --dbonly          \
    --force           \
    --nodeps          \
    --needed
}

```

`--log /dev/null` permite evitar a poluição desnecessária do log do pacman; `--needed` economizará algum tempo ignorando pacotes, já presentes no banco de dados; `--nodeps` permitirá a instalação de pacotes em cache, mesmo que os pacotes instalados dependam de versões mais recentes. O restante das opções permitirá o **pacman** operar sem ler/escrever o sistema de arquivos.

Popule a base de dados de sincronização:

```
# pacman -Sy

```

Inicie a geração da base de dados instalando arquivos de pacotes disponíveis localmente de `files.list`:

```
# recovery-pacman -U $(< files.list)

```

Instale o resto de `pkglist`:

```
# recovery-pacman -S $(< pkglist)

```

Atualize a base de dados local para que os pacotes que não sejam exigidos por qualquer outro pacote sejam marcados como instalados explicitamente e os outros como dependências. Você precisará ser extremamente cuidadoso no futuro ao remover pacotes, mas com a base de dados original perdida é o melhor que podemos fazer.

```
# pacman -D --asdeps $(pacman -Qq)
# pacman -D --asexplicit $(pacman -Qtq)

```

Opcionalmente, verifique todos os pacotes instalados por corrompimento:

```
# pacman -Qk

```

Opcionalmente, tente [pacman/Dicas e truques#Identificar arquivos que pertençam a nenhum pacote](/index.php/Pacman/Dicas_e_truques#Identificar_arquivos_que_pertençam_a_nenhum_pacote "Pacman/Dicas e truques").

Atualize todos os pacotes:

```
# pacman -Su

```