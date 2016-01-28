# Saltstack

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

From [docs.saltstack.com](http://docs.saltstack.com/):

_Salt is a new approach to infrastructure management. Easy enough to get running in minutes, scalable enough to manage tens of thousands of servers, and fast enough to communicate with them in seconds._

_Salt delivers a dynamic communication bus for instrastructures that can be used for orchestration, remote execution, configuration management and much more._

## Contents

*   [1 Installation](#Installation)
*   [2 Components of Salt Stack](#Components_of_Salt_Stack)
    *   [2.1 Salt Master](#Salt_Master)
    *   [2.2 Salt Minion](#Salt_Minion)
    *   [2.3 Salt Key](#Salt_Key)
    *   [2.4 Salt Cloud](#Salt_Cloud)
*   [3 Salt commands](#Salt_commands)
*   [4 See also](#See_also)

## Installation

Salt is available in [official repositories](/index.php/Official_repositories "Official repositories") as [salt-raet](https://www.archlinux.org/packages/?name=salt-raet) and [salt-zmq](https://www.archlinux.org/packages/?name=salt-zmq).

## Components of Salt Stack

Salt is at its core a Remote Execution solution. Running pre-defined or arbitrary commands on remote hosts. Salt functions on a master/minion topology. A master server acts as a central control bus for the clients (called minions), and the minions connect back to the master.

### Salt Master

Turning on the Salt master is easy, just turn it on! The default configuration is suitable for the vast majority of installations. The Salt master can be controlled with systemd.

```
# systemctl start salt-master

```

The Salt master can also be started in the foreground in debug mode, thus greatly increasing the command output:

```
# salt-master -l debug

```

The Salt master needs to bind to 2 TCP network ports on the system, these ports are 4505 and 4506.

### Salt Minion

The Salt Minion can operate with or without a Salt Master. This wiki assumes that the minion will be connected to the master. for information on how to run a master-less minion please see the masterless quickstart guide: [http://docs.saltstack.com/topics/tutorials/quickstart.html](http://docs.saltstack.com/topics/tutorials/quickstart.html)

The Salt minion only needs to be aware of one piece of information to run, the network location of the master. By default the minion will look for the DNS name **salt** for the master, making the easiest approach to set internal DNS to resolve the name salt back to the Salt Master IP. Otherwise the minion configuration file will need to be edited, edit the configuration option **master** to point to the DNS name or the IP of the Salt Master.

 `/etc/salt/minion`  `master: saltmaster.example.com` 

Now that the master can be found, start the minion in the same way as the master; with systemd.

```
# systemctl start salt-minion

```

Or in debug mode

```
# salt-minion -l debug

```

### Salt Key

Salt authenticates minion using public key encryption and authentication. For a minion to start accepting commands from the master the minion keys need to be accepted. the **salt-key** command is used to manage all of the keys on the master. To list the keys that are on the master run salt-key list command:

```
# salt-key -L

```

The keys that have been rejected, accepted and pending acceptance are listed. To accept a minion:

```
# salt-key -a minion.example.com

```

Or you can accept all keys at once with :

```
# salt-key -A

```

### Salt Cloud

Salt can also be used to provision cloud servers on most major cloud providers. In order to connect to these providers, additional dependencies may be required. [apache-libcloud](https://www.archlinux.org/packages/?name=apache-libcloud)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [python-apache-libcloud](https://www.archlinux.org/packages/?name=python-apache-libcloud)]</sup> is required for many popular providers such as Rackspace and Amazon, and can be found in the community repositories. Further details for configuring your cloud provider can be found at the official wiki: [http://docs.saltstack.com/en/latest/topics/cloud/](http://docs.saltstack.com/en/latest/topics/cloud/)

## Salt commands

After connecting and accepting the minion on the Salt master you can now send commands to the minion. Salt commands allow for a vast set of functions to be executed and for specific minion and groups of minions to be targeted for execution. This makes the **salt** command very powerful, but the command is also very usable, and easy to understand.

The **salt** command is compromised of command options, target specification, the function to execute, and arguments to the function. A simple command to start with looks like this:

```
# salt '*' test.ping

```

The ***** is the target, which specifies all minions, and **test.ping** tells the minions to run the **test.ping** function. This **salt** command will tell all of the minions to execute the **test.ping** in parallel and return the result.

for more commands see documentation or run:

```
# salt '*' sys.doc

```

## See also

*   [http://docs.saltstack.com/](http://docs.saltstack.com/) - Official documentation

Retrieved from "[https://wiki.archlinux.org/index.php?title=Saltstack&oldid=412505](https://wiki.archlinux.org/index.php?title=Saltstack&oldid=412505)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [System administration](/index.php/Category:System_administration "Category:System administration")

Hidden category:

*   [Pages with broken package links](/index.php/Category:Pages_with_broken_package_links "Category:Pages with broken package links")