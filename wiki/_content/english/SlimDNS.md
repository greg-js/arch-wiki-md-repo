Related articles

*   [PowerDNS](/index.php/PowerDNS "PowerDNS")
*   [PostgreSQL](/index.php/PostgreSQL "PostgreSQL")

[slimDNS](https://github.com/Torxed/slimDNS) is a simple DNS server. It's purpose is to be a self-contained, slim and uncomplicated executable.
It relies on [PostgreSQL](/index.php/PostgreSQL "PostgreSQL") for its zone and record information.

## Contents

*   [1 Installing slimDNS](#Installing_slimDNS)
*   [2 Manual setup *(optional)*](#Manual_setup_.28optional.29)
*   [3 Running](#Running)
*   [4 Configuration](#Configuration)
    *   [4.1 Adding a domain *(optional)*](#Adding_a_domain_.28optional.29)
    *   [4.2 Adding a `A` record](#Adding_a_.60A.60_record)
    *   [4.3 Adding a MX record / complex records](#Adding_a_MX_record_.2F_complex_records)
*   [5 Handy information](#Handy_information)

## Installing slimDNS

Install [slimDNS-git](https://aur.archlinux.org/packages/slimDNS-git/) or clone [github.com/Torxed/slimDNS](https://github.com/Torxed/slimDNS.git) and follow the manual setup instructions.

## Manual setup *(optional)*

Create a user/role called "slimdns"

```
   [postgres@machine~] createuser --interactive
   [postgres@machine~] psql
   > CREATE DATABASE slimdns OWNER slimdns;
   > ALTER USER slimdns WITH PASSWORD '<some secure random string>';

```

## Running

As root, [start](/index.php/Start "Start") and [enable](/index.php/Enable "Enable") `slimDNS.service`.
Or if preferred, running it manually is done by simply invoking the main script:

```
   [user@machine~] sudo python slimdns.py

```

## Configuration

Configuration is stored under `/etc/slimDNS/config.py`, any changes to the config requires a restart.

SlimDNS comes with a tool to modify the database, it's called `dnstools` (subject to name change). The tool takes a series of parameters in order and can create domains (zones) and records.

**Note:** Creating a domain, will not set up SOA or NS records by default. However, creating a record will automatically set up a SOA and NS record if the specified domain is not found.

### Adding a domain *(optional)*

```
   [user@machine~] python dnstool.py example.com

```

### Adding a `A` record

```
   [user@machine~] python dnstool.py example.com 46.21.102.81

```

**Note:** Again, if the domain `example.com` didn't exist, a domain entry would be inserted and appropriate SOA and NS records will be inserted as well for this new domain.

You can also add the same record, but define the record type:

```
   [user@machine~] python dnstool.py example.com 46.21.102.81 A

```

### Adding a MX record / complex records

Some records have more complex structure, for instance the SRV, MX or TXT records. In order to be generic in handling these records, enclose the content of the record and add all the necessary data needed for the desired record type.

```
   [user@machine~] python dnstool.py example.com "46.21.102.81 10" MX

```

This would create a MX record, with a priority or preference of 10.

## Handy information

*   Updates run time cache every 30 seconds.
*   Does support a forwarding DNS server, however, testing on this is limited
*   Upon each start, slimdns will attempt to create the database 'slimdns' if not found, but will need this optional permissions to work.
*   Might crash for no aparent reason :D