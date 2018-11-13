**Status de tradução:** Esse artigo é uma tradução de [Sound system](/index.php/Sound_system "Sound system"). Data da última tradução: 2018-09-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Sound_system&diff=0&oldid=537953) na versão em inglês.

Esse artigo é sobre gerenciamento básico de som. Para tópicos avançados, veja [áudio profissional](/index.php/Professional_audio "Professional audio").

## Contents

*   [1 Informações gerais](#Informações_gerais)
*   [2 Drivers e interface](#Drivers_e_interface)
*   [3 Servidores de som](#Servidores_de_som)
*   [4 Veja também](#Veja_também)

## Informações gerais

O sistema de som do Arch consiste em vários níveis:

*   Drivers e interface – suporte e controle de hardware
*   API (bibliotecas) de modo de usuário – utilizado e exigido por aplicativos
*   **(opcional)** Servidores de som de modo de usuário – melhor para desktop complexos, necessário para vários apps de áudio simultâneos e vital para as capacidades mais avançadas, por exemplo, áudio pro
*   **(opcional)** Frameworks de som – ambientes de aplicativos de alto nível não envolvendo processos de servidor

Uma instalação padrão do Arch já inclui o sistema de som do kernel ([ALSA](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)")), e muitos utilitários para ele podem ser instalados a partir dos [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Se você quiser recursos adicionais, pode alternar para [OSS](/index.php/OSS "OSS") ou instalar um dos vários [servidores de som](https://en.wikipedia.org/wiki/pt:Servidor_de_som "wikipedia:pt:Servidor de som").

## Drivers e interface

*   **[ALSA](/index.php/ALSA_(Portugu%C3%AAs) "ALSA (Português)")** — Um componente do kernel do Linux que fornece drivers de dispositivo e suporte de nível mais baixo para hardware de áudio.

	[http://www.alsa-project.org/](http://www.alsa-project.org/) || presente no kernel padrão

*   **[Open Sound System](/index.php/Open_Sound_System "Open Sound System") (OSS)** — Uma arquitetura de som alternativa para sistemas compatíveis com Unix e POSIX. O OSS versão 3 foi o sistema de som original para Linux e está no kernel, mas foi substituído pelo ALSA em 2002, quando o OSS versão 4 se tornou software proprietário. O OSSv4 tornou-se software livre novamente em 2007, quando a 4Front Technologies divulgou seu código-fonte e o forneceu sob a GPL. O OSS não possui suporte a uma variedade tão grande de hardware como o ALSA, mas é melhor para alguns.

	[http://www.opensound.com/](http://www.opensound.com/) || [oss](https://aur.archlinux.org/packages/oss/)

## Servidores de som

*   **[PulseAudio](/index.php/PulseAudio_(Portugu%C3%AAs) "PulseAudio (Português)")** — Um servidor de som muito popular, utilizável pela maioria dos aplicativos de desktop comuns hoje em dia. Muito bom em lidar com várias entradas simultâneas e também pode fazer áudio de rede. Muito fácil de começar a trabalhar, na verdade, muitas vezes tudo o que tem a fazer é instalar o pacote e ele será executado automaticamente. Não destinado a aplicativos pro audio de baixa latência.

	[https://www.freedesktop.org/wiki/Software/PulseAudio/](https://www.freedesktop.org/wiki/Software/PulseAudio/) || [pulseaudio](https://www.archlinux.org/packages/?name=pulseaudio)

*   **[JACK Audio Connection Kit](/index.php/JACK_Audio_Connection_Kit "JACK Audio Connection Kit")** — A edição mais antiga de um servidor de som para uso profissional de áudio, especialmente para aplicativos de baixa latência, incluindo gravação, efeitos, síntese em tempo real e muitos outros. Embora esta edição seja a mais antiga, ela mantém uma equipe de desenvolvimento muito ativa e dedicada, e a edição a ser usada não é clara, a tentativa e o erro geralmente são úteis.

	[http://jackaudio.org/](http://jackaudio.org/) || [jack](https://www.archlinux.org/packages/?name=jack)

*   **JACK2** — Esta é a edição mais recente do JACK, projetada explicitamente para sistemas multiprocessados e também inclui transporte pela rede.

	[https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2](https://github.com/jackaudio/jackaudio.github.com/wiki/Q_difference_jack1_jack2) || [jack2](https://www.archlinux.org/packages/?name=jack2)

*   **JACK2 with D-Bus** — Este é o JACK2 com uma arquitetura de inicialização diferente, capaz de funcionar bem em todos os momentos em coexistência com os aplicativos PulseAudio e não-JACK, o que é um problema para as outras duas categorias de configuração do JACK.

	[https://github.com/jackaudio/jackaudio.github.com/wiki/WalkThrough_User_jack_control](https://github.com/jackaudio/jackaudio.github.com/wiki/WalkThrough_User_jack_control) || [jack2-dbus](https://www.archlinux.org/packages/?name=jack2-dbus)

*   **[NAS](https://en.wikipedia.org/wiki/Network_Audio_System "wikipedia:Network Audio System")** — Este é um servidor de som suportado por alguns dos principais aplicativos.

	[https://www.radscan.com/nas/nas-links.html](https://www.radscan.com/nas/nas-links.html) || [nas](https://aur.archlinux.org/packages/nas/)

## Veja também

*   [MIDI](/index.php/MIDI "MIDI")
*   [Codecs](/index.php/Codecs "Codecs")
*   [Áudio profissional](/index.php/Professional_audio "Professional audio")
*   [PC speaker](/index.php/PC_speaker "PC speaker")