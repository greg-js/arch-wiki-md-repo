[Otter Browser](http://otter-browser.org) is a web browser which aims to recreate [Opera](/index.php/Opera "Opera") UI. It's based on [Qt5](/index.php/Qt "Qt") and QtWebKit, with experimental support of QtWebEngine.

## Contents

*   [1 Installation](#Installation)
*   [2 Tips and tricks](#Tips_and_tricks)
    *   [2.1 Experimental support for QtWebEngine](#Experimental_support_for_QtWebEngine)
*   [3 See also](#See_also)

## Installation

Otter Browser can be [installed](/index.php/Installed "Installed") with [otter-browser](https://aur.archlinux.org/packages/otter-browser/) or [otter-browser-git](https://aur.archlinux.org/packages/otter-browser-git/).

**Tip:** [qt5-webkit-ng](https://www.archlinux.org/packages/?name=qt5-webkit-ng) should be installed to make QtWebKit backend using up-to-date WebKit engine.

## Tips and tricks

### Experimental support for QtWebEngine

To use QtWebEngine based on Blink web engine, install [qt5-webengine](https://www.archlinux.org/packages/?name=qt5-webengine) and rebuild Otter package. After this you can go to **about:config** and select *qtwebengine* as *Backend*.

## See also

*   [Official project site](http://otter-browser.org)
*   [Project site on GitHub](http://github.com/OtterBrowser/otter-browser)