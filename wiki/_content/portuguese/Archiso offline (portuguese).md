**Status de tradução:** Esse artigo é uma tradução de [Archiso offline](/index.php/Archiso_offline "Archiso offline"). Data da última tradução: 2018-11-11\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Archiso_offline&diff=0&oldid=554772) na versão em inglês.

Artigos relacionados

*   [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)")

**Archiso Offline** é um complemento ao tradicional pacote [archiso](https://www.archlinux.org/packages/?name=archiso). Permitir que os usuários criem uma ISO de instalação offline com base no ISO oficial. Assim como a maioria das distribuições Linux tem como opção padrão, os usuários do Arch podem criar compilações ISO semelhantes com este pacote.

Um recurso adicional do Archiso Offline é que os pacotes AUR podem ser incluídos no processo de criação ISO.

## Contents

*   [1 Configuração](#Configuração)
    *   [1.1 Instalando pacotes](#Instalando_pacotes)
*   [2 Compilar a ISO](#Compilar_a_ISO)
    *   [2.1 Exemplo de processo de compilação](#Exemplo_de_processo_de_compilação)
*   [3 Veja também](#Veja_também)
    *   [3.1 Documentação e tutoriais](#Documentação_e_tutoriais)
    *   [3.2 Exemplo de script de compilação](#Exemplo_de_script_de_compilação)
    *   [3.3 Deficiências conhecidas](#Deficiências_conhecidas)

## Configuração

[Instale](/index.php/Instale "Instale") [archiso-offline-releng](https://aur.archlinux.org/packages/archiso-offline-releng/). Isso também vai instalar [archiso](https://www.archlinux.org/packages/?name=archiso) *(ou usar [archiso-git](https://aur.archlinux.org/packages/archiso-git/), se instalado)*.

Os passos de configuração depois de instalar este pacote são praticamente idênticos aos do [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)").
No entanto, por padrão, o Archiso vem com dois "perfis": *releng* e *baseline*. O Archiso Offline adiciona um perfil adicional chamado *offline_releng*.

O perfil *offline_releng* substitui todas as etapas dependentes da linha em um [processo de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") normal com pacotes hospedados localmente dentro do ISO. Então, ao invés de tentar buscar pacotes online, os pacotes são obtidos diretamente da ISO.

O processo de compilação permite isso criando o `packages.x86_64` e executando `pacman --noconfirm -w --cachedir ... <pacotes>` e colocando os arquivos em uma estrutura tipo HTTP sob `/srv/http`. Em seguida, apontando o `pacman.conf` do ISO para essa estrutura.
Os pacotes AUR também são originados, mas armazenados em cache de forma um pouco diferente. Mas os pacotes AUR são originados de `packages.aur`.
A lista completa de pacotes originados por padrão é `base-devel` e quaisquer pacotes listados em `packages.x86_64` da configuração oficial *releng*.

Pacotes adicionais podem ser adicionados conforme descrito em [Archiso (Português)#Configurar a mídia live](/index.php/Archiso_(Portugu%C3%AAs)#Configurar_a_mídia_live "Archiso (Português)")

### Instalando pacotes

Siga o mesmo procedimento descrito em [Archiso (Português)#Instalando pacotes](/index.php/Archiso_(Portugu%C3%AAs)#Instalando_pacotes "Archiso (Português)"), a única diferença sendo `packages.aur`, que é um recurso adicional no processo de criação, permitindo a possibilidade de incluir [pacotes AUR](https://aur.archlinux.org) para o meio offline.

**Nota:** Se os pacotes do AUR forem encontrados pelo processo de compilação, um usuário de compilação será criado automaticamente com a permissão `"%wheel ALL=(ALL) NO"` no sudoers. É um problema conhecido e uma solução ruim a longo prazo. Certifique-se de que o arquivo sudoers esteja correto depois de criar sua ISO off-line por enquanto.

## Compilar a ISO

Novamente, supondo que você tenha seguido a documentação do [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)"), mais especificamente as etapas [Archiso (Português)#Compilar a ISO](/index.php/Archiso_(Portugu%C3%AAs)#Compilar_a_ISO "Archiso (Português)"), você deve ter uma ISO em:

```
# ~/archlive/out/

```

### Exemplo de processo de compilação

Exemplo de **passos de instalação**:

```
# mkdir -p /tmp/archiso-offline
# cd /tmp/archiso-offline
# wget [https://aur.archlinux.org/cgit/aur.git/snapshot/archiso-offline-releng.tar.gz](https://aur.archlinux.org/cgit/aur.git/snapshot/archiso-offline-releng.tar.gz)
# tar xvzf archiso-offline-releng
# cd archiso-offline-releng
# makepkg -s
# sudo pacman -U *.xz

```

O **processo de compilação** em si:

```
# mkdir -p /tmp/iso_build_dir
# cp -r /usr/share/archiso/configs/offline_releng/* /tmp/iso_build_dir/
# cd /tmp/iso_build_dir
# echo "python" >> packages.x86_64
# echo "lighttpd2-git" >> packages.aur
# echo "systemctl enable lighttpd2" >> ./airootfs/root/customize_airootfs.sh
# rm -rf work*
# ./build.sh -v
# file out/*.iso

```

E deveria ser isso. Este exemplo instala o [python](https://www.archlinux.org/packages/?name=python) no ambiente ISO ativo, assim como [lighttpd2-git](https://aur.archlinux.org/packages/lighttpd2-git/). Também permite o início automático de **lighttpd2** assim que o ISO for inicializado.

## Veja também

### Documentação e tutoriais

*   [Página do projeto Archiso](https://projects.archlinux.org/archiso.git)
*   [Documentação oficial do Archiso](https://projects.archlinux.org/archiso.git/tree/docs)

### Exemplo de script de compilação

*   [Quatro tipos de scripts de compilação para o Archiso Offline.](https://github.com/Torxed/Scripts/tree/master/bash/build-scripts/isos)

### Deficiências conhecidas

Algumas coisas e problemas são conhecidos neste projeto.
O primeiro é que alguns pacotes podem ser hospedados localmente, mas não instalados localmente no ambiente ISO. Até hoje não há uma boa solução para isso, então todos os pacotes declarados em `packages.{X86_64, aur`} estão ambos instalados - e hospedados no ambiente ISO.

Outro grande problema é o usuário de compilação do AUR. Não há uma maneira clara de resolver isso, mas existem soluções melhores do que a existente hoje. Especialmente o uso de `sudoers`.