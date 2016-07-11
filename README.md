users_profiles
==============

[![Ansible Galaxy][galaxy_image]][galaxy_link]
[![Build Status][travis_image]][travis_link]
[![Latest Tag][tag_image]][tag_link]

An [Ansible](https://www.ansible.com/) role to manage system groups, system users, users authorized keys, and sudo specifications.

Requirements
------------

None.

Role Variables
--------------

```yaml
# list of system groups
users_profiles__groups: []
## group name
#  - name: string
## OPTIONAL: if set to true, group is removed from host
#    disabled: bool
## OPTIONAL: group id
#    gid: int
## OPTIONAL: system group flag
#    system: bool

# list of system users
users_profiles__list: []
## user name
#  - name: string
## OPTIONAL: should specified groups be appended
#    append: bool
## OPTIONAL: list of users authorized keys
#    authorized_keys: [ {
## authorized key
#      - key: string
## OPTIONAL: should be authorized key exclusive
#        exclusive: boolean
## OPTIONAL: ssh key options
#        key_options: string
## OPTIONAL: should directory containing authorized_keys file be managed by ansible
#        manage_dir: boolean
## OPTIONAL: if set to true, authorized key is removed
#        disabled: boolean
#    } ]
## OPTIONAL: user description (GECOS)
#    comment: string
## OPTIONAL: should be home directory created if it does not exists
#    createhome: bool
## OPTIONAL: user expiration time
#    expires: date
## OPTIONAL: should user removal be forced
#    force: bool
## OPTIONAL: primary user group
#    group: string
## OPTIONAL: list of additional user groups, all groups are removed if empty
#    groups: [ string ]
## OPTIONAL: user home directory
#    home: string
## OPTIONAL: group of user home directory
#    home_group: string
## OPTIONAL: access mode of user home directory
#    home_mode: string
## OPTIONAL: owener of user home directory
#    home_owner: string
## OPTIONAL: should be user home directory moved, if it's location differs
#    move_home: bool
## OPTIONAL: user password
#    password: string
## OPTIONAL: should be user home directory removed, when user is removed
#    remove: bool
## OPTIONAL: user's default shell
#    shell: string
## OPTIONAL: skeleton for home directory creation
#    skeleton: string
## OPTIONAL: list of users sudo specifications, if set to empty list specifications are removed
#    sudo: [ {
## specification host(s), mutiple values are concatenated with comma
#      - host: string | [ string ]
## OPTIONAL: specification operator(s), mutiple values are concatenated with comma
#        operator: string | [ string ]
## OPTIONAL: specification tag(s), mutiple values are concatenated with colon
#        tag: string | [ string ]
## specification command(s), mutiple values are concatenated with comma
#        command: string | [ string ]
#    } ]
## OPTIONAL: system user flag
#    system: bool
## OPTIONAL: user id
#    uid: int
## OPTIONAL: password update behavior
#    update_password: bool
## OPTIONAL: should be SSH key generated, if the isn't one
#    generate_ssh_key: bool
## OPTIONAL: bit lenght of generated SSH key
#    ssh_key_bits: int
## OPTIONAL: comment for generated SSH key
#    ssh_key_comment: string
## OPTIONAL: location of file containing generated SSH key
#    ssh_key_file: string
## OPTIONAL: passphrase used to encrypt generated SSH key
#    ssh_key_passphrase: string
## OPTIONAL: type of generated SSH key
#    ssh_key_type: string
## OPTIONAL: if set to true, user is removed from host
#    disabled: bool

# default value for exclusive option of authrozied keys
users_profiles__authorized_keys_exclusive: false

# default value for manage_dir option of authorized keys
users_profiles__authorized_keys_manage_dir: true

# prefix to prepend to filenames of files located in sudo configuration dropins directory
users_profiles__sudo_prefix: ""

# suffix to append to filenames of files located in sudo configuration dropins directory
users_profiles__sudo_suffix: ""

# list of default groups for all users managed by role
# to ignore these for selected user, that must have set option "append" to false in it's specification
users_profiles__users_default_groups_list: []

# should be default groups appended to potential existing user's group
users_profiles__users_default_groups_append: true
```

Dependencies
------------

- tomashavlas.pre-users_profiles
- tomashavlas.authorized_keys
- tomashavlas.sudo
- tomashavlas.system_groups
- tomashavlas.system_users

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: "tomashavlas.users_profiles"
      users_profiles__groups:
        - name: "sshusers"
      users_profiles__list:
        - name: "remoteuser"
          groups:
            - "sshusers"
```

For more examples see [test cases](https://github.com/tomashavlas/ansible-role-users_profiles/tree/master/tests).

License
-------

BSD

Author Information
------------------

Created by [Tomáš Havlas](https://github.com/tomashavlas) in 2016.

[galaxy_image]: https://img.shields.io/badge/galaxy-tomashavlas.users__profiles-blue.svg?style=flat
[galaxy_link]: https://galaxy.ansible.com/tomashavlas/users_profiles/
[tag_image]: https://img.shields.io/github/tag/tomashavlas/ansible-role-users_profiles.svg
[tag_link]: https://github.com/tomashavlas/ansible-role-users_profiles/tags
[travis_image]: https://travis-ci.org/tomashavlas/ansible-role-users_profiles.svg?branch=master
[travis_link]: https://travis-ci.org/tomashavlas/ansible-role-users_profiles/
