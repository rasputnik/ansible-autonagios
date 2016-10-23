auto-generated nagios config
============================

**proof of concept; not to be weaponized**

simple role (well, part of one) to generate 
nagios service checks for each host in an inventory group.

Poops them out into localhosts {{ config_dir }}/{{ hostname }}.cfg
- config_dir defaults to /tmp/nagios.

nb: since these example hosts are fictional, we are limited
to inventory varibles; when you do this for real,
hostvars and facts should also be available.

implementation
==============

    ansible-playbook -i hosts nagios.yml

the playbook runs against/on the nagios server (localhost by default),
and walks *groups.all* to find every server.

The master template generates 'universal' checks, and then
loads a 'partial' for every group that server belongs to
(typically 1, but this will handle many).

vars
====

We are running this against the nagios host, _not_ on the individual
servers. This affects var lookup within the templates.
For example, the *http_port* var of a given host is accessed as

    {{ hostvars[item].http_port }}

rather than just {{ http_port }}

group_vars/ holds the defaults for each group.

Role vars *aren't* likely to be visible to templates, sorry.
Let me know if you figure out a way to access them.

extending
=========

Should be straightforward. If you add a new group 'doodads', just
create 

* group_vars/doodads
* roles/autonagios/templates/doodads.j2

bugs
====

Yeah, probably. Please file issues.
