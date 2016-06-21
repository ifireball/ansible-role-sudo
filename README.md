sudo
====

[![Ansible Galaxy][galaxy_image]][galaxy_link]
[![Build Status][travis_image]][travis_link]
[![Latest Tag][tag_image]][tag_link]

An [Ansible](https://www.ansible.com/) role to install [sudo](https://www.sudo.ws/) and manage sudoers configuration - defaults, aliases, and specifications.

Aliases and global defaults are stored in main configuration file `/etc/sudoers`. Specifications and more specific defaults are stored in separate files in `/etc/sudoers.d/` directory.

Requirements
------------

None.

Role Variables
--------------

```yaml
# list of global sudo defaults
sudo__defaults: []
## sudo defaults option
#  - name: string
## OPTIONAL: sudo defaults value(s), mutiple values are concatenated with space and enclosed by double quotes, can be
## skipped for boolean defaults
#    value: int | string | [ string ]
## OPTIONAL: should value(s) be added to value list
#    include: bool
## OPTIONAL: should value(s) be removed from value list
#    exclude: bool

# list of sudo command aliases
sudo__cmnd_aliases: []
## command alias
#  - name: string
## alias value(s), mutiple values are concatenated with comma
#    command: string | [ string ]

# list of sudo host aliases
sudo__host_aliases: []
## sudo alias
#  - name: string
## alias value(s), mutiple values are concatenated with comma
#    host: string | [ string ]

# list of sudo operator aliases
sudo__runas_aliases: []
## operator alias
#  - name: string
## alias value(s), mutiple values are concatenated with comma
#    operator: string | [ string ]

# list of sudo user aliases
sudo__user_aliases: []
## user alias
#  - name: string
## alias value(s), mutiple values are concatenated with comma
#    user: string | [ string ]

# list of sudo specifications, defaults, specification or both must be set for specification file to be created
sudo__specs: []
## filename of sudo specification file
#  - name: string
## OPTIONAL: if set to False specification file is removed form host, defaults to True
#    enabled: bool
## OPTIONAL: list of sudo defaults, if command, host, operator, and user option are not set, then sudo default is
## recognized as global
#    defaults:
## sudo defaults option
#      - name: string
## OPTIONAL: make this defaults option command(s) specific, mutiple values are concatenated with comma
#        command: string | [ string ]
## OPTIONAL: make this defaults option host(s) specific, mutiple values are concatenated with comma
#        host: string | [ string ]
## OPTIONAL: make this defaults option operator(s) specific, mutiple values are concatenated with comma
#        operator: string | [ string ]
## OPTIONAL: make this defaults option user(s) specific, mutiple values are concatenated with comma
#        user: string | [ string ]
## OPTIONAL: sudo defaults value(s), mutiple values are concatenated with space and enclosed by double quotes, can be
## skipped for boolean defaults
#        value: int | string | [ string ]
## OPTIONAL: should value(s) be added to value list
#        include: bool
## OPTIONAL: should value(s) be removed from value list
#        exclude: bool
## OPTIONAL: list of sudo specifications
#    specs: []
## specification user(s), mutiple values are concatenated with comma
#      - user: string | [ string ]
## specification host(s), mutiple values are concatenated with comma
#        host: string | [ string ]
## OPTIONAL: specification operator(s), mutiple values are concatenated with comma
#        operator: string | [ string ]
## OPTIONAL: specification tag(s), mutiple values are concatenated with colon
#        tag: string | [ string ]
## specification command(s), mutiple values are concatenated with comma
#        command: string | [ string ]

# if set to True all files located in sudo configuration dropins directory not created by this role are removed
sudo__specs_purge_unmanaged: False

## OPTIONAL: list of sudo packages, defaults to OS specific value
# sudo__packages: string | [ string ]

## OPTIONAL: path to sudo I/O log directory, defaults to OS specific value
# sudo__iolog_dir: string

## OPTIONAL: filename pattern for sudo I/O log files, defaults to OS specific value
# sudo__iolog_filename: string
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: sudo
      sudo__defaults:
        - name: 'env_reset'
        - name: '!visiblepw'
        - name: 'secure_path'
          value: '/sbin:/bin:/usr/sbin:/usr/bin'
      sudo__specs:
        - name: 'wheel'
          specs:
            - user: '%wheel'
              host: 'ALL'
              operator: 'ALL'
              command: 'ALL'
```

License
-------

BSD

Author Information
------------------

Created by [Tomáš Havlas](https://github.com/tomashavlas) in 2016.

[galaxy_image]: https://img.shields.io/badge/galaxy-tomashavlas.sudo-blue.svg?style=flat
[galaxy_link]: https://galaxy.ansible.com/tomashavlas/sudo/
[tag_image]: https://img.shields.io/github/tag/tomashavlas/ansible-role-sudo.svg
[tag_link]: https://github.com/tomashavlas/ansible-role-sudo/tags
[travis_image]: https://travis-ci.org/tomashavlas/ansible-role-sudo.svg?branch=master
[travis_link]: https://travis-ci.org/tomashavlas/ansible-role-sudo/
