## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
*   [3 Configuração](#Configura.C3.A7.C3.A3o)
*   [4 Carregando módulos](#Carregando_m.C3.B3dulos)
    *   [4.1 Módulos de terceiros](#M.C3.B3dulos_de_terceiros)
*   [5 Iniciando/parando o daemon](#Iniciando.2Fparando_o_daemon)
*   [6 Links externos](#Links_externos)

## Introdução

O **InspIRCd** (Inspire IRC daemon) é um servidor de IRC leve e modular escrito em C++. Como é um dos poucos projectos escritos do zero evita cair num número de falhas de arquitectura e design que perseguem outros servidores mais antigos e derivados destes como o UnrealIRCd 3\. O InspIRCd é o servidor de IRC usado no conhecido [Chatspike IRC network](http://www.chatspike.net/).

## Instalação

**Nota:** Antes de começar, certifique-se de que você não tem um usuário ou grupo com nome `inspircd`, pois o pacote vai criar e executar usando os privilégios deste usuário (por motivos de segurança).

[Instale](/index.php/Instale "Instale") o pacote [inspircd](https://aur.archlinux.org/packages/inspircd/).

## Configuração

O arquivo de configuração `/etc/inspircd/inspircd.conf` é **obrigatório**, formatado em HTML e precisa ser criado na instalação.

Como você define seu arquivo de configuração dependerá muito das suas necessidades e configuração do sistema, motivo pelo qual não há nenhum arquivo de configuração definido por padrão.

**Dica:** Você pode usar o exemplo de arquivo de configuração (muito bem documentado) localizado em `/usr/share/inspircd/examples/inspircd.conf.example`. Copie este arquivo para `/etc/inspircd/inspircd.conf`, leia-o e edite-o cuidadosamente para atender às suas necessidades.

Seu formato HTML pode ser um pouco diferente do que a maioria das pessoas está acostumada. O formato de uma instrução dentro do arquivo de configuração se parece com o seguinte:

```
<nometag variable = "valor">

```

**Nota:** O arquivo de exemplo tem algumas linhas `<die value="qualquer coisa aqui>` no arquivo exemplo para garantir que você leia a coisa toda. Você deve remover essas entradas, caso contrário o servidor não iniciará.

Certifique-se de configurar o arquivo pid para `/var/lib/inspircd/inspircd.pid`, conforme explicado no pacote [script de instalação](https://aur.archlinux.org/cgit/aur.git/tree/inspircd.install?h=inspircd).

Mais informações estão disponíveis na página wiki de [configuração do InspIRCd](http://wiki.inspircd.org/Configuration).

## Carregando módulos

Por pré-definição, o InspIRCd não carrega nenhum módulo. Como todas as funcionalidades fora da [RFC 1459](http://tools.ietf.org/html/rfc1459) são consideradas como um módulo, sem carregar nenhum módulo o seu servidor não vai fazer nada que impressione.

Pode carregar módulos adicionado por exemplo:

```
<module name="m_silence.so">

```

Isto vai carregar o módulo m_silence (que disponibiliza a quase especificação padrão SILENCE). Tem de reiniciar o daemon para que as alterações façam efeito. Uma lista dos módulos disponíveis está disponível na página wiki de [módulos do InspIRCd](http://wiki.inspircd.org/modules).

### Módulos de terceiros

Para instalar um módulo de terceiros, salve o `[módulo].cpp` dentro de `[dir-compilação]/inspircd/src/inspircd/src/modules/` e continue o processo de compilação. Se você já compilou e instalou o InspIRCd e ter os arquivos fonte intactos, compile o módulo com `./configure -modupdate; make` e copie-o para: `/usr/lib/inspircd/modules/`.

## Iniciando/parando o daemon

Pode iniciar e parar o InspIRCd como habitual, executando:

```
sudo /etc/rc.d/inspircd {start|stop|restart}

```

A primeira inicialização algumas vezes falha, então tente reiniciar até você não ter mais erros. Depois disto você deve não ter quaisquer problemas. A razão por de trás disto é que por uma questão de segurança o daemon não executa como *root* como normalmente acontece, portanto o script tem de assegurar-se que o usuário **irc** tem permissões para ler e escrever os arquivos pid e log. Para iniciar no boot adicione (como sempre) [inspircd] à lista de [daemons] no arquivo **/etc/rc.conf**.

## Links externos

*   [Inspire IRCd (site)](http://www.inspircd.org)
*   [Inspire IRCd (wiki)](http://wiki.inspircd.org/Main_Page)
*   [Inspire IRCd (canal irc)](irc://irc.inspircd.org/inspircd)