Da página man do Xhost:

	O programa xhost é usado para adicionar e excluir nomes de host ou nomes de usuários para a lista permitida para fazer conexões com o servidor X. No caso dos hosts, isso fornece uma forma rudimentar de controle de privacidade e segurança. Só é suficiente para um ambiente de uma só estação de trabalho (usuário único), embora limite os piores abusos. Ambientes que exigem medidas mais sofisticadas devem implementar o mecanismo baseado em usuário ou usar os ganchos no protocolo para passar outros dados de autenticação para o servidor.

Veja *man xhost* para a informação completa.

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [xorg-xhost](https://www.archlinux.org/packages/?name=xorg-xhost).

## Uso

Para fornecer acesso a um aplicativo executado como sudo ou su para o servidor gráfico (também conhecido como sua sessão X e como a tela do seu computador), abra um terminal e digite como seu usuário normal (não use *su -*):

```
$ xhost +local:

```

Para voltar as coisas para o normal, com acesso controlado à tela X:

```
$ xhost -

```

## A saída 'cannot connect to X server :0.0'

O comando acima **xhost +** vai se livrar daquela saída, embora momentaneamente; uma forma de se livrar de forma permanente desse problema, além de muitas outras, é adicionar

```
xhost + >/dev/null

```

para seu arquivo `~/.bashrc`. Desta forma, cada vez que você abre o terminal, o comando é executado. Se você ainda não possui um arquivo .bashrc em seu diretório pessoal, é certo criar um com apenas essa linha nele. Se você não adicionar *>/dev/null*, cada vez que você abre um terminal, você verá uma mensagem não disruptiva dizendo: *access control disabled, clients can connect from any host*, que é a sua confirmação de que agora você pode executar *sudo <seu software>* sem problema.

**Atenção:** Este comando desabilita o controle de acesso, o que significa que qualquer usuário no sistema, ou em sua rede se o X estiver ouvindo na rede, tenha acesso ao seu $DISPLAY sem qualquer autenticação. Isso abre uma falha de segurança em seu sistema que permite que outros usuários iniciem aplicativos (incluindo registradores de chaves ou *keyloggers*) em seu servidor X.