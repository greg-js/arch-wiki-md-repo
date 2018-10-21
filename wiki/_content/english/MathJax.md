[MathJax](https://www.mathjax.org) is a JavaScript display engine for mathematics that works in all browsers. It is able to parse [TeX](https://en.wikipedia.org/wiki/TeX "wikipedia:TeX") input in html files to produce svg output, amongst other supported formats. The higher-level [Jupyter notebook](/index.php/Jupyter "Jupyter") depends on MathJax and other modules for plotting, running interactive code, etc.

MathJax can easily be embedded on any website to typeset your TeX. It is possible to quickly integrate MathJax with a distributed network service, see [here](https://www.mathjax.org/#docs) for the currently available CDN.

This article assumes you want a hard copy of MathJax on your system.

## Contents

*   [1 Installation and Configuration](#Installation_and_Configuration)
    *   [1.1 Local Usage](#Local_Usage)
    *   [1.2 Server Usage](#Server_Usage)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 MathJax and Plotly](#MathJax_and_Plotly)
    *   [2.2 TeX raw code visible while page is loading](#TeX_raw_code_visible_while_page_is_loading)

## Installation and Configuration

Install [mathjax](https://www.archlinux.org/packages/?name=mathjax) from the official repositories.

### Local Usage

To have MathJax parse the TeX code in `~/equations.html` and produce SVG output:

```
<head>
    ...
    <script ="/usr/share/mathjax/MathJax.js?config=TeX-AMS_SVG"></script>
    ...
</head>

```

Don't forget to include a configuration query string to tell MathJax about your desired i/o formats.

You can also configure MathJax inline, see [here](http://docs.mathjax.org/en/latest/config-files.html#common-configurations) for more details and configuration options.

Your browser should now render the symbols at `file:///home/user/equations.html`.

Note that the TeX delimiters MathJax uses by default are `\( ... \)` for inline math and `\[ ... \]` , `$$ ... $$` for outline math.

### Server Usage

In order to serve your clients with MathJax processed documents, you need your scripts to access its main file: `/usr/share/mathjax/MathJax.js`.

Let us assume the server's root directory is set to `/srv/http/`, creating symlinks will grant your scripts access to the installed package:

```
$ cp -rs /usr/share/mathjax /srv/http/mathjax

```

You can now have MathJax parse the TeX code in, say, `/srv/http/pages/equations.html` by including in its head:

```
<script src="../mathjax/MathJax.js?config=TeX-AMS_SVG"></script>

```

## Troubleshooting

### MathJax and Plotly

If you are using `plotly.js` as well, loading MathJax before Plotly might fail to render TeX code. Loading Plotly *before* MathJax should work. For example:

```
<head>
     <script src="path-to-plotly/plotly-latest.min.js"></script>
     <script src="path-to-mathjax/MathJax.js?config=TeX-AMS_SVG"></script>
</head>

```

You may also try different MathJax output.

### TeX raw code visible while page is loading

It can happen that MathJax takes some time to typeset and raw TeX code appears during the while, producing an unpleasant result.

You can fix this by setting `visibility: hidden` in some element's `css` properties, and catch the event MathJax emits after typesetting is done to show it:

```
MathJax.Hub.Queue( function () { 
    document.getElementById("myID").visibility = "visible";
});

```