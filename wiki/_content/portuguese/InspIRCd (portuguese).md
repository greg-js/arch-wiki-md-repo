## Contents

*   [1 Introdução](#Introdu.C3.A7.C3.A3o)
*   [2 Instalando o InspIRCd](#Instalando_o_InspIRCd)
*   [3 Configurando (mandatório)](#Configurando_.28mandat.C3.B3rio.29)
*   [4 Carregando módulos](#Carregando_m.C3.B3dulos)
*   [5 Iniciando/parando o daemon](#Iniciando.2Fparando_o_daemon)
*   [6 Links externos](#Links_externos)

## Introdução

O **InspIRCd** (Inspire IRC daemon) é um servidor de IRC leve e modular escrito em C++. Como é um dos poucos projectos escritos do zero evita cair num número de falhas de arquitectura e design que perseguem outros servidores mais antigos e derivados destes como o UnrealIRCd 3\. O InspIRCd é o servidor de IRC usado no conhecido [Chatspike IRC network](http://www.chatspike.net/).

## Instalando o InspIRCd

Antes de começar assegure-se que faz o seguinte:

1.  Verifique que não tem nenhum utilizador ou grupo chamado "irc" pois o daemon vai criar e correr usando os privilégios deste utilizador (por questões de segurança).
2.  Leia como compilar pacotes do [AUR](/index.php/AUR "AUR") (veja [ABS](/index.php/ABS "ABS")) ou instale o [yaourt](/index.php/Yaourt "Yaourt") (**recomendado**) que automatiza todo o processo.

Agora que já instalou o [yaourt](/index.php/Yaourt "Yaourt") pode instalar o [InspIRCd](/index.php/InspIRCd "InspIRCd") correndo o seguinte comando:

```
yaourt inspircd

```

## Configurando (mandatório)

Isto vai depender muito das suas necessidades e da configuração do sistema e portanto não há uma configuração predefinida. Há, no entanto, um ficheiro de configuração exemplo (muito bem documentado) localizado (como sempre) em **/etc/inspircd/inspircd.conf.example**. Leia e edite este ficheiro cuidadosamente e quando terminar mude o nome do ficheiro para **inspircd.conf**. O ficheiro inspircd.conf está formatado como um documento html, o que para a maioria das pessoas é de certa forma diferente do que estão habituadas. O formato de uma instrução dentro do ficheiro de configuração é semelhante ao seguinte:

```
 <nometag variavel="valor">

```

Note que existem alguns **<die value="qualquer coisa aqui">** no ficheiro de exemplo para assegurar que todo o ficheiro é lido. Tem de remover estas entradas caso constrário o servidor não vai iniciar. Mais informações estão disponíveis na página [InspIRCd configuration](http://wiki.inspircd.org/Configuration) da wiki.

## Carregando módulos

Por pré-definição, o InspIRCd não carrega nenhum módulo. Como todas as funcionalidades fora da[RFC 1459](http://tools.ietf.org/html/rfc1459) são encaradas como um módulo, sem carregar nenhum módulo o seu servidor não vai fazer nada que impressione. Pode carregar módulos adicionado por exemplo:

```
<module name="m_silence.so">

```

Isto vai carregar o módulo m_silence (que disponibiliza a quase standard especificação SILENCE). Tem de reiniciar o daemon para que as alterações façam efeito. Uma lista dos módulos disponíveis está disponível na página wiki [InspIRCd modules](http://wiki.inspircd.org/modules).

## Iniciando/parando o daemon

Pode iniciar e parar o InspIRCd como habitual, correndo:

```
sudo /etc/rc.d/inspircd {start|stop|restart}

```

A primeira inicialização pode falhar. Se tal acontecer tente reiniciar até que não obtenha nenhum erro. Depois disto não terá quaisquer problemas. A razão por de trás disto é que por uma questão de segurança o daemon não corre como root como normalmente acontece, portanto o script tem de assegurar-se que o utilizador **irc** tem permissões para ler e escrever os ficheiros pid e log. Para iniciar no boot adicione (como sempre) [inspircd] à lista de [daemons] no ficheiro **/etc/rc.conf file**.

## Links externos

*   [Inspire IRCd (website)](http://www.inspircd.org)
*   [Inspire IRCd (wiki)](http://wiki.inspircd.org/Main_Page)
*   [Inspire IRCd (canal de irc)](irc://irc.inspircd.org/inspircd)