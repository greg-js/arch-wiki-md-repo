**Status de tradução:** Esse artigo é uma tradução de [Web application package guidelines](/index.php/Web_application_package_guidelines "Web application package guidelines"). Data da última tradução: 2019-06-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Web_application_package_guidelines&diff=0&oldid=571774) na versão em inglês.

**[Diretrizes de criação de pacotes](/index.php/Padr%C3%B5es_de_empacotamento_do_Arch "Padrões de empacotamento do Arch")**

* * *

[32-bit](/index.php/Diretrizes_de_pacotes_32-bit "Diretrizes de pacotes 32-bit") – [CLR](/index.php/Diretrizes_de_pacotes_CLR "Diretrizes de pacotes CLR") – [Cross](/index.php/Diretrizes_de_pacotes_de_ferramentas_de_compila%C3%A7%C3%A3o_cruzada "Diretrizes de pacotes de ferramentas de compilação cruzada") – [Eclipse](/index.php/Diretrizes_de_pacotes_de_plugin_do_Eclipse "Diretrizes de pacotes de plugin do Eclipse") – [Electron](/index.php/Diretrizes_de_pacotes_Electron "Diretrizes de pacotes Electron") – [Free Pascal](/index.php/Diretrizes_de_pacotes_Free_Pascal "Diretrizes de pacotes Free Pascal") – [GNOME](/index.php/Diretrizes_de_pacotes_GNOME "Diretrizes de pacotes GNOME") – [Go](/index.php/Diretrizes_de_pacotes_Go "Diretrizes de pacotes Go") – [Haskell](/index.php/Diretrizes_de_pacotes_Haskell "Diretrizes de pacotes Haskell") – [Java](/index.php/Diretrizes_de_pacotes_Java "Diretrizes de pacotes Java") – [KDE](/index.php/Diretrizes_de_pacotes_KDE "Diretrizes de pacotes KDE") – [Kernel](/index.php/Diretrizes_de_pacotes_de_m%C3%B3dulos_de_kernel "Diretrizes de pacotes de módulos de kernel") – [Lisp](/index.php/Diretrizes_de_pacotes_Lisp "Diretrizes de pacotes Lisp") – [MinGW](/index.php/Diretrizes_de_pacotes_MinGW "Diretrizes de pacotes MinGW") – [Node.js](/index.php/Diretrizes_de_pacotes_Node.js "Diretrizes de pacotes Node.js") – [Nonfree](/index.php/Diretrizes_de_pacotes_de_aplicativos_n%C3%A3o_livres "Diretrizes de pacotes de aplicativos não livres") – [OCaml](/index.php/Diretrizes_de_pacotes_OCaml "Diretrizes de pacotes OCaml") – [Perl](/index.php/Diretrizes_de_pacotes_Perl "Diretrizes de pacotes Perl") – [PHP](/index.php/Diretrizes_de_pacotes_PHP "Diretrizes de pacotes PHP") – [Python](/index.php/Diretrizes_de_pacotes_Python "Diretrizes de pacotes Python") – [R](/index.php/Diretrizes_de_pacotes_R "Diretrizes de pacotes R") – [Ruby](/index.php/Diretrizes_de_pacotes_Ruby_Gem "Diretrizes de pacotes Ruby Gem") – [Rust](/index.php/Diretrizes_de_pacotes_Rust "Diretrizes de pacotes Rust") – [VCS](/index.php/Diretrizes_de_pacotes_VCS "Diretrizes de pacotes VCS") – [Web](/index.php/Diretrizes_de_pacotes_de_aplicativos_da_Web "Diretrizes de pacotes de aplicativos da Web") – [Wine](/index.php/Diretrizes_de_pacotes_Wine "Diretrizes de pacotes Wine")

Essa página descreve como empacotar aplicativos web.

## Usuário separado

Por motivos de segurança, cada aplicativo web deve ser executado como um usuário separado (sem privilégios) (p.ex., `*$pkgname*`).

**Nota:** Tradicionalmente, muitos aplicativos eram executados como o usuário/grupo `http`, o que pode ser considerado como inseguro, pois em tal cenário aplicativos podem ler os arquivos um dos outros.

Consulta as páginas man [systemd-sysusers(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sysusers.8), [sysusers.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sysusers.d.5), [systemd-tmpfiles(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-tmpfiles.8) e [tmpfiles.d(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/tmpfiles.d.5) para detalhes sobre como criar usuários com propriedade de arquivos e pastas para aquele usuário em um pacote.

## Estrutura de diretórios

O layout segue o [FHS](/index.php/FHS_(Portugu%C3%AAs) "FHS (Português)").

*   `/usr/share/webapps/*$pkgname*`: O *diretório de dados* do aplicativo detém os arquivos do aplicativo web. Arquivos são de propriedade do `root` e são, portanto, somente-leitura pelo usuário e grupo do aplicativo `*$pkgname*`.

*   `/etc/webapps/*$pkgname*`: O *diretório de configuração* do aplicativo detém arquivos de configuração para o aplicativo (por link simbólico para o *diretório de dados*). Os arquivos localizados aqui têm que ir para vetor [backup](/index.php/PKGBUILD_(Portugu%C3%AAs)#backup "PKGBUILD (Português)") e são de propriedade do usuário e grupo `*$pkgname*`.

**Atenção:** Arquivos potencialmente contendo informações de autenticação **devem ser protegidos** (p.ex., não podem ser lidos por nenhum outro usuário ou grupo no sistema, exceto `root` e `*$pkgname*`)!

*   `/run/*$pkgname*`: O *diretório de runtime* do aplicativo (de propriedade do usuário e grupo `*$pkgname*`). Ele pode ser usado para soquetes (p.ex., em configurações facilitando [ativação de soquete](/index.php/UWSGI#Socket_activation "UWSGI")).

**Nota:** De acordo com as diretrizes do pacote em [diretórios](/index.php/Diretrizes_de_empacotamento_do_Arch#Diretórios "Diretrizes de empacotamento do Arch"), `/run` não deve estar contido em um pacote. Use [tmpfiles](/index.php/Tmpfiles_(Portugu%C3%AAs) "Tmpfiles (Português)") para adicionar o diretório com permissões correspondentes.

*   `/var/cache/*$pkgname*`: O *diretório de cache* do aplicativo (de propriedade do usuário e do grupo `*$pkgname*`). Ele (ou subpastas nele) é vinculado ao *diretório de dados* para aplicativos que requerem diretórios de cache que podem ser escritos.

*   `/var/lib/*$pkgname*`: O *armazenamento persistente* do aplicativo (de propriedade do usuário e grupo `*$pkgname*`). Ele (ou subpastas nele) é vinculado ao *diretório de dados* para aplicativos que exigem diretórios de armazenamento persistentes.