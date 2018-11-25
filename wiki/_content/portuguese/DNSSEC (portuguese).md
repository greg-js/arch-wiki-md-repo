**Status de tradução:** Esse artigo é uma tradução de [DNSSEC](/index.php/DNSSEC "DNSSEC"). Data da última tradução: 2018-11-23\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=DNSSEC&diff=0&oldid=554637) na versão em inglês.

Artigos relacionados

*   [Unbound#DNSSEC validation](/index.php/Unbound#DNSSEC_validation "Unbound")

Do [artigo do Wikipédia sobre o DNSSEC](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions"):

	As Extensões de Segurança do Sistema de Nomes de Domínio ou, em inglês *Domain Name System Security Extensions* (DNSSEC), são um conjunto de especificações da IETF (Internet Engineering Task Force) para proteger certos tipos de informações fornecidas pelo Sistema de Nomes de Domínio (DNS), conforme usado em redes IP (Internet Protocol). É um conjunto de extensões para o DNS que fornecem aos clientes DNS (resolvedores ou *resolvers*) autenticação de origem de dados DNS, negação de existência autenticada e integridade de dados, mas não disponibilidade ou confidencialidade.

## Contents

*   [1 Validação básica de DNSSEC](#Validação_básica_de_DNSSEC)
    *   [1.1 Instalação](#Instalação)
    *   [1.2 Consulta com validação DNSSEC](#Consulta_com_validação_DNSSEC)
    *   [1.3 Testando](#Testando)
*   [2 Instalar um resolvedor de validação de DNSSEC](#Instalar_um_resolvedor_de_validação_de_DNSSEC)
*   [3 Habilitar DNSSEC em um software específico](#Habilitar_DNSSEC_em_um_software_específico)
*   [4 Hardware de DNSSEC](#Hardware_de_DNSSEC)
*   [5 Veja também](#Veja_também)

## Validação básica de DNSSEC

**Nota:** É necessária uma configuração adicional para as suas lookups de DNS DNSSEC por padrão. Veja [#Instalar um resolvedor de validação de DNSSEC](#Instalar_um_resolvedor_de_validação_de_DNSSEC) e [#Habilitar DNSSEC em um software específico](#Habilitar_DNSSEC_em_um_software_específico).

### Instalação

A ferramenta *drill* pode ser usada para validação básica de DNSSEC. Para usar o *drill*, [instale](/index.php/Instale "Instale") o pacote [ldns](https://www.archlinux.org/packages/?name=ldns).

Para outras ferramentas disponíveis, veja [Resolução de nome de domínio#Utilitários de pesquisa](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio#Utilitários_de_pesquisa "Resolução de nome de domínio").

### Consulta com validação DNSSEC

Então, para consultar com validação DNSSEC, use a opção `-D`:

```
$ drill -D *exemplo.com*

```

### Testando

Como um teste, use os seguintes domínios, adicionando a opção `-T`, que rastreia dos servidores raiz descendo até o domínio sendo resolvido:

```
$ drill -DT sigfail.verteiltesysteme.net

```

O resultado deve terminar com as seguintes linhas, indicando que a assinatura DNSSEC é falsa *(bogus)*:

```
[B] sigfail.verteiltesysteme.net.       60      IN      A       134.91.78.139
;; Error: Bogus DNSSEC signature
;;[S] self sig OK; [B] bogus; [T] trusted

```

Agora, para testar uma assinatura confiável:

```
$ drill -DT sigok.verteiltesysteme.net

```

O resultado deve terminar com as seguintes linhas, indicando que a assinatura é confiável:

```
[T] sigok.verteiltesysteme.net. 60      IN      A       134.91.78.139
;;[S] self sig OK; [B] bogus; [T] trusted

```

## Instalar um resolvedor de validação de DNSSEC

Para usar o DNSSEC em todo o sistema, você pode usar um resolvedor de DNS que seja capaz de validar registros de DNSSEC, para que todas as pesquisas de DNS passem por ele. Veja [Resolução de nome de domínio#Resolvedores](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio#Resolvedores "Resolução de nome de domínio") para as opções disponíveis. Observe que cada um requer opções específicas para ativar seu recurso de validação do DNSSEC.

Se você tentar visitar um site com um endereço IP falso *(spoofed)*, o resolvedor de validação impedirá que você receba os dados DNS inválidos e seu navegador (ou outro aplicativo) será informado de que não existe esse host. Como todas as pesquisas de DNS passam pelo resolvedor de validação, você não precisa de um software que tenha suporte a DNSSEC integrado ao usar essa opção.

## Habilitar DNSSEC em um software específico

Se você optar por não [#Instalar um resolvedor de validação de DNSSEC](#Instalar_um_resolvedor_de_validação_de_DNSSEC), será necessário usar o software que possui suporte a DNSSEC integrado para usar seus recursos. Muitas vezes isso significa que você deve corrigir o software sozinho. Uma lista de vários aplicativos corrigidos é encontrada [aqui](https://www.dnssec-tools.org/wiki/index.php?title=DNSSEC_Applications). Além disso, alguns navegadores web têm extensões ou complementos que podem ser instalados para implementar o DNSSEC sem corrigir o programa.

## Hardware de DNSSEC

Você pode verificar se o seu roteador, modem, AP, etc. suporta DNSSEC (muitos recursos diferentes) usando [dnssec-tester](http://www.dnssec-tester.cz/) (aplicativo baseado em Python e GTK+) para saber se é compatível com DNSSEC, e usando essa ferramenta você também pode enviar dados coletados para um servidor, para que outros usuários e fabricantes possam ser informados sobre a compatibilidade de seus dispositivos e, eventualmente, consertar o firmware (eles provavelmente serão encorajados a fazê-lo). (Antes de executar o dnssec-tester, certifique-se de que você não possui nenhum outro servidor de nomes em `/etc/resolv.conf`). Você também pode encontrar os resultados dos testes realizados no site [dnssec-tester](http://www.dnssec-tester.cz/).

## Veja também

*   [DNSSEC Resolver Test](http://dnssec.vs.uni-due.de/) - um teste simples para ver se você tem DNSSEC implementado em sua máquina.
*   [DNSSEC-Tools](https://www.dnssec-tools.org/)
*   [DNSSEC Visualizer](http://dnsviz.net) - uma ferramenta para visualizar o status de uma zona de DNS.
*   [RedHat: Securing DNS Traffic with DNSSEC](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/sec-Securing_DNS_Traffic_with_DNSSEC.html) - Artigo completo sobre a implementação do DNSSEC com *unbound*. Note que algumas ferramentas são específicas do RedHat e não são encontradas no Arch Linux.
*   [DNSSEC no Wikipedia em inglês](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions "wikipedia:Domain Name System Security Extensions") e [em português](https://en.wikipedia.org/wiki/pt:DNSSEC "wikipedia:pt:DNSSEC")