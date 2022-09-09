ginhouxnet.timesync
=========

This ansible role can configure chrony OR ntp for clock synchronization
it allow an easy switch between `chrony` and `ntpd`.


Requirements
------------

This role is built to only run on platforms defined in `meta/main.yml`


Role Variables
--------------

Necessary variables are defined on `defaults/main.yml` and specifics variables are in `vars/{{ ansible_os_family }}`


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

