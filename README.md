ansible-galera
======

This role configures Galera/MariaDB 5.5 cluster.

Requirements
------------

** You must add `jinja2.ext.loopcontrols` to your `jinja2_extensions` in your `ansible.cfg`.  **
** For RHEL: You must have EPEL repository present **

All other requirements are listed in metadata file.

Role Variables
--------------

The variables that can be passed to this role and a brief description about
them are as follows.

```
# MariaDB root user password
galera_root_password: 1qa2ws3ed

# MariaDB debian-sys-maint user password
galera_maintenance_password: 1qa2ws3ed

# Galera cluster authorization credentials
galera_cluster_user: replicator
galera_cluster_password: 1qa2ws3ed

# Address MariaDB will listen on
galera_bind_address: 127.0.0.1

# Nodes with this parameter set to zero will be configured as standalone,
# i.e. wsrep_cluster_address=gcomm://
galera_bootstrap: 0

# Unique Galera cluster identifier
galera_cluster_name: mycluster

# Addresses of cluster nodes to connect to
galera_cluster_members: [10.0.0.1, 10.0.0.2]

# Setup apt repository sources or not
galera_setup_repository: yes

# Install packages or not
galera_install_packages: yes
```

So you can deploy multiple cluster within single inventory grouped by galera_cluster_name and setup
interconnection by galera_cluster_members variable.

Examples
--------

Install galera cluster with default settings.

```
- hosts: cluster_one
  vars:
    - galera_cluster_name: cluster_one
    - galera_cluster_members: [10.0.0.1, 10.0.0.2, 10.0.0.3]
  roles:
    - role: galera

- hosts: cluster_two
  vars:
    - galera_cluster_name: cluster_two
    - galera_cluster_members: [10.0.0.1.1, 10.0.1.2, 10.0.1.3]
  roles:
    - role: galera
```

Inventory file:

```
[mycluster]
mysql01.domain.com galera_bootstrap=1
mysql02.domain.com
mysql03.domain.com
```

Dependencies
------------


License
-------

LGPL

Author Information
------------------

- Roman Gorodeckij, Holms Ltd.
- Alexey Medvedchikov, 2GIS, LLC
- Sergey Antipov, 2GIS, LLC

