SBD Backed Cluster
==================

This role sets up a Pacemaker cluster based with Storage-Based Death
used for STONITH.

Requirements
------------

* At least one shared disk to be used for Storage-Based Death
* Distributions tested:
  * CentOS 7
  * CentOS 8
  * Debian 9
  * Debian 10
  * Ubuntu 18.04 LTS
  * Ubuntu 20.04 LTS
  * Fedora 28-34 except Fedora 30

Role Variables
--------------
All variables are optional.

* timezone: Timezone for servers, will not configure if unset.
* setup_etc_hosts: Set names of nodes in `/etc/hosts`. Defaults to
  False.
* setup_etc_hosts_domain: Domain name to add to entries on
  `/etc/hosts`. Defaults to empty, highly recommended if
  setup_etc_hosts is true.
* pacemaker_name: Name of the cluster to create. Defaults to
  "BaseCluster".
* pacemaker_password: password for the `hacluster` account, used for
  authenticating Pacemaker daemon. Defaults to `highavailability`.
* pacemaker_iface: name of the network interface for communication.
  Will use first available interface if unset. Does not work if using
  CentOS 7, Debian 9, Ubuntu 18.04 or Fedora 28 and `setup_etc_hosts`
  is False.
* sbd_devices: list of block device paths to be used for Storage Based
  Death (at least one). Defaults to `[/dev/vdb]`.

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: base-cluster
          vars:
            timezone: Europe/Madrid
            setup_etc_hosts: True
            setup_etc_hosts_domain: my-cluster
            pacemaker_name: My Cluster
            pacemaker_password: ARandomString
            sbd_devices:
                - /dev/sdc
                - /dev/sdd
                - /dev/sde


License
-------

BSD

Author Information
------------------

Raúl Pedroche @pedrocheisback