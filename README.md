auto-generated nagios config
============================

**proof of concept; not to be weaponized (yet)**

simple role to generate nagios service checks from inventory groups.

This demo version creates a local config directory (/tmp/nagios by default)
with a {{ hostname }}.cfg for each host in the inventory.

nb: since these example hosts are fictional, we are limited
to inventory-level variables; on a realistic deployment,
hostvars and facts should also be available.

implementation
==============

    ansible-playbook -i hosts nagios.yml

the playbook walks *groups.all* to find every server, then runs a
'master template' (roles/autonagios/templates/host-template.yml)

The master template contains generic checks, and loads a 'partial' template 
for each group the server belongs to.

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
