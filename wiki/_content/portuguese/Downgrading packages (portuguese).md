Artigos relacionados

*   [Arch Build System (Português)](/index.php/Arch_Build_System_(Portugu%C3%AAs) "Arch Build System (Português)")
*   [makepkg (Português)](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)")
*   [pacman (Português)](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)")
*   [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive")

Antes de fazer o downgrade de um ou mais pacotes, considere o porquê de você desejar fazê-lo. Se é por causa de um erro, pesquise no [rastreador de erros](https://bugs.archlinux.org/) por tarefas existentes. Se não houver, adicione uma nova tarefa; é melhor corrigir erros, ou pelo menos avisar outros usuários sobre possíveis problemas.

**Atenção:**

*   Fazer downgrade de um pacote pode exigir que se faça downgrade de suas dependências também. Quando o número dos pacotes para se fazer downgrade é grande demais, considere usar um snapshot. Veja [Arch Linux Archive#How to restore all packages to a specific date](/index.php/Arch_Linux_Archive#How_to_restore_all_packages_to_a_specific_date "Arch Linux Archive").
*   Tenha cuidado com alterações a arquivos de configuração e scritps. Por agora, pacman pode tratar disso, desde que nós não ignoremos as travas de segurança.
*   Se o downgrade involve uma alteração de soname, toda a dependência pode precisar de downgrade ou [recompilação](/index.php/Frequently_asked_questions_(Portugu%C3%AAs)#E_se_eu_executar_uma_atualiza.C3.A7.C3.A3o_completa_do_sistema_e_houver_uma_atualiza.C3.A7.C3.A3o_para_uma_biblioteca_compartilhada.2C_mas_n.C3.A3o_para_os_aplicativos_que_dependem_dela.3F "Frequently asked questions (Português)") também.

## Contents

*   [1 Retorne para uma versão anterior do pacote](#Retorne_para_uma_vers.C3.A3o_anterior_do_pacote)
    *   [1.1 Usando o cache do pacman](#Usando_o_cache_do_pacman)
    *   [1.2 Fazendo downgrade do kernel](#Fazendo_downgrade_do_kernel)
    *   [1.3 Arch Linux Archive](#Arch_Linux_Archive)
    *   [1.4 Recompilar o pacote](#Recompilar_o_pacote)
    *   [1.5 Automação](#Automa.C3.A7.C3.A3o)
*   [2 Retornar do [testing]](#Retornar_do_.5Btesting.5D)

## Retorne para uma versão anterior do pacote

### Usando o cache do pacman

Se um pacote foi instalado em um estágio anterior, e o [cache do pacman](/index.php/Pacman_(Portugu%C3%AAs)#Limpando_o_cache_de_pacotes "Pacman (Português)") não foi limpado, instale uma versão anterior do `/var/cache/pacman/pkg/`.

Esse processo vai remover o pacote atual e instalar a versão anterior. Alteração nas dependências será tratada, mas o [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") não tratará de conflitos de versão. Se uma biblioteca ou outro pacote precisar de um downgrade com os pacotes, por favor esteja ciente de que você mesmo terá que fazer downgrade deste pacote também.

```
# pacman -U /var/cache/pacman/pkg/*pacote*-*versão_antiga*.pkg.tar.xz

```

Uma vez o pacote seja revertido, adicione-o temporariamente para a [seção IgnorePkg](/index.php/Pacman_(Portugu%C3%AAs)#Pular_pacotes_para_n.C3.A3o_serem_atualizados "Pacman (Português)") do `pacman.conf`, até a dificuldade com o pacote atualizado ser resolvida.

### Fazendo downgrade do kernel

Se você não consegue iniciar o sistema após uma atualização do kernel, então você pode fazer o downgrade do kernel usando um CD *live*. Use uma mídia de instalação do Arch Linux razoavelmente recente. Uma vez que ela tenha iniciado, monte a partição na qual seu sistema está instalado para `/mnt` e se você tiver `/boot` ou `/var` em partições separadas, monte-as lá também (p.ex. `mount /dev/sdc3 /mnt/boot`). Então, faça um [chroot](/index.php/Chroot "Chroot") no sistema:

```
# arch-chroot /mnt /bin/bash

```

Aqui você pode ir em `/var/cache/pacman/pkg` e fazer o downgrade dos pacotes. Faça o downgrade de pelo menos [linux](https://www.archlinux.org/packages/?name=linux), [linux-headers](https://www.archlinux.org/packages/?name=linux-headers) e de quaisquer módulos. Por exemplo:

```
# pacman -U linux-3.5.6-1-x86_64.pkg.tar.xz linux-headers-3.5.6-1-x86_64.pkg.tar.xz virtualbox-host-modules-4.2.0-5-x86_64.pkg.tar.xz

```

Saia do chroot (com `exit`), reinicie e agora deve funcionar.

### Arch Linux Archive

O [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive") é um *snapshot* diário dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais").

O *ALA* pode ser usado para instalar uma versão anterior de um pacote ou restaurar o sistema para uma data anterior.

### Recompilar o pacote

Se o pacote está indisponível, localize o [PKGBUILD](/index.php/PKGBUILD_(Portugu%C3%AAs) "PKGBUILD (Português)") correto e recompile-o com [makepkg](/index.php/Makepkg_(Portugu%C3%AAs) "Makepkg (Português)").

Para pacotes dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"), obtenha o PKGBUILD com [ABS](/index.php/ABS_(Portugu%C3%AAs) "ABS (Português)") e altere a versão do software. Alternativamente, localize o pacote no site de [pacotes](https://www.archlinux.org/packages), clique "View Changes" e navegue na versão desejada. Os arquivos estão disponíveis por meio de uma *snapshot* de `.tar.gz` e via uma visão de "árvore".

veja também [Arch Build System (Português)#Faça checkout de uma versão anterior de um pacote](/index.php/Arch_Build_System_(Portugu%C3%AAs)#Fa.C3.A7a_checkout_de_uma_vers.C3.A3o_anterior_de_um_pacote "Arch Build System (Português)").

Pacotes antigos do AUR podem ser compilados fazendo checkout de um commit antigo no repositório Git do pacote do AUR. Para PKGBUILDs do AUR pré-2015, veja [Arch User Repository (Português)#Repositórios Git para pacotes AUR3](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Reposit.C3.B3rios_Git_para_pacotes_AUR3 "Arch User Repository (Português)").

### Automação

[downgrader](https://aur.archlinux.org/packages/downgrader/) é uma ferramenta que funciona com libalpm, oferece suporte ao log do pacman e a fazer downgrade de pacotes usando o [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive"), cache local e [ARM](http://repo-arm.archlinuxcn.org).

O pacote [downgrade](https://aur.archlinux.org/packages/downgrade/) é um script Bash para faer downgrade de um (ou múltiplos) pacotes, usando o cache do pacman ou o [Arch Rollback Machine](/index.php/Arch_Rollback_Machine "Arch Rollback Machine"). Veja `man downgrade` para detalhes.

[agetpkg-git](https://aur.archlinux.org/packages/agetpkg-git/) lista/obtém/instala rapidamente pacotes do [Arch Linux Archive](/index.php/Arch_Linux_Archive "Arch Linux Archive").

## Retornar do [testing]

See [Official repositories#Disabling testing repositories](/index.php/Official_repositories#Disabling_testing_repositories "Official repositories").