**Note:** Toto je popis jak jsem rozběhl SAMBU na svém počítači. Rozhodně negarantuji, že podle tohoto návodu to půjde bez problémů i vám.

Nejprve - ujistěte se zda a jakou máte pracovní skupinu ve vaší domácí síti pro sdílení. Přijde na ní řada později.

Nyní nainstalujeme sambu. Přihlašte se jako root, aktualizujte seznam balíčků a nainstalujte nejnovější sambu následujícím způsobem.

```
pacman -S samba

```

Nyní nastavíme sdílení dat. Stále jako root se přepněte do adresáře kde je soubor smb.conf file (Tento soubor obsahuje nastavení samby)

```
cd /etc/samba

```

Ted začneme tento soubor editovat (ručně samozřejmě)

```
nano smb.conf

```

Můžete klidně použít jiný editor než je nano. Varianty jsou:

*   nano
*   pico
*   vi
*   gedit (toto není editor pro příkazovou řádku, musíte ho otevřít v novém okně)

Nyní k editaci. První sekce se jmenuje Global Parameters. Ta odkazuje na "blanketing" nastavení pro Sambu - většina editace bude hotova předtím. Zde je sekce Global Parametsrs z mého smb.conf pro příklad:

```
#Global Parameters
workgroup = HOME
netbios name = Bennett-DSLIN
encrypt passwords = yes

```

Workgroup name (pracovní skupina) znamená jakou pracovní skupinu chceme používat. (Pro Windows XP je většinou MSHOME a WORKGROUP.)
V "encrypt passwords" (šifrovat hesla) můžeme nechat nastaveno "yes". Můžete to změnit pokud nějaký počítač používá Windows 95 nebo Windows 98, nějaká dřívější vydání nepoužívají šifrování.
"netbios name" (název netbiosu) je nastavení jak bude váš počítač vidět v "Sítovém okolí" (nebo "Moje místa v síti" u Windows XP).

Je čas nastavit sdílení. Nejjednoduší je nastavit sdílení /home adresáře uživatele. Takto se nastaví i s možností zápisu:

```
[homes]
browseable = no
read only = no

```

Jestli chcete aby všichni viděli vaše soubory ale jen některá skupina mohla zapisovat (všichni mohou číst, pouze skupina "staff" může zapisovat) pak sekce bude vypadat takto:

```
[homes]
public = yes
writable = yes
write list = @staff

```

Pokud chcete aby uživatelé Windows viděli "čistý" /home (a nebyli zmateni tečkami před názvy adresářů (např ~/.bashrc), pak sekce bude vypadat takto:

```
[homes]
path = /home/%u/smb
browseable = no
read only = no

```

Přesouvání sdílení do domovského adresáře není zrovna praktické. Pokud chceme u několika uživatelů udělat vyjímku a povolit jim i jiný adresář:

```
[music]
path = /mnt/windows/Music/
browseable = yes
read only = yes
valid users = Bryan, Michael, David, Jane

```

"Path" je samozřejmě cesta k sdílenému adresáři. Skvěle jednoduché ne?

Pokud je smb.conf nastaven jak chceme uložíme ho a ukončíme editor. (To je Ctrl+O v nano a Ctrl+X pro konec)
Ted nastavíme "valid users" do seznamu uživatelů samby. Udělejte to takto:

```
smbpasswd -a <uzivatel>

```

Uživatelé a hesla musí být ve windows totožná !

Takto restartujeme sambu (zastavíme a znova spustíme):

```
/etc/rc.d/samba stop
/etc/rc.d/samba start

```

Vše je nastaveno a nezbývá než používat. U počítačů s Windows bude zřejmě nutné systém restartovat.