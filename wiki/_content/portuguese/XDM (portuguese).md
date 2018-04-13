Artigos relacionados

*   [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição")

Da Página do [Manual do XDM](http://www.xfree86.org/current/xdm.1.html):

	*Xdm gerencia uma coleção de telas do X, que podem estar na máquina local ou em servidores remotos. O projeto do xdm foi orientada pelas necessidades dos terminais X, assim como o padrão Open Group XDMCP, o Protocolo de Controle do Gerenciador de Tela X. Xdm fornece serviços similares aos fornecidos pelo init getty e login em terminais de caracteres: solicitando o nome de login e senha, autenticando o usuário, e executando uma "sessão"*

XDM fornece um simples e direto solicitador de login gráfico.

## Instalação

Instale o XDM:

```
# pacman -S xorg-xdm xorg-xconsole

```

Deixe o .xsession executável:

```
$ chmod 744 .xsession

```

Opciconalmente, instale o tema do Arch Linux para o XDM:

```
# pacman -S xdm-archlinux

```

Veja [Gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") para informações adicionais.