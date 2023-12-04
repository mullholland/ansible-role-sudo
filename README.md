# [Ansible role sudo](#sudo)

Install and configure sudo permissions

|GitHub|Downloads|Version|
|------|---------|-------|
|[![github](https://github.com/mullholland/ansible-role-sudo/actions/workflows/molecule.yml/badge.svg)](https://github.com/mullholland/ansible-role-sudo/actions/workflows/molecule.yml)|[![downloads](https://img.shields.io/ansible/role/d/mullholland/sudo)](https://galaxy.ansible.com/mullholland/sudo)|[![Version](https://img.shields.io/github/release/mullholland/ansible-role-sudo.svg)](https://github.com/mullholland/ansible-role-sudo/releases/)|
## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/mullholland/ansible-role-sudo/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: true
  gather_facts: true
  vars:
    sudo_defaults:
      - 'env_reset'
      - 'mail_badpass'
      - 'secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"'

    sudo_sudoers:
      - name: user1
        commands:
          - hosts: "ALL"
            as: "ALL:ALL"
            command: "ALL"
            nopasswd: false
      - name: user2
        commands:
          - hosts: "ALL"
            as: "ALL:ALL"
            command: "ALL"
            nopasswd: false

    sudo_aliases:
      - name: "GROUPONE"
        type: "user"
        alias: "user1, user2, user3"
      - name: "SANDBOX"
        type: "host"
        alias: "devhost1, devhost2"
      - name: "WEB"
        type: "runas"
        alias: "www-data, apache"
      - name: "POWER"
        type: "cmnd"
        alias: "/sbin/shutdown, /sbin/halt, /sbin/reboot, /sbin/restart"

    sudo_groups:
      - name: sudogroup
        commands:
          - hosts: "ALL"
            as: "ALL:ALL"
            command: "ALL"
            nopasswd: false

  roles:
    - role: "mullholland.sudo"
```



## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/mullholland/ansible-role-sudo/blob/master/defaults/main.yml):

```yaml
---
# package name
sudo_package: sudo

# manage sudoers files and delete unknown files
sudo_manage_exclusive: true

sudo_defaults: []
# - 'env_reset'
# - 'mail_badpass'
# - 'secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"'

# hosts - as - command
# *user1* ALL=(ALL:ALL) ALL  =>  The first field indicates the username that the rule will apply to (user1)
# user1 *ALL*=(ALL:ALL) ALL  =>  The first “ALL” indicates that this rule applies to all hosts.
# user1 ALL=(*ALL*:ALL) ALL  =>  This “ALL” indicates that the user1 user can run commands as all users.
# user1 ALL=(ALL:*ALL*) ALL  =>  This “ALL” indicates that the user1 user can run commands as all groups.
# user1 ALL=(ALL:ALL) *ALL*  =>  The last “ALL” indicates these rules apply to all commands.
sudo_sudoers: []
# - name: user1
#   commands: []  # optional
#   # - hosts: "ALL"  # optional => default "ALL"
#   #   as: "ALL:ALL"  # optional => default "ALL:ALL"
#   #   command: ALL  # required
#   #   nopasswd: false  # optional => default "false"

# Aliases
# names must start with a capital letter
# type maybe:
#  - host  => for Host Aliases
#  - user  => for User Aliases
#  - runas => for Runas Aliases
#  - cmnd  => for Command Aliases
#
# type name = alias
sudo_aliases: []
# - name: "GROUPONE"
#   type: "user"
#   alias: "user1, user2, user3"
# - name: "SANDBOX"
#   type: "host"
#   alias: "devhost1, devhost2"
# - name: "WEB"
#   type: "runas"
#   alias: "www-data, apache"
# - name: "POWER"
#   type: "cmnd"
#   alias: "/sbin/shutdown, /sbin/halt, /sbin/reboot, /sbin/restart"

sudo_groups: []
# - name: sudouser
#   commands: []  # optional
#   # - hosts: "ALL"  # optional => default "ALL"
#   #   as: "ALL:ALL"  # optional => default "ALL:ALL"
#   #   command: ALL  # required
#   #   nopasswd: false  # optional => default "false"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/mullholland/ansible-role-sudo/blob/master/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://mullholland.net) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/mullholland/ansible-role-sudo/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/r/mullholland/enterpriselinux)|all|
|[Amazon](https://hub.docker.com/r/mullholland/amazonlinux)|Candidate|
|[Fedora](https://hub.docker.com/r/mullholland/fedora/)|all|
|[Ubuntu](https://hub.docker.com/r/mullholland/ubuntu)|all|
|[Debian](https://hub.docker.com/r/mullholland/debian)|all|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-sudo/issues).

## [License](#license)

[MIT](https://github.com/mullholland/ansible-role-sudo/blob/master/LICENSE).

## [Author Information](#author-information)

[Mullholland](https://mullholland.net)
