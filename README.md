ansible-adagios-agent-windows
=========

Ansible role for installing Adagios agent on Windows. Adagios agent is a bundle of NSClient++ and Adagios (OKconfig) tools for Nagios NRPE checks mainly used by Adagios running on Nagios / Naemon monitoring servers. The role uses another Github repository that handles the installation process. https://github.com/opinkerfi/adagios-agent-windows

Requirements
------------

pip install pywinrm

Role Variables
--------------

Adagios agent version to be downloaded/installed from https://github.com/opinkerfi/adagios-agent-windows 
```
adagios_agent_version: "1.0.0.1"
```

Hosts / monitoring servers that are allowed to connect with the NRPE service can be controlled with allowed_hosts variable
```
allowed_hosts: "127.0.0.1,::1,adagios-server"
```

Example Playbook
----------------

test.yml

```
- hosts: windows
  gather_facts: true
  vars:
    temp_path: '{{ ansible_env.TEMP }}'
    allowed_hosts: "127.0.0.1,adagios-server"
    adagios_agent_version: "1.0.0.1"
  tasks:
    - name: show temp path
      debug:
        var: temp_path

    - name: show env ProgramFiles
      debug:
        var: ansible_env['ProgramFiles']
  roles:
    - ../../ansible-adagios-agent-windows

```

Clone this repository and cd into it, then run:
```
vagrant up
ansible-playbook -i tests/inventory tests/test.yml
```

License
-------

BSD

Author Information
------------------

Opin Kerfi ehf - https://opinkerfi.is