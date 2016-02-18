"*Java é uma linguagem de programação orientada a objeto desenvolvida na década de 90 por uma equipe de programadores chefiada por James Gosling, na empresa Sun Microsystems. Diferentemente das linguagens convencionais, que são compiladas para código nativo, a linguagem Java é compilada para um bytecode que é executado por uma máquina virtual. A linguagem de programação Java é a linguagem convencional da Plataforma Java, mas não sua única linguagem.*" — [Wikipedia](https://en.wikipedia.org/wiki/pt:Java_(linguagem_de_programa%C3%A7%C3%A3o) "wikipedia:pt:Java (linguagem de programação)")

Arch Linux suporta oficialmente as versões de código aberto da [OpenJDK](http://openjdk.java.net/) 7 e 8\. Ambas as jvm podem ser instaladas sem conflito e ter o uso alternado entre si com ajuda do script auxiliar `archlinux-java`. Vários outros ambientes Java estão disponíveis no [AUR](/index.php/AUR "AUR"), sem suporte oficial.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Suporte Oficial](#Suporte_Oficial)
        *   [1.1.1 OpenJDK 7:](#OpenJDK_7:)
        *   [1.1.2 OpenJDK 8:](#OpenJDK_8:)
    *   [1.2 Sem suporte Oficial(AUR)](#Sem_suporte_Oficial.28AUR.29)
        *   [1.2.1 JAVA SE (Oracle)](#JAVA_SE_.28Oracle.29)
            *   [1.2.1.1 Java SE 6/7](#Java_SE_6.2F7)
        *   [1.2.2 BEA JRockit JIT JVM (+JDK)](#BEA_JRockit_JIT_JVM_.28.2BJDK.29)
*   [2 Plugin para Firefox](#Plugin_para_Firefox)
*   [3 Banco do Brasil](#Banco_do_Brasil)

## Instalação

### Suporte Oficial

Abaixo estão listados os pacotes disponíveis no [official repositories](/index.php/Official_repositories "Official repositories"):

#### OpenJDK 7:

| Package name | Use |
| [jre7-openjdk-headless](https://www.archlinux.org/packages/?name=jre7-openjdk-headless) | Ambiente java de execução (*JRE*) sem ferramenta gráfica - versão 7 |
| [jre7-openjdk](https://www.archlinux.org/packages/?name=jre7-openjdk) | Completo Ambiente java de execução (*JRE*) - versão 7 |
| [jdk7-openjdk](https://www.archlinux.org/packages/?name=jdk7-openjdk) | Java Development Kit (*JDK*) - versão 7 |
| [openjdk7-doc](https://www.archlinux.org/packages/?name=openjdk7-doc) | OpenJDK javadoc - versão 7 |
| [openjdk7-src](https://www.archlinux.org/packages/?name=openjdk7-src) | OpenJDK código fonte - versão 7 |

#### OpenJDK 8:

| Package name | Use |
| [jre8-openjdk-headless](https://www.archlinux.org/packages/?name=jre8-openjdk-headless) | Ambiente java de execução (*JRE*) sem ferramenta gráfica - versão 8 |
| [jre8-openjdk](https://www.archlinux.org/packages/?name=jre8-openjdk) | Completo Ambiente java de execução (*JRE*) - versão 8 |
| [jdk8-openjdk](https://www.archlinux.org/packages/?name=jdk8-openjdk) | Java Development Kit (*JDK*) - versão 8 |
| [openjdk8-doc](https://www.archlinux.org/packages/?name=openjdk8-doc) | OpenJDK javadoc - versão 8 |
| [openjdk8-src](https://www.archlinux.org/packages/?name=openjdk8-src) | OpenJDK código fonte - versão 8 |

**Nota:** A instalação da JDK instalará também a JRE como dependência.

### Sem suporte Oficial([AUR](/index.php/AUR "AUR"))

Veja mais detalhes em [Instalando Pacotes do AUR](/index.php/Arch_User_Repository_(Portugu%C3%AAs)#Instalando_pacotes "Arch User Repository (Português)").

#### JAVA SE (Oracle)

Versão mais recente disponivéis no [AUR](/index.php/AUR "AUR") nos pacotes mais populares em [jre](https://aur.archlinux.org/packages/jre/) e [jdk](https://aur.archlinux.org/packages/jdk/).

##### Java SE 6/7

Outras versões antigas em [jre6](https://aur.archlinux.org/packages/jre6/)/[jre7](https://aur.archlinux.org/packages/jre7/) e [jdk6](https://aur.archlinux.org/packages/jdk6/)/[jdk7](https://aur.archlinux.org/packages/jdk7/).

#### BEA JRockit JIT JVM (+JDK)

Você também pode instalar a versão JIT do Java no [AUR](/index.php/AUR "AUR"). [jrockit](https://aur.archlinux.org/packages/jrockit/)

## Plugin para Firefox

É preciso instalar o plugin [icedtea-web](https://www.archlinux.org/packages/?name=icedtea-web).

**Nota:** Para java Oracle disponível no [AUR](/index.php/AUR "AUR") não é necessario este passo pois o plugin está incluso.

## Banco do Brasil

Depois de instalar o openjdk e icedtea normalmente, como root faça:

```
# mkdir -p /etc/.java/.systemPrefs
# chmod 755 -R /etc/.java

```

Feito isto, o Banco do Brasil funcionará no Firefox. No Chromiun não deu certo.

Fonte: [http://profs.if.uff.br/tjpp/blog/entradas/banco-do-brasil-em-64-bits-solucao-definitiva#comment_089c9be82a78a97217ae294ca47dd6de](http://profs.if.uff.br/tjpp/blog/entradas/banco-do-brasil-em-64-bits-solucao-definitiva#comment_089c9be82a78a97217ae294ca47dd6de)