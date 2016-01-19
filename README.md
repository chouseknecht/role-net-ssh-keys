Net-SSH-Keys
============

Use Ansible core network modules to add SSH keys to existing users on a network device.   

Requirements
------------

Requires the following components:

- Ansible 2.0 
- [privateip/ansible-modules/core working branch](https://github.com/privateip/ansible-modules-core/tree/working)
- net_config.py action plugin (not available publicly)

Role Variables
--------------

netkeys_use_ssl:

> For non-SSH connections specifies whether or not to use SSL. Defaults to True. 

netkeys_username:

> Name of the account being created.

netkeys_password:

> Password of the account being created.

netkeys_transport:

> Supported connection transports: cli, nxapi

netkeys_delegate_to:

> Name of a host to delegate to. See [Ansible Delegation](http://docs.ansible.com/ansible/playbooks_delegation.html#delegation).   

net_users:

> List of users. Each user is an object with attributes: username, key


Example Playbook
----------------

```
- name: Add each user's public SSH key 
  hosts: all
  connection: local
  vars:
      net_users:
          - { username: chouseknecht,
              key: "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQC1igsIlcmTa/yfsJnTtnrEX7PP/a01gwbXcig6JOKyrUmJB8E6c/wtZwP115VSyDRTO6TEL/sBFUpkSw01zM8ydNATErh8meBlAlbnDq5NLhDXnMizgG0VNn0iLc/WplFTqkefsHXa8NtIxAtyEVIj/fKbK3XfBOdEpE3+MJYNtGlWyaod28W+5qmQPZDQys+YnE4OjSwN7D3g85/7dtLFvDH+lEC4ooJOaxVFr9VSMXUIkaRF6oI+R1Zu803LFSCTb4BfFOYOHPuQ/rEMP0KuUzggvP+TEBY14PEA2FoHOn+oRsT0ZR2+loGRaxSVqCQKaEHbNbkm+6Rllx2NQRO0BJxCSKRU1iifInLPxmSc4gvsHCKMAWy/tGkmKHPWIfN8hvwyDMK5MNBp/SJ1pVx4xuFDQjVWNbll0yk2+72uJgtFHHwEPK9QsOz45gX85vS3yhYCKrscS/W9h2l36SWwQXuGy4fXotE7esPsvNGAzBndHX1O8RMPg47qJXz059RyoGforoa9TnzIs3hIv+ts7ESx3OEq3HNk0FJ+wDka7IM7WQpGrVToJ0vfDy9Q46nw54vv5Zc/u4OZF3F5twHmyf3rLYKXRDuCvZQKT2iWQKVX6j63bq6orA5hwl22zndxWZNtOwtq8Sd0Ns0K/Fo/ggYDDGBtr68DwhA+MrxrHw=="
            }
  roles:
      - { role: ansible-testing.net-ssh-keys,
          netkeys_username: "{{ admin_username }}",
          netkeys_password: "{{ admin_password }}",
          netkeys_tranport: cli,
          netkeys_delegate_to: "{{ delegate_to_host }}" 
        }
```

License
-------

MIT

Author Information
------------------

Chris Houskenecht

[RedHat | Ansible](http://www.ansible.com)
