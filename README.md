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
| `glance_database_url` | `sqlite:////var/lib/glance/glance.sqlite` | Database URI |
| `glance_user` | `glance` | Admin user for the image service as defined on Keystone |
| `glance_pass` | `glance_pass_default` | Password for the image service as defined on Keystone |
| `glance_bind_host` | `0.0.0.0` | IP address glance API will bind to |
| `glance_port` | `9292` | Desired glance service port |
| `glance_protocol` | `http` | Desired glance protocol (http/https) - WiP, do not use. |
| `keystone_admin_port` | `35357` | Keystone admin service port |
| `keystone_hostname` | `localhost` | Hostname/IP address where the keystone service runs |
| `keystone_port` | `5000` | Keystone service port |
| `keystone_protocol` | `http` | Desired glance protocol (http/https) - WiP, do not use |
| `glance_hostname` | `localhost` | Hostname/IP used internally during configuration. localhost is usually ok |
| `glance_log_dir` | `/var/log/glance` | Log directory (it must exist) |

### RabbitMQ (must exist)

| Name | Default value | Description | Note |
|---  |---  |---  |--- |
| `glance_rabbit_userid` | `rabbit_username_default` | RabbitMQ username for console auth ||
| `glance_rabbit_password` | `rabbit_pass_default` | RabbitMQ password for console auth ||
| `glance_rabbit_virtual_host`| `/` | RabbitMQ virtual host for console auth ||
| `glance_rabbit_retry_interval` | `1` | Frequency to retry connecting to RabbitMQ ||
| `glance_rabbit_host` | `localhost` | The RabbitMQ broker address where a single node is used ||
| `glance_rabbit_port` | `5672` | The RabbitMQ broker port where a single node is used ||
| `glance_rabbit_hosts` | `$rabbit_host:$rabbit_port` | RabbitMQ HA cluster host:port pairs ||
| `glance_rabbit_ha_queues` | `False` | Use HA queues in RabbitMQ (x-ha-policy: all) ||

Dependencies
------------

None.

Example Playbook
----------------

    - hosts: glance001
      roles:
        - role: openstack-glance
          glance_database_url: "mysql://{{ MYSQL_GLANCE_USER }}:{{ MYSQL_GLANCE_PASS }}@{{ DATABASE_HOSTNAME }}/{{ MYSQL_GLANCE_DB }}"
          glance_hostname: glance
          glance_pass: "{{ GLANCE_PASS }}"
          keystone_hostname: keystone
          rabbit_hostname: rabbitmq
          rabbit_username: glance
          rabbit_pass: "{{ RABBIT_GLANCE_PASS }}"

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
