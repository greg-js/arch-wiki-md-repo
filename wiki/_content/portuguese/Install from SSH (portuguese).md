Este artigo possui o intuito de mostrar aos usuários como instalar o Arch através de uma conexão [SSH](/index.php/SSH "SSH"). Considere esta forma de instalação a padrão nos seguintes cenários:

*   Home Theater Personal Computer (HTPC) sem um monitor conectado (p. ex., um SDTV)
*   Um PC localizado em outra cidade, estado, país (casa do amigo, de um parente, etc.)
*   Um PC que pode ser tranquilamente instalado remoto, para que você possa desfrutar do conforto de sua estação de trabalho com capacidades de copiar/colar coisas da Wiki do Arch.

## Na máquina remota (destino)

**Nota:** Esses passos exigem acesso físico à máquina. Obviamente, se estiver localizado fisicamente em outro lugar, isso precisará ser coordenado com outra pessoa.

Inicie a máquina destino em um ambiente Arch *live* por meio de uma [imagem Live CD/USB](/index.php/Category:Getting_and_installing_Arch_(Portugu%C3%AAs) "Category:Getting and installing Arch (Português)"): isso vai autenticar o usuário como root.

Neste ponto, configure a rede na máquina destino como, por exemplo, sugerido no [Guia de instalação#Conectar à Internet](/index.php/Guia_de_instala%C3%A7%C3%A3o#Conectar_.C3.A0_Internet "Guia de instalação").

Em seguida, configure uma senha de root que é necessária para uma conexão SSH, já que a senha padrão do Arch para root é vazia:

```
# passwd

```

Agora, certifique-se que `PermitRootLogin yes` está presente (e descomentado) no `/etc/ssh/sshd_config`. Essa configuração vai permitir o login como root com autenticação com senha no servidor SSH.

**Nota:** Se o computador destino está atrás de algum roteador NAT, a porta SSH (22, por padrão) deverá ser obviamente encaminhada para o endereço IP de LAN da máquina em questão. O uso de encaminhamento de porta não está no escopo deste guia.

Finalmente, [inicie](/index.php/Inicie "Inicie") o daemon openssh com `sshd.service`, que está incluído por padrão no *live CD*.

**Nota:** Após a instalação, é recomendado melhorar a segurança do SSH. O primeiro passo seria remover `PermitRootLogin yes` do `/etc/ssh/sshd_config`.

## Na máquina local

Na máquina local, conecte à máquina destino via SSH com o seguinte comando:

```
$ ssh root@*endereço.ip.do.destino*

```

A partir daqui, uma mensagem de boas-vindas do ambiente *live* será apresentada, e será possível administrar a máquina como se estivesse sentado em frente ao teclado físico. Neste ponto, se a intenção apenas instalar o Arch da mídia *live*, siga o guia em [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Se a intenção é editar uma instalação Linux existente que está com problemas, siga o artigo wiki [Instalar a partir de um Linux existente](/index.php/Instalar_a_partir_de_um_Linux_existente "Instalar a partir de um Linux existente").

**Dica:** Considere instalar um [multiplexador de terminal](/index.php/List_of_applications#Terminal_multiplexers "List of applications") no sistema live (em memória) da máquina destino, de forma que se você for desconectado, você pode reconectar à sessão do seu multiplexador.