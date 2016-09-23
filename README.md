# ansible-samba

A role to install and configure a samba standalone file server on a target host.


## Requirements

### Ansible version

Minimum required ansible version is 2.0.

## Description

['Install the necessary packages', 'Create and configure samba shares', 'Generate all shares directories if they do not exist yet', 'Manage users and passwords']

## Role Variables

### Variables conditionally loaded

Those variables from `vars/*.{yml,json}` are loaded dynamically during task
runtime using the `include_vars` module.

Variables loaded from `vars/Debian.yml`.

```yaml
# File: vars/Debian.yml
#
# default vars for a debian system or derivative
#
samba_services:
  - smbd
  - nmbd
samba_packages:
  - samba

```

Variables loaded from `vars/RedHat.yml`.

```yaml
# vars/RedHat.yml
#
# default vars for a redhat system or derivative
#

samba_services:
  - smb
samba_packages:
  - samba
  # - samba-common-tools
  # - samba-common-libs

```

### Default vars

Defaults from `defaults/main.yml`.

```yaml
---

samba_workgroup: 'WORKGROUP'
samba_server_string: '%h file server'
# samba_server_string: 'Fileserver %m'

# samba_log:
#   log_size: 5000
#   log_file: /var/log/samba/log.%m

# samba_security: 'user'
samba_map_to_guest: 'Bad User'

samba_load_printers: 'no'
samba_load_homes: 'no'
samba_shares_root: '/srv/shares'

# samba defaults = 0744
samba_shares_create_mask: 664

# samba defaults = 0755
samba_shares_directory_mask: 775

samba_shares_force_dir_mode: 775
samba_shares_force_create_mode: 660

```


## Installation

### Install with Ansible Galaxy

```shell
ansible-galaxy install archf.samba
```

Basic usage is:

```yaml
- hosts: all
  roles:
    - role: archf.samba
```

### Install with git

If you do not want a global installation, clone it into your `roles_path`.

```shell
git clone git@github.com:archf/ansible-samba.git /path/to/roles_path
```

But I often add it as a submdule in a given `playbook_dir` repository.

```shell
git submodule add git@github.com:archf/ansible-samba.git <playbook_dir>/roles/samba
```

As the role is not managed by Ansible Galaxy, you do not have to specify the
github user account.

Basic usage is:

```yaml
- hosts: all
  roles:
  - role: samba
```

## Ansible role dependencies

None.

## Todo

  * printer issue
  * selinux configuration
  * firewall contiguration

## License

MIT.

## Author Information

Felix Archambault.

## Role stack

This role was carefully selected to be part an ultimate deck of roles to manage
your infrastructure.

All roles' documentation is wrapped in this [convenient guide](http://127.0.0.1:8000/).


---
This README was generated using ansidoc. This tool is available on pypi!

```shell
pip3 install ansidoc

# validate by running a dry-run (will output result to stdout)
ansidoc --dry-run <rolepath>

# generate you role readme file
ansidoc <rolepath>
```

You can even use it programatically from sphinx. Check it out.