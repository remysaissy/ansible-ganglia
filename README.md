ansible-ganglia
===============

[![Build Status](https://travis-ci.org/remysaissy/ansible-ganglia.png?branch=master)](https://travis-ci.org/remysaissy/ansible-ganglia)

Installs and configure the Ganglia monitoring system.

Configuration
-------------

There are a few things to configure before using this role.

### Specify which nodes are "Ganglia Collector Daemon" ###

For the "Ganglia Collector Daemon node", add to the inventory file
_<root>/production/inventory_
```yml
 node.domain.com is_ganglia_meta=1
```

### Specify which nodes should install "Ganglia Web Daemon" ###

For the "Ganglia Web Daemon node", add to the inventory file
_<root>/production/inventory_
```yml
 node.domain.com is_ganglia_web=1
```

### Configure the "Ganglia Collector Daemon" ###

The collector is configured through the variable _ganglia_config_gmetad_ which is located in _roles/ganglia/defaults/main.yml_.
Simply copy paste this hash in the relevant group vars and adapt the settings.
For example:
_<root>/production/groups_vars/ParisDC1_
```yml
ganglia_config_gmetad:
	...
```

_<root>/production/groups_vars/BerlinDC2_
```yml
ganglia_config_gmetad:
	...
```
Also, multiple data sources are supported but facts are not used to discover it automatically.
So you will have to specify the name of the nodes for these data sources in the group vars.

### Configure the "Ganglia Monitor Daemon" ###

The monitor is configured through the variable _ganglia_config_gmond_ which is located in _roles/ganglia/defaults/main.yml_.
Simply copy paste this hash in the relevant group vars and adapt the settings.
For example:
_<root>/production/groups_vars/ParisDC1_
```yml
ganglia_config_gmond:
	...
```

_<root>/production/groups_vars/BerlinDC2_
```yml
ganglia_config_gmond:
	...
```

Each node installed with Ganglia Monitor also has the python extension package too.
Though the _ganglia_config_gmond_ option, you can also configure several data sources.
One gmond configuration file and one systemV service will be created per data source.


### TODO ###

- Use ganglia_config_gmetad and ganglia_config_gmond to discover the ports to open for the firewall
- Add support for installing extensions
- Add support for installing a version not available in the official Operating System repository

Usage
-----

In all nodes
```yml
 roles: 
    - { role: 'ganglia' }
```

Supported Operating Systems
---------------------------

This role has been tested on CentOS 6.5 and on an Ubuntu Trusty.
However, some options in the Ganglia Monitor template are not yet available on both platforms (like sflow support) and you should only comment it for the gmond config file to be parsed properly.

#### License

Licensed under the MIT License. See the LICENSE file for details.


#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/ansibles/monit/issues)!