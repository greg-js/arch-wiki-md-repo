# mod_python

**Warning:** mod_python is [discontinued](http://blog.dscpl.com.au/2010/06/modpython-project-is-now-officially.html) and have multiple security, performance and stability issues. It is strongly recommended to use [mod_wsgi](/index.php/Mod_wsgi "Mod wsgi") instead.

Mod_python is an [Apache](/index.php/Apache "Apache") module that embeds the [Python](http://www.python.org) interpreter within the server. With mod_python you can write web-based applications in Python that will run many times faster than traditional CGI and will have access to advanced features such as ability to retain database connections and other data between hits and access to Apache internals. A more detailed description of what mod_python can do is available in this O'Reilly [article](http://www.onlamp.com/pub/a/python/2003/10/02/mod_python.html).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Test Mod_Python](#Test_Mod_Python)
*   [4 See Also](#See_Also)

## Installation

Install the [mod_python](https://aur.archlinux.org/packages/mod_python/) package in the [AUR](/index.php/AUR "AUR").

## Configuration

*   Add this line to `/etc/httpd/conf/httpd.conf`:

```
LoadModule python_module modules/mod_python.so

```

*   Restart Apache

```
# httpd -k restart

```

*   Check to make sure that Apache loaded correctly

## Test Mod_Python

*   Add this block to `/etc/httpd/conf/httpd.conf`:

```
<Directory /home/www/html> 
   AddHandler mod_python .py
   PythonHandler mod_python.publisher 
   PythonDebug On 
</Directory>

```

*   Create a file in `/home/www/html/` called `mptest.py` and add this as contents:

```
from mod_python import apache
def handler(req):
    req.content_type = 'text/plain'
    req.send_http_header()
    req.write("Hello World!")
    return apache.OK

```

*   Restart Apache

```
# apachectl restart

```

*   Check to make sure that Apache loaded correctly

*   Navigate to `[http://yoursite.com/mptest.py/handler](http://yoursite.com/mptest.py/handler)` and you should see a site that just says:

```
Hello World!

```

With the configuration written above, you can also point your browser to any URL ending in .py in the test directory. You can for example point your browser to `/foobar.py` and it will be handled by mptest.py.

## See Also

*   [Gentoo Wiki Mod_Python](http://gentoo-wiki.com/Apache_Modules_mod_python)
*   [mod_python Tutorial](http://webpython.codepoint.net/mod_python)
*   [http://www.modpython.org/](http://www.modpython.org/)
*   [mod_python manual](http://www.modpython.org/live/current/doc-html/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Mod_python&oldid=388039](https://wiki.archlinux.org/index.php?title=Mod_python&oldid=388039)"