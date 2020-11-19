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
* pacemaker_name: Name of the cluster to create, defaults to "CentOSCluster".
* pacemaker_password: password for the `hacluster` account, used for authenticating
  Pacemaker daemon.
* sbd_devices: list of block device paths to be used for Storage Based Death (at
  least one), defaults to `[/dev/vdb]`.
* setup_etc_hosts: Set names of nodes in `/etc/hosts`, defaults to True.

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