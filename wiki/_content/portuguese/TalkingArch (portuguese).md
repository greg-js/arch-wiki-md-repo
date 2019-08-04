**Status de tradução:** Esse artigo é uma tradução de [TalkingArch](/index.php/TalkingArch "TalkingArch"). Data da última tradução: 2019-07-30\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=TalkingArch&diff=0&oldid=578354) na versão em inglês.

Esta página descreve uma imagem de CD / USB inicializável personalizada para usuários cegos. A versão modificada é basicamente equivalente à imagem oficial do Archiso, mas o sistema deve começar a falar assim que você inicializar com ela. O discurso é fornecido através da placa de som, usando o sintetizador de software eSpeak e o leitor de tela Speakup. Também é possível usar um display braille via brltty. Você pode obter a imagem [desta página](https://talkingarch.info/).

Como a imagem Archiso, esta imagem é compatível com a arquitetura x86_64\. Além disso, é adequado para um CD gravável ou um pendrive. Basta baixá-lo e gravá-lo no meio de sua escolha.

Uma assinatura GPG separada é fornecida na página de download.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Créditos](#Créditos)
*   [2 Instalação do CD](#Instalação_do_CD)
*   [3 Suporte a braille](#Suporte_a_braille)
*   [4 Mantendo sua instalação de Arch Linux com fala habilitada](#Mantendo_sua_instalação_de_Arch_Linux_com_fala_habilitada)
*   [5 Masterizando imagens ISO com fala habilitada](#Masterizando_imagens_ISO_com_fala_habilitada)
*   [6 Mais recursos](#Mais_recursos)
*   [7 Aviso](#Aviso)

### Créditos

O sistema de compilação, que é uma referência à configuração do Archiso releng, é mantido por Kelly Prescott e por Kyle, e as imagens e o site principal são hospedados por Kyle. Agradeço a Chris Brannon, o antigo mantenedor, e às seguintes pessoas por enviarem valiosos comentários sobre este projeto: Chuck Hallenbeck, Julien Claassen, Alastair Irving, Tyler Spivey, Keith Hinton e muitos outros. Obrigado também por Tyler Littlefield, que anteriormente hospedou os arquivos.

## Instalação do CD

A lista de etapas a seguir é um breve guia para instalar o Arch Linux usando este CD. As instruções assumem que sua partição raiz será montada em `/mnt`.

1.  Você pode simplesmente pressionar `enter` no prompt de inicialização ou aguardar o tempo limite do gerenciador de boot. O processo de inicialização começará nesse ponto. Se você tiver um alto-falante do console, você ouvirá um bipe quando o prompt de inicialização estiver na tela. Caso contrário, aguarde cerca de 10 a 20 segundos após o CD começar a girar, ou cerca de 3 a 5 segundos depois que o sistema começar a inicializar a partir do USB, e então pressione `enter` para inicializar a imagem.
2.  Você é fortemente encorajado a ler a documentação do Arch Linux, especialmente o [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"). Execute o procedimento de instalação descrito no [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação"), conforme modificado pelas instruções abaixo.
3.  Você precisará instalar os pacotes `espeakup` e `alsa-utils`. O [Guia de instalação](/index.php/Guia_de_instala%C3%A7%C3%A3o "Guia de instalação") menciona que você pode instalar pacotes adicionais anexando seus nomes ao comando pacstrap. Por exemplo, `pacstrap/ mnt base espeakup alsa-utils`
4.  Se você ouviu uma gravação de voz informando que várias placas de som foram detectadas e você selecionou um cartão pressionando enter no bipe, um arquivo /etc/asound.conf foi gerado para configurar o ALSA para usar o cartão selecionado como padrão. Você precisará copiar este arquivo executando `cp /etc/asound.conf /mnt/etc`
5.  Enquanto estiver no arch-chroot, ative o serviço systemd de espeakup executando `systemctl enable espeakup.service`
6.  Quando você inicializa o sistema a partir do disco rígido, ele deve começar a falar.

## Suporte a braille

A imagem mais recente inclui brltty, para quem possui telas braille. O pacote brltty disponível no CD foi compilado com o menor número de dependências possível. É empacotado como brltty-minimal no Arch User Repository. Se você deseja usar o braille, você precisará fornecer o parâmetro brltty no prompt de inicialização. Alternativamente, você pode iniciar o brltty a partir do shell, após o sistema ter inicializado.

O parâmetro de inicialização do brltty consiste em três campos separados por vírgulas: driver, device e table. O primeiro é o driver para seu monitor, o segundo é o nome do arquivo do dispositivo e o terceiro é um caminho relativo para uma tabela de conversão. Você pode usar "auto" para especificar que o driver deve ser detectado automaticamente. Encorajo-vos a ler a documentação do brltty para uma explicação mais completa do programa.

Por exemplo, suponha que você tenha um dispositivo conectado a /dev/ttyS0, a primeira porta serial. Você deseja usar a tabela de texto em inglês dos EUA e o driver deve ser detectado automaticamente. Aqui está o que você deve digitar no prompt de inicialização:

```
arch32 brltty=auto,ttyS0,en_US

```

Uma vez que o brltty esteja funcionando, você pode querer desabilitar a fala. Você pode fazer isso através da tecla "print screen", também conhecida como sysrq. No meu teclado qwerty, essa tecla está localizada diretamente acima da tecla insert, entre F12 e scroll lock.

## Mantendo sua instalação de Arch Linux com fala habilitada

Você não precisa fazer nada de extraordinário para manter a instalação. Tudo deve funcionar perfeitamente.

## Masterizando imagens ISO com fala habilitada

Este processo é agora bastante simples. Basta pegar e instalar o pacote talkingarch-git do AUR. Depende do archiso-git, então você precisa disso também. Veja /usr/share/doc/talkingarch/README para instruções completas.

## Mais recursos

O TalkingArch tem um canal de IRC no #talkingarch no irc.talkabout.cf. Sinta-se à vontade para entrar e conversar com os mantenedores ou com qualquer outra pessoa no canal. Você também pode alcançar os mantenedores por [e-mail](mailto:support@talkingarch.tk).

## Aviso

Este não é um lançamento oficial. Não é endossado por ninguém além de seus mantenedores. Ele é fornecido apenas para a conveniência de usuários cegos e deficientes visuais e não oferece garantia.