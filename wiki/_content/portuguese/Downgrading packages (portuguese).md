Artigos relacionados

*   [Arch Build System](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)")

Antes de fazer o downgrade de um ou mais pacotes, considere o porquê de você desejar fazê-lo. Se é por causa de um erro, pesquise no [rastreador de erros](https://bugs.archlinux.org/) por tarefas existentes. Se não houver, adicione uma nova tarefa; é melhor corrigir erros, ou pelo menos avisar outros usuários sobre possíveis problemas.

**Atenção:**

*   Fazer downgrade de um pacote pode exigir que se faça downgrade de suas dependências também. Quando o número dos pacotes para se fazer downgrade é grande demais, considere usar um snapshot. Veja [Arch Linux Archive (Português)#Como restaurar todos os pacotes para uma data específica](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs)#Como_restaurar_todos_os_pacotes_para_uma_data_específica "Arch Linux Archive (Português)").
*   Tenha cuidado com alterações a arquivos de configuração e scritps. Por agora, pacman pode tratar disso, desde que nós não ignoremos as travas de segurança.
*   Se o downgrade involve uma alteração de soname, toda a dependência pode precisar de downgrade ou [recompilação](/index.php/Frequently_asked_questions_(Portugu%C3%AAs)#E_se_eu_executar_uma_atualização_completa_do_sistema_e_houver_uma_atualização_para_uma_biblioteca_compartilhada,_mas_não_para_os_aplicativos_que_dependem_dela? "Frequently asked questions (Português)") também.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Retorne para uma versão anterior do pacote](#Retorne_para_uma_versão_anterior_do_pacote)
    *   [1.1 Usando o cache do pacman](#Usando_o_cache_do_pacman)
    *   [1.2 Fazendo downgrade do kernel](#Fazendo_downgrade_do_kernel)
    *   [1.3 Arch Linux Archive](#Arch_Linux_Archive)
    *   [1.4 Recompilar o pacote](#Recompilar_o_pacote)
    *   [1.5 Automação](#Automação)
*   [2 Retornar do [testing]](#Retornar_do_[testing])

## Retorne para uma versão anterior do pacote

### Usando o cache do pacman

Se um pacote foi instalado em um estágio anterior, e o [cache do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Limpando_o_cache_de_pacotes "Pacman (Português)") não foi limpado, instale uma versão anterior do `/var/cache/pacman/pkg/`.

Esse processo vai remover o pacote atual e instalar a versão anterior. Alteração nas dependências será tratada, mas o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") não tratará de conflitos de versão. Se uma biblioteca ou outro pacote precisar de um downgrade com os pacotes, por favor esteja ciente de que você mesmo terá que fazer downgrade deste pacote também.

```
# pacman -U /var/cache/pacman/pkg/*pacote*-*versão_antiga*.pkg.tar.xz

```

Uma vez o pacote seja revertido, adicione-o temporariamente para a [seção IgnorePkg](/index.php/Pacman_(Portugu%C3%AAs)#Pular_pacotes_para_não_serem_atualizados "Pacman (Português)") do `pacman.conf`, até a dificuldade com o pacote atualizado ser resolvida.

### Fazendo downgrade do kernel

Em caso de problema com um novo kernel, é possível fazer downgrade dos pacotes de Linux para as últimas que estejam funcionando [#Usando o cache do pacman](#Usando_o_cache_do_pacman). Vá para o diretório `/var/cache/pacman/pkg` e faça downgrade de pelo menos [linux](https://www.archlinux.org/packages/?name=linux), [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) e qualquer módulo do kernel. Por exemplo:

```
# pacman -U linux-4.15.8-1-x86_64.pkg.tar.xz linux-headers-4.15.8-1-x86_64.pkg.tar.xz virtualbox-host-modules-arch-5.2.8-4-x86_64.pkg.tar.xz

```

**Dica:** Se você não conseguir inicializar após uma atualização do kernel, você pode fazer downgrade do kernel com um [chroot](/index.php/Change_root_(Portugu%C3%AAs) "Change root (Português)") para o sistema. Inicialize usando uma [mídia de instalação em flash USB](/index.php/M%C3%ADdia_de_instala%C3%A7%C3%A3o_em_flash_USB "Mídia de instalação em flash USB") com Arch Linux e monte a partição onde seu sistema está instalado para `/mnt`. Se você tiver `/boot` ou `/var` em partições separadas, monte-as também em `/mnt` (por exemplo, `mount /dev/sdc3 /mnt/boot`). Então, faça um *chroot* no sistema usando: `# arch-chroot /mnt /bin/bash` Agora você pode entrar no diretório de cache *pacman* e fazer o downgrade dos pacotes do Linux usando o comando indicado acima. Uma vez feito isso, saia do chroot (com `exit`) e reinicie.

### Arch Linux Archive

O [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)") é um *snapshot* diário dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Ele pode ser usado para [instalar uma versão anterior de um pacote](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs)#Como_fazer_downgrade_de_um_pacote "Arch Linux Archive (Português)") ou [restaurar o sistema para uma data anterior](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs)#Como_restaurar_todos_os_pacotes_para_uma_data_específica "Arch Linux Archive (Português)").

### Recompilar o pacote

Se o pacote está indisponível, localize o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") correto e recompile-o com [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)").

Para pacotes dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), obtenha o PKGBUILD com [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") e altere a versão do software. Alternativamente, localize o pacote no site de [pacotes](https://www.archlinux.org/packages), clique "View Changes" e navegue na versão desejada. Os arquivos estão disponíveis por meio de uma *snapshot* de `.tar.gz` e via uma visão de "árvore".

Veja também [Arch Build System (Português)#Faça checkout de uma versão anterior de um pacote](/index.php/Arch_Build_System_(Portugu%C3%AAs)#Faça_checkout_de_uma_versão_anterior_de_um_pacote "Arch Build System (Português)").

Pacotes antigos do AUR podem ser compilados fazendo checkout de um commit antigo no repositório Git do pacote do AUR. Para PKGBUILDs do AUR pré-2015, veja [Arch User Repository (Português)#Repositórios Git para pacotes AUR3](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Repositórios_Git_para_pacotes_AUR3 "Arch User Repository (Português)").

### Automação

[downgrader](https://aur.archlinux.org/packages/downgrader/) é uma ferramenta que funciona com libalpm, oferece suporte ao log do pacman e a fazer downgrade de pacotes usando o [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)"), cache local e [ARM](http://repo-arm.archlinuxcn.org).

O pacote [downgrade](https://aur.archlinux.org/packages/downgrade/) é um script Bash para faer downgrade de um (ou múltiplos) pacotes, usando o cache do pacman ou o [Arch Rollback Machine](/index.php/Arch_Rollback_Machine_(Portugu%C3%AAs) "Arch Rollback Machine (Português)"). Veja `man downgrade` para detalhes.

[agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/) lista/obtém/instala rapidamente pacotes do [Arch Linux Archive](/index.php/Arch_Linux_Archive_(Portugu%C3%AAs) "Arch Linux Archive (Português)").

## Retornar do [testing]

Veja [Repositórios oficiais#Desabilitando repositórios de teste](/index.php/Reposit%C3%B3rios_oficiais#Desabilitando_repositórios_de_teste "Repositórios oficiais").