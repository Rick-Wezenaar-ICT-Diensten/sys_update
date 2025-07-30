Role Name
=========

Ansible role to update your RedHat / Dedbian / Suse based machines.

Requirements
------------

- Ansible setup + role layout (/home/ansible is base and /home/ansible/roles/sys_update would be this role)
- inventories/prod/hosts.ini in your ansible base (so if your base is /home/ansible then you have /home/ansible/inventories/prod/hosts.ini)

Role Variables
--------------

/home/ansible/host_vars/<hostname>.yml for each host you want to address
the contents of the file would be something like:

health_tcp_ports: [22, 80, 443]

/home/ansible/group_vars/all.yml
this file contains the apps of all machines, like:

apps:
  plex:
    - chronyd
    - zabbix-agent2
  vps:
    - chronyd
    - nginx
    - zabbix-agent2
    ...
  ...
etc.

Dependencies
------------

community.general

Example Playbook
----------------

create a file with the following contents:

---
- name: Universal System Update
  hosts: linux_all
  become: yes
  gather_facts: yes

  # Keep your existing variables but move them under ./vars
  vars_files:
    - vars/zabvars.yml
    - vars/mountvars.yml
    - vars/appvars.yml

  roles:
    - sys_update
  
License
-------

GNU

Author Information
------------------

Rick Wezenaar - rick@wezenaar.org
