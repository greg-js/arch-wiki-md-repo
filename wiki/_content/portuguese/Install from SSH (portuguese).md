**Status de tradução:** Esse artigo é uma tradução de [Install from SSH](/index.php/Install_from_SSH "Install from SSH"). Data da última tradução: 2019-06-28\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Install_from_SSH&diff=0&oldid=575492) na versão em inglês.

Este artigo possui o intuito de mostrar aos usuários como instalar o Arch através de uma conexão [SSH](/index.php/SSH_(Portugu%C3%AAs) "SSH (Português)"). Considere esta abordagem quando o host está em local remoto ou você quiser usar capacidade de copiar/colar de um cliente SSH para fazer a instalação do Arch.

## Na máquina remota (destino)

**Nota:** Esses passos exigem acesso físico à máquina. Se o host estiver localizado fisicamente em outro lugar, isso pode ser coordenado com outra pessoa.

Inicie a máquina destino em um ambiente Arch *live* por meio de uma [imagem CD/USB Live](/index.php/Obtendo_e_instalando_o_Arch "Obtendo e instalando o Arch"): isso vai autenticar o usuário como root.

Neste ponto, configure a rede na máquina destino como, por exemplo, sugerido no [Guia de instalação#Conectar à internet](/index.php/Guia_de_instala%C3%A7%C3%A3o#Conectar_à_internet "Guia de instalação").

Em seguida, configure uma senha de root que é necessária para uma conexão SSH, já que a senha padrão do Arch para root é vazia:

```
# passwd

```

Agora, certifique-se que `PermitRootLogin yes` está presente (e descomentado) no `/etc/ssh/sshd_config`. Essa configuração vai permitir o login como root com autenticação com senha no servidor SSH.

Finalmente, [inicie](/index.php/Inicie "Inicie") o daemon openssh com `sshd.service`, que está incluído por padrão no *live CD*.

**Nota:** A menos que precise, após a instalação é recomendado remover `PermitRootLogin yes` do `/etc/ssh/sshd_config`.

**Dica:** Se o computador destino está atrás de algum roteador NAT, e você precisar de acesso externo, a porta SSH (22, por padrão) deverá ser encaminhada para o endereço IP de LAN da máquina destino.

## Na máquina local

Na máquina local, conecte à máquina destino via SSH com o seguinte comando:

```
$ ssh root@*endereço.ip.do.destino*

```

A partir daqui, uma mensagem de boas-vindas do ambiente *live* será apresentada, e será possível administrar a máquina como se estivesse sentado em frente ao teclado físico. Neste ponto, se a intenção apenas instalar o Arch da mídia *live*, siga o guia em [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Se a intenção é editar uma instalação Linux existente que está com problemas, siga o artigo wiki [Instalar a partir de um Linux existente](/index.php/Instalar_a_partir_de_um_Linux_existente "Instalar a partir de um Linux existente").

**Dica:** Considere instalar um [multiplexador de terminal](/index.php/List_of_applications#Terminal_multiplexers "List of applications") no sistema live (em memória) da máquina destino, de forma que se você for desconectado, você pode reconectar à sessão do seu multiplexador.