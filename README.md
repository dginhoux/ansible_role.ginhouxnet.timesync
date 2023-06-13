# ROLE dginhoux.ntp_sync



## DESCRIPTION

This ansible role can configure chrony OR ntp for clock synchronization.<br />
it allow an easy switch between `chrony`, `timesync`, and `ntpd`.



## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip node with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `skip_check_platform_compatibility=true`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36, 37, 38 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.ntp_sync
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.ntp_sync dginhoux.ntp_sync
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.ntp_sync
      ansible.builtin.include_role:
        name: dginhoux.ntp_sync
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
ntp_enabled: true
ntp_install_package: true
ntp_remove_package: true
ntp_install_tzdata: true
ntp_manage_config: true
ntp_manage_services: true

ntp_daemon_choice: ntp
# ntp_daemon_choice: chrony
# ntp_daemon_choice: timesyncd

ntp_timezone: Europe/Paris

ntp_servers:
  - "ntp1.infra.ginhoux.net"
  - "ntp2.infra.ginhoux.net"
  - "ntp3.infra.ginhoux.net"

ntp_pools:
  - "0.fr.pool.ntp.org"
  - "1.fr.pool.ntp.org"
  - "2.fr.pool.ntp.org"
  - "3.fr.pool.ntp.org"

ntp_chrony_allow:
  - "127.0.0.1/32"
  - "192.168.0.0/16"

ntp_ntpd_tinker_panic: false

ntp_ntpd_restrict:
  - "127.0.0.1 nomodify"
  - "-4 default kod notrap nomodify nopeer noquery"
  - "-6 default kod notrap nomodify nopeer noquery"
  - "192.168.0.0 mask 255.255.0.0 nomodify notrap"
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.


* RedHat Family 

```yaml
ntp_daemon_conf:
  ntp:
    ntp_daemon_install_package:
      - ntpsec
    ntp_daemon_remove_package:
      - chrony
    ntp_daemon_enable_service:
      - ntp
    ntp_daemon_disable_service:
      - chronyd
      - systemd-timesyncd
    ntp_daemon_config_file: /etc/ntp.conf
  chrony:
    ntp_daemon_install_package:
      - chrony
    ntp_daemon_remove_package:
      - ntp
    ntp_daemon_enable_service:
      - chronyd
    ntp_daemon_disable_service:
      - ntp
      - systemd-timesyncd
    ntp_daemon_config_file: /etc/chrony/chrony.conf
  timesyncd:
    ntp_daemon_install_package: []
    ntp_daemon_remove_package:
      - chrony
      - ntp
    ntp_daemon_enable_service:
      - systemd-timesyncd
    ntp_daemon_disable_service:
      - chronyd
      - ntp
    ntp_daemon_config_file: /etc/systemd/timesyncd.conf

ntp_tzdata_package:
  - tzdata
ntp_timezone_file: /etc/sysconfig/clock

ntp_chrony_driftfile: /var/lib/chrony/drift
ntp_chrony_keyfile: /etc/chrony.keys
ntp_chrony_confdir: /etc/chrony
ntp_chrony_logdir: /var/log/chrony
ntp_chrony_envfile: /etc/sysconfig/chronyd

ntp_ntpd_driftfile: /var/lib/ntp/drift
```

* Debian Family 

```yaml
ntp_daemon_conf:
  ntp:
    ntp_daemon_install_package:
      - ntp
    ntp_daemon_remove_package:
      - chrony
    ntp_daemon_enable_service:
      - ntp
    ntp_daemon_disable_service:
      - chronyd
      - systemd-timesyncd
    ntp_daemon_config_file: /etc/ntp.conf
  chrony:
    ntp_daemon_install_package:
      - chrony
    ntp_daemon_remove_package:
      - ntp
    ntp_daemon_enable_service:
      - chronyd
    ntp_daemon_disable_service:
      - ntp
      - systemd-timesyncd
    ntp_daemon_config_file: /etc/chrony/chrony.conf
  timesyncd:
    ntp_daemon_install_package: []
    ntp_daemon_remove_package:
      - chrony
      - ntp
    ntp_daemon_enable_service:
      - systemd-timesyncd
    ntp_daemon_disable_service:
      - chronyd
      - ntp
    ntp_daemon_config_file: /etc/systemd/timesyncd.conf

ntp_tzdata_package:
  - tzdata
ntp_timezone_file: /etc/timezone

ntp_chrony_driftfile: /var/lib/chrony/chrony.drift
ntp_chrony_keyfile: /etc/chrony/chrony.keys
ntp_chrony_confdir: /etc/chrony
ntp_chrony_logdir: /var/log/chrony
ntp_chrony_envfile: /etc/default/chrony
ntp_ntpd_driftfile: /var/lib/ntp/drift
```


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
