CentOS 7+ Cluster
=================

This role sets up a Pacemaker cluster based on CentOS 7+, with Storage-Based Death used
for STONITH.

Requirements
------------

* At least one shared disk to be used for Storage-Based Death

Role Variables
--------------
All variables are optional

* timezone: Timezone for servers, will not configure if unset.
* setup_etc_hosts: Set names of nodes in `/etc/hosts`. Defaults to
  True.
* pacemaker_name: Name of the cluster to create. Defaults to
  "CentOSCluster".
* pacemaker_password: password for the `hacluster` account, used for
  authenticating Pacemaker daemon. Defaults to `highavailability`.
* pacemaker_iface: name of the network interface for communication.
  Will use first available interface if unset. Does not work if using
  CentOS 7 and `setup_etc_hosts` is False.
* sbd_devices: list of block device paths to be used for Storage Based
  Death (at least one). Defaults to `[/dev/vdb]`.

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: base-cluster
          vars:
            timezone: Europe/Madrid
            setup_etc_hosts: False
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