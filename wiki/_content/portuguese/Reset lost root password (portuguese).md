**Status de tradução:** Esse artigo é uma tradução de [Reset root password](/index.php/Reset_root_password "Reset root password"). Data da última tradução: 2018-10-27\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Reset_root_password&diff=0&oldid=549091) na versão em inglês.

Este guia irá mostrar-lhe como redefinir uma senha de [root](/index.php/Usu%C3%A1rio_root "Usuário root") esquecida. Vários métodos estão listados para ajudá-lo a realizar isso.

**Atenção:** Um invasor pode usar os métodos mencionados abaixo para entrar em seu sistema. Não importa o quão seguro o sistema operacional seja ou como as senhas são boas, ter acesso físico equivale a carregar um sistema operacional alternativo e expor seus dados, a menos que você use [criptografia de disco](/index.php/Criptografia_de_disco "Criptografia de disco").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Usando um LiveCD](#Usando_um_LiveCD)
    *   [1.1 Alterando a raiz](#Alterando_a_raiz)
*   [2 Usando GRUB para chamar bash](#Usando_GRUB_para_chamar_bash)
*   [3 Veja também](#Veja_também)

## Usando um LiveCD

Com um LiveCD, alguns métodos estão disponíveis: alterar a raiz e usar o comando `passwd`, ou apagar a entrada do campo da senha diretamente editando o arquivo de senha. Qualquer LiveCD compatível com Linux pode ser usado, embora para mudar de raiz deve corresponder ao tipo de arquitetura instalada. Aqui, descrevemos apenas como redefinir sua senha com *chroot*, uma vez que a edição manual do arquivo de senha é significativamente mais arriscada.

### Alterando a raiz

1.  Inicie o LiveCD e [monte](/index.php/Mount "Mount") a partição raiz de seu sistema principal.
2.  Use o comando `passwd --root PONTO_DE_MONTAGEM NOME_USUÁRIO` para definir a nova senha (você não será perguntado sobre a anterior).
3.  Desmonte a partição raiz.
4.  Reinicie e insira sua nova senha. Se você não conseguir lembrar dela, vá para o passo 1.

## Usando GRUB para chamar bash

1.  Selecione uma entrada de inicialização adequada no menu do [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") e pressione `e` para editar a linha.
2.  Selecione a linha de kernel e pressione `e` novamente para editá-la.
3.  Acrescente `init=/bin/bash` ao final da linha.
4.  Pressione `Ctrl-X` para inicializar (essa alterações é apenas temporária e não será salva em seu menu.lst). Após a incialização, você estará em um prompt do bash.
5.  Seus sistema de arquivos raiz está montado como somente leitura agora, então remonte-o como leitura/escrita executando `mount -n -o remount,rw /`.
6.  Use o comando `passwd` para criar uma nova senha de *root*.
7.  Reinicialize digitando `reboot -f` e não perca sua senha novamente!

**Nota:** Alguns teclados podem não ser carregados corretamente pelo sistema init com este método e você não poderá digitar nada no prompt do bash. Se for esse o caso, você terá que usar outro método.

## Veja também

*   [Esse guia](http://www.howtoforge.com/how-to-reset-a-forgotten-root-password-with-knoppix-p2) para um exemplo.