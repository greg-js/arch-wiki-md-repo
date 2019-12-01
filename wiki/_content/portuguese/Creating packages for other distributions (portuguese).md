**Status de tradução:** Esse artigo é uma tradução de [Creating packages for other distributions](/index.php/Creating_packages_for_other_distributions "Creating packages for other distributions"). Data da última tradução: 2019-08-10\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Creating_packages_for_other_distributions&diff=0&oldid=577806) na versão em inglês.

Artigos relacionados

*   [Criando pacotes](/index.php/Criando_pacotes "Criando pacotes")

[Arch é o melhor](/index.php/Arch_is_the_best "Arch is the best"). Mas você ainda pode querer empacotar para outras distribuições.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Geral](#Geral)
*   [2 Debian](#Debian)
    *   [2.1 Dicas e truques sobre o Debian](#Dicas_e_truques_sobre_o_Debian)
        *   [2.1.1 Sobrescrever tratamento de dependências](#Sobrescrever_tratamento_de_dependências)
        *   [2.1.2 Configurar um chroot](#Configurar_um_chroot)
    *   [2.2 Veja também sobre o Debian](#Veja_também_sobre_o_Debian)
*   [3 Fedora](#Fedora)
    *   [3.1 Veja também sobre o Fedora](#Veja_também_sobre_o_Fedora)
*   [4 openSUSE](#openSUSE)
    *   [4.1 Criando pacotes do Arch no OBS com OSC](#Criando_pacotes_do_Arch_no_OBS_com_OSC)
        *   [4.1.1 Criando um pacote](#Criando_um_pacote)
        *   [4.1.2 Gerenciando um pacote](#Gerenciando_um_pacote)
        *   [4.1.3 Dicas e truques sobre o openSUSE](#Dicas_e_truques_sobre_o_openSUSE)
        *   [4.1.4 Programa com o pacote ca-certificates-utils](#Programa_com_o_pacote_ca-certificates-utils)
        *   [4.1.5 Veja também sobre o openSUSE](#Veja_também_sobre_o_openSUSE)
*   [5 Veja também](#Veja_também)

## Geral

*   [Virtualização](/index.php/Virtualiza%C3%A7%C3%A3o "Virtualização") é uma forma óbvia, mas requer manutenção de sistema(s) adicional(is).
*   Use ferramentas de empacotamento específica de distribuição. Exemplos: [dh-make](https://aur.archlinux.org/packages/dh-make/), [dpkg](https://www.archlinux.org/packages/?name=dpkg) (Debian), [rpm-org](https://aur.archlinux.org/packages/rpm-org/) (Fedora). Atalhos como [dpkg-deb](http://tldp.org/HOWTO/html_single/Debian-Binary-Package-Building-HOWTO/) ou [checkinstall](https://aur.archlinux.org/packages/checkinstall/) pode ser adequado para tarefas menos complexas.
*   [Chroot](/index.php/Chroot_(Portugu%C3%AAs) "Chroot (Português)") para criar um sistema base dentro (apesar de separada do) Arch. Por exemplo: [debootstrap](https://www.archlinux.org/packages/?name=debootstrap) (Debian), [dnf](https://aur.archlinux.org/packages/dnf/) (Fedora). Isso foi adicionado para beneficiar a construção em um ambiente mínimo e limpo.
*   Use chroot com ferramentas de empacotamento de uma forma automatizada. Exemplos: [pbuilder-ubuntu](https://aur.archlinux.org/packages/pbuilder-ubuntu/) (Debian), [mock-git](https://aur.archlinux.org/packages/mock-git/) (Fedora).
*   Uma forma diferente de lidar (possivelmente incompatível) com dependências é com [vínculo estático](http://jurjenbokma.com/ApprenticesNotes/getting_statlinked_binaries_on_debian.xhtml). Por favor, note que a maioria das distribuições não gostam dessa prática.
*   A prática comum se aplica independentemente da distribuição usada. Por exemplo, [não compilar pacotes como root](https://bbs.archlinux.org/viewtopic.php?id=67561).

## Debian

[Debian Packaging Tutorial](https://www.debian.org/doc/manuals/packaging-tutorial/packaging-tutorial.pdf) explica as bases, descrevendo o uso das seguintes ferramentas:

*   **cowdancer** — Interface de cópia e escrita para o pbuilder

	[https://packages.debian.org/sid/cowdancer](https://packages.debian.org/sid/cowdancer) || [cowdancer](https://aur.archlinux.org/packages/cowdancer/)

*   **debootstrap** — Uma ferramenta usada para criar um sistema base Debian do zero, sem exibir a disponibilidade de dpkg ou apt.

	[https://packages.debian.org/sid/debootstrap](https://packages.debian.org/sid/debootstrap) || [debootstrap](https://www.archlinux.org/packages/?name=debootstrap)

*   **devscripts** — Scripts para facilitara vida de um mantenedor de pacote do Debian

	[https://packages.debian.org/sid/devscripts](https://packages.debian.org/sid/devscripts) || [devscripts](https://aur.archlinux.org/packages/devscripts/)

*   **dh-autoreconf** — Complemento ao Debhelper para chamar autoreconf e limpar após a compilação

	[https://packages.debian.org/sid/dh-autoreconf](https://packages.debian.org/sid/dh-autoreconf) || [dh-autoreconf](https://aur.archlinux.org/packages/dh-autoreconf/)

*   **dh-make** — Ferramenta que converte os arquivos fonte em fonte de pacote do Debian

	[https://packages.debian.org/sid/dh-make](https://packages.debian.org/sid/dh-make) || [dh-make](https://aur.archlinux.org/packages/dh-make/)

*   **[dpkg](https://en.wikipedia.org/wiki/pt:dpkg "wikipedia:pt:dpkg")** — O gerenciador de pacotes do Debian

	[https://packages.debian.org/sid/dpkg](https://packages.debian.org/sid/dpkg) || [dpkg](https://www.archlinux.org/packages/?name=dpkg)

*   **dput** — Ferramenta de envio de pacotes do Debian

	[https://packages.debian.org/sid/dput](https://packages.debian.org/sid/dput) || [dput](https://aur.archlinux.org/packages/dput/)

*   **equivs** — Contorne dependências de pacotes do Debian

	[https://launchpad.net/ubuntu/+source/equivs](https://launchpad.net/ubuntu/+source/equivs) || [equivs](https://aur.archlinux.org/packages/equivs/)

*   **git-buildpackage** — Ferramentas do Debian para integrar o sistema de compilação de pacotes com Git

	[https://honk.sigxcpu.org/piki/projects/git-buildpackage/](https://honk.sigxcpu.org/piki/projects/git-buildpackage/) || [git-buildpackage](https://aur.archlinux.org/packages/git-buildpackage/)

*   **pbuilder-ubuntu** — Ambiente de chroot para compilação de pacotes do Debian

	[https://launchpad.net/ubuntu/+source/pbuilder](https://launchpad.net/ubuntu/+source/pbuilder) || [pbuilder-ubuntu](https://aur.archlinux.org/packages/pbuilder-ubuntu/)

*   **[quilt](https://en.wikipedia.org/wiki/Quilt_(software) "wikipedia:Quilt (software)")** — Gerencia uma série de patches mantendo rastro de alterações que cada patch faz

	[http://savannah.nongnu.org/projects/quilt](http://savannah.nongnu.org/projects/quilt) || [quilt](https://www.archlinux.org/packages/?name=quilt)

### Dicas e truques sobre o Debian

#### Sobrescrever tratamento de dependências

O *dpkg* não reconhece as dependências instaladas pelo [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)"). Isso significa que `dpkg-buildpackage` geralmente falhará com erros como:

```
dpkg-checkbuilddeps: Unmet build dependencies: build-essential:native debhelper (>= 8.0.0)
dpkg-buildpackage: warning: build dependencies/conflicts unsatisfied; aborting

```

Para contornar isso, use a opção `-d`:

```
$ dpkg-buildpackage -d -us -uc

```

Você também pode precisar sobrescrever `dh_shlibdeps` adicionando as seguintes linhas ao `debian/rules`:

```
override_dh_shlibdeps:
   dh_shlibdeps --dpkg-shlibdeps-params=--ignore-missing-info

```

**Nota:** Quaisquer dependências de tempo de execução (e números de versão correspondentes) devem ser adicionadas manualmente ao `debian/control`, onde `${shlibs:Depends}` agora não tem significado.

**Atenção:** Mesmo *se* você conseguir compilar um pacote com sucesso desta forma, é **fortemente recomendado** construir em um ambiente limpo (como o chroot) para prevenir qualquer incompatibilidade.

#### Configurar um chroot

Veja o [How-To do Pbuilder](https://wiki.ubuntu.com/PbuilderHowto) para uma introdução ao *pbuilder-ubuntu*. O uso de *cowdancer*, além disso, é recomendado, pois [cópia em gravação](https://en.wikipedia.org/wiki/pt:C%C3%B3pia_em_grava%C3%A7%C3%A3o "wikipedia:pt:Cópia em gravação") oferece um benefício de desempenho significativo.

*   [debian-archive-keyring](https://www.archlinux.org/packages/?name=debian-archive-keyring), [ubuntu-keyring](https://www.archlinux.org/packages/?name=ubuntu-keyring) e [gnupg1](https://aur.archlinux.org/packages/gnupg1/) do [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") são necessários.
*   *eatmydata* está disponível como [libeatmydata](https://www.archlinux.org/packages/?name=libeatmydata) e [lib32-libeatmydata](https://aur.archlinux.org/packages/lib32-libeatmydata/) no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)"). Para evitar erros de `LD_PRELOAD`, deve ser instalado dentro e fora do chroot. Como os caminhos são diferentes no Arch e Debian, crie os links simbólicos a seguir:

```
# ln -s /usr/lib/libeatmydata.so.1.1.1 /usr/lib/libeatmydata/libeatmydata.so
# ln -s /usr/lib/libeatmydata.so.1.1.1 /usr/lib/libeatmydata/libeatmydata.so.1

```

*   [Exemplo de pbuilderrc](https://gist.githubusercontent.com/AladW/71352540eca7de2197c7/raw/c28f6d96c0beb116f99e1ff0bd16599c356855ed/gistfile1.sh)
*   Para criar um pacote fonte para o pbuilder lidar:

```
$ dpkg-buildpackage -d -us -uc -S

```

### Veja também sobre o Debian

*   [Política do Debian](https://www.debian.org/doc/debian-policy/)
*   [Novo Guia do Mantenedor](https://www.debian.org/doc/manuals/maint-guide/)
*   [Quilt no empacotamento do Debian](http://raphaelhertzog.com/2012/08/08/how-to-use-quilt-to-manage-patches-in-debian-packages/)

## Fedora

[Como criar um pacote RPM](https://fedoraproject.org/wiki/How_to_create_an_RPM_package)

*   **rpm-org** — Fork do RPM.org, usado na maioria das distros RPM

	[http://www.rpm.org/](http://www.rpm.org/) || [rpm-org](https://aur.archlinux.org/packages/rpm-org/)

*   **mock** — Pega RPMs fonte e compila RPMs a partir deles em um chroot

	[https://github.com/rpm-software-management/mock/wiki](https://github.com/rpm-software-management/mock/wiki) || [mock](https://aur.archlinux.org/packages/mock/)

### Veja também sobre o Fedora

*   [Copr](https://copr.fedoraproject.org/)

## openSUSE

O [Open Build Service (OBS)](http://openbuildservice.org/) é um sistema genérico para criar e distribuir pacotes de fontes de uma maneira automática, consistente e reproduzível. Suporta pelo menos pacotes .deb, .rpm e Arch.

### Criando pacotes do Arch no OBS com OSC

**Nota:** Para criar, você deve enviar o arquivo PKGBUILD, bem como dos arquivos de origem (carregando ou permitindo que o OBS baixe os arquivos). O OBS usa máquinas virtuais sem suporte de rede e não pode baixar nenhum arquivo.

#### Criando um pacote

1.  Crie uma conta no [[1]](https://build.opensuse.org/)
2.  [Instale](/index.php/Instale "Instale") o pacote [osc](https://aur.archlinux.org/packages/osc/). A documentação upstream está disponível [aqui](http://en.opensuse.org/openSUSE:OSC).
3.  Crie um projeto exemplo `home:foo`.
4.  Crie um subprojeto exemplo `home:foo:bar` (opcional, mas recomendável).
5.  Crie um novo pacote exemplo `ham` com `osc meta pkg -e home:foo:bar ham`. Salve o XML criado e, então, sai.
6.  Mude para um diretório de trabalho limpe e, então, façacheckout do projeto que você acabou de criar: `osc co home:foo:bar/ham`.
7.  Agora, use *cd* para ir entrar nele: `cd home:foo:bar/ham`.

#### Gerenciando um pacote

Agora é hora de decidir como administraremos nosso projeto. Existem duas maneiras práticas de fazer isso:

1.  Manter um PKGBUILD mais seus arquivos auxiliares (como scripts *.install) em um sistema de controle de versão (como git, hg) e faça o OBS rastreá-lo;
2.  Manter um pacote inteiramente no próprio OBS.

A primeira versão é mais flexível e dinâmica. Para prosseguir:

*   A partir do diretório do seu projeto, crie um arquivo `_service` com o seguinte conteúdo:

```
<services>
  <service name="tar_scm">
    <param name="scm">git</param>
    <param name="url">git://<seu_repo_aqui></param>
    <param name="versionformat">git%cd~%h</param>
    <param name="versionprefix"><sua_versão_aqui></param>
    <param name="filename"><nome_do_seu_pacote></param>
  </service>
  <service name="recompress">
    <param name="file">*.tar</param>
    <param name="compression">xz</param>
  </service>
  <service name="set_version"/>
</services>
```

Aqui está um exemplo para [gimp-git](https://aur.archlinux.org/packages/gimp-git/):

```
<services>
  <service name="tar_scm">
    <param name="scm">git</param>
    <param name="url">git://git.gnome.org/gimp.git</param>
    <param name="versionformat">git%cd~%h</param>
    <param name="versionprefix">2.9.1</param>
    <param name="filename">gimp-git</param>
  </service>
  <service name="recompress">
    <param name="file">*.tar</param>
    <param name="compression">xz</param>
  </service>
  <service name="set_version"/>
</services>
```

*   Faça o OBS rastreá-lo: `osc add _service`
*   Se você tiver outros arquivos para incluir no repositório, apenas continue como antes: adicione os arquivos no diretório do projeto e faça a OBS rastreá-los (o OBS usa o subversion como seu SCM subjacente, portanto, esse processo pode já ser familiar para você)
*   Faça check-in (=upload) seus arquivos no repo `osc ci -m "mensagem de commit (p.ex., atualiza pacote xxx para versão yyy"`.

Agora, após um tempo, OBS vai começar a compilar seu pacote.

#### Dicas e truques sobre o openSUSE

*   Para ver o progresso da compilação do seu pacote, faça *cd* para seu diretório de trabalho, então: `osc results`.
*   Há três repositórios, Arch:Core, Arch:Extra e Arch:Community. [community] pode ser anexado como um "caminho de repositório" após adicionar o repositório principal do Arch ao projeto.

#### Programa com o pacote ca-certificates-utils

Se a criação do OBS falhar por causa do pacote ca-certificates-utils, você poderá adicionar essa linha à configuração do seu projeto (na página do projeto, vá para Advanced -> Project Config).

```
Prefer: ca-certificates-utils ca-certificates

```

#### Veja também sobre o openSUSE

*   Repo exemplo: [arch-deepin](https://build.opensuse.org/project/show/home:metakcahura:arch-deepin)
*   [Diretrizes de empacotamentos do openSUSE](http://en.opensuse.org/openSUSE:Packaging_guidelines)
*   [Portal:Packaging do wiki do openSUSE](http://en.opensuse.org/Portal:Packaging)

## Veja também

*   [BBS - PKGBUILD equivalentes para outras distros](https://bbs.archlinux.org/viewtopic.php?id=175409)
*   [BBS - Discussão original](https://bbs.archlinux.org/viewtopic.php?id=182198)