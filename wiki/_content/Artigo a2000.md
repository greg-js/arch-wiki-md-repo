# Artigo a2000

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

[![Tango-document-new.png](/images/f/f0/Tango-document-new.png)](/index.php/File:Tango-document-new.png)

**This article is a stub.**

**Notes:** please use the first argument of the template to provide more detailed indications. (Discuss in [Talk:Artigo a2000#](https://wiki.archlinux.org/index.php/Talk:Artigo_a2000))

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**This article or section needs language, wiki syntax or style improvements.**

**Reason:** This is a scribble note, not an article (Discuss in [Talk:Artigo a2000#](https://wiki.archlinux.org/index.php/Talk:Artigo_a2000))

```
# modprobe via_velocity speed_duplex=2

```

Note: If you issue the command: openssl engine padlock

You will probably get this in return: (padlock) VIA PadLock (no-RNG, ACE)

From what I have read this deals with VIA's RNG being a bit buggy or insecure or something.

Getting padlock to work: (please feel free to help with the formatting of the page. I dont wiki often)

Add to /etc/modprobe.d/modprobe.conf:

```
$ alias aes padlock

```

Benchmarks without padlock (3 runs):

```
$ openssl speed -evp aes-128-cbc

```

Output:

```
$ OpenSSL 1.0.0e 6 Sep 2011
built on: Tue Sep  6 17:15:38 UTC 2011
type             16 bytes     64 bytes     256 bytes    1024 bytes   8192 bytes
aes-128-cbc      10936.73k    11720.66k    11994.71k    23021.57k    23194.28k
aes-128-cbc      10792.41k    11681.17k    11985.58k    23021.91k    23197.01k
aes-128-cbc      10791.26k    11642.79k    11980.71k    23022.59k    23197.01k
```

Add to /etc/ssl/openssl.cnf (before [new_oids] section):

```
openssl_conf = openssl_def

[openssl_def]
engines = openssl_engines

[openssl_engines]
padlock = padlock_engine

[padlock_engine]
default_algorithms = ALL

```

after padlock (3 runs):

```
$ type             16 bytes     64 bytes    256 bytes   1024 bytes   8192 bytes
aes-128-cbc      58133.80k   143263.17k   234075.05k   297064.11k   342171.65k
aes-128-cbc      58162.57k   142958.08k   234077.53k   296989.70k   341712.90k
aes-128-cbc      58151.15k   143278.68k   234072.58k   297020.42k   342166.19k
```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Artigo_a2000&oldid=370332](https://wiki.archlinux.org/index.php?title=Artigo_a2000&oldid=370332)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Storage](/index.php/Category:Storage "Category:Storage")

Hidden categories:

*   [Pages flagged with Template:Stub](/index.php/Category:Pages_flagged_with_Template:Stub "Category:Pages flagged with Template:Stub")
*   [Pages or sections flagged with Template:Style](/index.php/Category:Pages_or_sections_flagged_with_Template:Style "Category:Pages or sections flagged with Template:Style")