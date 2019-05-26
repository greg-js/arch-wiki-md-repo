**Status de tradução:** Esse artigo é uma tradução de [Running GUI applications as root](/index.php/Running_GUI_applications_as_root "Running GUI applications as root"). Data da última tradução: 2019-05-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Running_GUI_applications_as_root&diff=0&oldid=569424) na versão em inglês.

**Atenção:** Todos os métodos a seguir têm implicações de segurança que os usuários devem estar cientes. Como colocado por Emmanuele Bassi, um desenvolvedor do GNOME: "*não existem razões *reais* tecnológicas e comprovadas por que alguém deveria executar um aplicativo GUI como root. Ao executar aplicativos GUI como um usuário administrador, você está literalmente executando milhões de linhas de código que não foram auditados corretamente para executar sob privilégios elevados, você também está executando código que tocará em arquivos dentro de seu $HOME e poderá alterar sua propriedade no sistema de arquivos; conectar-se via IPC a ainda mais códigos em execução, etc. Você está abrindo uma enorme falha de segurança [...].*"[[1]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5)

Evita executar aplicativos gráficos como [root](/index.php/Usu%C3%A1rio_root "Usuário root") se possível, veja [#Contornar aplicativos gráficos como root](#Contornar_aplicativos_gráficos_como_root).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Contornar aplicativos gráficos como root](#Contornar_aplicativos_gráficos_como_root)
    *   [1.1 sudoedit](#sudoedit)
    *   [1.2 GVFS](#GVFS)
*   [2 Xorg](#Xorg)
    *   [2.1 Métodos pontuais](#Métodos_pontuais)
    *   [2.2 Métodos alternativos](#Métodos_alternativos)
        *   [2.2.1 Xhost](#Xhost)
        *   [2.2.2 Permitir permanentemente acesso de root](#Permitir_permanentemente_acesso_de_root)
*   [3 Wayland](#Wayland)
    *   [3.1 Usar xhost](#Usar_xhost)

## Contornar aplicativos gráficos como root

### sudoedit

Para editar arquivos como root, use [sudoedit](/index.php/Sudoedit "Sudoedit").

### GVFS

O acesso aos arquivos e diretórios privilegiados é possível através do [GVFS](/index.php/GVFS "GVFS") especificando o [backend](https://wiki.gnome.org/Projects/gvfs/backends) `admin` no esquema de URI[[2]](https://bugzilla.redhat.com/show_bug.cgi?id=1274451#c27)[[3]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c2), por exemplo:

```
$ nautilus admin:///root/

```

ou

```
$ gedit admin:///etc/fstab

```

**Dica:** Isso também pode ser feito na barra de local/seletor de arquivo do aplicativo: por exemplo, no [nautilus](https://www.archlinux.org/packages/?name=nautilus) ou no [gedit](https://www.archlinux.org/packages/?name=gedit), digite `Ctrl+L` e preencha o esquema `admin://` no caminho do recurso. O mesmo efeito pode ser obtido pela barra de endereços de servidor [Outros locais](https://wiki.gnome.org/Apps/Files?action=AttachFile&do=get&target=network.png).

## Xorg

Por padrão, e por motivos de segurança, o root não poderá se conectar a um [servidor X](/index.php/Servidor_X "Servidor X") de usuário não-root. Existem várias maneiras de permitir que o root faça isso, no entanto, se necessário.

A maneira correta e recomendada de executar aplicativos GUI no X com privilégios elevados é criar uma política [Polkit](/index.php/Polkit "Polkit"), conforme mostrado em [neste tópico de fórum](https://bbs.archlinux.org/viewtopic.php?pid=999328#p999328). Isto deve, no entanto, "*ser usado somente para programas legados*", como [pkexec(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pkexec.1) lembra. Os aplicativos devem "*adiar as operações privilegiadas para um pedaço de código auditável, autocontido, **mínimo**, que é executado após executar um escalonamento de privilégios e ser descartado quando não for necessário*"[[4]](https://bugzilla.gnome.org//show_bug.cgi?id=772875#c5). Isso pode ser o objeto de um relatório de bug para o projeto upstream.

### Métodos pontuais

Esses métodos envolvem o aplicativo em uma estrutura de elevação e descartam os privilégios adquiridos depois que ele sai:

*   [kdesu](https://www.archlinux.org/packages/?name=kdesu), [kdesu(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/kdesu.1)

```
$ kdesu *aplicativo*

```

*   [sudo](/index.php/Sudo "Sudo") (deve estar [configurado adequadamente](/index.php/Sudo#Configuration "Sudo"))

```
$ sudo *aplicativo*

```

*   [sux](https://aur.archlinux.org/packages/sux/) (wrapper do su que transferirá suas credenciais X)

```
$ sux root *aplicativo*

```

### Métodos alternativos

Esses métodos permitirão que o root se conecte a um servidor X de usuário não-root, mas apresentam níveis variados de riscos de segurança, especialmente se você executar o ssh. Se você estiver protegido por um firewall, considere-o seguro o suficiente para suas necessidades.

#### Xhost

[Xhost](/index.php/Xhost_(Portugu%C3%AAs) "Xhost (Português)") pode ser usado para permitir temporariamente acesso como root.

#### Permitir permanentemente acesso de root

	**Método 1**: Adicionar a linha

```
session         optional        pam_xauth.so

```

para `/etc/pam.d/su` e `/etc/pam.d/su-l`. Então, mude para seu usuário root usando `su` ou `su -`.

	**Método 2**: Globalmente no `/etc/profile`

Adicione a seguinte linha ao `/etc/profile`:

```
export XAUTHORITY=/home/*usuario*/.Xauthority

```

Isso vai permitir permanentemente que o root se conecte a um servidor X de usuário não-root.

Ou meramente especifique um aplicativo em particular:

```
export XAUTHORITY=/home/*usuario*/.Xauthority *nome-do-aplicativo*

```

sendo `*nome-do-aplicativo*` o nome do aplicativo em particular (p.ex., *kwrite*)

## Wayland

Tentar executar um aplicativo gráfico como root via [su](/index.php/Su "Su"), [sudo](/index.php/Sudo "Sudo") ou [pkexec](/index.php/Polkit "Polkit") em uma sessão Wayland (por exemplo, [GParted](/index.php/GParted "GParted") ou [Gedit](/index.php/Gedit "Gedit")), falhará com um erro semelhante a este:

```
$ sudo gedit
No protocol specified
Unable to init server: Não foi possível conectar: Conexão recusada

(gedit:2349): Gtk-WARNING **: cannot open display: :0

```

Antes do Wayland, a execução de aplicativos de GUI com privilégios elevados poderia ser implementada adequadamente criando uma política de [Polkit](/index.php/Polkit "Polkit") ou, mais perigosamente, executando o comando em um terminal, prefixando o comando com `sudo`; mas sob (X)Wayland isso não funciona mais, já que o padrão foi feito para permitir que o usuário que iniciou o servidor X conectasse clientes a ele (veja o [relatório de erro](https://bugzilla.redhat.com/show_bug.cgi?id=1266771) e [os](https://cgit.freedesktop.org/xorg/xserver/commit/?id=c4534a3) [commits](https://cgit.freedesktop.org/xorg/xserver/commit/?id=76636ac) [upstream](https://cgit.freedesktop.org/xorg/xserver/commit/?id=4b4b908) aos quais ele se refere).

Evite executar aplicativos gráficos como root se possível, veja [#Contornar aplicativos gráficos como root](#Contornar_aplicativos_gráficos_como_root).

Uma solução mais versátil, embora mais insegura, permite que qualquer aplicativo gráfico seja executado como root [usando o xhost](#Usar_xhost).

### Usar xhost

Uma solução mais versátil – embora muito menos segura – é usar [xhost](/index.php/Xhost_(Portugu%C3%AAs) "Xhost (Português)") para permitir temporariamente que o usuário root acesse a sessão X do usuário local[[5]](https://bugzilla.redhat.com/show_bug.cgi?id=1274451#c64). Para fazer isso, execute o seguinte comando como o usuário atual (não privilegiado):

```
$ xhost si:localuser:root

```

Para remover esse acesso após o aplicativo ter sido fechado:

```
$ xhost -si:localuser:root

```