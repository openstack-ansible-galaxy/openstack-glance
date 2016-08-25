Glance OpenStack Ansible Role
=========

**Status**
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-glance.svg?branch=master)](https://travis-ci.org/openstack-ansible-galaxy/openstack-glance) on master branch
* [![Build Status](https://travis-ci.org/openstack-ansible-galaxy/openstack-glance.svg?branch=development)](https://travis-ci.org/openstack-ansible-galaxy/openstack-glance) on development branch
* [![Ansible Galaxy](http://img.shields.io/badge/dguerri-openstack--glance-blue.svg)](https://galaxy.ansible.com/list#/roles/1768) on Ansible Galaxy

OpenStack Glance image service installation

_Tested on Ubuntu Precise (12.04) and Trusty (14.04)_

Requirements
------------

A DBMS already configured with a user and a database (when applicable).

A RabbitMQ server. See below.

A Keystone server. See below.

For RHEL/CentOS, RHOSP or RDO repositories are needed.

Role Variables
--------------


### Glance (set by this role)

| Name | Default value | Description |
|---  |---  |---  |
| `openstack_glance_database_url` | `sqlite:////var/lib/glance/glance.sqlite` | Database URI |
| `openstack_glance_user` | `glance` | Admin user for the image service as defined on Keystone |
| `openstack_glance_pass` | `glance_pass_default` | Password for the image service as defined on Keystone |
| `openstack_glance_bind_host` | `0.0.0.0` | IP address glance API will bind to |
| `openstack_glance_port` | `9292` | Desired glance service port |
| `openstack_glance_protocol` | `http` | Desired glance protocol (http/https) - WiP, do not use. |
| `openstack_glance_keystone_admin_port` | `35357` | Keystone admin service port |
| `openstack_glance_keystone_hostname` | `localhost` | Hostname/IP address where the keystone service runs |
| `openstack_glance_keystone_port` | `5000` | Keystone service port |
| `openstack_glance_keystone_protocol` | `http` | Desired glance protocol (http/https) - WiP, do not use |
| `openstack_glance_rabbit_hostname` | `localhost` | Hostname/IP address where the RabbitMQ service runs |
| `openstack_glance_rabbit_username` | `rabbit_username_default` | RabbitMQ username for glance |
| `openstack_glance_rabbit_password` | `rabbit_pass_default` | RabbitMQ password for glance |
| `openstack_glance_hostname` | `localhost` | Hostname/IP used internally during configuration. localhost is usually ok |
| `openstack_glance_log_dir` | `/var/log/glance` | Log directory (it must exist) |


Dependencies
------------

None.

Example Playbook
----------------

    - hosts: glance001
      roles:
        - role: openstack-glance
          openstack_glance_database_url: "mysql://{{ MYSQL_GLANCE_USER }}:{{ MYSQL_GLANCE_PASS }}@{{ DATABASE_HOSTNAME }}/{{ MYSQL_GLANCE_DB }}"
          openstack_glance_hostname: glance
          openstack_glance_pass: "{{ GLANCE_PASS }}"
          openstack_glance_keystone_hostname: keystone
          openstack_glance_rabbit_hostname: rabbitmq
          openstack_glance_rabbit_username: glance
          openstack_glance_rabbit_password: "{{ RABBIT_GLANCE_PASS }}"

---

A complete Ansible playbook demo, which uses this role, is available on Github (openstack-ansible-galaxy/vagrant-ansible-openstack) <https://github.com/openstack-ansible-galaxy/vagrant-ansible-openstack>

---

Credits
-------
RedHat suport implemented by Abel Boldú <abel.boldu@gmx.com>


License
-------

Apache

Author Information
------------------

Copyright (c) 2015 Davide Guerri <davide.guerri@gmail.com>
