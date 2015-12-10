# VeryNice

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

VeryNice is a daemon, available in the [AUR](/index.php/AUR "AUR"), for dynamically adjusting the nice levels of executables. The nice level represents the priority of the executable when allocating CPU resources. Simply define executables for which responsiveness is important, like X or multimedia applications, as _goodexe_ in `/etc/verynice.conf`. Similarly, CPU-hungry executables running in the background, like make, can be defined as _badexe_. This prioritisation greatly improves system responsiveness under heavy load.

## Installation

**Note:** VeryNice hasn't been updated since 2014 and the official homepage is down.

Install [verynice](https://aur.archlinux.org/packages/verynice/)<sup><small>AUR</small></sup>.

To start verynice:

 `# systemctl start verynice.service` 

To enable it to run on boot:

 `# systemctl enable verynice.service` 

## Configuration

VeryNice automatically reads configuration information both from a central location (/etc/verynice.conf ) and from the home directories of individual users, in the ~/.verynicerc file. The format of both kinds of configuration files is the same. More restrictive settings in the global configuration generally take precedence over individual users' settings. Of course the settings in a user's ~/.verynicerc file only affect that user's processes. A sample verynice.conf file is usually installed in /etc/verynice.conf or /usr/local/etc/verynice.conf.

<table border="2">

<tbody>

<tr>

<th>Parameter</th>

<th>Function</th>

<th>Default</th>

<th>Values</th>

<th>Permissions</th>

<th>Multiple?</th>

</tr>

<tr>

<td>notnice</td>

<td>Set the nice-level of "goodexe" processes</td>

<td>-4</td>

<td>Any negative number greater than -20</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>batchjob</td>

<td>Set the nice-level of "badexe" processes</td>

<td>18</td>

<td>Any positive number less than 20</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>runaway</td>

<td>Set the bad karma (nice) level at which runawayexe processes are killed with SIGTERM</td>

<td>20</td>

<td>Any positive number</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>kill</td>

<td>Set the bad karma (nice) level at which runawayexe processes are killed with SIGKILL</td>

<td>22</td>

<td>Any positive number</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>badkarmarate</td>

<td>Set the amount of bad karma generated per second of 100% cpu usage (for small bad karma levels)</td>

<td>.0167</td>

<td>Any positive real number</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>badkarmarestorationrate</td>

<td>Set the amount of bad karma removed per second of 0% cpu usage</td>

<td>.0167</td>

<td>Any positive real number</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>periodicity</td>

<td>Set the approximate number of seconds between iterations through the process analysis code of VeryNice</td>

<td>60</td>

<td>Any positive integer. Large values use less CPU. Small values give more precise performance.</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>rereadcfgperiodicity</td>

<td>Set the approximate number of program cycles (periodicities, above) between attempts to reread the configuration files of VeryNice</td>

<td>60</td>

<td>Any positive integer. Be aware that reconfiguring requires looking up the .verynicerc file in each user's home directory and does not affect existing processes.</td>

<td>Central</td>

<td>no</td>

</tr>

<tr>

<td>immuneuser</td>

<td>Inhibit VeryNice from modifying the nice level of a user's processes, except for "goodexe", below, if set in the central config file.</td>

<td>(none)</td>

<td>Any user name, unquoted</td>

<td>Central</td>

<td>yes</td>

</tr>

<tr>

<td>immuneexe</td>

<td>Inhibit VeryNice from modifying the nice level of certain executables</td>

<td>(none)</td>

<td>Any substring of the complete path to the executable, quoted with double quotes ("). If it begins with '/', it must match the complete path precisely.</td>

<td>Central/User</td>

<td>yes</td>

</tr>

<tr>

<td>badexe</td>

<td>Force the nice level of an executable to the BATCHJOB level</td>

<td>(none)</td>

<td>(As above)</td>

<td>Central/User</td>

<td>yes</td>

</tr>

<tr>

<td>goodexe</td>

<td>Force the nice level of an executable to the NOTNICE level. This is typically used for real-time multimedia applications which need high priority</td>

<td>(none)</td>

<td>(As above)</td>

<td>Central/User</td>

<td>yes</td>

</tr>

<tr>

<td>runawayexe</td>

<td>Mark an executable as a potential runaway process. Only processes specially marked will ever be killed by VeryNice</td>

<td>(none)</td>

<td>(As above)</td>

<td>Central/User</td>

<td>yes</td>

</tr>

<tr>

<td>hungryexe</td>

<td>Mark an executable as "assumed to be CPU hungry". Such a process will be treated as if it were using 100% of the CPU, regardless of its actual CPU usage. This is appropriate for programs that do their real work in lots of short-lived subprocesses, such as make(1).</td>

<td>(none)</td>

<td>(As above)</td>

<td>Central/User</td>

<td>yes</td>

</tr>

</tbody>

</table>

## See also

[Project Site](https://web.archive.org/web/20130621090315/http://thermal.cnde.iastate.edu/~sdh4/verynice/) (via the Internet Archive)

Retrieved from "[https://wiki.archlinux.org/index.php?title=VeryNice&oldid=410128](https://wiki.archlinux.org/index.php?title=VeryNice&oldid=410128)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System administration](/index.php/Category:System_administration "Category:System administration")