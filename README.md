auto-generated nagios config
============================

**proof of concept; not to be weaponized!**

simple role (well, part of one) to generate 
nagios configurations for each host in an inventory group.

nb: all the hosts in the groups are fictional so we are limited
to inventory varibles; when you do this for real,
hostvars and facts should also be available

nb 2: the loop within loop trick has been tested on 2.1.1.0;
      should work there (or better).
