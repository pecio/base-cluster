CentOS 7 Cluster requisites
===========================

This role sets up a CentOS 7 node so it can become a Pacemaker cluster
member.

Requirements
------------

* A shared disk to be used for Storage-Based Death

Role Variables
--------------

TBD

Example Playbook
----------------

    - hosts: servers
      roles:
         - base-cluster

License
-------

BSD

Author Information
------------------

Raúl Pedroche