[Croscore Fonts](https://en.wikipedia.org/wiki/Croscore_fonts "wikipedia:Croscore fonts") are free and open source high quality fonts from the Chromium OS Project. These fonts are metrically compatible with [MS Fonts](/index.php/MS_Fonts "MS Fonts") and have better rendering instructions for FreeType library.

## Installation

Packages in the official repositories:

*   [ttf-croscore](https://www.archlinux.org/packages/?name=ttf-croscore) - Includes Arimo (sans-serif), Tinos (serif) and Cousine (monospace)

Packages are available in [AUR](/index.php/AUR "AUR"):

*   [ttf-carlito](https://aur.archlinux.org/packages/ttf-carlito/) - Includes Carlito (matches Microsoft Calibri)
*   [ttf-caladea](https://aur.archlinux.org/packages/ttf-caladea/) - Includes Caladea (matches Microsoft Cambria)

## System-wide Usage

Append following lines to your font configuration file, eg. /etc/fonts/local.conf:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>

  <alias>
    <family>serif</family>
    <prefer><family>Tinos</family></prefer>
  </alias>
  <alias>
    <family>sans-serif</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>sans</family>
    <prefer><family>Arimo</family></prefer>
  </alias>
  <alias>
    <family>monospace</family>
    <prefer><family>Cousine</family></prefer>
  </alias>

  <match>
    <test name="family"><string>Arial</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Helvetica</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Verdana</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Tahoma</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Arimo</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Times New Roman</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Tinos</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Times</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Tinos</string>
    </edit>
  </match>
  <match> <!-- NOT metric-compatible! -->
    <test name="family"><string>Consolas</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Cousine</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Courier New</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Cousine</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Calibri</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Carlito</string>
    </edit>
  </match>
  <match>
    <test name="family"><string>Cambria</string></test>
    <edit name="family" mode="assign" binding="strong">
      <string>Caladea</string>
    </edit>
  </match>

</fontconfig>

```