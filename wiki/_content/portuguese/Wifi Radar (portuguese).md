Artigos relacionados

*   [Configuração de rede sem fio](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio "Configuração de rede sem fio")

[WiFi Radar](https://wifi-radar.tuxfamily.org/) é um pequeno programa GUI que permite alternar redes sem fio com facilidade.

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [wifi-radar](https://www.archlinux.org/packages/?name=wifi-radar).

## Configuração

A [documentação](https://wifi-radar.tuxfamily.org/support/user-manual.html) do projeto dá uma boa visão geral para a interface de usuário.

*wifi-radar* deve ser executado com privilégios administrativos. Edite `/etc/sudoers` usando o comando *visudo* e adicione:

```
*seuusuário*     ALL=(ALL) NOPASSWD: /usr/sbin/wifi-radar

```

Então, execute *wifi-radar* a partir do menu de aplicativo para visualizar as redes disponíveis ou para configurar sua instalação.

Para opções do arquivo de configuração, veja o [manual](https://wifi-radar.tuxfamily.org/support/user-manual.html) do projeto.

**Dica:**

*   Você pode editar `/etc/conf.d/wifi-radar` para definir uma interface de rede em particular que você deseje usar.
*   Alguns usuários tiveram que definir `ifup required` com `ON` para que o WiFi Radar funcionasse adequadamente.