Ansible Role : dginhoux.timesync
=========

This ansible role can configure chrony OR ntp for clock synchronization
it allow an easy switch between `chrony`, `timesync`, and `ntpd`.


Requirements
------------

This role require a supported platform defined in `meta/main.yml`.
It will skip node with unsupported platform ; this behaviour can be bypassed by settings this variable `asserts_bypass=True`.


Role Variables
--------------

Necessary variables are defined on `defaults/main.yml`.
Specifics variables are in `vars/{{ ansible_os_family }}`.


Dependencies
------------

none


Example Playbook
----------------



License
-------

BSD


Author Information
------------------

https://github.com/dginhoux/

