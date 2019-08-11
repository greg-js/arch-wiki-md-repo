**Status de tradução:** Esse artigo é uma tradução de [uswsusp](/index.php/Uswsusp "Uswsusp"). Data da última tradução: 2019-08-01\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Uswsusp&diff=0&oldid=578639) na versão em inglês.

[µswsusp](http://suspend.sourceforge.net/) (**u**serspace **s**oft**w**are **susp**end) é um conjunto de ferramentas de espaço de usuário usadas para hibernação (suspender para disco) e suspender (suspender para RAM ou standby) em sistemas Linux. Isso consiste em:

***s2ram*** - um wrapper em torno do mecanismo do kernel de suspensão para RAM, permitindo que o usuário execute algumas manipulações de adaptador gráfico do usuário antes de suspender e depois de retomar isso pode ajudar a trazer os gráficos (e todo o sistema) de volta à vida após o currículo. Incorpora a funcionalidade de [vbetool](https://www.archlinux.org/packages/?name=vbetool) e [radeontool](https://www.archlinux.org/packages/?name=radeontool), bem como alguns truques próprios. Inclui uma lista de configurações de hardware de trabalho, juntamente com os conjuntos de operações apropriados a serem executados para retomá-los com êxito. Isso é feito por uma lista de permissões de hardware mantida pelo HAL - *s2ram* traduz as opções do banco de dados HAL em parâmetros *s2ram*.

**Nota:** Como o HAL está obsoleto e os drivers do KMS podem salvar o estado da placa gráfica diretamente sem as peculiaridades do espaço do usuário, o desenvolvimento do *s2ram* está descontinuado e nenhuma outra entrada na lista de permissões é aceita. Se um driver KMS estiver em uso, o *s2ram* suspenderá diretamente a máquina.

***s2disk*** - a implementação de referência do software userspace suspender (µswsusp); coordena as etapas necessárias para suspender o sistema (como travar os processos, preparar o espaço de troca, etc.) e manipula a gravação e leitura de imagens. *s2disk* já possui suporte a compressão e criptografia da imagem e outros recursos (por exemplo, uma boa barra de progresso, salvar a imagem em um disco remoto, jogar tetris enquanto retoma, etc.) podem ser facilmente adicionados.

***s2both*** - combina as funcionalidades de *s2ram* e *s2disk* e é muito útil quando a bateria está quase esgotada. *s2both* escreve o instantâneo do sistema para o swap (assim como o *s2disk*), mas depois coloca a máquina em STR (assim como *s2ram*). Se a bateria tiver energia suficiente, você pode retomar rapidamente a partir do STR, caso contrário, você ainda pode retomar a partir do disco sem perder o seu trabalho.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Configuração](#Configuração)
    *   [2.1 Suporte a criptografia](#Suporte_a_criptografia)
    *   [2.2 Recriar initramfs](#Recriar_initramfs)
    *   [2.3 Exemplo de configuração](#Exemplo_de_configuração)
*   [3 Uso](#Uso)
    *   [3.1 Autônomo](#Autônomo)
    *   [3.2 Com systemd](#Com_systemd)
*   [4 Solução de problemas](#Solução_de_problemas)
    *   [4.1 Minha máquina não está na lista branca](#Minha_máquina_não_está_na_lista_branca)
    *   [4.2 s2ram -f não funciona](#s2ram_-f_não_funciona)
    *   [4.3 s2ram não funciona com qualquer combinação de opções](#s2ram_não_funciona_com_qualquer_combinação_de_opções)
*   [5 Veja também](#Veja_também)

## Instalação

[Instale](/index.php/Instale "Instale") [uswsusp-git](https://aur.archlinux.org/packages/uswsusp-git/).

## Configuração

Você deve editar `/etc/suspend.conf` antes de tentar suspender para o disco.

*   Se estiver usando uma partição swap:

```
resume device = /dev/disk/*by-label/swap*

```

sendo que `*by-label/swap*` deve ser substituído com o dispositivo de bloco correto contendo a partição swap.

*   Se estiver usando um [arquivo swap](/index.php/Arquivo_swap "Arquivo swap"):

```
resume device = /dev/sd*XN*  # a partição que contém o arquivo swap
resume offset = *123456*

```

sendo que `*X*` e `*N*` são a letra do dispositivo e o número da partição, respectivamente, e `123456` é a posição a partir do início do dispositivo de retomada no qual o cabeçalho do arquivo swap está localizado. O deslocamento da retomada pode ser obtido executando:

```
# swap-offset *seu_arquivo_swap*

```

*   O parâmetro `image size` (opcional) pode ser usado para limitar o tamanho da imagem de instantâneo do sistema criada por *s2disk*. Se não for possível criar uma imagem do tamanho desejado, o *s2disk* vai suspender de qualquer maneira, usando uma imagem maior. Se o tamanho da imagem estiver definido como 0, a imagem será o menor possível.

*   O parâmetro `shutdown method` (opcional) especifica a operação que será executada quando a máquina estiver pronta para ser desligada. Se definido como `reboot`, a máquina será reinicializada imediatamente. Se definido para `platform`, a máquina será desligada usando operações especiais de gerenciamento de energia disponíveis no kernel, que podem ser necessárias para que o hardware seja reinicializado corretamente após o reinício, e pode fazer com que o sistema retome mais rapidamente. Se definido como `shutdown`, a máquina simplesmente será desligada, o que pode causar problemas para alguns hardwares.

*   Se o parâmetro `compute checksum` estiver definido como `y`, as ferramentas *s2disk* e *resume* usarão o algoritmo MD5 para verificar a integridade da imagem.

*   Se o parâmetro `compress` estiver definido como `y`, as ferramentas *s2disk* e *resume* usarão o algoritmo de compactação LZF para compactar/descompactar a imagem.

*   Se `splash` estiver definido como `y`, *s2disk* e/ou *resume* usarão um sistema inicial. Atualmente, há suporte a *splashy* e [fbsplash](https://aur.archlinux.org/packages/fbsplash/), mas *splashy* não está disponível no Arch Linux.
    **Nota:** Isso exige opções adicionais ao `configure` para µswsusp (`--enable-splashy` e `--enable-fbsplash`, respectivamente).

*   A opção `resume pause` introduzirá um atraso depois de retomar com sucesso da hibernação, para permitir que o usuário leia as estatísticas (velocidade de leitura e gravação, tamanho da imagem, etc.)

*   Se `threads` estiver ativado, o *s2disk* usará vários encadeamentos para compactar, criptografar e gravar a imagem. Isso deve acelerar as coisas. Para detalhes, leia os comentários em [suspend.c](http://git.kernel.org/?p=linux/kernel/git/rafael/suspend-utils.git;a=blob;f=suspend.c;h=166a62f03ea9daaba271e7cebf94c76881d4266f;hb=HEAD)

### Suporte a criptografia

*   gere uma chave com o utilitário *suspend-keygen* incluído no pacote;
*   escreva o nome da chave em `/etc/suspend.conf`;

```
encrypt = y
RSA key file = *caminho_para_arquivo_de_chave*

```

### Recriar initramfs

**Nota:** Sempre que você modificar `/etc/suspend.conf`, **você precisará reconstruir** seu initramfs. Se você não fizer isso, e o Linux não conseguir encontrar sua imagem na inicialização, você não verá uma mensagem de erro indicando isso. Seu processo de inicialização irá travar depois de iniciar o hook `uresume`, normalmente após a mensagem com a versão libgcrypt.

Edite seu arquivo `/etc/mkinitcpio.conf` e adicione "uresume" à entrada HOOKS.

```
HOOKS="base udev autodetect block **uresume** filesystems"

```

e [reconstrua o ramdisk](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio").

### Exemplo de configuração

 `/etc/suspend.conf` 
```
snapshot device = /dev/snapshot

resume device = /dev/disk/by-label/swap

# tamanho da imagem é em bytes
image size = 1468006400

#suspend loglevel = 2

compute checksum = y

compress = y

#encrypt = y

#early writeout = y

#splash = y

# até 60 (segundos)
#resume pause = 30  

threads = y
```

## Uso

### Autônomo

Para suspender para o disco, execute:

```
# s2disk

```

Para suspender para a RAM, execute primeiro:

```
# s2ram --test

```

para ver se sua máquina está no banco de dados das máquinas que sabe-se que funciona. Se retornar algo como `Machine matched entry xyz`, então prossiga e execute:

```
# s2ram

```

Caso contrário, o parâmetro `--force` será necessário, possivelmente combinado com outros parâmetros (consulte `s2ram --help`). Pode falhar.

Agora você poderia tentar suspender chamando diretamente *s2disk* na linha de comando:

```
# s2disk

```

Provavelmente, é necessário recorrer a uma ferramenta de espaço de usuário que chama internamente *s2disk*.

### Com systemd

Para colocar seu sistema em hibernação, conhecido como *Suspensão para o Disco*, com `systemctl hibernate`, [edite](/index.php/Edite "Edite") o `systemd-hibernate.service`, adicionando:

 `/etc/systemd/system/systemd-hibernate.service.d/override.conf` 
```
[Service]
ExecStart=
ExecStartPre=-/usr/bin/run-parts -v -a pre /usr/lib/systemd/system-sleep
ExecStart=/usr/bin/s2disk
ExecStartPost=-/usr/bin/run-parts -v --reverse -a post /usr/lib/systemd/system-sleep
```

Depois disso, execute `systemctl hibernate` para colocar seu sistema em hibernação. Faça alterações semelhantes em `systemd-hybrid-sleep.service` (substitua *s2disk* por *s2both*) para ativar o modo de suspensão híbrido baseado no µswsusp.

## Solução de problemas

### Minha máquina não está na lista branca

Se *s2ram* não corresponder a sua máquina a uma entrada em sua lista de desbloqueio, ela exibirá algumas strings de identificação de propósito geral para sua máquina (as mesmas fornecidas `s2ram -i`). Neste caso, você pode tentar forçar *s2ram* a suspender sua máquina usando `s2ram -f`.

### `s2ram -f` não funciona

Se `s2ram -f` não funcionar, tente as diferentes alternativas oferecidas por *s2ram*. Execute `s2ram -h` para obter uma lista das opções possíveis:

 `# s2ram -h` 
```
Usage: s2ram [-nhi] [-fspmrav]

Options:
    -h, --help:       this text.
    -n, --test:       test if the machine is in the database.
                      returns 0 if known and supported
    -i, --identify:   prints a string that identifies the machine.
    -f, --force:      force suspending, even on unknown machines.

The following options are only available with -f/--force:
    -s, --vbe_save:   save VBE state before suspending and restore after resume.
    -p, --vbe_post:   VBE POST the graphics card after resume
    -m, --vbe_mode:   get VBE mode before suspend and set it after resume
    -r, --radeontool: turn off the backlight on radeons before suspending.
    -a, --acpi_sleep: set the acpi_sleep parameter before suspend
                      1=s3_bios, 2=s3_mode, 3=both
    -v, --pci_save:   save the PCI config space for the VGA card.

```

Experimente as seguintes variações:

```
  s2ram -f -a 1
  s2ram -f -a 2
  s2ram -f -a 3
  s2ram -f -p -m
  s2ram -f -p -s
  s2ram -f -m
  s2ram -f -s
  s2ram -f -p
  s2ram -f -a 1 -m
  s2ram -f -a 1 -s

```

Se nenhuma dessas combinações funcionar, inicie novamente, mas adicione a opção `-v`.

Note que misturar a opção `-a` e as opções do [vbetool](https://www.archlinux.org/packages/?name=vbetool) (`-p`, `-m`, `-s`) normalmente é apenas uma medida de último recurso, geralmente não faz muito sentido.

Se você encontrar várias combinações que funcionam (por exemplo, `s2ram -f -a 3` e `s2ram -f -p -m` funcionam na sua máquina), o método do kernel (`-a`) deve ser preferido sobre os métodos do espaço do usuário (`-p`, `-m`, `-s`).

Verifique todas as combinações em ambos os casos ao relatar o sucesso para os desenvolvedores do *s2ram*:

*   ao executar o *s2ram* a partir do console
*   ao executar o *s2ram* a partir do X

### s2ram não funciona com qualquer combinação de opções

Existe um truque que não corresponde a uma opção de linha de comando porque requer operações adicionais de você. Ele é marcado com NOFB na lista branca e usado para os laptops que são suspensos e retomados corretamente apenas se nenhum framebuffer for usado. Se você verificar que nenhuma opção de linha de comando do *s2ram* funciona, você pode tentar desabilitar o framebuffer. Para fazer isso, você precisa editar a configuração do gerenciador de inicialização, remover quaisquer valores possíveis `vga=<foo>` da linha do kernel e reinicializar. Isso, pelo menos, se você usar o framebuffer VESAFB (como no kernel padrão do Arch). Se você usar um driver de framebuffer diferente, consulte a documentação do driver para ver como desabilitá-lo.

## Veja também

*   [Site oficial do Uswsusp](http://suspend.sourceforge.net/)
*   [Arquivo HOWTO](http://git.kernel.org/?p=linux/kernel/git/rafael/suspend-utils.git;a=blob;f=HOWTO;h=116cddaa76cbdec69eb8b1e87b7df8931d3a73da;hb=HEAD) incluído no código-fonte do kernel Linux
*   `/usr/share/doc/suspend/README` Documentação do Uswsusp
*   `/usr/share/doc/suspend/README.s2ram-whitelist` README do s2ram-whitelist