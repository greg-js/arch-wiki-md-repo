**Status de tradução:** Esse artigo é uma tradução de [Environment variables](/index.php/Environment_variables "Environment variables"). Data da última tradução: 2018-08-24\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Environment_variables&diff=0&oldid=536709) na versão em inglês.

Artigos relacionados

*   [Aplicativos padrão](/index.php/Default_applications "Default applications")

Uma variável de ambiente é um objeto nomeado que contém dados usados por um ou mais aplicativos. Em termos simples, é uma variável com um nome e um valor. O valor de uma variável ambiental pode, por exemplo, ser a localização de todos os arquivos executáveis no sistema de arquivos, o editor padrão que deve ser usado ou as configurações de localidade do sistema. Os usuários novos no Linux geralmente podem encontrar essa maneira de gerenciar as configurações um pouco incontrolável. No entanto, as variáveis de ambiente fornecem uma maneira simples de compartilhar configurações entre vários aplicativos e processos no Linux.

## Contents

*   [1 Utilitários](#Utilit.C3.A1rios)
*   [2 Definindo variáveis](#Definindo_vari.C3.A1veis)
    *   [2.1 Globalmente](#Globalmente)
    *   [2.2 Por usuário](#Por_usu.C3.A1rio)
        *   [2.2.1 Aplicativos gráficos](#Aplicativos_gr.C3.A1ficos)
    *   [2.3 Por sessão](#Por_sess.C3.A3o)
*   [3 Exemplos](#Exemplos)
    *   [3.1 Programas padrão](#Programas_padr.C3.A3o)
    *   [3.2 Usando pam_env](#Usando_pam_env)
*   [4 Veja também](#Veja_tamb.C3.A9m)

## Utilitários

O pacote [coreutils](https://www.archlinux.org/packages/?name=coreutils) contém os programas *printenv* e *env*. Para listar as variáveis de ambiente atuais com valores:

```
$ printenv

```

**Nota:** Algumas variáveis de ambiente são específicas do usuário. Verifique comparando as saídas de *printenv* como um usuários comum e como *root*.

O utilitário `env` pode ser usado para executar um comando sob um ambiente modificado. O seguinte exemplo vai iniciar *xterm* com a variável de ambiente `EDITOR` definida para `vim`. Isso não afetará a variável de ambiente global `EDITOR`.

```
$ env EDITOR=vim xterm

```

O comando *set*, embutido no [Bash](/index.php/Bash "Bash"), permite alterar as variáveis de opções shell e definir os parâmetros posicionais, ou para exibir os nomes das variáveis de shell. Para mais informações, veja [a documentação do *set*](http://www.gnu.org/software/bash/manual/bash.html#The-Set-Builtin).

Cada processo armazena seu ambiente no arquivo `/proc/$PID/environ`. Esse arquivo contém um par de chave-valor delimitado por um caractere nulo (`\x0`). Um formato mais legível para humanos pode ser obtido com o [sed](/index.php/Utilit%C3%A1rios_principais#sed "Utilitários principais"), p.ex. `sed 's:\x0:
:g' /proc/$PID/environ`.

## Definindo variáveis

### Globalmente

A maioria das distribuições do Linux diz-lhe para alterar ou adicionar definições de variáveis de ambiente em `/etc/profile` ou em outros locais. Tenha em mente que também existem arquivos de configuração específicos do pacote contendo configurações de variáveis, como `/etc/locale.conf`. Certifique-se de manter e gerenciar as variáveis de ambiente e prestar atenção aos inúmeros arquivos que podem conter variáveis de ambiente. Em princípio, qualquer script shell pode ser usado para inicializar variáveis ambientais, mas seguindo as convenções UNIX tradicionais, essas declarações devem estar presentes apenas em determinados arquivos.

Os seguintes arquivos devem ser usados para definir variáveis de ambiente globais em seu sistema: `/etc/environment`, `/etc/profile` e arquivos de configuração específicos do shell. Cada um desses arquivos tem diferentes limitações, então você deve selecionar cuidadosamente o apropriado para seus propósitos.

*   `/etc/environment` é usado pelo módulo pam_env e é agnóstico do shell, portanto script ou expansão glob não podem ser usados. O arquivo aceita apenas pares `*variável=valor*`. Veja [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) e [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5) para detalhes.

*   Arquivos de configuração globais de seu [shell](/index.php/Shell_de_linha_de_comando "Shell de linha de comando"), inicializa variáveis e executa scripts. Por exemplo, [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") ou [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").
*   `/etc/profile` inicializa variáveis para shells de login *apenas*. Ele, porém, executa scripts e pode ser usado por todos os shells compatíveis com [Bourne shell](https://en.wikipedia.org/wiki/Bourne_shell "wikipedia:Bourne shell").

Neste exemplo, adicionamos o diretório `~/bin` ao `PATH` para o respectivo usuário. Para fazer isso, basta colocar isso em seu arquivo de configuração global de variável de ambiente (`/etc/profile` ou `/etc/bash.bashrc`):

```
# Se o ID do usuário for maior ou igual a 1000 & se ~/bin existir e é um diretório e se ~/bin ainda não estiver no seu $PATH
# então exporta ~/bin para seu $PATH.
if [[ $UID -ge 1000 && -d $HOME/bin && -z $(echo $PATH | grep -o $HOME/bin) ]]
then
    export PATH="${PATH}:$HOME/bin"
fi

```

### Por usuário

**Nota:** O daemon dbus e a instância de usuário do systemd não herdam quaisquer variáveis de ambiente definidas em lugares como `~/.bashrc` etc. Isso significa que, por exemplo, programas ativados por dbus, como o GNOME Files não vão usá-las por padrão. Veja [Systemd/User#Environment variables](/index.php/Systemd/User#Environment_variables "Systemd/User").

Nem sempre você deseja definir uma variável de ambiente globalmente. Por exemplo, você pode querer adicionar `/home/meu_usuário/bin` à variável `PATH`, mas não deseja que todos os outros usuários em seu sistema tenham isso em seus `PATH` também. Variáveis de ambiente locais pode ser definidos em muitos arquivos diferentes:

*   `~/.pam_environment` é o equivalente específico de usuário de `/etc/security/pam_env.conf` [[1]](https://github.com/linux-pam/linux-pam/issues/6), usado pelo módulo pam_env. Veja [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) e [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5) para detalhes.
*   Arquivos de configuração de usuário de seu [shell](/index.php/Shell_de_linha_de_comando "Shell de linha de comando"), por exemplo [Bash#Configuration files](/index.php/Bash#Configuration_files "Bash") ou [Zsh#Startup/Shutdown files](/index.php/Zsh#Startup.2FShutdown_files "Zsh").
*   `~/.profile` é usado por muitos shells como reserva, veja [Wikipedia:pt:Shell do Unix#Arquivos de configuração](https://en.wikipedia.org/wiki/pt:Shell_do_Unix#Arquivos_de_configura.C3.A7.C3.A3o "wikipedia:pt:Shell do Unix").
*   [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") vai carregar variáveis de ambiente de `~/.config/environment.d/*.conf` veja [environment.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/environment.d.5) e [https://wiki.gnome.org/Initiatives/Wayland/SessionStart](https://wiki.gnome.org/Initiatives/Wayland/SessionStart).

Para adicionar um diretório para o `PATH` para uso local, coloque o seguinte em `~/.bash_profile`:

```
export PATH="${PATH}:/home/meu_usuário/bin"

```

Para atualizar a variável, autentique-se novamente ou use *source* para recarregar o arquivo: `$ source ~/.bash_profile`.

#### Aplicativos gráficos

Variáveis de ambiente para aplicativos de interface gráfica de usuário (GUI) podem ser definidos em [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)"), ou em [xprofile](/index.php/Xprofile_(Portugu%C3%AAs) "Xprofile (Português)") ao usar um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição"), por exemplo:

 `~/.xinitrc` 
```
export PATH="${PATH}:~/scripts"
export GUIVAR=value
```

### Por sessão

Às vezes, são necessárias definições ainda mais rigorosas. Pode-se querer executar temporariamente executáveis a partir de um diretório específico criado sem ter que digitar o caminho absoluto para cada um, ou editar arquivos de configuração do shell pelo curto período de tempo necessário para executá-los.

Nesse caso, você pode definir a variável `PATH` em sua sessão atual, combinada com o comando *export*. Enquanto você não terminar, a variável `PATH` usará as configurações temporárias. Para adicionar um diretório específico da sessão para `PATH`, emita:

```
$ export PATH="${PATH}:/home/meu_usuário/tmp/usr/bin"

```

## Exemplos

A seção a seguir lista uma série de variáveis de ambiente comuns usadas por um sistema Linux e descreve seus valores.

*   `DE` indica o ambiente desktop (*D*esktop *E*nvironment) sendo usado. [xdg-open](/index.php/Xdg-open "Xdg-open") vai usá-la para escolher um aplicativo seletor de arquivo mais amigável para o usuário que o ambiente desktop fornece. Alguns pacotes precisam ser instalados para usar esse recurso. Para o [GNOME](/index.php/GNOME_(Portugu%C3%AAs) "GNOME (Português)"), que seria o [libgnome](https://aur.archlinux.org/packages/libgnome/); para o [Xfce](/index.php/Xfce "Xfce") esse seria o [exo](https://www.archlinux.org/packages/?name=exo). Valores reconhecidos da variável `DE` são: `gnome`, `kde`, `xfce`, `lxde` e `mate`.

	A variável de ambiente `DE` precisa ser exportada antes de iniciar o gerenciador de janela. Por exemplo:

 `~/.xinitrc` 
```
export DE="xfce"
exec openbox
```

	Isso fará com que *xdg-open* use o mais amigável *exo-open*, porque ele presume que está executando dentro do Xfce. Use *exo-preferred-applications* para configurar.

*   `DESKTOP_SESSION` é similar ao `DE`, mas usado no ambiente desktop [LXDE](/index.php/LXDE "LXDE"): quando `DESKTOP_SESSION` é definido para `LXDE`, *xdg-open* vai usar associações de arquivos do *pcmanfm*.

*   `PATH` contém uma lista, separada por caractere de dois pontos, de diretórios nos quais seu sistema procura por arquivos executáveis. Quando um comando comum (p.ex.: *ls*, *rc-update* ou *emerge*) é interpretado pelo shell (p.ex., *bash* ou *zsh*), o shell procura por um arquivo executável com o mesmo nome que seu comando nos diretórios listados, e o executa. Para executar os executáveis que não estão listados no `PATH`, o caminho absoluto para o executável deve ser dado: `/bin/ls`.

**Nota:** É aconselhável não incluir o diretório de trabalho atual (`.`) no seu `PATH` por motivos de segurança, pois pode enganar o usuário para executar comandos maliciosos.

*   `HOME` contém o caminho para o diretório inicial do usuário atual. Esta variável pode ser usada por aplicativos para associar arquivos de configuração e tal como com o usuário que está executando-o.

*   `PWD` contém o caminho para o seu diretório de trabalho.

*   `OLDPWD` contém o caminho de seu diretório de trabalho anterior, isto é, o valor de `PWD` antes do último *cd* ser executado.

*   `TERM` contém o tipo de terminal em execução, como `xterm-256color`. Ele é usado por programas em execução no terminal que desejem usam capacidades específicas do terminal.

*   `MAIL` contém a localização de e-mails de entrada. A configuração tradicional é `/var/spool/mail/$LOGNAME`.

*   `ftp_proxy` e `http_proxy` contêm o servidor de proxy FTP e HTTP, respectivamente:

```
ftp_proxy="ftp://192.168.0.1:21"
http_proxy="http://192.168.0.1:80"

```

*   `MANPATH` contém uma lista, separada por caractere de dois pontos, de diretório nos quais o *man* pesquisa por páginas man.

**Nota:** No `/etc/profile`, há um comentário que afirma "Man é muito melhor que nós para descobrir isso", então essa variável geralmente deve ser deixada no seu padrão, isto é, `/usr/share/man:/usr/local/share/man`

*   `INFODIR` contém uma lista, separada por caracteres de dois pontos, de diretórios nos quais o comando *info* pesquisa por páginas info, p.ex.: `/usr/share/info:/usr/local/share/info`

*   `TZ` pode ser usado para definir um fuso horário diferente como o do usuário. Os fusos listados em `/usr/share/zoneinfo/` podem ser usados como referências, por exemplo `TZ=":/usr/share/zoneinfo/Pacific/Fiji"`. Ao apontar a variável `TZ` para um arquivo de *zoneinfo*, deve-se iniciar com um caractere de dois pontos, conforme [o manual do GNU](https://www.gnu.org/software/libc/manual/html_node/TZ-Variable.html).

### Programas padrão

*   `SHELL` contém o caminho para o [shell preferido](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html#tag_08_03) do usuário. Note que isso não é necessariamente o shell que está sendo usado no momento, apesar do [Bash](/index.php/Bash "Bash") definir essa variável na inicialização.

*   `PAGER` contém o comando para executar o programa de listagem de conteúdo dos arquivos, p.ex. `/bin/less`.

*   `EDITOR` contém o comando para executar o programa leve usado para edição de arquivos, p.ex. `/usr/bin/nano`. Por exemplo, você pode escrever uma opção interativa entre o *gedit* sob [X](/index.php/X_(Portugu%C3%AAs) "X (Português)") ou *nano*, neste exemplo:

```
export EDITOR="$(if [[ -n $DISPLAY ]]; then echo 'gedit'; else echo 'nano'; fi)"

```

*   `VISUAL` contém o comando para executar o editor de pleno direito que é usado para tarefas mais exigentes, como a edição de mensagens de correio (p.ex., `vi`, [vim](/index.php/Vim "Vim"), [emacs](/index.php/Emacs "Emacs") etc).

*   `BROWSER` contém o caminho para o navegador web. Útil para configurar um arquivo de configuração de shell interativo para que ele possa ser alterado dinamicamente dependendo da disponibilidade de um ambiente gráfico, como o [X](/index.php/X_(Portugu%C3%AAs) "X (Português)"):

```
if [ -n "$DISPLAY" ]; then
    export BROWSER=firefox
else 
    export BROWSER=links
fi

```

### Usando pam_env

O módulo [PAM](/index.php/PAM "PAM") [pam_env(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.8) carrega as variáveis a serem definidas no ambiente dos seguintes arquivos: `/etc/security/pam_env.conf`, `/etc/environment` e `~/.pam_environment`.

*   `/etc/environment` deve consistir de pares `*VARIÁVEL*=*valor*` simples em linhas separadas, por exemplo: `EDITOR=NANO` 

*   `/etc/security/pam_env.conf` e `~/.pam_environment` compartilham o mesmo formato a seguir: `VARIÁVEL [DEFAULT=*valor*] [OVERRIDE=*valor*]` `@{HOME}` e `@{SHELL}` são variáveis especiais que expandem para o que está definido no `/etc/passwd`. O exemplo a seguir ilustra como expandir a variável de ambiente `HOME` em outra variável: `XDG_CONFIG_HOME   DEFAULT=@{HOME}/.config` 
    **Nota:** As variáveis `${HOME}` e `${SHELL}` não são vinculadas as variáveis de ambiente `HOME` e `SHELL`, elas não estão definidas por padrão.
    O formato também permite expandir variáveis definidas nos valores de outras variáveis usando `${*VARIÁVEL*}` , tipo isso: `GNUPGHOME        DEFAULT=${XDG_CONFIG_HOME}/gnupg` Pares `*VARIÁVEL*=*valor*` também são permitidos, mas não há suporte a expansão de variável naqueles pares. Veja [pam_env.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/pam_env.conf.5) para mais informações.

**Nota:** Esses arquivos são lidos antes de outros arquivos, em especial antes de `~/.profile`, `~/.bash_profile` e `~/.zshenv`.

## Veja também

*   [Documentação do Gentoo Linux](https://wiki.gentoo.org/wiki/Handbook:X86/Working/EnvVar)
*   [Ubuntu Community Wiki - Variáveis de ambiente](https://help.ubuntu.com/community/EnvironmentVariables)