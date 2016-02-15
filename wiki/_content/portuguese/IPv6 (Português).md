Não somente pela demora mas também pelo 250k de memória usado pelo módulo IPv6, relata-se que se desabilitar o módulo nota-se uma melhora ao acesso a rede pelos softwares que erroneamente tentam consultar servidores com essa nova versão. Aliás, o [Firefox](/index.php/Firefox "Firefox") está na lista dos aplicativos afetados. Então, até a adoção generalizada do IPv6, a desativação do módulo é recomendada.

Desde a versão Oficial do Kernel26 do Arch Linux e do pacote 2.6.16.2-1, o IPv6 não é compilado diretamente no Kernel, mas como um módulo intitulado ipv6\. Muitos usuário não necessita deste recurso, e pode obter benefícios de performance (muitos programas consultam primeiro o endereço IPv6, mesmo sem saber que possui conectividade IPv6) e mais memória livre (250k, é um módulo grande e poderoso) se for removido.

## Contents

*   [1 1° Método: Desativar até quando for necessário](#1.C2.B0_M.C3.A9todo:_Desativar_at.C3.A9_quando_for_necess.C3.A1rio)
*   [2 2° Método: Desabilitar a funcionalidade](#2.C2.B0_M.C3.A9todo:_Desabilitar_a_funcionalidade)
*   [3 Desabilitando o IPv6 durante a pre-inicialização do processo](#Desabilitando_o_IPv6_durante_a_pre-inicializa.C3.A7.C3.A3o_do_processo)
*   [4 Fontes Adicionais](#Fontes_Adicionais)

## 1° Método: Desativar até quando for necessário

O módulo ipv6 normalmente é carregado no boot. Existe muitos programas que também irá carregar o módulo ipv6 após a inicialização do sistema. Na verdades, este programas carregam o net-pf-10, que é um aliase para ipv6\. Você pode parar toda essa atividade se quiser. Adicionado a seguinte linha no arquivo `/etc/modprobe.d/modprobe.conf` irá desativar o carregamento automático do ipv6, mas ainda permite o carregamento manual se necessário.

```
# Desabilitando o carregamento automático do IPv6
alias net-pf-10 off

```

## 2° Método: Desabilitar a funcionalidade

Um outro método é desabilitar o módulo completamente, adicionando a seguinte linha no arquivo `/etc/modprobe.d/modprobe.conf`:

```
options ipv6 disable=1

```

**Nota:** Este método **não** impede realmente o carregamento do módulo. O módulo é carregado para a memória (250k de memória) mas desabilita a funcionalidade. Veja [Fontes Adicionais](#Additional_resources) ir para o post no Fórum Internacional do Arch Linux sobre está discursão.

## Desabilitando o IPv6 durante a pre-inicialização do processo

Você pode também adicionar `/etc/modprobe.d/modprobe.conf` para seu `/etc/mkinitcpio.conf` e [rebuild the kernel ram disk](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio")

## Fontes Adicionais

*   [Kernel modules](/index.php/Kernel_modules "Kernel modules")
*   [ipv6](https://www.kernel.org/doc/Documentation/networking/ipv6.txt) - Documentação kernel.org
*   [Post no Fórum Arch Linux Internacional](https://bbs.archlinux.org/viewtopic.php?pid=901860) sobre as diferenças entre o 1° Método e 2° Método, mostrados acima.