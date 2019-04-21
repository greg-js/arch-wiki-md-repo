**Status de tradução:** Esse artigo é uma tradução de [PuTTY](/index.php/PuTTY "PuTTY"). Data da última tradução: 2019-04-16\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=PuTTY&diff=0&oldid=571401) na versão em inglês.

Artigos relacionados

*   [ssh](/index.php/Ssh_(Portugu%C3%AAs) "Ssh (Português)")
*   [telnet](/index.php/Telnet_(Portugu%C3%AAs) "Telnet (Português)")
*   [Proxy settings](/index.php/Proxy_settings "Proxy settings")

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/) é uma *port* do popular cliente de interface gráfica para conexão SSH, Telnet, Rlogin e serial para Windows. Ele tem suporte para opções avançadas de log e termcap, bem como uma aparência muito configurável e a capacidade de encaminhar portas ou criar um túnel SOCKS através de um destino SSH. Para começar, simplesmente execute o PuTTY, digite o nome do host do host ao qual você gostaria de se conectar e pressione Open para abrir.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
*   [3 Importando chaves](#Importando_chaves)
*   [4 Suporte a 256 cores](#Suporte_a_256_cores)

## Instalação

[Instale](/index.php/Instale "Instale") [putty](https://www.archlinux.org/packages/?name=putty).

## Configuração

As configurações podem ser modificadas através das abas à esquerda, no entanto, elas serão redefinidas se não forem salvas. Para salvar suas configurações, digite um nome na caixa, em "Saved Sessions", e clique em "Save". Para carregá-las novamente mais tarde, clique no nome do seu salvamento e clique em "Load". Isso permite que você mantenha de forma persistente suas configurações visuais, termcap e de conexão entre as conexões e também permite que você mantenha um salvamento por host usado regularmente. O salvamento "Default Settings" é automaticamente carregado toda vez que você inicia o PuTTY, então salve sob esse nome com cuidado.

**Dica:** PuTTY ganhou suporte a ECDSA, Ed25519 e outros [tipos de chave SSH](/index.php/SSH_keys "SSH keys") padrão com a versão 0.68 (fevereiro de 2017).[[1]](http://www.chiark.greenend.org.uk/~sgtatham/putty/changes.html) Teste-a e remova eventuais *fallbacks* para tipos de chave legados que você usou.

## Importando chaves

O PuTTY usa seu próprio formato para armazenar as chaves privadas no lado do cliente. Para importar uma chave que você gerou anteriormente, você precisa usar o comando `puttygen`.

```
$ puttygen *arquivo-de-chave* -o *saída-chave-de-chave*.ppk

```

sendo `*arquivo-de-chave*` um arquivo de chave privada existente e `*saída-arquivo-de-chave*.ppk` o arquivo que receberá a chave.

Se o `*arquivo-de-chave*` estiver protegido com uma senha, você será solicitado a inseri-la, mas a chave ainda será protegida posteriormente no `*saída-arquivo-de-chave*.ppk`.

Após isso, você pode importá-la para fazer uma conexão SSH: *Connection > SSH > Auth > Private key file for authentication* e clique em *Browse...* para adicioná-la.

## Suporte a 256 cores

*Settings > Connection > Data : Terminal-type string = putty-256color*

Para testar suporte a cor, execute o seguinte comando[[2]](http://www.commandlinefu.com/commands/view/5879/show-numerical-values-for-each-of-the-256-colors-in-bash):

```
for code in {0..255}; do echo -e "\e[38;05;${code}m $code: Test"; done

```

Veja [256colours](http://www.robmeerman.co.uk/unix/256colours) para detalhes.