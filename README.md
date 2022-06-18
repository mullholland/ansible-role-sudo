# [sudo](#sudo)

|GitHub|GitLab|
|------|------|
|[![github](https://github.com/mullholland/ansible-role-sudo/workflows/Ansible%20Molecule/badge.svg)](https://github.com/mullholland/ansible-role-sudo/actions)|[![gitlab](https://gitlab.com/mullholland/ansible-role-sudo/badges/master/pipeline.svg)](https://gitlab.com/mullholland/ansible-role-sudo)|[![quality](https://img.shields.io/ansible/quality/unset)](https://galaxy.ansible.com/mullholland/sudo)|

description

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
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


## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
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





## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/mullholland):

-   [debian9](https://hub.docker.com/r/mullholland/docker-molecule-debian9)
-   [debian10](https://hub.docker.com/r/mullholland/docker-molecule-debian10)
-   [debian11](https://hub.docker.com/r/mullholland/docker-molecule-debian11)
-   [ubuntu1804](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu1804)
-   [ubuntu2004](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu2004)
-   [ubuntu2204](https://hub.docker.com/r/mullholland/docker-molecule-ubuntu2204)
-   [centos7](https://hub.docker.com/r/mullholland/docker-molecule-centos7)
-   [centos-stream8](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream8)
-   [centos-stream9](https://hub.docker.com/r/mullholland/docker-molecule-centos-stream9)
-   [ubi8](https://hub.docker.com/r/mullholland/docker-molecule-ubi8)
-   [fedora35](https://hub.docker.com/r/mullholland/docker-molecule-fedora35)
-   [fedora36](https://hub.docker.com/r/mullholland/docker-molecule-fedora36)
-   [amazonlinux](https://hub.docker.com/r/mullholland/docker-molecule-amazonlinux)
-   [rockylinux8](https://hub.docker.com/r/mullholland/docker-molecule-rockylinux8)
-   [almalinux8](https://hub.docker.com/r/mullholland/docker-molecule-almalinux8)

The minimum version of Ansible required is 2.10, tests have been done to:

-   The previous versions.
-   The current version.
-   The [devel](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-devel-from-github-with-pip) version.





If you find issues, please register them in [GitHub](https://github.com/mullholland/ansible-role-sudo/issues)

## [License](#license)

MIT


## [Author Information](#author-information)

[Mullholland](https://github.com/mullholland)

## [Special Thanks](#special-thanks)

Template inspired by [Robert de Bock](https://github.com/robertdebock)
