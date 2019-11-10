**Status de tradução:** Esse artigo é uma tradução de [Gnumeric](/index.php/Gnumeric "Gnumeric"). Data da última tradução: 2019-11-08\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Gnumeric&diff=0&oldid=562505) na versão em inglês.

[Gnumeric](https://en.wikipedia.org/wiki/Gnumeric "wikipedia:Gnumeric") é um poderoso aplicativo de planilha que pode importar e exportar em vários formatos, incluindo .csv, HTML, LaTeX, Lotus 1-2-3, OpenDocument Spreadsheet e Microsoft Excel.

## Instalação

[Instale](/index.php/Instale "Instale") [gnumeric](https://www.archlinux.org/packages/?name=gnumeric).

As dependências opcionais são [psiconv](https://www.archlinux.org/packages/?name=psiconv) (para suporte ao arquivo Psion 5), [python2-gobject2](https://www.archlinux.org/packages/?name=python2-gobject2) (para suporte ao plugin python) e [yelp](https://www.archlinux.org/packages/?name=yelp) (para exibição do manual de ajuda).

## Dicas e truques

Gnumeric respeita seu [locale](/index.php/Locale_(Portugu%C3%AAs) "Locale (Português)") para o separador decimal numérico e o usa para exportação, por exemplo, para arquivos .csv também. Por exemplo:

*   com um locale alemão `de`, um número é mostrado como `0,5` *(vírgula)*,
*   com um locale inglês `en`, um número é mostrado como `0.5` *(ponto)*.

Para iniciar o Gnumeric com um locale diferente, execute:

```
 LC_NUMERIC="en" gnumeric

```

## Veja também

*   [Site oficial do Gnumeric](http://www.gnumeric.org/)