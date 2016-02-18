Graphviz is a package to draw graphs. It generates images in various formats from a text file written in DOT language.

## Contents

*   [1 Installation](#Installation)
*   [2 Font](#Font)
*   [3 Example](#Example)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [graphviz](https://www.archlinux.org/packages/?name=graphviz) package.

## Font

You need to install a font to include strings in the graph. For information how to install fonts, see [Fonts](/index.php/Fonts "Fonts").

To see what fonts are available:

```
$ fc-list

```

To see what fonts dot is using:

```
$ dot example.dot -Tpng -o foo.png -v 2>&1 | grep font

```

## Example

Here is a dot file example.

 `example.dot` 
```
digraph graph_name {
  graph [
    charset = "UTF-8";
    label = "sample graph",
    labelloc = "t",
    labeljust = "c",
    bgcolor = "#343434",
    fontcolor = white,
    fontsize = 18,
    style = "filled",
    rankdir = TB,
    margin = 0.2,
    splines = spline,
    ranksep = 1.0,
    nodesep = 0.9
  ];

  node [
    colorscheme = "rdylgn11"
    style = "solid,filled",
    fontsize = 16,
    fontcolor = 6,
    fontname = "Migu 1M",
    color = 7,
    fillcolor = 11,
    fixedsize = true,
    height = 0.6,
    width = 1.2
  ];

  edge [
    style = solid,
    fontsize = 14,
    fontcolor = white,
    fontname = "Migu 1M",
    color = white,
    labelfloat = true,
    labeldistance = 2.5,
    labelangle = 70
  ];

  // node define
  alpha [shape = box];
  beta [shape = box];
  gamma [shape = Msquare];
  delta [shape = box];
  epsilon [shape = trapezium];
  zeta [shape = Msquare];
  eta;
  theta [shape = doublecircle];

  // edge define
  alpha -> beta [label = "a-b", arrowhead = normal];
  alpha -> gamma [label = "a-g"];
  beta -> delta [label = "b-d"];
  beta -> epsilon [label = "b-e", arrowhead = tee];
  gamma -> zeta [label = "g-z"];
  gamma -> eta [label = "g-e", style = dotted];
  delta -> theta [arrowhead = crow];
  zeta -> theta [arrowhead = crow];
}
```

To generate a png image from this file:

```
$ dot -Tpng example.dot -o example.png

```

## See also

*   [The official Graphviz website](http://www.graphviz.org/)