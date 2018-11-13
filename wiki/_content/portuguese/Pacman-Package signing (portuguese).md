**Status de tradução:** Esse artigo é uma tradução de [Pacman/Package signing](/index.php/Pacman/Package_signing "Pacman/Package signing"). Data da última tradução: 2018-10-25\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Pacman/Package_signing&diff=0&oldid=551079) na versão em inglês.

Artigos relacionados

*   [GnuPG](/index.php/GnuPG "GnuPG")
*   [DeveloperWiki:Package signing](/index.php/DeveloperWiki:Package_signing "DeveloperWiki:Package signing")

Para determinar se os pacotes são autênticos, o *pacman* usa [chaves GnuPG](http://www.gnupg.org/) em um modelo de [rede de confiança](http://www.gnupg.org/gph/en/manual.html#AEN385). As Chaves Mestras de Assinatura (*Master Signing Keys*) são encontradas [aqui](https://www.archlinux.org/master-keys/). Pelo menos três dessas Chaves Mestras de Assinatura são usadas para assinar cada uma das próprias chaves de Desenvolvedor e de *Trusted User* que, por sua vez, são usadas para assinar seus pacotes. O usuário também possui uma chave PGP única que é gerada quando você configura *pacman-key*. Portanto, a rede de confiança liga a chave do usuário às chaves mestras.

Exemplos de redes de confiança:

*   **Pacotes personalizados**: Você mesmo fez o pacote e o assinou com sua própria chave.
*   **Pacotes não oficiais**: Um desenvolvedor fez o pacote e o assinou. Você usou sua chave para assinar aquela chave de desenvolvedor.
*   **Pacotes oficiais**: Um desenvolvedor fez o pacote e o assinou. A chave do desenvolvedor foi assinada pelas chaves mestras do Arch Linux. Você usou sua chave para assinar as chaves mestras e você confia nelas como garantia dos desenvolvedores.

**Nota:** O protocolo HKP usa 11371/tcp para comunicação. Para obter as chaves assinadas dos servidores (usando *pacman-key*), essa porta é necessária para comunicação.

## Contents

*   [1 Configuração](#Configuração)
    *   [1.1 Configurando o pacman](#Configurando_o_pacman)
    *   [1.2 Inicializando o chaveiro](#Inicializando_o_chaveiro)
*   [2 Gerenciando o chaveiro](#Gerenciando_o_chaveiro)
    *   [2.1 Verificando as chaves mestras](#Verificando_as_chaves_mestras)
    *   [2.2 Adicionando as chaves de desenvolvedor](#Adicionando_as_chaves_de_desenvolvedor)
    *   [2.3 Adicionando chaves não oficiais](#Adicionando_chaves_não_oficiais)
    *   [2.4 Depurando com gpg](#Depurando_com_gpg)
*   [3 Solução de problemas](#Solução_de_problemas)
    *   [3.1 Não foi possível importar chaves](#Não_foi_possível_importar_chaves)
    *   [3.2 Desabilitando verificação de assinatura](#Desabilitando_verificação_de_assinatura)
    *   [3.3 Redefinindo todas as chaves](#Redefinindo_todas_as_chaves)
    *   [3.4 Removendo pacotes obsoletos](#Removendo_pacotes_obsoletos)
    *   [3.5 Assinatura tem confiança desconhecida](#Assinatura_tem_confiança_desconhecida)
    *   [3.6 Atualizando chaves via proxy](#Atualizando_chaves_via_proxy)
*   [4 Veja também](#Veja_também)

## Configuração

### Configurando o pacman

A opção `SigLevel` no `/etc/pacman.conf` determina quanta confiança é exigida para instalar um pacote. Para uma explicação detalhada de `SigLevel`, veja a [página man do pacman.conf](https://www.archlinux.org/pacman/pacman.conf.5.html#_package_and_database_signature_checking) e os comentários no arquivo em si. A verificação de assinatura pode ser definida globalmente ou por repositório. Se `SigLevel` estiver definido globalmente na seção `[options]` para exigir que todos os pacotes seja assinados, então os pacotes que você compilar também precisarão ser assinados usando *makepkg*.

**Nota:** Apesar de todos os pacotes oficiais serem agora assinados, desde Junho de 2012 a assinatura da base de dados é um trabalho em progresso. Se `Required` estiver definido, então `DatabaseOptional` também deve ser definido.

Uma configuração padrão pode ser usada para instalar apenas os pacotes que estão assinados pelas chaves confiadas:

 `/etc/pacman.conf`  `SigLevel = Required DatabaseOptional` 

Isso porque `TrustedOnly` é um parâmetro padrão compilado no *pacman*. Então, a linha acima leva ao mesmo resultado que uma opção global de:

```
SigLevel = Required DatabaseOptional TrustedOnly

```

A linha acima pode ser obtida a nível de repositório mais abaixo na configuração, p.ex.:

```
[core]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

adiciona explicitamente verificação de assinatura para pacotes do repositório, mas não exige que o banco de dados seja assinado. `Optional` aqui desligaria um `Required` global para esse repositório

**Atenção:** A opção de SigLevel `TrustAll` existe para propósito de depuração e facilita muito confiar em chaves que não foram verificadas. Você deve usar `TrustedOnly` para todos os repositórios oficiais.

### Inicializando o chaveiro

Para configurar o chaveiro (*keyring*) do *pacman*, use:

```
# pacman-key --init

```

Para essa inicialização, uma [entropia](https://en.wikipedia.org/wiki/Entropy_(computing) é exigida. Mover seu mouse por aí, pressionar caracteres aleatórios no teclado e executar algumas atividades de disco (por exemplo, em outro console, executando `ls -R /` ou `find / -name foo` ou `dd if=/dev/sda8 of=/dev/tty7`) deve gerar entropia. Se o seu sistema ainda não possui entropia suficiente, esta etapa pode levar horas; se você ativamente gerar entropia, ele irá completar muito mais rapidamente.

A aleatoriedade criada é usada para configurar um chaveiro (`/etc/pacman.d/gnupg`) e a chave de assinatura GPG do seu sistema.

**Nota:** Se você precisa executar `pacman-key --init` em um computador que não gera muita entropia (por exemplo, um servidor *headless* - sem monitor e periféricos), a geração de chaves pode levar muito tempo. Para gerar pseudo-entropia, instale [haveged](/index.php/Haveged "Haveged") ou [rng-tools](/index.php/Rng-tools "Rng-tools") na máquina de destino e inicie o serviço correspondente antes de executar `pacman-key --init`.

## Gerenciando o chaveiro

### Verificando as chaves mestras

A configuração inicial de chaves é alcançada usando:

```
# pacman-key --populate archlinux

```

Tire um tempo para verificar as [Chaves Mestras de Assinatura](https://www.archlinux.org/master-keys/) quando solicitado, pois estes são usados para coassinar (e, portanto, confiar) todas as outras chaves do empacotador.

As chaves PGP são muito grandes (2048 bits ou mais) para que os humanos trabalhem com elas, então eles geralmente são *hashed* para criar uma impressão digital de 40 dígitos que pode ser usada para verificar manualmente que duas chaves são iguais. Os últimos oito dígitos da impressão digital servem como um nome para a chave conhecida como "ID da chave (curta)" (os últimos *dezesseis* dígitos da impressão digital seriam 'ID da chave longa').

### Adicionando as chaves de desenvolvedor

As chaves oficiais de desenvolvedor e [Trusted Users](/index.php/Trusted_Users_(Portugu%C3%AAs) "Trusted Users (Português)") *(TU)* são assinadas pelas chaves mestras, então você não precisa usar *pacman-key* para assiná-las você mesmo. Sempre que o *pacman* encontra uma chave que ele não reconhece, ele solicitará fazer o download de um chaveiro (`keyserver`) configurado no `/etc/pacman.d/gnupg/gpg.conf` (ou usando a opção `--keyserver` na linha de comando). O Wikipédia mantém uma [lista de servidores de chave](https://en.wikipedia.org/wiki/Key_server_(cryptographic) "wikipedia:Key server (cryptographic)").

Depois de ter baixado uma chave do desenvolvedor, você não terá que baixá-la novamente e pode ser usada para verificar quaisquer outros pacotes assinados por esse desenvolvedor.

**Nota:** O pacote [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring), que é uma dependência de [pacman](https://www.archlinux.org/packages/?name=pacman), contém as chaves mais recentes. No entanto, as chaves também podem ser atualizadas manualmente usando `pacman-key --refresh-keys` (como root). Ao fazer `--refresh-keys`, sua chave local também será pesquisada no servidor de chaves remoto e você receberá uma mensagem sobre o fato de não ser encontrada. Isso não é motivo para se preocupar.

### Adicionando chaves não oficiais

Esse método pode ser usado, por exemplo, para adicionar sua própria chave para o chaveiro do *pacman*, ou para permitir [repositórios não oficiais de usuários](/index.php/Unofficial_user_repositories "Unofficial user repositories") assinados.

Primeiro, obtenha o **ID de chave** (`*id-chave*`) de seu dono. Então, adicione-o ao chaveiro usando um dos métodos abaixo:

1.  Se a chave estiver localizado em um servidor de chave, importe-a com: `# pacman-key --recv-keys*id-chave*` 
2.  Caso contrário, se um link para um arquivo de chave for fornecido, baixe-a e então execute: `# pacman-key --add */caminho/para/arquivo/de/chave*` 

É recomendado verificar a impressão digital, assim como qualquer chave mestra ou outra chave que você vai assinar:

```
$ pacman-key --finger *id-chave*

```

Finalmente, você deve assinar localmente a chave importada:

```
# pacman-key --lsign-key *id-chave*

```

Agora, você confia nessa chave para assinar pacotes.

### Depurando com gpg

Para fins de depuração, você pode acessar o chaveiro do *pacman* diretamente com *gpg*, p.ex.:

```
# gpg --homedir /etc/pacman.d/gnupg --list-keys

```

## Solução de problemas

**Atenção:** *pacman-key* depende do [tempo](/index.php/System_time "System time"). Se o relgógio do seu sistema estiver errado, você vai receber:
```
erro: pacote: assinatura de "Usuário <email@archlinux.org>" é inválida
erro: falha ao submeter transação (pacote inválido ou corrompido (assinatura PGP))
Ocorreram erros e, portanto, nenhum pacote foi atualizado.

```

### Não foi possível importar chaves

Existem várias origens possíveis deste problema:

*   Um pacote [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) desatualizado.
*   Data incorreta.
*   Seu provedor de internet bloqueou a porta usada para importar chaves PGP.
*   Seu cache do *pacman* contém cópia de pacotes de tentativas anteriores.
*   `dirmngr` não está configurado corretamente.

Você pode estar travado por causa do pacote [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring) estar desatualizado, ao fazer uma sincronização de atualização. Experimente [atualizar o sistema](/index.php/Pacman_(Portugu%C3%AAs)#Atualizando_pacotes "Pacman (Português)") pode corrigi-lo primeiro.

Se você ainda estiver tendo problema, certifique-se de que o arquivo `/root/.gnupg/dirmngr_ldapservers.conf` existe e que você consegue executar com sucesso `#dirmngr`. Se falhar, crie um arquivo vazio e execute novamente `#dirmngr`.

Se isso não ajudar e sua data estiver correta, você poderia tentar trocar para o servidor do MIT, que fornece uma porta alternativa. Para fazer isso, edite `/etc/pacman.d/gnupg/gpg.conf` e altere o linha `keyserver` para:

```
keyserver hkp://pgp.mit.edu:11371

```

Se mesmo a porta 80 não resolver (por exemplo, quando a empresa usar algum tipo de proxy "transparente" de somente http em vez de rota, então você poderia usar:

```
keyserver hkps://hkps.pool.sks-keyservers.net:443

```

Se você estiver com IPv6 desabilitado, *gpg* vai falhar quando ele encontrar algum endereço IPv6\. Neste caso, tente com um servidor de chave somente IPv4, como:

```
keyserver hkp://ipv4.pool.sks-keyservers.net:11371

```

Se você esquecer de executar `pacman-key --populate archlinux`, você pode obter alguns erros durante a importação de chaves.

Se nada disso ajudar, seu cache do *pacman*, localizado em `/var/cache/pacman/pkg/`, pode conter pacotes não assinados de tentativas anteriores. Tente limpar o cache manualmente ou executar:

```
# pacman -Sc

```

que remove todos os pacotes em cache que não foram instalados.

### Desabilitando verificação de assinatura

**Atenção:** Use com cuidado. Desabilitar assinatura de pacote vai permitir que o *pacman* instale automaticamente pacotes não confiáveis.

Se você não está preocupado com assinatura de pacote, você pode desabilitar por completo a verificação de assinatura PGP. Edite o `/etc/pacman.conf` e descomente a seguinte linha sob `[options]`:

```
SigLevel = Never

```

Você precisa comentar quaisquer configurações de SigLevel específica de repositórios também porque elas sobrescrevem as configurações globais. Isso vai resultar em nenhuma verificação de assinatura, que era o comportamento padrão antes do pacman 4\. Se você decidir fazer isso, você não precisa configurar um chaveiro com *pacman-key*. Você pode alterar essa opção posteriormente para habilitar a verificação de pacote.

### Redefinindo todas as chaves

Se você quiser remover ou redefinir todas as chaves instaladas no seu sistema, você pode remover a pasta `/etc/pacman.d/gnupg` como *root* e executar novamente `pacman-key --init` e, em seguida, adicionar as chaves como preferidas.

### Removendo pacotes obsoletos

Se os mesmos pacotes continuam falhando e você tem certeza que fez tudo que as coisas do *pacman-key* corretamente, tente removê-los em `rm /var/cache/pacman/pkg/*pacote_ruim**` de forma que sejam baixados novamente.

Essa pode ser a solução se você obtiver uma mensagem como `erro: linux: assinatura de "usuário <usuário@exemplo.com.br>" é inválida` ou similar ao atualizar (i.e. você pode não ser a vítima de um ataque Man-in-The-Middle - MITM no final das contas, e sim o seu arquivo baixado estava corrompido).

### Assinatura tem confiança desconhecida

Algumas vezes ao executar `pacman -Suy`, você pode encontrar esse erro:

```
error: *nome-pacote*: a assinatura de "*empacotador*" tem confiança desconhecida

```

Isso ocorre porque a chave do `*empacotador*` usada no pacote `*nome-pacote*` não está presente e/ou não é confiável no banco de dados gpg local do pacman-key. O Pacman parece não conseguir sempre verificar se a chave foi recebida e marcada como confiável antes de continuar. Mitigue [assinando manualmente a chave não confiável localmente](#Adicionando_chaves_não_oficiais) ou [redefinindo todas as chaves](#Redefinindo_todas_as_chaves).

### Atualizando chaves via proxy

Para usar um proxy ao atualizar chaves, a opção `honor-http-proxy` deve ser configurar em ambos `/etc/gnupg/dirmngr.conf` e `/etc/pacman.d/gnupg/dirmngr.conf`. Veja [GnuPG#Use a keyserver](/index.php/GnuPG#Use_a_keyserver "GnuPG") para mais informações.

**Nota:** Se o *pacman-key* for usado sem a opção `honor-http-proxy` e falhar, uma reinicialização pode resolver o problema.

## Veja também

*   [DeveloperWiki:Package Signing Proposal for Pacman](/index.php/DeveloperWiki:Package_Signing_Proposal_for_Pacman "DeveloperWiki:Package Signing Proposal for Pacman")
*   [Pacman Package Signing – 1: Makepkg and Repo-add](http://allanmcrae.com/2011/08/pacman-package-signing-1-makepkg-and-repo-add/)
*   [Pacman Package Signing – 2: Pacman-key](http://allanmcrae.com/2011/08/pacman-package-signing-2-pacman-key/)
*   [Pacman Package Signing – 3: Pacman](http://allanmcrae.com/2011/08/pacman-package-signing-3-pacman/)
*   [Pacman Package Signing – 4: Arch Linux](http://allanmcrae.com/2011/12/pacman-package-signing-4-arch-linux/)